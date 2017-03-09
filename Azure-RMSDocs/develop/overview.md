---
title: "概述 - RMS SDK 4.2 | Azure RMS"
description: "AD RMS 和 Azure RMS 是一种信息保护技术，可帮助保护数字信息免遭未经授权的使用。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8A13494E-C1D7-407D-BCD1-A406915EA578
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 19afce2a84e979ca1a25ec2ff6473dd3d6edd610


---

# <a name="overview"></a>概述

Microsoft Rights Management SDK 4.2 是一种信息保护技术，可用于多个平台。  它提供软件开发工具包 (SDK) 或框架，专为客户端计算机和设备设计，以帮助保护对流经“启用权限”的应用程序的信息的访问和使用。 这些平台的 SDK 提供了简单 API，便于应用程序开发人员保护或使用数字内容、检索模板、从服务器获取策略以及执行其他相关的权限管理任务。

有关当前受支持的平台的详细信息，请参阅有关 [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 的开发人员文档门户。

以下只是其中一些可能出现的方案：

-   某律师事务所希望阻止在移动设备上打印或转发敏感电子邮件消息。
-   计算机辅助设计和制造软件的开发人员希望限制只有研发部门的一小组用户无需使用密码即可访问图纸。
-   图形设计移动应用程序的所有者希望使用单个许可证，以允许免费查看其图像的低分辨率副本，但需要付费才能访问高分辨率版本。
-   联机文档库的所有者希望在文档下载到移动设备时，基于用户身份启用查看、打印或编辑文档的权限。
-   公司希望将敏感员工信息发布到将查看和编辑权限限制到特定用户的内部网站。

可以下载 MS RMS SDK 4.2，在确认和接受其许可证协议的情况下，你可以通过第三方软件进行自由分发，从而支持客户端访问在你的环境中使用和部署 AD RMS 服务器或者使用和部署 或 Azure RMS 服务时权限受保护的内容。 有关详细信息，请参阅[入门](get-started.md)。

## <a name="sdk-highlights"></a>SDK 亮点


MS RMS SDK 4.2 提供了一些很棒的新功能，包括以下方面：

-   **重新设计的 API** – MS RMS SDK 4.2 API 经过重新设计，实现了最大程度的简单易用性，使开发人员能够使用简单、透明的加密和解密 API，从而以最少的工作量实现统一的 RMS 行为。
-   **对 AD RMS 和 Azure RMS 的混合支持** – 通过单个启用 RMS 的应用程序即可使用和保护来自 AD RMS 服务器（使用 AD RMS 的移动设备扩展）和 Azure RMS 服务的内容。 MS RMS SDK 4.2 以透明方式发现 IT 管理员可以配置的相关终点。
-   **自带身份验证库** – 作为应用程序开发人员，你可以选择对 MS RMS SDK 4.2 使用何种身份验证库。 无论是 [Azure AD 身份验证库](https://msdn.microsoft.com/library/jj573266.aspx)还是你组织的自定义库，MS RMS SDK 4.2 都可以分离身份验证堆栈，以便你选择最能满足需求的库。
-   **自带用户界面** - MS RMS SDK 4.2 现在允许你实现自定义用户界面。 从保护内容和选择模板到显示和更改权限，同时使用受保护的内容，MS RMS SDK 4.2 不会在你的应用程序上强制执行任何内置 UI。 不过，如果你愿意，也可以通过我们的 [GitHub 帐户](https://github.com/AzureAD/)对所有平台都使用 Microsoft RMS UI 库。
-   **脱机访问受保护的内容** – MS RMS SDK 4.2 允许你的应用程序用户即使在没有 Internet 连接的情况下也能访问受保护的内容。 MS RMS SDK 4.2 以安全方式缓存受保护内容的使用策略，以便你的用户可以脱机访问受 RMS 保护的数据。

使用[入门](get-started.md)指南开始你的受保护信息设备应用程序项目。

## <a name="related-topics"></a>相关主题

* [Microsoft Rights Management SDK](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md)
* [入门](get-started.md)
* [Azure AD 身份验证库](https://msdn.microsoft.com/en-us/library/jj573266.aspx)
* [GitHub 帐户](https://github.com/AzureAD/)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


