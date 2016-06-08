---
# required metadata

title: 概述 | Azure RMS
description: Rights Management Services (RMS) 是一种信息保护技术，可帮助保护数字信息免遭未经授权的使用。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 此 SDK 内容不是最新的。 在短时间内，请在 MSDN 上找到[最新版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)的文档。 **
# 概述

Rights Management Services (RMS) 是一种信息保护技术，可帮助保护数字信息免遭未经授权的使用。 通过启用权限的应用程序，内容所有者将能够定义可以对内容进行打开、修改、打印、转发或执行其他操作的人员。

## 概述

AD RMS 由 [服务器](ad-rms-server.md) 和 [客户端](ad-rms-client.md) 组件组成。 服务器组件包括在 Windows Server（如 Windows Server 2008 R2）上或通过云（通过 Azure 中的 RMS Web 服务）运行的多个 Web 服务。 客户端组件可以在客户端或服务器操作系统上运行，包含使应用程序可以加密和解密内容、检索模板和吊销列表、从服务器获取许可证和证书以及执行其他相关权限管理任务的功能。

有关详细信息，请参阅[应用程序类型](application-types.md)。

以下只是几个可以应用在 Rights Management Services SDK 2.1 上构建的应用程序的方案。

-   一个律师事务所希望阻止打印或转发敏感电子邮件消息。
-   计算机辅助设计和制造软件的开发人员希望限制只有研发部门的一小组用户无需使用密码即可访问图纸。
-   图形设计网站的所有者希望使用单个许可证，该许可证允许免费查看其图像的较低分辨率副本，但需要付费才能访问高分辨率版本。
-   联机文档库的所有者希望基于用户身份启用查看、打印或编辑文档的权限。
-   公司希望将敏感员工信息发布到将查看和编辑权限限制到特定用户的内部网站。

有关 AD RMS 服务器、AD RMS 客户端及其功能的详细信息，请参阅 TechNet 内容以获取 [针对 AD RMS 的 IT 专业人员文档](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)。

若要开始使用，请参阅 [入门](getting-started-with-ad-rms-2-0.md)。

## 相关主题

* [AD RMS 概念](application-types.md)
* [AD RMS 与 AD RMS 2.1 之间的差异](differences-between-ad-rms-and-ad-rms-2-0.md)
* [入门](getting-started-with-ad-rms-2-0.md)
* [针对 AD RMS 的 IT 专业人员文档](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)
* [服务器](ad-rms-server.md)
* [客户端](ad-rms-client.md)
 

 





<!--HONumber=Jun16_HO1-->


