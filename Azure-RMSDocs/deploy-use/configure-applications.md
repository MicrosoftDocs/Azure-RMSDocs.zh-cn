---
title: "为 Azure Rights Management 服务配置应用程序 | Azure 信息保护"
description: "有关管理员配置应用程序和服务以支持 Azure 信息保护的 Azure Rights Management 保护服务的说明。 例如，Word 2013 和 Word 2010 等 Office 应用程序，以及 Exchange Online（传输规则、数据丢失防护、请勿转发和邮件加密）与 SharePoint Online（受保护库）等服务。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 3c54f0c2f3fcbd312bb3ade521e5dd7f4a12eb85


---

# <a name="configuring-applications-for-azure-rights-management"></a>为 Azure Rights Management 配置应用程序

>*适用于：Azure 信息保护、Office 365*

> [!NOTE]
> 此信息适用于已部署了 Azure 信息保护的 IT 管理员和顾问。 如果你要寻找有关如何针对特定应用程序使用 Rights Management 功能，或者如何打开权限保护文件的用户帮助和信息，请使用你的应用程序附带的帮助和指南。
>
> 例如，对于 Office 应用程序，请单击帮助图标并输入搜索词，例如 **Rights Management** 或 **IRM**。 有关适用于 Windows 的 RMS 共享应用程序，请参阅 [Rights Management 共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)。

在为组织部署 Azure 信息保护之后，请使用以下信息配置应用程序和服务以支持 Azure 信息保护中的 Azure Rights Management 服务。 其中包括 Word 2013 和 Word 2010 等 Office 应用程序，以及 Exchange Online（传输规则、数据丢失预防、请勿转发和消息加密）与 SharePoint Online（受保护库）等服务。 有关这些应用程序和服务如何支持 Rights Management 的信息，请参阅[应用程序如何支持 Azure Rights Management 服务](../understand-explore/applications-support.md)。

> [!IMPORTANT]
> 有关受支持的版本和其他要求的信息，请参阅 [Azure Rights Management 的要求](../get-started/requirements-azure-rms.md)。

-   [Office 365：客户端和联机服务配置](configure-office365.md)

    -   [Exchange Online：IRM 配置](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online 和 OneDrive for Business：IRM 配置](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Office 应用程序：客户端配置](configure-office-apps.md)

    -   [Office 2016 和 Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [共享应用程序：客户端安装和配置](configure-sharing-app.md)

    -   [适用于 Windows 的 RMS 共享应用程序：安装和配置](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [适用于移动平台的 RMS 共享应用程序：安装和管理](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


若要配置本地服务器，例如 Exchange Server 和 SharePoint Server，请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

> [!TIP]
> 有关配置为使用 Azure Rights Management 服务的应用程序的高级示例和屏幕截图，请参阅[运行中的 Azure RMS：管理员和用户看到的内容](../understand-explore/what-admins-users-see.md)。


除了这些应用程序和服务外，还有一些支持 Rights Management API 的其他应用程序。 此类别包括使用 Rights Management SDK 内部编写的业务线应用程序，以及来自软件供应商的使用 Rights Management SDK 编写的应用程序。 对于这些应用程序，请按照应用程序随附的说明操作。

## <a name="next-steps"></a>后续步骤
将应用程序配置为支持 Azure Rights Management 服务后，使用 [Azure 信息保护部署路线图](../plan-design/deployment-roadmap.md)检查在你向用户和管理员推出 Azure 信息保护前，是否有想要执行的其他配置步骤。 如果没有，你可能会发现以下操作信息很有用：

- [验证 Azure Rights Management 服务](verify.md)

- [使用 Azure Rights Management 服务帮助用户保护文件](help-users.md)

- [记录和分析 Azure Rights Management 服务](log-analyze-usage.md)

- [Azure 信息保护租户密钥的操作](operations-tenant-key.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]




<!--HONumber=Jan17_HO4-->


