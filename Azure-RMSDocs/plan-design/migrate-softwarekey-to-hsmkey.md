---
title: "将软件保护密钥迁移到 HSM 保护密钥 - AIP"
description: "此说明是从 AD RMS 到 Azure 信息保护的迁移路径中的一部分，仅当你的 AD RMS 密钥是软件保护密钥，且希望使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护时才适用。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3b9350462f363ed365c3f37aabad79ce7338b531
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>步骤 2：软件保护密钥到 HSM 保护密钥的迁移

>*适用于：Active Directory Rights Management Services、Azure 信息保护*


此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当你的 AD RMS 密钥是软件保护密钥，且希望使用 Azure 密钥保管库中 HSM 保护的租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回[步骤 2.从 AD RMS 中导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) 中，然后选择其他配置。

此过程分为四部分，可将 AD RMS 配置导入到 Azure 信息保护，以在 Azure 密钥保管库中生成由你管理的 Azure 信息保护租户密钥 (BYOK)。

必须首先从 AD RMS 配置数据中提取服务器许可方证书 (SLC) 密钥并将该密钥传送到本地 Thales HSM，然后打包 HSM 密钥并将其传送到 Azure 密钥保管库，之后授权 Azure 信息保护中的 Azure Rights Management 服务可以访问密钥保管库，最后导入配置数据。

因为你的 Azure 信息保护租户密钥将由 Azure 密钥保管库存储并进行管理，所以除 Azure 信息保护以外，此部分的迁移还需要 Azure 密钥保管库中的管理。 如果 Azure 密钥保管库由你以外的管理员为你的组织管理，则你需要与该管理员协作完成这些过程。

在开始之前，请确保你的组织有一个已在 Azure 密钥保管库中创建的密钥保管库，且该保管库支持 HSM 保护的密钥。 尽管不是必需的，但我们建议你有一个专用于 Azure 信息保护的密钥保管库。 此密钥保管库将配置为允许 Azure 信息保护中的 Azure Rights Management 服务访问，所以此密钥保管库存储的密钥应限制为仅适用于 Azure 信息保护密钥。


> [!TIP]
> 如果你将对 Azure 密钥保管库执行配置步骤，而尚不熟悉此 Azure 服务，你可能会发现先阅读 [Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)（Azure 密钥保管库入门）可能会有所帮助。 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>第 1 部分：从配置数据中提取 SLC 密钥，并将密钥导入到本地 HSM

