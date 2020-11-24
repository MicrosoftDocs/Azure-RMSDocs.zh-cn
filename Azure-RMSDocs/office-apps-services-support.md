---
title: Office 应用和服务如何支持 AIP 中的 Azure RMS
description: 最终用户 Office 应用程序（例如 Word 和 Outlook）和 Office 服务（例如 Exchange 和 SharePoint）如何使用 AIP 中的 Azure 权限管理服务来帮助保护组织的数据。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/31/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1aba9e7f0d6cea7edde34d66e571a6eef4599555
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "95566064"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Office 应用程序和服务如何支持 Azure 权限管理 

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

最终用户 Office 应用程序和 Office 服务可使用 Azure 信息保护中的 Azure 权限管理服务来帮助保护组织的数据。 Office 应用程序包括 Word、Excel、PowerPoint 和 Outlook。 Office 服务是 Exchange 和 Microsoft SharePoint。 支持 Azure 权限管理服务的 Office 配置通常使用术语“信息权限管理 (IRM)”。

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Office 应用程序：Word、Excel、PowerPoint、Outlook
这些应用程序可以本机方式支持 Azure 权限管理，让用户能够将保护应用于已保存文档，或者应用于要发送的电子邮件。 用户可以应用[模板](configure-policy-templates.md)以应用保护。 或者，在 Word、Excel 和 PowerPoint 中，用户还可以针对访问、权限和使用限制选择自定义设置。

例如，用户可以配置 Word 文档，使仅组织中的人员可以访问该文档。 或者，控制 Excel 电子表格是否可以编辑，或限制为只读，或者禁止打印。 对于时间敏感型文件，可以配置一个过期时间，在过期之后无法再访问该文件。 此配置可由用户或通过应用保护模板直接执行。 对于 Outlook，用户还可以选择“不要转发”选项来帮助防止数据泄漏。

如果已准备好配置 Office 应用，请参阅 [office 应用：客户端配置](configure-office-apps.md)。

