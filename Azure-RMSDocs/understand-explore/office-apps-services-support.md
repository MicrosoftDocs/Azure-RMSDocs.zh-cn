---
# required metadata

title: Office 应用程序和服务 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Office 应用程序和服务
最终用户 Office 应用程序（例如 Word、Excel、PowerPoint 和 Outlook）和 Office 服务（例如 Exchange 和 SharePoint）可使用 Microsoft Azure Rights Management 来帮助保护组织的数据。

## Office 应用程序：Word、Excel、PowerPoint、Outlook
这些应用程序通过使用信息权限管理 (IRM) 以本机方式支持权限管理，让用户能够将保护应用于已保存文档，或者应用于要发送的电子邮件。 用户可以应用模板或选择针对访问、权限和使用限制的高度自定义设置。 

例如，用户可以通过配置文件仅允许组织内人员访问该文件，还可以控制是否允许编辑该文件、是否将其限制为只读，以及是否禁止打印该文件。 对于时间敏感型文件，可以配置一个过期时间（直接由用户配置，或者应用模板进行配置），在过期之后无法再访问该文件。 对于 Outlook，用户还可以选择“不要转发”选项来帮助防止数据泄漏 **** 。

## Exchange Online 和 Exchange Server
使用 Exchange Online 或 Exchange Server 时，你可以使用信息权限管理 (IRM) 集成，它提供更多信息保护解决方案：

-   **Exchange ActiveSync IRM** ，让移动设备能够保护和使用受保护的电子邮件。

-   **Outlook Web 应用**的 RMS 支持，其实施方法与 Outlook 客户端类似，让用户能够通过模板或指定各个选项来保护电子邮件，用户能够阅读和使用发送给他们的受保护电子邮件。

-   适用于 Outlook 客户端的**保护规则** ，管理员能够配置这些规则，以便自动将 RMS 模板应用于发送给指定收件人的电子邮件。 例如，在将内部电子邮件发送至法律部门时，只允许法律部门成员阅读这些邮件，而且不能转发。 在发送电子邮件之前，用户可以看到应用于电子邮件的保护，而默认情况下，如果他们确定该电子邮件不是必须发送的，则可将其删除。 电子邮件在发送之前进行了加密。 有关详细信息，请参阅 Exchange 库中的 [Outlook 保护规则](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)和[创建 Outlook 保护规则](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)。

-   **传输规则** ，管理员能够配置这些规则，根据各种属性（例如发件人、收件人、邮件主题和内容），自动将 RMS 模板应用于电子邮件。 这些规则在概念上类似于保护规则，但不允许用户取消保护；这些规则可以应用于 Outlook Web Access 和通过移动设备发送的电子邮件；在从客户端发送电子邮件之前，这些规则不对其进行加密。 有关详细信息，请参阅 Exchange 库中的[创建传输保护规则](https://technet.microsoft.com/library/dd302432.aspx)。

-   **数据丢失预防 (DLP) 策略** ，包含一系列筛选邮件的条件，有助于防止机密或敏感内容（例如个人信息或信用卡信息）的数据丢失。 检测到敏感数据时，可以使用策略提示，根据电子邮件中的内容，警告用户他们可能需要应用信息保护。 有关详细信息，请参阅 Exchange 库中的[数据丢失预防](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)。

-   **Office 365 邮件加密** ，使用传输规则将加密电子邮件发送到公司外部人员，该电子邮件在浏览器中阅读，浏览器界面与 Outlook Web App 相似。 你可以在公司的加密电子邮件中自定义免责声明文本和标题文本，甚至添加你公司的徽标。 有关详细信息，请参阅 Office 网站上的 [Office 365 邮件加密](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx)。

如果使用 Exchange Server，则可以通过部署 RMS 连接器，将其用作内部部署服务器和 RMS 云服务之间的中继，从而利用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]的信息保护功能。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

## SharePoint Online 和 SharePoint Server
使用 SharePoint Online 或 SharePoint Server 时，你可以使用信息权限管理 (IRM) 集成，让管理员保护列表或库，这样当用户签出文档时，文件将会受到保护，只有授权人员能够根据你指定的信息保护策略来查看和使用文件。 例如，文件可能是只读的，可能会禁用文本复制，可能会阻止保存本地副本，可能会阻止打印文件。

对于列表和库，始终由管理员（永远不会由最终用户）应用信息保护。 对于该容器中的所有文档，信息保护是在列表或库级别上应用的，而不是在单独文件级别上应用。  如果你使用 SharePoint Online，用户还可以对其 OneDrive for Business 库应用 IRM。

必须首先为 SharePoint 启用 IRM 服务。 然后，为库指定信息权限管理。 对于 SharePoint Online 和 OneDrive for Business，用户还可以为其 OneDrive for Business 库指定信息权限管理。 SharePoint 不使用权限策略模板，虽然你可以选择的 SharePoint 配置设置非常匹配你可以在模板中指定的设置。

如果使用 SharePoint Server，则可以通过部署 RMS 连接器，将其用作内部部署服务器和 RMS 云服务之间的中继，从而利用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]的信息保护功能。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

> [!NOTE]
> 目前，将 IRM 用于 SharePoint 时有一些限制：
> 
> -   不能使用在 Azure 经典门户中管理的默认模板或自定义模板。
> -   不支持带 .PPDF 文件扩展名的受保护 PDF 文件。 当你使用本机支持 RMS 的 PDF 阅读器时时，支持带 PDF 文件扩展名的文件以及受 RMS 本机保护的文件。
> -   由于移动设备上的 Office 尚不支持 RMS，因此这些设备必须使用浏览器来查看已使用 RMS 保护的文件，并且这些文件是只读的。

Azure RMS 会在从 SharePoint 下载文档时为文档应用使用限制和数据加密，而不是在 SharePoint 中首次创建文档或将其上载到库中时进行此类操作。 有关如何在下载文档前对其进行保护的信息，请参阅 SharePoint 文档中的 [OneDrive for Business 和 SharePoint Online 中的数据加密](https://technet.microsoft.com/library/dn905447.aspx) 。

有关在 SharePoint 中使用 Azure RMS 的详细信息，请参阅 Office 博客中的以下文章： [SharePoint 和 SharePoint 中的信息权限管理的新增功能](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## 后续步骤

若要查看其他应用程序和服务如何支持 Azure Rights Management，请参阅[应用程序如何支持 Azure Rights Management](applications-support.md)。

<!--HONumber=Apr16_HO3-->


