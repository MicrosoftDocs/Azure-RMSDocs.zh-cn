---
title: Office 应用和服务如何支持 AIP 中的 Azure RMS
description: 最终用户 Office 应用程序（例如 Word 和 Outlook）和 Office 服务（例如 Exchange 和 SharePoint）如何使用 AIP 中的 Azure 权限管理服务来帮助保护组织的数据。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/21/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c302972e8a048ec851af85cdba9d86bd7fbcc971
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42803813"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Office 应用程序和服务如何支持 Azure 权限管理 

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

最终用户 Office 应用程序和 Office 服务可使用 Azure 信息保护中的 Azure 权限管理服务来帮助保护组织的数据。 Office 应用程序包括 Word、Excel、PowerPoint 和 Outlook。 Office 服务包括 Exchange 和 SharePoint。 支持 Azure 权限管理服务的 Office 配置通常使用术语“信息权限管理 (IRM)”。

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Office 应用程序：Word、Excel、PowerPoint、Outlook
这些应用程序可以本机方式支持 Azure 权限管理，让用户能够将保护应用于已保存文档，或者应用于要发送的电子邮件。 用户可以应用模板以应用保护。 或者，在 Word、Excel 和 PowerPoint 中，用户还可以针对访问、权限和使用限制选择自定义设置。 

例如，用户可以配置 Word 文档，使仅组织中的人员可以访问该文档。 或者，控制 Excel 电子表格是否可以编辑，或限制为只读，或者禁止打印。 对于时间敏感型文件，可以配置一个过期时间，在过期之后无法再访问该文件。 此配置可由用户或通过应用模板直接执行。 对于 Outlook，用户还可以选择“不要转发”选项来帮助防止数据泄漏  。

除了对 Azure 权限管理的本机 Office 支持之外，这些应用程序还支持与 [Azure 信息保护客户端](./rms-client/aip-client.md)一起安装的 Azure 信息保护栏。 此栏会显示标签，方便用户对包含敏感数据的文档和电子邮件自动应用保护。

如果已准备好配置 Office 应用和 Azure 信息保护客户端：

- 若要配置 Office 应用，请参阅 [Office 应用：客户端配置](configure-office-apps.md)。

- 若要安装和配置 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端：安装和配置客户端](configure-client.md)。

## <a name="exchange-online-and-exchange-server"></a>Exchange Online 和 Exchange Server
在使用 Exchange Online 或 Exchange Server 时，可以配置支持 Azure 权限管理的信息权限管理 (IRM) 选项。 此配置允许 Exchange 提供以下保护解决方案：

-   **Exchange ActiveSync IRM** ，让移动设备能够保护和使用受保护的电子邮件。

-   针对“Outlook 网页版”的电子邮件保护支持，其实现方式类似于 Outlook 客户端。 此配置允许用户通过使用模板或指定单个选项来保护电子邮件。 用户可以阅读和使用他们接收到的受保护的电子邮件。

-   适用于 Outlook 客户端的“保护规则”，管理员能够配置这些规则，以便自动将保护模板应用于发送给指定收件人的电子邮件。 例如，在将内部电子邮件发送至法律部门时，只允许法律部门成员阅读这些邮件，而且不能转发。 在发送电子邮件之前，用户可以看到应用于电子邮件的保护，而默认情况下，如果他们确定不需要这种保护，则可将其删除。 电子邮件在发送之前进行了加密。 有关详细信息，请参阅 Exchange 库中的 [Outlook 保护规则](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)和[创建 Outlook 保护规则](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)。

