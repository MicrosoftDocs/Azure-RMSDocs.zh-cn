---
title: "将软件保护密钥迁移到软件保护密钥 - AIP"
description: "此说明是从 AD RMS 到 Azure 信息保护的迁移路径中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 60370cc34184b28f5cdecf6ad51f9ba58dd4816a
ms.sourcegitcommit: 77b0936bea2700eb12b580e5738e077d447d5686
translationtype: HT
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>步骤 2：软件保护密钥到软件保护密钥的迁移

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*


此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回[步骤 4：从 AD RMS 中导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) 中，然后选择其他配置。

使用以下步骤将 AD RMS 配置导入到 Azure 信息保护，以生成由 Microsoft 管理的 Azure 信息保护租户密钥。

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>将配置数据导入 Azure 信息保护

1. 在连接 Internet 的工作站上，使用 [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) cmdlet 连接到 Azure Rights Management 服务：

    ```
    Connect-AadrmService
    ```
    出现提示时，输入 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。

2. 使用 [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) cmdlet 上载首先导出的受信任发布域 (.xml) 文件。 如果有多个 .xml 文件（因为有多个受信任的发布域），请选择包含已导出的受信任发布域的文件，在 Azure 信息保护中使用该文件来保护迁移后的内容。 使用以下命令：

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword <secure string> -Active $True -Verbose
    ```
    可以使用 [ConvertTo-SecureString -AsPlaintext](https://technet.microsoft.com/library/hh849818.aspx) 或 [Read-Host](https://technet.microsoft.com/library/hh849945.aspx) 指定密码作为安全字符串。 使用 ConvertTo-SecureString 并且密码具有特殊字符时，在单引号之间输入密码或转义特殊字符。
    
    例如：首先运行 **$TPD_Password = Read-host-AsSecureString**，并输入早前指定的密码。 然后运行 **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Active $true -Verbose**。 出现提示时，确认要执行此操作。
    
3.  该命令完成后，请对你通过导出受信任的发布域创建的每个剩余 .xml 文件重复执行步骤 3。 例如，如果已将 AD RMS 群集升级到加密模式 2，则至少应拥有一个要导入的其他文件。 但对于这些文件，在运行 Import 命令时将 **-Active** 设为 **false**。 例如：**Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword $TPD_Password -Active $false -Verbose**

4.  使用 [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```
    Disconnect-AadrmService
    ```


现在可以转到[步骤 5：激活 Azure 信息保护租户](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

