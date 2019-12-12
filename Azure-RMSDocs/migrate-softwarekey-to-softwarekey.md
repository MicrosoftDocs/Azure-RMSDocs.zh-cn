---
title: 将软件保护密钥迁移到软件保护密钥 - AIP
description: 此说明是从 AD RMS 到 Azure 信息保护的迁移路径中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6b96c9d12277ec85ca1a726907eb5d8c6ca7c391
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935412"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>步骤 2：软件保护密钥到软件保护密钥的迁移

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)


此说明是[从 AD RMS 到 Azure 信息保护的迁移路径](migrate-from-ad-rms-to-azure-rms.md)中的一部分，仅当 AD RMS 密钥是软件保护密钥，且希望使用软件保护租户密钥迁移到 Azure 信息保护时才适用。 

如果这不是你选择的配置方案，请返回到[步骤4。从 AD RMS 导出配置数据并将其导入到 Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) ，然后选择其他配置。

使用以下步骤将 AD RMS 配置导入到 Azure 信息保护，以生成由 Microsoft 管理的 Azure 信息保护租户密钥。

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>将配置数据导入 Azure 信息保护

1. 在连接 internet 的工作站上，使用[AipService](/powershell/module/aipservice/connect-aipservice) cmdlet 连接到 Azure Rights Management 服务：

    ```
    Connect-AipService
    ```
    出现提示时，输入 Azure Rights Management 租户管理员凭据（通常，你将使用作为 Azure Active Directory 或 Office 365 全局管理员的帐户）。

2. 使用 AipServiceTpd cmdlet 上传每个导出[的](/powershell/module/aipservice/import-aipservicetpd)受信任发布域（.xml）文件。 例如，如果已将 AD RMS 群集升级到加密模式 2，则至少应拥有一个要导入的其他文件。 
    
    若要运行此 cmdlet，需要先前为每个配置数据文件指定的密码。 
    
    例如，首先运行以下命令以存储密码：
    
        $TPD_Password = Read-Host -AsSecureString
    
    输入指定的密码以导出第一个配置数据文件。 然后，使用 E:\contosokey1.xml 作为示例配置文件，运行以下命令并确认希望执行此操作：
    ```
    Import-AipServiceTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. 上传每个文件后，请运行[AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)以标识与 AD RMS 中当前活动的 SLC 密钥相匹配的已导入的密钥。 该密钥将成为 Azure 权限管理服务的活动租户密钥。

4.  使用[AipServiceService](/powershell/module/aipservice/disconnect-aipservice) cmdlet 断开与 Azure Rights Management 服务的连接：

    ```
    Disconnect-AipServiceService
    ```

你现在已准备好进入[步骤5。激活 Azure Rights Management 服务](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service)。


