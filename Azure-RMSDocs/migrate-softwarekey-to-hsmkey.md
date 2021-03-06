---
title: 将软件保护密钥迁移到 HSM 保护密钥 - AIP
description: 此说明是从 AD RMS 到 Azure 信息保护的迁移路径中的一部分，仅当你的 AD RMS 密钥是软件保护密钥，且希望使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护时才适用。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ca88715d32b3f5e7564c8382b8a63cd41d13140e
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386451"
---
# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>步骤 2：软件保护密钥到 HSM 保护密钥的迁移

>***适用** 于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当你的 AD RMS 密钥是软件保护密钥，且希望使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回到 [步骤4。从 AD RMS 导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) ，然后选择其他配置。

此过程分为四部分，可将 AD RMS 配置导入到 Azure 信息保护，以在 Azure 密钥保管库中生成由你管理的 Azure 信息保护租户密钥 (BYOK)。

必须首先从 AD RMS 配置数据中提取服务器许可方证书 (SLC) 密钥，然后将该密钥传输到本地 nCipher HSM，接下来，将 HSM 密钥传输到 Azure Key Vault，然后授权 azure 信息保护中的 Azure Rights Management 服务访问密钥保管库，然后导入配置数据。

因为你的 Azure 信息保护租户密钥将由 Azure 密钥保管库存储并进行管理，所以除 Azure 信息保护以外，此部分的迁移还需要 Azure 密钥保管库中的管理。 如果 Azure Key Vault 由你以外的其他管理员为贵组织进行管理，则你必须与该管理员协作完成这些过程。

在开始之前，请确保你的组织有一个已在 Azure 密钥保管库中创建的密钥保管库，且该保管库支持 HSM 保护的密钥。 尽管不是必需的，但我们建议你有一个专用于 Azure 信息保护的密钥保管库。 此密钥保管库将配置为允许 Azure 信息保护中的 Azure Rights Management 服务访问，所以此密钥保管库存储的密钥应限制为仅适用于 Azure 信息保护密钥。


> [!TIP]
> 如果即将对 Azure 密钥保管库执行配置步骤，而尚不熟悉此 Azure 服务，则可能会发现先阅读 [Azure Key Vault 入门](/azure/key-vault/key-vault-get-started)可能会有所帮助。 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>第 1 部分：从配置数据中提取 SLC 密钥，并将密钥导入到本地 HSM

