---
# required metadata

title: 步骤 2：软件保护密钥到软件保护密钥的迁移 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# 步骤 2：软件保护密钥到软件保护密钥的迁移

这些说明是[从 AD RMS 到 Azure Rights Management 的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当你的 AD RMS 密钥是软件保护密钥，且你希望使用软件保护的租户密钥迁移到 Azure Rights Management 时才适用。 

如果这不是你选择的配置方案，请返回[步骤 2.从 AD RMS 中导出配置数据并将其导入到 Azure RMS 中](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)，然后选择其他配置。

使用以下过程将 AD RMS 配置导入到 Azure RMS，以生成由 Microsoft 管理的 Azure RMS 租户密钥。

## 将配置数据导入到 Azure RMS

1.  在连接 Internet 的工作站上，下载并安装用于 Azure RMS 的 Windows PowerShell 模块（最低版本 2.1.0.0），其中包括 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet。

    > [!TIP]
    > 如果你以前已下载并安装过该模块，请通过运行以下命令检查版本号： `(Get-Module aadrm -ListAvailable).Version`

    有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。

2.  使用“以管理员身份运行” **** 选项启动 Windows PowerShell，然后使用 [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) cmdlet 连接到 Azure RMS 服务：

    ```
    Connect-AadrmService
    ```
    出现提示时，输入 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。

3.  使用 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet 上载首先导出的受信任发布域 (.xml) 文件。 如果你有多个 .xml 文件（因为有多个受信任发布域），请选择包含已导出受信任发布域的文件，你要在 Azure RMS 中使用该文件来在迁移后保护内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    例如：**Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    出现提示时，输入你先前指定的密码，并确认要执行此操作。

4.  该命令完成后，请对你通过导出受信任发布域创建的每个剩余 .xml 文件重复执行步骤 3。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。 例如：**Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) cmdlet 断开与 Azure RMS 服务的连接：

    ```
    Disconnect-AadrmService
    ```

现在可以转到[步骤 3。激活你的 RMS 租户](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration)。



<!--HONumber=Apr16_HO3-->


