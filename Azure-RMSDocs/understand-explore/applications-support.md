---
# required metadata

title: 应用程序如何支持 Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 应用程序如何支持 Azure Rights Management
使用以下信息可以帮助你了解最常使用的最终用户应用程序（例如 Office 应用程序，包括 Word、Excel、PowerPoint 和 Outlook）和服务（例如 Exchange 和 SharePoint）如何才能使用 Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 来帮助保护组织的数据。 
> [!NOTE]
> 若要验证 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 支持的应用程序和版本，请参阅 [Azure Rights Management 的要求](../get-started/requirements-azure-rms.md)。

某些情况下，将根据你配置的策略来自动应用信息保护。 例如，SharePoint 库、分类文件和 Exchange 传输规则就属于此种情况。 在其他情况下，用户必须自动通过应用程序（不管是通过选择模板还是通过选择特定选项）来应用信息保护。 例如，用户可通过电子邮件来共享文件，或者通过将访问权限和使用权限限制给选定用户或组织外部用户来保护现有文件。

利用模板，用户（以及配置策略的管理员）能够更加轻松地应用正确级别的保护，并将访问权限限制给组织内部人员。 虽然 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]附带了两个默认模板，但你可能还希望创建自定义模板，以减少使用模板指定各个选项所需的时间。 有关详细信息，请参阅[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)。

对于用户必须自行应用信息保护的情况，请务必为他们提供有关信息保护应用方式和时机的说明和指导。 这些说明应该专门针对他们使用的特定应用程序和版本及其使用方式，有关信息保护应用时机和方式的指导应该适用于你的企业。 有关详细信息，请参阅[帮助用户使用 Azure Rights Management 保护文件](../deploy-use/help-users.md)。

有关如何为 Azure RMS 配置这些应用程序的信息，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)。

> [!TIP]
> 有关使用 Azure RMS 的应用程序的示例和屏幕截图，请参阅 [运行中的 Azure RMS：管理员和用户看到的内容](what-admins-users-see.md)。


## 后续步骤

了解有关以下各项如何支持 Azure RMS 的详细信息：

-   [Windows 和移动平台的 RMS 共享应用程序](sharing-app-support.md)

-   [Office 应用程序和服务](office-apps-services-support.md)

-   [运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器](file-server-support.md)

-   [支持 RMS API 的其他应用程序](api-support.md)



<!--HONumber=Apr16_HO4-->


