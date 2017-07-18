---
title: "使用 Azure 信息保护的 Office 应用和服务"
description: "最终用户 Office 应用程序（例如 Word、Excel、PowerPoint 和 Outlook）和 Office 服务（例如 Exchange 和 SharePoint）如何使用 Azure Rights Management 服务来帮助保护组织的数据。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7fe044ab9b8e253e3095af5828a33926271bc42b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="office-applications-and-services"></a>Office 应用程序和服务

>*适用于：Azure 信息保护、Office 365*

最终用户 Office 应用程序（例如 Word、Excel、PowerPoint 和 Outlook）和 Office 服务（例如 Exchange 和 SharePoint）如何使用 Azure 信息保护中的 Azure Rights Management 服务来帮助保护组织的数据。

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Office 应用程序：Word、Excel、PowerPoint、Outlook
这些应用程序通过使用信息权限管理 (IRM) 以本机方式支持权限管理，让用户能够将保护应用于已保存文档，或者应用于要发送的电子邮件。 用户可以应用模板，在 Word、Excel 和 PowerPoint 中，用户还可以针对访问、权限和使用限制选择高度自定义设置。 

例如，用户可以通过配置 Word 文档仅允许组织内人员访问该文档，还可以控制是否允许编辑 Excel 电子表格、是否将其限制为只读，以及是否禁止打印该电子表格。 对于时间敏感型文件，可以配置一个过期时间（直接由用户配置，或者应用模板进行配置），在过期之后无法再访问该文件。 在 Outlook 中，除了选择模板，用户还可以选择“不要转发”选项来帮助防止数据泄漏。

除了本机 IRM 支持之外，这些应用程序还支持与 [Azure 信息保护客户端](../rms-client/aip-client.md)一起安装的 Azure 信息保护栏。 此栏会显示标签，方便用户对包含敏感数据的文档和电子邮件自动应用 Rights Management 保护。

如果已准备好配置 Office 应用和 Azure 信息保护客户端：

- 若要配置 Office 应用，请参阅 [Office 应用：客户端配置](../deploy-use/configure-office-apps.md)。

- 若要安装和配置 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端：安装和配置客户端](../deploy-use/configure-client.md)。

## <a name="exchange-online-and-exchange-server"></a>Exchange Online 和 Exchange Server
使用 Exchange Online 或 Exchange Server 时，你可以使用信息权限管理 (IRM) 集成，它提供更多信息保护解决方案：

-   **Exchange ActiveSync IRM** ，让移动设备能够保护和使用受保护的电子邮件。

-   **Outlook Web 应用**的 RMS 支持，其实施方法与 Outlook 客户端类似，让用户能够通过模板或指定各个选项来保护电子邮件，用户能够阅读和使用发送给他们的受保护电子邮件。

-   适用于 Outlook 客户端的**保护规则**，管理员能够配置这些规则，以便自动将 Rights Management 模板应用于发送给指定收件人的电子邮件。 例如，在将内部电子邮件发送至法律部门时，只允许法律部门成员阅读这些邮件，而且不能转发。 在发送电子邮件之前，用户可以看到应用于电子邮件的保护，而默认情况下，如果他们确定该电子邮件不是必须发送的，则可将其删除。 电子邮件在发送之前进行了加密。 有关详细信息，请参阅 Exchange 库中的 [Outlook 保护规则](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)和[创建 Outlook 保护规则](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)。

