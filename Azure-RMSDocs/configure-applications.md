---
title: 为 Azure Rights Management 配置应用程序 - AIP
description: 有关管理员配置应用程序和服务以支持 Azure 信息保护的 Azure Rights Management 保护服务的说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 38853e038b708950228473e703e364e0a021ec6e
ms.sourcegitcommit: 8499602fba94fbfa28d7682da2027eeed6583c61
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83746357"
---
# <a name="configuring-applications-for-azure-rights-management"></a>为 Azure Rights Management 配置应用程序

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> 此信息适用于已部署了 Azure 信息保护的 IT 管理员和顾问。 如果你要寻找有关如何针对特定应用程序使用 Rights Management 功能，或者如何打开权限保护文件的用户帮助和信息，请使用你的应用程序附带的帮助和指南。
>
> 例如，对于 Office 应用程序，请单击帮助图标并输入搜索词，例如 **Rights Management** 或 **IRM**。 有关适用于 Windows 的 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端用户指南](./rms-client/client-user-guide.md)。

为组织部署 Azure 信息保护之后，请使用以下信息配置应用程序、Azure 信息保护客户端和服务。 例如，Word 2019、Word 2016 和 Word 2013 等 Office 应用程序。 还包括 Exchange Online （传输规则、数据丢失防护、请勿转发和消息加密）和 Microsoft SharePoint （受保护的库）等服务。 若要了解这些应用程序和服务如何支持 Azure 信息保护中的数据保护服务，请参阅[应用程序如何支持 Azure 权限管理服务](applications-support.md)。

> [!IMPORTANT]
> 有关支持的版本和其他要求的信息，请参阅[Azure 信息保护的要求](requirements.md)。

-   [Office 365：联机服务的配置](configure-office365.md)

    -   [Exchange Online：IRM 配置](configure-office365.md#exchangeonline-irm-configuration)

    -   [Microsoft 365 和 OneDrive 中的 SharePoint： IRM 配置](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)

- [Office 应用程序：客户端配置](configure-office-apps.md)

    -   [Office 365 应用、Office 2019、Office 2016 和 Office 2013](configure-office-apps.md#office365-apps-office-2019-office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office2010)

-   [Azure 信息保护客户端：安装和配置客户端](configure-client.md)

若要配置本地服务器（如 Exchange Server 和 SharePoint Server），请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

除了这些应用程序和服务外，还有一些支持 Rights Management API 的其他应用程序。 此类别包括使用 Rights Management SDK 内部编写的业务线应用程序，以及来自软件供应商的使用 Rights Management SDK 编写的应用程序。 对于这些应用程序，请按照应用程序随附的说明操作。

## <a name="next-steps"></a>后续步骤
将应用程序配置为支持 Azure Rights Management 服务后，使用 [Azure 信息保护部署路线图](deployment-roadmap.md)检查在你向用户和管理员推出 Azure 信息保护前，是否有想要执行的其他配置步骤。 如果没有，你可能会发现以下操作信息很有用：

- [验证 Azure Rights Management 服务](verify.md)

- [使用 Azure Rights Management 服务帮助用户保护文件](help-users.md)

- [记录和分析 Azure Rights Management 服务](log-analyze-usage.md)

- [针对 Azure 信息保护租户密钥的操作](operations-tenant-key.md)


