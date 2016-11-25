---
title: "应用程序如何支持 Azure Rights Management 服务 | Azure 信息保护"
description: "了解最常使用的最终用户应用程序（例如 Office 应用程序，包括 Word、Excel、PowerPoint 和 Outlook）和服务（例如 Exchange 和 SharePoint）如何才能使用 Azure 信息保护中的 Azure Rights Management 来帮助保护组织的文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: fdb862b0d4f3d0a6b3411b38a314e28b5f1f9edc


---

# <a name="how-applications-support-the-azure-rights-management-service"></a>应用程序如何支持 Azure Rights Management 服务

>*适用于：Azure 信息保护、Office 365*

使用以下信息可帮助了解最常使用的最终用户应用程序（例如 Office 应用程序，包括 Word、Excel、PowerPoint 和 Outlook）和服务（例如 Exchange 和 SharePoint）如何才能使用 Azure 信息保护中的 Azure Rights Management 来帮助保护组织的文档和电子邮件。 
> [!NOTE]
> 若要验证 Azure Rights Management 服务支持的应用程序和版本，请参阅[支持 Azure Rights Management 数据保护的应用程序](../get-started/requirements-applications.md)。

在某些情况下，Azure Rights Management 服务会根据管理员配置的策略自动应用保护。 例如，SharePoint 库、分类文件和 Exchange 传输规则就属于此种情况。 在其他情况下，最终用户必须自动通过应用程序（不管是通过选择模板还是通过选择特定选项）来应用信息保护。 例如，用户可通过电子邮件来共享文件，或者通过将访问权限和使用权限限制给选定用户或组织外部用户来保护现有文件。

利用模板，用户（以及配置策略的管理员）能够更加轻松地应用正确级别的保护，并将访问权限限制给组织内部人员。 虽然 Azure Rights Management 服务附带了两个默认模板，但你可能还希望创建自定义模板，以减少使用模板指定各个选项所需的时间。 有关详细信息，请参阅[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)。

对于用户必须自行应用信息保护的情况，请务必为他们提供有关信息保护应用方式和时机的说明和指导。 这些说明应该专门针对他们使用的特定应用程序和版本及其使用方式，有关信息保护应用时机和方式的指导应该适用于你的企业。 有关详细信息，请参阅[帮助用户使用 Azure Rights Management 服务保护文件](../deploy-use/help-users.md)。

有关如何为 Azure 信息保护中的 Azure Rights Management 服务配置这些应用程序的信息，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)。

> [!TIP]
> 有关使用 Azure Rights Management 服务的应用程序的示例和屏幕截图，请参阅[运行中的 Azure RMS：管理员和用户看到的内容](what-admins-users-see.md)。

搜索服务能以不同的方式与 Rights Management 集成。 例如： 

- Exchange Online 和 Exchange Server 使用服务端索引，因而用户的受 RMS 保护的电子邮件将自动显示在其搜索结果中。 

- SharePoint Online 和 SharePoint Server 仅针对下载对文件应用 Rights Management 保护，这意味着 SharePoint 上的索引和搜索结果不受此文档保护解决方案影响。 但是，如果你希望将文档存储在 SharePoint 中而不希望搜索结果中返回该文档，请在将其上传到 SharePoint 之前用 RMS 进行保护。

- Windows 桌面搜索在设备的不同用户间使用共享索引，以便持续保护受保护文档中的数据，它不对受 RMS 保护的文件进行索引。 这意味着，不仅你的搜索结果不包含已保护的文件，你还可以放心，登录或连接到你的电脑的其他用户的搜索结果中也不会显示包含敏感数据的文件。 



## <a name="next-steps"></a>后续步骤

了解有关以下各项如何支持 Azure Rights Management 服务的详细信息：

-   [适用于 Windows 和移动平台的 RMS 共享应用程序](sharing-app-support.md)

-   [Office 应用程序和服务](office-apps-services-support.md)

-   [运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器](file-server-support.md)

-   [支持 RMS API 的其他应用程序](api-support.md)




<!--HONumber=Nov16_HO2-->


