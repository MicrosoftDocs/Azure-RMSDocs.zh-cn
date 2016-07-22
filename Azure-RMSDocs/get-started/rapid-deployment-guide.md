---
title: "Azure Rights Management 快速部署指南 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c994d616-cff6-4930-9228-a7f7d198a160
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 01c2436218e0d7fd80a31cdc037d9dc8933e42f2


---

# Azure Rights Management 快速部署指南

*适用于：Azure Rights Management、Office 365*

本指南是对“部署和使用”部分中的配置信息的补充，通过从要实施的特定方案的列表中进行选择，帮助你更加快速地部署和使用 Azure Rights Management (Azure RMS)。

这些方案包含管理员指令和随附的最终用户文档。 在向最终用户提供文档（说明或公告）之前，你需要首先针对业务需求和现有工作流对本文档进行自定义。 一组说明或公告示例显示了最终用户文档的最终样式。

每个方案都附带了一个要求列表，其中包含了其他所需信息的链接，以便你按照任意顺序独立部署这些解决方案。

此处所列的方案都是最常见的示例。 因为在组织内以及组织间的大量方案中，都可使用 Azure RMS 来保护信息，所以你可以定义自己的方案并将其部署到你的环境中，也可以使用相同的模式部署给用户。 通过侧重于特定方案，你的 Azure RMS 部署将更加贴合你的业务目标。 此外，我们的经验是用户更愿意密切、系统地遵循特定于方案的说明，而非“保护敏感文档”之类的一般性指南。

在推出这些解决方案之前，你可能希望向最终用户发送广泛公告，让他们知道即将发生一些更改以帮助保护公司数据，且可能需要他们也做出一些改变。 下表后面包含了一个示例通信。

> [!NOTE]
> 如果你对本指南有任何问题和意见，请使用本页上的反馈机制或发送电子邮件消息至 [AskIPTeam@Microsoft.com](mailto:%20askipteam@microsoft.com?subject=Rapid%20Deployment%20Guide%20feedback)。

## Azure RMS 的方案
为了帮助你更加快速地部署 Azure RMS 以解决具体的业务问题，请选择与你的业务目标最接近的方案，并根据需要进行调整。



**通过电子邮件安全地将 Office 文件发送给另一个组织中的用户，并能够跟踪对该文件的后续访问（企业间协作）。**

例如：

- 向客户发送价目表、路线图或发行计划

- 向供应商发送工单或营销规范

- 向合作伙伴发送招标或报价请求 (RFQ)

请参阅：[方案 - 与另一组织中的用户共享 Office 文件](scenario-share-office-file-externally.md)

**确保在 SharePoint 库中存储的文档保持受你控制**

例如：

- 部门电子表格和报告

- 针对设计文档或其他可交付成果的跨团队协作

请参阅：[方案 - 保留对 SharePoint 中所存储文档的控制](scenario-sharepoint.md)

**高层管理人员可以安全地通过电子邮件交换特权信息**

例如：

- 共享收购计划

- 讨论或传播法律问题

- 有关潜在裁员或其他敏感话题的信息

请参阅：[方案 - 高级管理人员安全地交换特权信息](scenario-executives-email.md)

**自动保护文件服务器上的所有文件**

例如：

- 必须保留在公司内部以避免知识产权损失的 CAD 文档

- 必须保密，防止公开披露以保持竞争优势的营销促销计划和日期

请参阅：[方案 - 保护文件服务器共享上的文件](scenario-fci.md)

**严格保护你的机密性最强、对业务影响最大的文档**

例如：

- 你的公司所特有的配方或公式信息

- 高度机密的接管或并购计划

- 自然资源开发数据

请参阅：[方案 - 保护你最重要的&#40;几个&#41;文件](scenario-secure-most-valuable-files.md)

**安全发送公司机密电子邮件和附件**

例如：

- 公司愿景陈述

- 组织结构图、重组新闻或促销公告

- 公司政策信息

请参阅：[方案 - 发送公司机密电子邮件](scenario-company-confidential-email.md)

**持续保护工作文件夹中的 Office 文件**

例如：

- 针对公司机密项目的本地编辑的 Word 文档

- 包含敏感数据或高度业务影响数据的本地创建的电子表格

- 禁止泄露或意外与组织外人员共享的本地存储的工作进度 PowerPoint 演示文稿，除非这些演示文稿是最终版本

请参阅：[方案 - 配置工作文件夹的持续保护](scenario-work-folders.md)




## 推出前的用户公告
你可以使用以下示例通信邮件来通知用户，部署 Azure RMS 后将发生一些更改。 复制粘贴以下文本，由组织领导团队中的某位成员（最好是首席执行官）通过电子邮件发送给所有人。 考虑对本文本进行任何更改，以使消息与用户和你的组织更加相关。

![Azure RMS 快速部署的用户文档横幅示例](../media/AzRMS_ExampleBanner.png)

### 旨在保护数据安全的更改
你是否曾经有过误将某个文档发送给合作伙伴后，希望阻止对该文档的访问？ 你是否想过有任何方法知道哪些客户阅读了你发送的最新产品新闻？ 你是否需要共享机密产品信息，而不必担心这些信息可能发送给不应看到的人员？

你将很快能够做到这些事情，因为 IT 部门正在推出一些更改，实施 Microsoft Azure Rights Management (Azure RMS) 作为企业数据保护解决方案。 许多这些解决方案将自动应用我们所需的保护，而你无需做出任何改变。 但也有一些更改可能需要你进行些许改变，在这种情况下，IT 部门将给你发送信息和说明，如果你有任何疑问或问题，还能获得技术支持部门的支持。

例如，若要跟踪（必要时撤消）你所共享的文档，需使用文档跟踪网站：

![Azure RMS 文档跟踪屏幕截图](../media/AzRMS_Tutorial_5_Screenshots.png)

若要抢先了解它的工作原理，请观看这段时长 2 分钟的视频：[Azure RMS 文档跟踪和撤消](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

该组织最有价值的资产之一就是数据 - 我们每天生成、存储和使用的数据。 它使我们具有一定的竞争优势，并帮助我们取得成功。 正因如此，我们必须保留对数据的控制并确保没有访问权限的人员无法访问数据，这一点非常重要。

我们实施的解决方案将能帮助我们保护重要数据的安全，并为你提供用于控制这些数据的工具。 感谢你在我们实施这些更改的过程中所给予的合作。




<!--HONumber=Jul16_HO3-->


