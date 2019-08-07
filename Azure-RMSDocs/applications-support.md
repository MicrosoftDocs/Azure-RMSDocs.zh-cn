---
title: 应用如何支持 AIP 中的 Azure 权限管理
description: 了解最常使用的应用程序 (如 Office 应用) 和服务 (例如 Exchange 和 SharePoint) 如何使用 azure 信息保护中的 Azure Rights Management 服务来帮助保护组织的文档和电子邮件。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f57664cc5841f9bfde48e4bb50ea111414e5a910
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68789525"
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>应用程序如何支持 Azure Rights Management 服务

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用以下信息可帮助了解最常使用的最终用户应用程序和服务如何才能使用 Azure 信息保护中的 Azure 权限管理来帮助保护组织的文档和电子邮件。 这些应用程序包括 Word、Excel、PowerPoint 和 Outlook。 服务包括 Exchange 和 SharePoint。

> [!NOTE]
> 若要验证 Azure Rights Management 服务支持的应用程序和版本，请参阅[支持 Azure Rights Management 数据保护的应用程序](./requirements-applications.md)。

在某些情况下，Azure Rights Management 服务会根据管理员配置的策略自动应用保护。 例如，SharePoint 库和 Exchange 传输规则就属于此种情况。 在其他情况下，最终用户必须从其应用程序自行应用保护。 例如，用户选择一个配置为应用保护的分类标签，或者选择一个模板或特定选项。 当用户保护要共享的文件，并且限制选定用户或组织外的用户的访问或使用时，用户应用的保护是典型保护。

利用模板，用户（以及配置策略的管理员）能够更加轻松地应用正确级别的保护，并将访问权限限制给组织内部人员。 虽然 Azure 权限管理服务随附两个默认模板，但你可能还希望创建自定义模板，以减少用户和管理员指定各个选项所需的时间。 有关模板的详细信息，请参阅[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)。

对于用户必须自行应用保护的情况，请务必为他们提供有关保护应用方式和时机的说明和指导。 让说明具有对用户使用的应用程序和版本以及使用方法的针对性。 此外，还针对用户应在何时采用什么方式应用适用于你的业务的保护，提供了指导。 有关详细信息，请参阅[帮助用户使用 Azure Rights Management 服务保护文件](help-users.md)。

有关如何为 Azure 信息保护中的 Azure Rights Management 服务配置这些应用程序的信息，请参阅[为 Azure Rights Management 配置应用程序](configure-applications.md)。

搜索服务能以不同的方式与 Rights Management 集成。 例如： 

- Exchange Online 和 Exchange Server 使用服务端索引，因而用户的受保护的电子邮件将自动显示在其搜索结果中。 

- SharePoint Online 和 SharePoint Server 仅在下载时对文件应用 Rights Management 保护。 此实现意味着 SharePoint 上的索引和搜索结果不受此文档保护解决方案的影响。 但是，如果你希望将文档存储在 SharePoint 中且不希望在搜索结果中返回该文档，请在将其上传到 SharePoint 之前，对其进行保护。

- Windows 桌面搜索在设备的不同用户间使用共享索引，以便持续保护受保护文档中的数据，它不对受保护的文件进行索引。 这意味着，不仅你的搜索结果不包含已保护的文件，你还可以放心，登录或连接到你的电脑的其他用户的搜索结果中也不会显示包含敏感数据的文件。 

## <a name="next-steps"></a>后续步骤

深入了解以下各种应用程序和服务如何支持 Azure 权限管理服务：

-   [Office 应用程序和服务](office-apps-services-support.md)

-   [运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器](file-server-support.md)

-   [支持 RMS API 的其他应用程序](api-support.md)

