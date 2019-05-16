---
title: 将 HSM 保护密钥迁移到 HSM 保护密钥 - AIP
description: 要使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护是从 AD RMS 到 Azure 信息保护，并仅适用于你的 AD RMS 密钥是 HSM 保护密钥和您的迁移路径的一部分的说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c72552bc2fe6c321f532c9bdbce3946ad301ca6d
ms.sourcegitcommit: 383b1fa5e65255420d7ec6fbe2f9b17f4439e33e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65708874"
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>步骤 2：HSM 保护密钥到 HSM 保护密钥的迁移

>适用范围：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*


此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当你的 AD RMS 密钥是 HSM 保护密钥，且希望使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回[步骤 4：从 AD RMS 中导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) 中，然后选择其他配置。

> [!NOTE]
> 这些说明假定你的 AD RMS 密钥受模块保护。 这是最典型的情况。 

此过程分为两部分，可将 HSM 密钥和 AD RMS 配置导入到 Azure 信息保护，以生成由你管理的 Azure 信息保护租户密钥 (BYOK)。

因为你的 Azure 信息保护租户密钥将由 Azure 密钥保管库存储并进行管理，所以除 Azure 信息保护以外，此部分的迁移还需要 Azure 密钥保管库中的管理。 如果 Azure Key Vault 由你以外的其他管理员为贵组织进行管理，则你必须与该管理员协作完成这些过程。

在开始之前，请确保你的组织有一个已在 Azure 密钥保管库中创建的密钥保管库，且该保管库支持 HSM 保护的密钥。 尽管不是必需的，但我们建议你有一个专用于 Azure 信息保护的密钥保管库。 此密钥保管库将配置为允许 Azure Rights Management 服务访问，所以此密钥保管库存储的密钥应限制为仅适用于 Azure 信息保护密钥。


> [!TIP]
> 如果即将对 Azure Key Vault 执行配置步骤，而尚不熟悉此 Azure 服务，则可能会发现先阅读 [Azure Key Vault 入门](/azure/key-vault/key-vault-get-started)可能会有所帮助。 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>第 1 部分：将 HSM 密钥传送到 Azure Key Vault

由 Azure 密钥保管库的管理员完成这些过程。

1. 对于想存储在 Azure Key Vault 中的每个导出的 SLC 密钥，请按照 Azure Key Vault 文档中的说明，使用[为 Azure Key Vault 实现自带密钥 (BYOK)](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault)，但以下情况例外：

   - 不要执行**生成你的租户密钥**中的步骤，因为你已从 AD RMS 部署获得等效物。 相反，标识从 nCipher 安装 AD RMS 服务器使用的密钥，并在迁移期间使用此密钥。 nCipher 加密密钥文件通常名为**密钥 <*keyAppName*><*keyIdentifier* >** 本地服务器上。

     将密钥上传到 Azure 密钥保管库时，可以看到显示的密钥属性，其中包括密钥 ID。 输出结果将会类似于 https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 请记下此 URL，因为 Azure 信息保护管理员需要用它命令 Azure Rights Management 服务将此密钥用作其租户密钥。

2. 在连接 Internet 的工作站上，在 PowerShell 会话中，使用[集 AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) cmdlet 来授权 Azure Rights Management 服务主体访问将存储 Azure 信息的密钥保管库保护租户密钥。 所需的权限有解密、加密、unwrapkey、wrapkey、验证和签名。
    
    例如，如果已为 Azure 信息保护创建的密钥保管库名为 contoso-byok-ky，并且你的资源组名为 contoso-byok-rg，请运行以下命令：
    
        Set-AzKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get


现在，你已经在 Azure 密钥保管库中为 Azure 信息保护中的 Azure Rights Management 服务准备好了 HSM 密钥，接下来可以导入 AD RMS 配置数据。

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>第 2 部分：将配置数据导入到 Azure 信息保护

由 Azure 信息保护的管理员完成这些过程。

1. 在连接 Internet 的工作站和 PowerShell 会话中，通过使用 [Connnect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) cmdlet 连接到 Azure Rights Management。
    
    然后通过使用 [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) cmdlet 上传每个受信任的发布域 (.xml) 文件。 例如，如果已将 AD RMS 群集升级到加密模式 2，则至少应拥有一个要导入的其他文件。
    
    若要运行此 cmdlet，需要先前为每个配置数据文件指定的密码以及在上一步中标识的密钥的 URL。
    
    例如，使用 C:\contoso-tpd1.xml 配置数据文件和我们上一步中的密钥 URL 值，首先运行以下命令以存储密码：
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
    输入指定的密码以导出配置数据文件。 然后，运行以下命令并确认希望执行此操作：
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword $TPD_Password –KeyVaultKeyUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```
    
    作为此导入的一部分，将导入 SLC 密钥并且密钥将被自动设置为已存档。

2.  在上传完每个文件后，请运行 [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) 以指定哪个导入的密钥与 AD RMS 群集中当前活动的 SLC 密钥相匹配。 该密钥将成为 Azure Rights Management 服务的活动租户密钥。

3.  使用 [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```
    Disconnect-AadrmService
    ```

如果之后需要确认正在 Azure 密钥保管库中使用的 Azure 信息保护租户密钥，请使用 [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) Azure RMS cmdlet。

现在可以转到[步骤 5：激活 Azure 权限管理服务](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)。


