---
title: "步骤 2&colon; 软件保护密钥到软件保护密钥的迁移 | Azure 信息保护"
description: "此说明是从 AD RMS 到 Azure 信息保护的迁移路径中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 931642ea9070a7581b428bcd04756048673fe3c0
ms.openlocfilehash: e6bffd31e7f198a767531fb343b8146246078004


---


# 步骤 2：软件保护密钥到软件保护密钥的迁移

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*


此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回[步骤 2.从 AD RMS 中导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) 中，然后选择其他配置。

使用以下步骤将 AD RMS 配置导入到 Azure 信息保护，以生成由 Microsoft 管理的 Azure 信息保护租户密钥。

## 将配置数据导入 Azure 信息保护

1.  在连接 Internet 的工作站上，下载并安装用于 Azure Rights Management 的 Windows PowerShell 模块（最低版本 2.5.0.0），其中包括 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet。 Azure Rights Management 服务 (Azure RMS) 为 Azure 信息保护提供数据保护服务。

    > [!TIP]
    > 如果你以前已下载并安装过该模块，请通过运行以下命令检查版本号： `(Get-Module aadrm -ListAvailable).Version`

    有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。

2.  使用“以管理员身份运行”  选项启动 Windows PowerShell，然后使用 [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) cmdlet 连接到 Azure RMS 服务：

    ```
    Connect-AadrmService
    ```
    出现提示时，输入 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。

3.  使用 [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) cmdlet 上载首先导出的受信任发布域 (.xml) 文件。 如果有多个 .xml 文件（因为有多个受信任的发布域），请选择包含已导出的受信任发布域的文件，在 Azure 信息保护中使用该文件来保护迁移后的内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    可以使用 [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) 或 [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) 指定密码作为安全字符串。 使用 ConvertTo-SecureString 并且密码具有特殊字符时，在单引号之间输入密码或转义特殊字符。
    
    例如：首先运行 **$TPD_Password = Read-host-AsSecureString**，并输入早前指定的密码。 然后运行 **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**。 出现提示时，确认要执行此操作。
    
4.  该命令完成后，请对你通过导出受信任的发布域创建的每个剩余 .xml 文件重复执行步骤 3。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。 例如：**Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

5.  使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```
    Disconnect-AadrmService
    ```


现在可以转到[步骤 3。激活 Azure 信息保护租户](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)。





<!--HONumber=Sep16_HO4-->


