---
title: 将软件保护密钥迁移到软件保护密钥 - AIP
description: 此说明是从 AD RMS 到 Azure 信息保护的迁移路径中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ee5ee97c6ff7a1bc3f817fa5ce6a086e7e691dd4
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255455"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>步骤 2：软件保护密钥到软件保护密钥的迁移

>适用范围：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回[步骤 4：从 AD RMS 中导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) 中，然后选择其他配置。

使用以下步骤将 AD RMS 配置导入到 Azure 信息保护，以生成由 Microsoft 管理的 Azure 信息保护租户密钥。

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>将配置数据导入 Azure 信息保护

1. 在连接 Internet 的工作站上，使用 [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) cmdlet 连接到 Azure Rights Management 服务：

    ```
    Connect-AadrmService
    ```
    出现提示时，输入 Azure Rights Management 租户管理员凭据（通常，你将使用作为 Azure Active Directory 或 Office 365 全局管理员的帐户）。

2. 使用 [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) cmdlet 上传每个导出的受信任的发布域 (.xml) 文件。 例如，如果已将 AD RMS 群集升级到加密模式 2，则至少应拥有一个要导入的其他文件。 
    
    若要运行此 cmdlet，需要先前为每个配置数据文件指定的密码。 
    
    例如，首先运行以下命令以存储密码：
    
        $TPD_Password = Read-Host -AsSecureString
    
    输入指定的密码以导出第一个配置数据文件。 然后，使用 E:\contosokey1.xml 作为示例配置文件，运行以下命令并确认希望执行此操作：
    ```
    Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. 在上传完每个文件后，请运行 [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) 以标识与 AD RMS 中当前活动的 SLC 密钥相匹配的导入的密钥。 该密钥将成为 Azure 权限管理服务的活动租户密钥。

4.  使用 [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```
    Disconnect-AadrmService
    ```

现在可以转到[步骤 5：激活 Azure 权限管理服务](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)。


