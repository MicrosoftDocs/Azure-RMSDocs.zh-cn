---
title: 为 Azure Rights Management 配置应用程序 - AIP
description: 有关管理员配置应用程序和服务以支持 Azure 信息保护的 Azure Rights Management 保护服务的说明。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1f8100e22f1608ebbd678ec5f97f77b4abd53ff0
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383646"
---
# <a name="configuring-applications-for-azure-rights-management"></a>为 Azure Rights Management 配置应用程序

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> 此信息适用于已部署了 Azure 信息保护的 IT 管理员和顾问。 如果你要寻找有关如何针对特定应用程序使用 Rights Management 功能，或者如何打开权限保护文件的用户帮助和信息，请使用你的应用程序附带的帮助和指南。
>
> 例如，对于 Office 应用程序，请单击帮助图标并输入搜索词，例如 **Rights Management** 或 **IRM**。 有关适用于 Windows 的 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端用户指南](./rms-client/clientv2-user-guide.md)。

为组织部署 Azure 信息保护后，请使用以下信息来配置应用程序、Azure 信息保护客户端和服务，例如：

- **Office 应用程序**，如 word 2019、word 2016 和 word 2013。 
- **服务**（如 Exchange Online (传输规则、数据丢失防护、请勿转发和消息加密) 和 Microsoft SharePoint (受保护的库) 。 

若要了解这些应用程序和服务如何支持 Azure 信息保护中的数据保护服务，请参阅[应用程序如何支持 Azure 权限管理服务](applications-support.md)。

> [!IMPORTANT]
> 有关支持的版本和其他要求的信息，请参阅 [Azure 信息保护的要求](requirements.md)。

-   [Office 365：联机服务的配置](configure-office365.md)

    -   [Exchange Online：IRM 配置](configure-office365.md#exchangeonline-irm-configuration)

    -   [Microsoft 365 和 OneDrive 中的 SharePoint： IRM 配置](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)

- [Office 应用程序：客户端配置](configure-office-apps.md)

    -   [Office 365 应用、Office 2019、Office 2016 和 Office 2013](configure-office-apps.md#office365-apps-office-2019-office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office2010)

-   [Azure 信息保护客户端：安装和配置客户端](configure-client.md)

若要配置本地服务器（如 Exchange Server 和 SharePoint Server），请参阅 [部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

除了这些应用程序和服务外，还有一些支持 Rights Management API 的其他应用程序。 此类别包括使用 Rights Management SDK 内部编写的业务线应用程序，以及来自软件供应商的使用 Rights Management SDK 编写的应用程序。 对于这些应用程序，请按照应用程序随附的说明操作。

## <a name="next-steps"></a>后续步骤

将应用程序配置为支持 Azure Rights Management 服务后，使用 [AIP 部署路线图进行分类、标记和保护](deployment-roadmap-classify-label-protect.md) ，以检查向用户和管理员推出 Azure 信息保护之前是否需要执行其他配置步骤。 

如果没有，你可能会发现以下操作信息很有用：

- [验证 Azure Rights Management 服务](verify.md)

- [使用 Azure Rights Management 服务帮助用户保护文件](help-users.md)

- [记录和分析 Azure Rights Management 服务](log-analyze-usage.md)

- [针对 Azure 信息保护租户密钥的操作](operations-tenant-key.md)