有关相关的已知问题，请参阅 [AIP Office 应用程序中的已知问题](known-issues.md#aip-known-issues-in-office-applications)。

## <a name="exchange-online-and-exchange-server"></a>Exchange Online 和 Exchange Server
使用 Exchange Online 或 Exchange 服务器 时，可以配置 Azure 信息保护的选项。 此配置允许 Exchange 提供以下保护解决方案：

-   **Exchange ActiveSync IRM**，让移动设备能够保护和使用受保护的电子邮件。

-   针对“Outlook 网页版”的电子邮件保护支持，其实现方式类似于 Outlook 客户端。 此配置允许用户通过使用保护模板或选项来保护电子邮件。 用户可以阅读和使用他们接收到的受保护的电子邮件。

-   管理员可以配置适用于 Outlook 客户端的“保护规则”，以便自动将保护模板和选项应用于发送给指定收件人的电子邮件。 例如，在将内部电子邮件发送至法律部门时，只允许法律部门成员阅读这些邮件，而且不能转发。 在发送电子邮件之前，用户可以看到应用于电子邮件的保护，而默认情况下，如果他们确定不需要这种保护，则可将其删除。 电子邮件在发送之前进行了加密。 有关详细信息，请参阅 Exchange 库中的 [Outlook 保护规则](/exchange/outlook-protection-rules-exchange-2013-help)和[创建 Outlook 保护规则](/exchange/create-an-outlook-protection-rule-exchange-2013-help)。

-   管理员可以配置“邮件流规则”，以便将保护模板自动应用于电子邮件。 该规则基于发件人、收件人、邮件主题和内容等属性。 这些规则在概念上与保护规则类似，但不允许用户删除保护，因为保护是由 Exchange 服务而不是客户端设置的。 由于保护是由服务设置的，因此用户使用何种设备或操作系统并不重要。 有关详细信息，请参阅针对 Exchange 本地部署的 [Exchange Online 中的电子邮件流规则（传输规则）](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules)和[创建传输保护规则](/exchange/create-a-transport-protection-rule-exchange-2013-help)。

-   “数据丢失预防 (DLP) 策略”包含一系列筛选邮件的条件，有助于防止机密或敏感内容的数据丢失。 其中，可以指定的操作之一是通过指定一个保护模板或选项来应用加密作为保护。 检测到敏感数据时，可以使用策略提示，警告用户他们可能需要应用保护。 有关详细信息，请参阅 Exchange Online 文档中的[数据丢失防护](/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)。

-   **消息加密** 支持将受保护的电子邮件和受保护的 Office 文档作为附件发送到任何设备上的任何电子邮件地址。 对于没有使用 Azure AD 的用户帐户，Web 体验支持社交标识提供者或一次性密码。 有关详细信息，请参阅从 Microsoft 365 文档中的 [Azure 信息保护基础上设置新 Microsoft 365 消息加密功能](/microsoft-365/compliance/set-up-new-message-encryption-capabilities) 。 若要帮助你查找与此配置相关的其他信息，请参阅 [Microsoft 365 消息加密](/microsoft-365/compliance/ome)"。

如果使用本地 Exchange，可以通过部署 Azure 权限管理连接器结合使用 Azure 权限管理服务和 IRM 功能。 此连接器充当本地服务器和 Azure 权限管理服务之间的中继。

有关保护模板的详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。

如需深入了解可用于保护电子邮件的电子邮件选项，请参阅[电子邮件的“不得转发”选项](configure-usage-rights.md#do-not-forward-option-for-emails)和[电子邮件的“仅加密”选项](configure-usage-rights.md#encrypt-only-option-for-emails)。

如果已准备好配置 Exchange 以保护电子邮件：

- 对于 Exchange Online，请参阅 [Exchange Online：IRM 配置](configure-office365.md#exchangeonline-irm-configuration)。

- 对于 Exchange 內部部署，请参阅[部署 Azure 权限管理连接器](deploy-rms-connector.md)。


## <a name="sharepoint-in-microsoft-365-and-sharepoint-server"></a>Microsoft 365 和 SharePoint Server 中的 SharePoint

在 Microsoft 365 或 SharePoint Server 中使用 SharePoint 时，可以使用 SharePoint 信息权限管理 (IRM) 功能来保护文档。 通过此功能，管理员可以保护列表或库，这样当用户签出文档时，所下载的文件将会受到保护，如此只有授权人员能够根据指定的信息保护策略来查看和使用文件。 例如，文件可能是只读的，可能会禁用文本复制，可能会阻止保存本地副本，可能会阻止打印文件。

Word、PowerPoint、Excel 和 PDF 文档均支持此 SharePoint IRM 保护。 默认情况下，保护仅限于下载文档的人员。 可以使用名为“允许组保护”的配置选项更改此默认值，该选项将保护扩展到你指定的组。 例如，可以指定一个具有编辑库中文档权限的组，以便同一组用户可以在 SharePoint 的外部编辑该文档，而不考虑是哪个用户下载了该文档。 或者，可以指定未在 SharePoint 中授予权限的组，但该组中的用户需要从 SharePoint 外部访问该文档。 对于 SharePoint 列表和库，始终由管理员（绝不会是最终用户）配置此保护。 在站点级别设置权限，默认情况下，这些权限将由该站点中的任何列表或库继承。 如果在 Microsoft 365 中使用 SharePoint，则用户还可以配置其 Microsoft OneDrive 库以进行 IRM 保护。

若要实现更精细的控制，可以配置该站点中的列表或库，使其停止从其父级继承权限。 然后，可以在该级别（列表或库）配置 IRM 权限，并将其称为“唯一权限”。 但是，应始终在容器级别设置权限；不能在单个文件上设置权限。 

必须首先为 SharePoint 启用 IRM 服务。 然后，为库指定 IRM 权限。 对于 SharePoint 和 OneDrive，用户还可以为其 OneDrive 库指定 IRM 权限。 SharePoint 不使用权限策略模板，虽然可以选择的 SharePoint 配置设置与可以在模板中指定的某些设置相匹配。

如果使用 SharePoint Server，可通过部署 Azure 权限管理连接器，使用此 IRM 保护。 此连接器充当本地服务器和权限管理云服务之间的中继。 有关详细信息，请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

> [!NOTE]
> 使用 SharePoint IRM 时有一些限制：
> 
> - 不能使用在 Azure 门户中管理的默认模板或自定义保护模板。 
> 
> - 不支持带 .ppdf 文件扩展名的受保护 PDF 文件。 有关查看受保护的 PDF 文档的详细信息，请参阅 [Microsoft 信息保护的受保护 PDF 阅读器](./rms-client/protected-pdf-readers.md)。
> 
> - 不支持共同创作（多人同时对文档进行编辑）。 若要在受 IRM 保护的库中编辑文档，必须首先签出和下载文档，然后在 Office 应用程序中编辑该文档。 因此，一次只能有一人编辑文档。

对于不受 IRM 保护的库，如果你将保护仅应用于随后上传到 SharePoint 或 OneDrive 的文件，则以下操作不会使用此文件：共同创作、用于 web 的 Office、搜索、文档预览、缩略图、电子数据展示和数据丢失防护 (DLP) 。

> [!IMPORTANT]
> SharePoint IRM 可以与应用保护的敏感度标签结合使用。 同时使用这两个功能时，受保护的文件的行为会发生更改。 有关详细信息，请参阅 [在 SharePoint 和 OneDrive 中启用 Office 文件的敏感度标签](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)。

使用 SharePoint IRM 保护时，Azure Rights Management 服务会在从 SharePoint 下载文档时为文档应用使用限制和数据加密，而不是在 SharePoint 中首次创建文档或将其上传到库时进行此操作。 有关如何在下载文档前对其进行保护的信息，请参阅 SharePoint 文档 [中的 OneDrive 和 sharepoint 中的数据加密](/microsoft-365/compliance/data-encryption-in-odb-and-spo?redirectSourcePath=%252fen-us%252farticle%252f6501b5ef-6bf7-43df-b60d-f65781847d6c) 。

虽然不再是新的，但 Microsoft 365 博客中的以下文章还包含一些可能有用的其他信息： [SharePoint 中的信息 Rights Management 的新增功能](https://www.microsoft.com/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

对于即将发生的更改，请参阅 [SharePoint 安全性、管理和迁移更新](https://techcommunity.microsoft.com/t5/Microsoft-SharePoint-Blog/Updates-to-SharePoint-security-administration-and-migration/ba-p/549585)。

如果已准备好为 SharePoint 配置 IRM ：

- Microsoft 365 中的 SharePoint，请参阅 [Microsoft 365 和 OneDrive： IRM 配置中的 sharepoint](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)。

- 对于 Sharepoint Server，请参阅[部署 Azure 权限管理连接器](deploy-rms-connector.md)。


## <a name="next-steps"></a>后续步骤

如果你有 Microsoft 365，你可能会对查看 [Microsoft 365 中的文件保护解决方案](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect)感兴趣，这提供了在 Microsoft 365 中保护文件的建议功能。

若要查看其他应用程序和服务如何支持 Azure 信息保护中的 Azure Rights Management 服务，请参阅[应用程序如何支持 Azure Rights Management 服务](applications-support.md)。

如果已准备好开始部署（包括配置这些应用程序和服务），请参阅 [Azure 信息保护部署路线图](deployment-roadmap.md)。