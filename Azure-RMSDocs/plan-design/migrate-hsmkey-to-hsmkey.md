---
title: "将 HSM 保护密钥迁移到 HSM 保护密钥 - AIP"
description: "此说明是从 AD RMS 到 Azure 信息保护的迁移路径中的一部分，仅当你的 AD RMS 密钥是 HSM 保护密钥，且希望使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护时才适用。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 936b6e66c7ca0f94e437b91847166b51cf939b3f
ms.sourcegitcommit: 384461f0e3fccd73cd7eda3229b02e51099538d4
translationtype: HT
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>步骤 2：HSM 保护密钥到 HSM 保护密钥的迁移

>*适用于：Active Directory Rights Management Services、Azure 信息保护*


此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当你的 AD RMS 密钥是 HSM 保护密钥，且希望使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回[步骤 4：从 AD RMS 中导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) 中，然后选择其他配置。

> [!NOTE]
> 这些说明假定你的 AD RMS 密钥受模块保护。 这是最典型的情况。 

此过程分为两部分，可将 HSM 密钥和 AD RMS 配置导入到 Azure 信息保护，以生成由你管理的 Azure 信息保护租户密钥 (BYOK)。

因为你的 Azure 信息保护租户密钥将由 Azure 密钥保管库存储并进行管理，所以除 Azure 信息保护以外，此部分的迁移还需要 Azure 密钥保管库中的管理。 如果 Azure 密钥保管库由你以外的管理员为你的组织管理，则你需要与该管理员协作完成这些过程。

在开始之前，请确保你的组织有一个已在 Azure 密钥保管库中创建的密钥保管库，且该保管库支持 HSM 保护的密钥。 尽管不是必需的，但我们建议你有一个专用于 Azure 信息保护的密钥保管库。 此密钥保管库将配置为允许 Azure Rights Management 服务访问，所以此密钥保管库存储的密钥应限制为仅适用于 Azure 信息保护密钥。


> [!TIP]
> 如果你将对 Azure 密钥保管库执行配置步骤，而尚不熟悉此 Azure 服务，你可能会发现先阅读 [Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)（Azure 密钥保管库入门）可能会有所帮助。 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>第 1 部分：将 HSM 密钥传送到 Azure 密钥保管库

由 Azure 密钥保管库的管理员完成这些过程。

1.  按照 Azure 密钥保管库文档的说明，使用 [Implementing bring your own key (BYOK) for Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault)（为 Azure 密钥保管库实施自带密钥 (BYOK)），以下情况例外：

    - 不要执行**生成你的租户密钥**中的步骤，因为你已从 AD RMS 部署获得等效物。 而是标识 AD RMS 服务器使用的从 Thales 安装获得的密钥，并在迁移期间使用此密钥。 Thales 加密的密钥文件通常在本地服务器上名为 **key<*keyAppName*><*keyIdentifier*>**。

    将密钥上传到 Azure 密钥保管库后，可以看到密钥显示的属性，其中包括密钥 ID。 类似于 https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333。 请记下此 URL，因为 Azure 信息保护管理员需要用它命令 Azure Rights Management 服务将此密钥用作租户密钥。

2. 在连接 Internet 的工作站上的 PowerShell 会话中，使用 [Set-AzureRmKeyVaultAccessPolicy](/powershell/resourcemanager/azurerm.keyvault/v2.7.0/set-azurermkeyvaultaccesspolicy) cmdlet 来授权 Azure Rights Management 服务主体访问将存储 Azure 信息保护租户密钥的密钥保管库。 所需的权限有解密、加密、unwrapkey、wrapkey、验证和签名。
    
    例如，如果已为 Azure 信息保护创建的密钥保管库名为 contoso-byok-ky，并且你的资源组名为 contoso-byok-rg，请运行以下命令：
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get


现在，你已经在 Azure 密钥保管库中为 Azure 信息保护中的 Azure Rights Management 服务准备好了 HSM 密钥，接下来可以导入 AD RMS 配置数据。

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>步骤 2：将配置数据导入到 Azure 信息保护

由 Azure 信息保护的管理员完成这些过程。

1.  在连接 Internet 的工作站和 PowerShell 会话中，通过使用 [Connnect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) cmdlet 连接到 Azure Rights Management。
    
    然后通过使用 [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) cmdlet 上传首先导出的受信任发布域 (.xml) 文件。 如果你有多个 .xml 文件（因为有多个受信任发布域），请选择包含与 HSM 密钥对应的已导出受信任发布域的文件，你要在 Azure RMS 中使用该文件来在迁移后保护内容。 
    
    若要运行此 cmdlet，将需要在上一步中标识的密钥的 URL。
    
    例如，使用上一步的密钥 URL 值和 TPD 文件 C:\contoso-tpd1.xml，将运行：
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```
    
    出现提示时，输入你先前指定的密码，并确认要执行此操作。

2.  该命令完成后，请对通过导出受信任的发布域所创建的每个剩余 .xml 文件重复执行步骤 1。 例如，如果已将 AD RMS 群集升级到加密模式 2，则至少应拥有一个要导入的其他文件。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。  

3.  使用 [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > 如果之后需要确认正在 Azure 密钥保管库中使用的 Azure 信息保护租户密钥，请使用 [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) Azure RMS cmdlet。

现在可以转到[步骤 5：激活 Azure 信息保护租户](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
