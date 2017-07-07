---
title: "对 Azure RMS 数据保护的服务器支持 - AIP"
description: "通过使用 Rights Management 连接器识别可使用 Azure 信息保护中的 Azure Rights Management 服务的本地服务器产品。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/22/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 87e887bb121b3d92065153a5d264767ef87d517b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的本地服务器

>*适用于：Azure 信息保护、Office 365*

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
    > 你也可以在运行更高版本的 Windows Server 的服务器上使用这些 cmdlet，好处是这些 cmdlet 可以保护所有文件类型。 RMS 连接器仅保护 Office 文件。 有关操作说明，请参阅[使用 Windows Server 文件分类基础结构 &#40;FCI&#41; 的 RMS 保护](../rms-client/configure-fci.md)。

Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 支持 Rights Management 连接器。

有关如何为这些本地服务器配置 Rights Management 连接器的详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

## <a name="next-steps"></a>后续步骤
若要查看其他要求，请参阅 [Azure Rights Management 的要求](requirements-azure-rms.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]