-   **传输规则**，管理员能够配置这些规则，以便根据各种属性（例如发件人、收件人、邮件主题和内容），自动将 Rights Management 模板应用于电子邮件。 这些规则在概念上类似于保护规则，但不允许用户取消保护；这些规则可以应用于 Outlook Web Access 和通过移动设备发送的电子邮件；在从客户端发送电子邮件之前，这些规则不对其进行加密。 有关详细信息，请参阅 Exchange 库中的[创建传输保护规则](https://technet.microsoft.com/library/dd302432.aspx)。

-   **数据丢失预防 (DLP) 策略** ，包含一系列筛选邮件的条件，有助于防止机密或敏感内容（例如个人信息或信用卡信息）的数据丢失。 检测到敏感数据时，可以使用策略提示，根据电子邮件中的内容，警告用户他们可能需要应用信息保护。 有关详细信息，请参阅 Exchange 库中的[数据丢失预防](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)。

-   **Office 365 邮件加密** ，使用传输规则将加密电子邮件发送到公司外部人员，该电子邮件在浏览器中阅读，浏览器界面与 Outlook Web App 相似。 你可以在公司的加密电子邮件中自定义免责声明文本和标题文本，甚至添加你公司的徽标。 有关详细信息，请参阅 Office 网站上的 [Office 365 邮件加密](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx)。

如果使用 Exchange Server，则可以通过部署 RMS 连接器（用作本地服务器和 Azure Rights Management 服务之间的中继），将信息保护功能和 Azure Rights Management 服务结合使用。

如果准备为 Exchange 配置 IRM：

- 对于 Exchange Online，请参阅 [Exchange Online：IRM 配置](../deploy-use/configure-office365.md#exchange-online-irm-configuration)。

- 对于 Exchange 內部部署，请参阅[部署 Azure 权限管理连接器](../deploy-use/deploy-rms-connector.md)。


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online 和 SharePoint Server

使用 SharePoint Online 或 SharePoint Server 时，可以使用信息权限管理 (IRM) 来保护文档。 通过此配置，管理员可以保护列表或库，这样当用户签出文档时，所下载的文件将会受到保护，如此只有授权人员能够根据指定的信息保护策略来查看和使用文件。 例如，文件可能是只读的，可能会禁用文本复制，可能会阻止保存本地副本，可能会阻止打印文件。

默认情况下，保护仅限于下载文档的人员。 但是，你可以使用配置选项来更改此设置，该选项将保护范围扩展到所有在 SharePoint 或你指定的组中访问文档的用户。

对于 SharePoint 列表和库，始终由管理员（绝不会是最终用户）配置信息保护。 在站点级别设置权限，默认情况下，这些权限将由该站点中的任何列表或库继承。 如果使用 SharePoint Online，用户还可以对其 OneDrive for Business 库配置 IRM 保护。

若要实现更精细的控制，可以配置该站点中的列表或库，使其停止从其父级继承权限。 然后，可以在该级别（列表或库）配置 IRM 权限，并将其称为“唯一权限”。 但是，应始终在容器级别设置权限；不能在单个文件上设置权限。 

必须首先为 SharePoint 启用 IRM 服务。 然后，为库指定 IRM 权限。 对于 SharePoint Online 和 OneDrive for Business，用户还可以为其 OneDrive for Business 库指定 IRM 权限。 SharePoint 不使用权限策略模板，虽然可以选择的 SharePoint 配置设置与可以在模板中指定的某些设置相匹配。

如果使用 SharePoint Server，可通过部署 Azure 权限管理连接器，使用此 IRM 保护。 此连接器充当本地服务器和权限管理云服务之间的中继。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

> [!NOTE]
> 目前，使用 SharePoint IRM 时存在一些限制：
> 
> - 不能使用在 Azure 经典门户中管理的默认模板或自定义模板。 
> 
> - 不支持带 .PPDF 文件扩展名的受保护 PDF 文件。 使用本机支持 Rights Management 的 PDF 阅读器时，支持带 .PDF 文件扩展名的文件以及受 Rights Management 本机保护的文件。


使用 IRM 保护时，Azure 权限管理服务会在从 SharePoint 下载文档时为文档应用使用限制和数据加密，而不是在 SharePoint 中首次创建文档或将其上传到库时进行此类操作。 有关如何在下载文档前对其进行保护的信息，请参阅 SharePoint 文档中的 [OneDrive for Business 和 SharePoint Online 中的数据加密](https://technet.microsoft.com/library/dn905447.aspx) 。

虽然不再是新文章，但以下 Office 博客中的帖子中仍可能提供了一些有用的附加信息：[What’s New with Information Rights Management in SharePoint and SharePoint Online](https://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)（SharePoint 和 SharePoint Online 中信息权限管理的新增内容）

如果已准备好为 SharePoint 配置 IRM ：

- 对于 SharePoint Online，请参阅 [SharePoint Online 和 OneDrive for Business：IRM 配置](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)。

- 对于 Sharepoint Server，请参阅[部署 Azure 权限管理连接器](../deploy-use/deploy-rms-connector.md)。


## <a name="next-steps"></a>后续步骤

若要查看其他应用程序和服务如何支持 Azure 信息保护中的 Azure Rights Management 服务，请参阅[应用程序如何支持 Azure Rights Management 服务](applications-support.md)。

如果已准备好开始部署（包括配置这些应用程序和服务），请参阅 [Azure 信息保护部署路线图](/plan-design/deployment-roadmap.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]