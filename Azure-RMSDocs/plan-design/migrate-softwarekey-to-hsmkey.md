---
# required metadata

title: 步骤 2：软件保护密钥到 HSM 保护密钥的迁移 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 步骤 2：软件保护密钥到 HSM 保护密钥的迁移

这些说明是[从 AD RMS 到 Azure Rights Management 的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当你的 AD RMS 密钥是软件保护密钥，且你希望使用 HSM 保护的租户密钥迁移到 Azure Rights Management 时才适用。 

如果这不是你选择的配置方案，请返回[步骤 2.从 AD RMS 中导出配置数据并将其导入到 Azure RMS 中](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)，然后选择其他配置。

此过程分为三部分，用于将 AD RMS 配置导入到 Azure RMS，以生成由你管理的 Azure RMS 租户密钥 (BYOK)。

必须首先从配置数据中提取服务器许可方证书 (SLC) 密钥并将该密钥传输到本地 Thales HSM，然后打包 HSM 密钥并将其传输到 Azure RMS，最后导入配置数据。

## 第 1 部分：从配置数据中提取 SLC，并将密钥导入到本地 HSM

1.  按照[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)主题中的“实现自带密钥 (BYOK)”[](plan-implement-tenant-key.md#BKMK_ImplementBYOK)部分中的以下步骤进行操作：

    -   **生成和传送租户密钥 – 通过 Internet**：**准备连接你的 Internet 的工作站**

    -   **生成和传送租户密钥 – 通过 Internet**： **准备你的未连接工作站**

    不用按照这些步骤生成租户密钥，因为你在导出的配置数据 (.xml) 文件中已有等效项。 你将改为运行命令以从该文件中提取此密钥并将其导入到本地 HSM。

2.  在断开连接的工作站上，运行以下命令：

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    例如，对于北美地区：**KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    其他信息:

    -   ImportRmsCentrallyManagedKey 参数指示该操作是导入 SLC 密钥。

    -   如果你未在命令中指定密码，则将提示你指定它。

    -   KeyIdentifier 参数指定用于创建密钥文件名的密钥友好名称。 你必须使用仅小写的 ASCII 字符。

    -   ExchangeKeyPackage 参数指定特定于区域的密钥交换密钥 (KEK) 软件包，该软件包的名称以“BYOK-KEK-pkg-”开头。

    -   NewSecurityWorldPackage 参数指定特定于区域的安全体系包，该包的名称以“BYOK-SecurityWorld-pkg-”开头。

    此命令将生成以下项：

    -   HSM 密钥文件：%NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   已删除 SLC 的 RMS 配置数据文件：%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  如果你有多个 RMS 配置数据文件，请对这些文件的其余部分重复执行步骤 2。

现在，你已提取 SLC 使其成为基于 HSM 的密钥，你已可以将其打包并传输到 Azure RMS 了。

## 第 2 部分：打包 HSM 密钥并将其传输到 Azure RMS

1.  按照[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)中的[实现自带密钥 (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) 部分中的以下步骤进行操作：

    -   **生成和传送租户密钥 – 通过 Internet**： **准备要传送的租户密钥**

    -   **生成和传送租户密钥 – 通过 Internet**： **将你的租户密钥传送到 Azure RMS**

现在，你已将 HSM 密钥传输到 Azure RMS，已可以导入 AD RMS 配置数据（其中只包含指向新传输的租户密钥的指针）了。

## 第 3 部分：将配置数据导入到 Azure RMS

1.  仍在连接 Internet 的工作站上的 Windows PowerShell 会话中，从断开连接的工作站复制删除了 SLC 的 RMS 配置文件 (%NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  上载第一个文件。 如果你有多个 .xml 文件（因为有多个受信任发布域），请选择包含与 HSM 密钥对应的已导出受信任发布域的文件，你要在 Azure RMS 中使用该文件来在迁移后保护内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    例如：**Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    出现提示时，输入你先前指定的密码，并确认要执行此操作。

3.  该命令完成后，请对你通过导出受信任发布域创建的每个剩余 .xml 文件重复执行步骤 2。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。 例如：**Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet 断开与 Azure RMS 服务的连接：

    ```
    Disconnect-AadrmService
    ```

现在可以转到[步骤 3。激活你的 RMS 租户](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)。




<!--HONumber=Apr16_HO3-->