1.  Azure 密钥保管库管理员：使用 Azure 密钥保管库文档的 [Implementing bring your own key (BYOK) for Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault)（为 Azure 密钥保管库实施自带密钥 (BYOK)）部分中的下列步骤：

    -   **生成密钥并将其传送到 Azure 密钥保管库 HSM**：[步骤 1：准备你的连接 Internet 的工作站](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **生成和传送租户密钥 - 通过 Internet**：[步骤 2：准备你的未连接工作站](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    不用按照这些步骤生成租户密钥，因为你在导出的配置数据 (.xml) 文件中已有等效项。 你将改为运行工具以从该文件中提取此密钥并将其导入到本地 HSM。 在运行时，该工具将创建两个文件：

    - 新的不含密钥的配置数据文件（之后准备将其导入到你的 Azure 信息保护租户）。

    - 含密钥的 PEM 文件（为密钥容器，之后准备将其导入到你的本地 HSM）。

2. Azure 信息保护管理员或 Azure 密钥保管库管理员：在未连接工作站上，从 [Azure RMS migration toolkit](https://go.microsoft.com/fwlink/?LinkId=524619)（Azure RMS 迁移工具包）中运行 TpdUtil 工具。 例如，在 E 驱动器（在此驱动器上复制名为 ContosoTPD.xml 的配置数据文件）上安装了该工具时：

    ```
        E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    如果你有多个 RMS 配置数据文件，请对这些文件的其余部分运行此工具。

    若要查看有关该工具的帮助（包含说明、用法和示例），请运行不带参数的 TpdUtil.exe

    此命令的其他信息：

    - **/Tpd**：指定导出的 AD RMS 配置数据文件的完整路径和名称。 参数的全称是 **TpdFilePath**。

    - **/Otpd**：指定不带密钥的配置数据文件的输出文件名。 参数的全称是 **OutPfxFile**。 如果不指定此参数，默认输出文件为带有后缀 **_keyless** 的原始文件名，且将其存储在当前文件夹中。

    - **/Opem**：指定 PEM 文件的输出文件名，其中包含提取的密钥。 参数的全称是 **OutPemFile**。 如果不指定此参数，默认输出文件为带有后缀 **_key** 的原始文件名，且将其存储在当前文件夹中。

    - 如果运行此命令（通过使用 **TpdPassword** 参数全称或 **pwd** 参数简称）时未指定密码，那么系统将提示你指定它。

3. 在同一个未连接工作站上，按照 Thales 文档附加并配置 Thales HSM。 通过使用以下命令现可以将你的密钥导入到附加 Thales HSM 中，需要将命令中的 ContosoTPD.pem 替换为你自己的文件名称：

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >如果有多个文件，请选择与 HSM 密钥对应的文件，你要在 Azure RMS 中使用该文件以在迁移后保护内容。

    这将生成与以下类似的输出显示：

    **密钥生成参数：**

    **操作 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 要执行的操作 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 导入**

    **应用程序 &nbsp;&nbsp;&nbsp;&nbsp; 应用程序&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 简单**

    **验证 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 验证配置密钥的安全性 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 是**

    **类型 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 密钥类型 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; 包含 RSA 密钥的 PEM 文件 &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 密钥标识符 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 密钥名称 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **已成功导入密钥。**

    **密钥路径：C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

此输出确认现已将私钥迁移到本地 Thales HSM 设备，附有保存到一个密钥的加密副本（在本例中为“key_simple_contosobyok”）。 

现已提取 SLC 密钥，并将其导入到本地 HSM，可以打包 HSM 保护的密钥并将其传送到 Azure 密钥保管库。

> [!IMPORTANT]
> 完成此步骤后，从未连接工作站安全地清除这些 PEM 文件，以确保未经授权的人员不能访问这些文件。 例如，运行“cipher /w:E”安全地从 E: 驱动器删除所有文件。

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>第 2 部分：打包 HSM 密钥并将其传送到 Azure 密钥保管库

1.  Azure 密钥保管库管理员：使用 Azure 密钥保管库文档的 [Implementing bring your own key (BYOK) for Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault)（为 Azure 密钥保管库实施自带密钥 (BYOK)）部分中的下列步骤：

    -   [步骤 4：准备要传送的密钥](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

    -   [步骤 5：将密钥传送到 Azure 密钥保管库](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azure-key-vault)

    请勿按照这些步骤来生成你的密钥对，因为你已经具有该密钥。 而是运行命令从本地 HSM 传送此密钥（本例中，KeyIdentifier 参数使用“contosobyok”）。

    将密钥传送到 Azure 密钥保管库之前，请确保在创建具有降低的权限的密钥副本（步骤 4.1）时，以及在加密密钥（步骤 4.3）时，KeyTransferRemote.exe 实用工具返回“结果：成功”。

    将密钥上传到 Azure 密钥保管库时，可以看到显示的密钥属性，其中包括密钥 ID。 类似于 **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**。 请记下此 URL，因为 Azure 信息保护管理员需要用它命令 Azure 信息保护中的 Azure Rights Management 服务将此密钥用作租户密钥。

    现在，你已将 HSM 密钥传送到 Azure 密钥保管库，接下来可以导入 AD RMS 配置数据。

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>步骤 3：将配置数据导入到 Azure 信息保护

1.  Azure 信息保护管理员：在连接 Internet 的工作站和 PowerShell 会话中，复制在运行 TpdUtil 工具后删除了 SLC 密钥的新配置数据文件 (.xml)。

2. 使用 [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx) cmdlet 上传第一个.xml 文件。 如果有多个这些文件（因为有多个受信任的发布域），请选择要与 Azure 信息保护配合使用的 HSM 密钥相对应的文件，以在迁移后保护内容。

    若要运行此 cmdlet，将需要在上一步中标识的密钥的 URL。

    例如，使用上一步的密钥 URL 值和配置数据文件 C:\contoso_keyless.xml，将运行：

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```

    出现提示时，输入你先前为配置数据文件指定的密码，并确认要执行此操作。

    如果你有多个配置数据文件，请对这些文件的其余部分重复运行此命令。 例如，如果已将 AD RMS 群集升级到加密模式 2，则至少应拥有一个要导入的其他文件。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。



3.  使用 [Disconnect-AadrmService](https://msdn.microsoft.com/library/azure/dn629416.aspx) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > 如果之后需要确认正在 Azure 密钥保管库中使用的 Azure 信息保护租户密钥，请使用 [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) Azure RMS cmdlet。


现在可以转到[步骤 3。激活 Azure 信息保护租户](migrate-from-ad-rms-phase1.md#step-3-activate-your-azure-information-protection-tenant)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


