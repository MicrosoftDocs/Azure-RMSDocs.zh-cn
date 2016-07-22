---
title: "从 AD RMS 迁移到 Azure Rights Management - 阶段 4 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ea4dd88ed749092fd02135d8ca25b621f74fe72f
ms.openlocfilehash: 7ed3569475362272ace055862fe8bb3ee072036a


---

# 迁移阶段 4 - 迁移后任务

*适用于：Active Directory Rights Management Services、Azure Rights Management*


使用以下信息，完成从 AD RMS 迁移到 Azure Rights Management (Azure RMS) 的阶段 4。 这些过程涉及[从 AD RMS 迁移到 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 中的步骤 8-9。


## 步骤 8. 解除 AD RMS 的授权

可选：从 Active Directory 中删除服务连接点 (SCP) 以防止计算机发现你的本地权限管理基础结构。 由于你在注册表中配置的重定向（例如，通过运行迁移脚本），此步骤是可选的。 若要删除服务连接点，请使用 [Rights Management Services 管理工具包](http://www.microsoft.com/download/details.aspx?id=1479)中的 AD SCP 注册工具。

监视 AD RMS 服务器的活动，例如，通过检查[系统运行状况报告中的请求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest 表](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)，或者[审核用户对受保护内容的访问权限](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)。 当你确认 RMS 客户端将不再与这些服务器进行通信，并且客户端成功使用 Azure RMS 时，你可以从这些服务器中删除 AD RMS 服务器角色。 当你调查为什么客户端未使用 Azure RMS 时，如果你使用的是专用服务器，你可能希望采取警告步骤，即先关闭服务器一段时间，以确保没有报告可能需要重新启动这些服务器以确保服务连续性的问题。

解除 AD RMS 服务器的授权后，你可能想要利用此机会来查看你在 Azure 经典门户中的模板并将其合并以使用户有较少的选项，或重新配置它们，或者甚至添加新模板。 这还将是发布默认模板的好时机。 有关详细信息，请参阅[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)。

## 步骤 9. 重新键入你的 Azure RMS 租户密钥
迁移完成时，如果 AD RMS 部署使用的是 RMS 加密模式 1，则此步骤是必需的，因为重新键入将创建使用 RMS 加密模式 2 的新租户密钥。 将 Azure RMS 与加密模式 1 配合使用仅在迁移过程中受支持。

迁移完成时，此步骤是可选的但建议使用（即使你已以 RMS 加密模式 2 运行），因为它可帮助保护你的 Azure RMS 租户密钥，使 AD RMS 密钥免遭潜在的安全漏洞的威胁。 当你重新键入 Azure RMS 租户密钥（也称为“滚动密钥”）时，将创建新的密钥，并将原始密钥存档。 但是，由于从一个密钥移到另一个密钥并不会立即发生，而是经过几周才会发生，请不要等到你怀疑原始密钥受到破坏再进行，而应在迁移完成时，立即重新键入你的 Azure RMS 租户密钥。

若要重新键入你的 Azure RMS 租户密钥，请执行以下操作：

-   如果你的 Azure RMS 租户密钥由 Microsoft 管理：若要执行此操作，[请与 Microsoft 支持部门联系](../get-started/information-support.md#to-contact-microsoft-support)以创建**请求重新键入 Azure RMS 租户密钥的 Azure Rights Management 支持案例**。 必须证明你是你 Azure RMS 租户的管理员，还须了解此过程将需要几天才能确认。 收取标准支持费用：重新键入租户密钥并不是免费支持服务。

-   如果你的 Azure RMS 租户密钥由你管理 (BYOK)：重复执行 BYOK 过程以通过 Internet 或亲自生成并创建新的密钥。

有关管理 Azure RMS 租户密钥的详细信息，请参阅[你的 Azure Rights Management 租户密钥的操作](../deploy-use/operations-tenant-key.md)。

## 后续步骤

完成迁移后，请检查[部署路线图](deployment-roadmap.md)以确定是否需要执行其他任何部署任务。




<!--HONumber=Jun16_HO5-->


