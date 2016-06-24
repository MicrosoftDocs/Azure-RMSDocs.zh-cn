---
# required metadata

title: 步骤 2&colon; HSM 保护密钥到 HSM 保护密钥的迁移 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 步骤 2：HSM 保护密钥到 HSM 保护密钥的迁移

*适用于：Active Directory Rights Management Services、Azure Rights Management*


这些说明是[从 AD RMS 到 Azure Rights Management 的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当你的 AD RMS 密钥是 HSM 保护密钥，且你希望使用 HSM 保护的租户密钥迁移到 Azure Rights Management 时才适用。 

如果这不是你选择的配置方案，请返回[步骤 2.从 AD RMS 中导出配置数据并将其导入到 Azure RMS 中](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)，然后选择其他配置。

> [!NOTE]
> 这些说明假定你的 AD RMS 密钥受模块保护。 这是常见的情况。 如果你的 AD RMS 密钥受 OCS 保护，请在按这些说明操作之前联系 [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key)。

此过程分为两部分，可将 HSM 密钥和 AD RMS 配置导入到 Azure RMS，以生成由你管理的 Azure RMS 租户密钥 (BYOK)。

你必须先打包 HSM 密钥以便随时可将其传输到 Azure RMS，然后再将其连同配置数据一起导入。

## 第 1 部分：打包 HSM 密钥以便随时可将其传输到 Azure RMS

1.  使用过程**生成并传输租户密钥 - 通过 Internet**，并按照[计划和实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md)中的“实现自带密钥 (BYOK)”[](plan-implement-tenant-key.md#BKMK_ImplementBYOK)部分中的步骤进行操作，但以下情况例外：

    -   不要遵循 **生成你的租户密钥**中的步骤，因为你已从 AD RMS 部署获得等效物。 你必须标识 AD RMS 服务器使用的从 Thales 安装获得的密钥，并在迁移期间使用此密钥。 Thales 加密的密钥文件通常在本地服务器上名为 **key_(keyAppName)_(keyIdentifier)**。

    -   不要遵循**将你的租户密钥传送到 Azure RMS** 中的步骤，因为此操作使用 Add-AadrmKey 命令。  你应该在上载所导出的受信任发布域时，使用 Import-AadrmTpd 命令传输你准备好的 HSM 密钥。

2.  在已连接 Internet 的工作站上，通过 Windows PowerShell 会话重新连接到 Azure RMS 服务。

现在，你已经为 Azure RMS 准备好了 HSM 密钥，接下来可以导入 HSM 密钥文件和 AD RMS 配置数据。

## 第 2 部分：将 HSM 密钥和配置数据导入到 Azure RMS

1.  仍在连接 Internet 的工作站上的 Windows PowerShell 会话中，上载首先导出的受信任发布域 (.xml) 文件。 如果你有多个 .xml 文件（因为有多个受信任发布域），请选择包含与 HSM 密钥对应的已导出受信任发布域的文件，你要在 Azure RMS 中使用该文件来在迁移后保护内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    例如：**Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    出现提示时，输入你先前指定的密码，并确认要执行此操作。

2.  该命令完成后，请对你通过导出受信任发布域创建的每个剩余 .xml 文件重复执行步骤 1。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。  例如：**Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet 断开与 Azure RMS 服务的连接：

    ```
    Disconnect-AadrmService
    ```

现在可以转到[步骤 3。激活你的 RMS 租户](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).



<!--HONumber=Apr16_HO4-->