1.  Azure Key Vault 管理员：对于想存储在 Azure Key Vault 中的每个导出的 SLC 密钥，请使用 Azure Key Vault 文档的[为 Azure Key Vault 实现自带密钥 (BYOK)](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault) 部分中的以下步骤：

    -   **生成密钥并将其传输到 AZURE KEY VAULT HSM**： [步骤1：准备连接到 internet 的工作站](/azure/key-vault/key-vault-hsm-protected-keys#step-1-prepare-your-internet-connected-workstation)

    -   **生成和传送你的租户密钥–通过 internet**： [步骤2：准备你的未连接工作站](/azure/key-vault/key-vault-hsm-protected-keys#step-2-prepare-your-disconnected-workstation)

    不用按照这些步骤生成租户密钥，因为你在导出的配置数据 (.xml) 文件中已有等效项。 你将改为运行工具以从该文件中提取此密钥并将其导入到本地 HSM。 在运行时，该工具将创建两个文件：

    - 新的不含密钥的配置数据文件（之后准备将其导入到你的 Azure 信息保护租户）。

    - 含密钥的 PEM 文件（为密钥容器，之后准备将其导入到你的本地 HSM）。

2. Azure 信息保护管理员或 Azure 密钥保管库管理员：在未连接工作站上，从 [Azure RMS migration toolkit](https://go.microsoft.com/fwlink/?LinkId=524619)（Azure RMS 迁移工具包）中运行 TpdUtil 工具。 例如，在 E 驱动器（在此驱动器上复制名为 ContosoTPD.xml 的配置数据文件）上安装了该工具时：

    ```PowerShell
    E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    如果你有多个 RMS 配置数据文件，请对这些文件的其余部分运行此工具。

    若要查看有关该工具的帮助（包含说明、用法和示例），请运行不带参数的 TpdUtil.exe

    此命令的其他信息：

    - **/Tpd**：指定导出的 AD RMS 配置数据文件的完整路径和名称。 参数的全称是 **TpdFilePath**。

    - **/Otpd**：指定不带密钥的配置数据文件的输出文件名。 参数的全称是 **OutPfxFile**。 如果不指定此参数，默认输出文件为带有后缀 **_keyless** 的原始文件名，且将其存储在当前文件夹中。

    - **/Opem**：指定 PEM 文件的输出文件名，其中包含提取的密钥。 参数的全称是 **OutPemFile**。 如果不指定此参数，默认输出文件为带有后缀 **_key** 的原始文件名，且将其存储在当前文件夹中。

    - 如果运行此命令（通过使用 TpdPassword 参数全称或 pwd 参数简称）时未指定密码，那么系统将提示你指定它。

3. 在同一工作站上，根据 nCipher 文档附加和配置 nCipher HSM。 你现在可以使用以下命令将你的密钥导入到附加的 nCipher HSM 中，你需要将自己的文件名替换为 Contosotpd.pem：

    ```sh
    generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA
    ```

    > [!NOTE]
    >如果有多个文件，请选择与 HSM 密钥对应的文件，你要在 Azure RMS 中使用该文件以在迁移后保护内容。

    这将生成与以下类似的输出显示：

    **密钥生成参数：**

    **&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 执行 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 导入操作的操作操作**

    **应用 &nbsp; &nbsp; &nbsp; &nbsp; 程序应用程序 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 简单**

    **验证 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 验证配置密钥的安全性 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 是**

    **类型 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 键类型 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; RSA**

    **&nbsp; &nbsp; 包含 RSA key e:\ContosoTPD.pem 的 pemreadfile PEM 文件 &nbsp; &nbsp;**

    **ident &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 密钥标识符 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; contosobyok**

    **plainname &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 密钥名称 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ContosoBYOK**

    **已成功导入密钥。**

    **密钥路径：C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

此输出确认已将私钥迁移到本地 nCipher HSM 设备，并使用保存到密钥 (在本示例中为 "key_simple_contosobyok" ) 的加密副本。 

现已提取 SLC 密钥，并将其导入到本地 HSM，可以打包 HSM 保护的密钥并将其传送到 Azure 密钥保管库。

> [!IMPORTANT]
> 完成此步骤后，从未连接工作站安全地清除这些 PEM 文件，以确保未经授权的人员不能访问这些文件。 例如，运行“cipher /w: E”安全地从 E: 驱动器删除所有文件。

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>第 2 部分：打包 HSM 密钥并将其传送到 Azure 密钥保管库

Azure Key Vault 管理员：对于想存储在 Azure Key Vault 中的每个导出的 SLC 密钥，请使用 Azure Key Vault 文档的[为 Azure Key Vault 实现自带密钥 (BYOK)](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault) 部分中的以下步骤：

- [步骤 4：准备要传输的密钥](/azure/key-vault/key-vault-hsm-protected-keys#step-4-prepare-your-key-for-transfer)

- [步骤 5：将密钥传输到 Azure 密钥保管库](/azure/key-vault/key-vault-hsm-protected-keys#step-5-transfer-your-key-to-azure-key-vault)

请勿按照这些步骤来生成你的密钥对，因为你已经具有该密钥。 而是运行命令从本地 HSM 传送此密钥（本例中，KeyIdentifier 参数使用“contosobyok”）。

将密钥传送到 Azure 密钥保管库之前，请确保在创建具有降低的权限的密钥副本（步骤 4.1）时，以及在加密密钥（步骤 4.3）时，KeyTransferRemote.exe 实用工具返回“结果：成功”。

将密钥上传到 Azure 密钥保管库时，可以看到显示的密钥属性，其中包括密钥 ID。 它的外观将类似于 **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** 。 请记下此 URL，因为 Azure 信息保护管理员需要用它命令 Azure 信息保护中的 Azure Rights Management 服务将此密钥用作租户密钥。

然后使用 [AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) cmdlet 来授权 Azure Rights Management 服务主体访问密钥保管库。 所需的权限有解密、加密、unwrapkey、wrapkey、验证和签名。

例如，如果你为 Azure 信息保护创建的密钥保管库名为 contosorms-byok-kv，并且资源组名为 **contosorms-byok**，请运行以下命令：

```sh
Set-AzKeyVaultAccessPolicy -VaultName "contosorms-byok-kv" -ResourceGroupName "contosorms-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get
```

现在，你已将 HSM 密钥传送到 Azure 密钥保管库，接下来可以导入 AD RMS 配置数据。

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>步骤 3：将配置数据导入到 Azure 信息保护

1. Azure 信息保护管理员：在连接 internet 的工作站和 PowerShell 会话中，复制新的配置数据文件 ( 在运行 TpdUtil 工具后删除了 SLC 密钥的) 。

2. 使用 [AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd) cmdlet 上传每个 .xml 文件。 例如，如果已将 AD RMS 群集升级到加密模式 2，则至少应拥有一个要导入的其他文件。

    若要运行此 cmdlet，需要先前为配置数据文件指定的密码以及在上一步中标识的密钥的 URL。

    例如，使用 C:\contoso_keyless.xml 配置数据文件和我们上一步中的密钥 URL 值，首先运行以下命令以存储密码：
    
    ```PowerShell
    $TPD_Password = Read-Host -AsSecureString
    ```
    
   输入指定的密码以导出配置数据文件。 然后，运行以下命令并确认希望执行此操作：

    ```PowerShell
    Import-AipServiceTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```

    作为此导入的一部分，将导入 SLC 密钥并且密钥将被自动设置为已存档。

3. 上传每个文件后，请运行 [AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) 以指定与 AD RMS 群集中当前活动的 SLC 密钥相匹配的导入密钥。

4. 使用 [AipServiceService](/powershell/module/aipservice/disconnect-aipservice) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```PowerShell
    Disconnect-AipServiceService
    ```

如果以后需要确认 Azure 信息保护租户密钥在 Azure Key Vault 中使用的密钥，请使用 [AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) Azure RMS cmdlet。


你现在已准备好进入 [步骤5。激活 Azure Rights Management 服务](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)。


