---
title: 对 Azure RMS 数据保护的服务器支持 - AIP
description: 通过使用 Rights Management 连接器识别可使用 Azure 信息保护中的 Azure Rights Management 服务的本地服务器产品。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8e160908ac568b0657cc92b838959eb95da624b3
ms.sourcegitcommit: a26d033ccd557839b61736284456370393f3b52a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67156655"
---
# <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的本地服务器

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用 Azure Rights Management 连接器时 Azure 信息保护支持以下本地服务器产品。 该连接器充当本地服务器和 Azure Rights Management 服务（Azure 信息保护使用该服务保护 Office 文档和电子邮件）之间的通信接口（中继）。 

若要使用该连接器，必须配置 Active Directory 林和 Azure Active Directory 之间的目录同步。

-   **Exchange Server**：

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**：

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器**：

    -   Windows Server 2016

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > 由于运行 Windows Server 2008 R2 的文件服务器未使用内置文件管理任务操作来应用 Rights Management 保护，在这种情况下，不能使用 Rights Management 连接器。 但是，如果你配置自定义文件管理任务以运行可通过使用 Azure RMS 来保护文件的可执行文件或脚本，则可以在这些操作系统上使用文件分类基础结构和 Azure RMS。 例如，使用 [AzureInformationProtection cmdlet](/powershell/azureinformationprotection/vlatest/aip) 的 Windows PowerShell 脚本。
    > 
    > 你也可以在运行更高版本的 Windows Server 的服务器上使用这些 cmdlet，好处是这些 cmdlet 可以保护所有文件类型。 RMS 连接器仅保护 Office 文件。 有关操作说明，请参阅[使用 Windows Server 文件分类基础结构 &#40;FCI&#41; 的 RMS 保护](./rms-client/configure-fci.md)。

Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 支持 Rights Management 连接器。

有关如何为这些本地服务器配置 Rights Management 连接器的详细信息，请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

## <a name="next-steps"></a>后续步骤
若要查看其他要求，请参阅 [Azure Rights Management 的要求](requirements.md)。