-   “邮件流规则”，管理员配置该规则将保护模板自动应用于电子邮件。 该规则基于发件人、收件人、邮件主题和内容等属性。 该规则在概念上类似于保护规则，但不允许用户删除保护。 该规则可应用于 Outlook 网页版和通过移动设备发送的电子邮件。 此外，在从客户端发送电子邮件之前，该规则不会对电子邮件进行加密。 有关详细信息，请参阅 Exchange 库中的[创建传输保护规则](https://technet.microsoft.com/library/dd302432.aspx)。

-   “数据丢失预防 (DLP) 策略”，包含一系列筛选邮件的条件，有助于防止机密或敏感内容的数据丢失。 机密或敏感内容的示例包括个人信息或信用卡信息。 检测到敏感数据时，可以使用策略提示，警告用户他们可能需要应用保护。 有关详细信息，请参阅 Exchange 库中的[数据防护丢失](https://technet.microsoft.com/library/jj150527(v=exchg.160\).aspx)。

-   **Office 365 邮件加密**，支持以附件形式向任何设备上的任何地址发送受保护的电子邮件和受保护的 Office 文档。 对于没有使用 Azure AD 的用户帐户，Web 体验支持社交标识提供者或一次性密码。 有关详细信息，请参阅 Office 网站上的 [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)（设置构建在 Azure 信息保护之上新的 Office 365 邮件加密功能）。

如果使用本地 Exchange，可以通过部署 Azure 权限管理连接器结合使用 Azure 权限管理服务和 IRM 功能。 此连接器充当本地服务器和 Azure 权限管理服务之间的中继。

如果准备为 Exchange 配置 IRM：

- 对于 Exchange Online，请参阅 [Exchange Online：IRM 配置](configure-office365.md#exchange-online-irm-configuration)。

- 对于 Exchange 內部部署，请参阅[部署 Azure 权限管理连接器](deploy-rms-connector.md)。


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online 和 SharePoint Server

使用 SharePoint Online 或 SharePoint Server 时，可以使用 SharePoint 信息权限管理 (IRM) 功能来保护文档。 通过此功能，管理员可以保护列表或库，这样当用户签出文档时，所下载的文件将会受到保护，如此只有授权人员能够根据指定的信息保护策略来查看和使用文件。 例如，文件可能是只读的，可能会禁用文本复制，可能会阻止保存本地副本，可能会阻止打印文件。

Word、PowerPoint、Excel 和 PDF 文档均支持此 SharePoint IRM 保护。 默认情况下，保护仅限于下载文档的人员。 可以使用名为“允许组保护”的配置选项更改此默认值，该选项将保护扩展到你指定的组。 例如，可以指定一个具有编辑库中文档权限的组，以便同一组用户可以在 SharePoint 的外部编辑该文档，而不考虑是哪个用户下载了该文档。 或者，可以指定未在 SharePoint 中授予权限的组，但该组中的用户需要从 SharePoint 外部访问该文档。 

对于 SharePoint 列表和库，始终由管理员（绝不会是最终用户）配置此保护。 在站点级别设置权限，默认情况下，这些权限将由该站点中的任何列表或库继承。 如果使用 SharePoint Online，用户还可以对其 OneDrive for Business 库配置 IRM 保护。

若要实现更精细的控制，可以配置该站点中的列表或库，使其停止从其父级继承权限。 然后，可以在该级别（列表或库）配置 IRM 权限，并将其称为“唯一权限”。 但是，应始终在容器级别设置权限；不能在单个文件上设置权限。 

必须首先为 SharePoint 启用 IRM 服务。 然后，为库指定 IRM 权限。 对于 SharePoint Online 和 OneDrive for Business，用户还可以为其 OneDrive for Business 库指定 IRM 权限。 SharePoint 不使用权限策略模板，虽然可以选择的 SharePoint 配置设置与可以在模板中指定的某些设置相匹配。

如果使用 SharePoint Server，可通过部署 Azure 权限管理连接器，使用此 IRM 保护。 此连接器充当本地服务器和权限管理云服务之间的中继。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

> [!NOTE]
> 目前，使用 SharePoint IRM 时存在一些限制：
> 
> - 不能使用在 Azure 门户中管理的默认模板或自定义保护模板。 
> 
> - 不支持带 .ppdf 文件扩展名的受保护 PDF 文件。 支持含 .pdf 文件扩展名的文件，并在下载该文件时，可使用在本地支持权限管理的 PDF 应用程序打开它。 例如，适用于 Windows 的 Azure 信息保护客户端包含这些受保护的 PDF 文件的查看器。 在[启用 RMS 的应用程序表](./requirements-applications.md#rms-enlightened-applications)中列出了备用 PDF 查看器。
> 
> - 当同时有多人对文档进行编辑时，不支持共同创作。 若要在受 IRM 保护的库中编辑文档，必须首先签出和下载文档，然后在 Office 应用程序中编辑该文档。 因此，一次只能有一人编辑文档。

对于不受 IRM 保护的库，如果保护要上传到 SharePoint 或 OneDrive 的文件，则以下各项不适用于此文件：共同创作、Office Online、搜索、文档预览、缩略图、电子数据展示和数据丢失防护 (DLP)。

使用 SharePoint IRM 保护时，Azure Rights Management 服务会在从 SharePoint 下载文档时为文档应用使用限制和数据加密，而不是在 SharePoint 中首次创建文档或将其上传到库时进行此操作。 有关如何在下载文档前对其进行保护的信息，请参阅 SharePoint 文档中的 [OneDrive for Business 和 SharePoint Online 中的数据加密](https://technet.microsoft.com/library/dn905447.aspx) 。

虽然不再是新文章，但以下 Office 365 博客中的帖子中仍可能提供了一些有用的附加信息：[SharePoint 和 SharePoint Online 中信息权限管理的新增内容](https://www.microsoft.com/en-us/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

如果已准备好为 SharePoint 配置 IRM ：

- 对于 SharePoint Online，请参阅 [SharePoint Online 和 OneDrive for Business：IRM 配置](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)。

- 对于 Sharepoint Server，请参阅[部署 Azure 权限管理连接器](deploy-rms-connector.md)。


## <a name="next-steps"></a>后续步骤

如果你有 Office 365，则可能有兴趣查看 [Office 365 中的文件保护解决方案](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect)，其中提供了用于保护 Office 365 中的文件的建议功能。

若要查看其他应用程序和服务如何支持 Azure 信息保护中的 Azure Rights Management 服务，请参阅[应用程序如何支持 Azure Rights Management 服务](applications-support.md)。

如果已准备好开始部署（包括配置这些应用程序和服务），请参阅 [Azure 信息保护部署路线图](deployment-roadmap.md)。
