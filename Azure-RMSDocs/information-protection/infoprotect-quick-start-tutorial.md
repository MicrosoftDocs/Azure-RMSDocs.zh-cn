---
title: "Azure 信息保护快速入门教程 | Azure 权限管理"
description: "该入门教程用于快速试用适合你组织的 Microsoft Azure 信息保护，只需 4 个步骤，所需时间不到 15 分钟。"
author: cabailey
manager: mbaldwin
ms.date: 07/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1260b9e5-dba1-41de-84fd-609076587842
translationtype: Human Translation
ms.sourcegitcommit: cac95dec84f99d2e6caa3458dc8284defe2324bc
ms.openlocfilehash: 7dc988365c1fa86827d1a7edc33c0a2eb6180f0e


---

# Azure 信息保护快速入门教程 

*适用于：Azure 信息保护预览版*

使用该教程快速试用适合你组织的 Azure 信息保护预览版，只需 4 个步骤，所需时间不到 15 分钟。 你也可以激活 Azure 权限管理服务，查看并修改默认的 Azure 信息保护策略，安装 Azure 信息保护客户端，然后使用 Word 文档在实际操作中了解分类、标签和保护。

本教程针对的是 IT 管理员和顾问，旨在帮助他们将 Azure 信息保护作为组织的企业信息保护解决方案进行评估。 在生产环境中，将由管理员执行激活服务、配置信息保护策略和为用户安装客户端等操作。 为文档设置标签的操作将由最终用户完成。 本教程中包含了这两组操作，用于演示对组织的数据进行分类、设置标签和保护的端到端场景。 

如果在完成本教程、使用 Azure 信息保护预览版中有任何问题，或者你想要查看别人对此版本的评论，请访问 [Azure 信息保护 Yammer 站点](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)。

## 先决条件 
若要完成本教程，你需要满足以下先决条件：

- 具有包括 Azure 权限管理的任何订阅，该订阅将为你提供访问 Azure 信息保护预览版的权限。 Azure 信息保护可用于支持 Azure 权限管理的所有区域。 有关免费试用版的可用订阅和链接的详细信息，请参阅[《Azure RMS requirements: Cloud subscriptions that support Azure RMS》](../get-started/requirements-subscriptions.md)（Azure RMS 要求：支持 Azure RMS 的云订阅）。

- 具有 Azure 订阅，以便你可以访问 Azure 门户以配置 Azure 信息保护策略。 如果你的组织还没有 Azure 订阅，则可以通过注册免费试用版来获取订阅：转到 [Azure 入门](https://account.windowsazure.com/organization)页并按照说明进行操作。

  > [!TIP] 
  > 如果你需要获取其中一个或这两个订阅，请提前进行，因为该过程有时需要一定的时间才能完成。

- 用于登录到 Office 365 管理中心或 Azure 经典门户的管理员帐户，你可以使用该帐户来激活 Rights Management 服务。 此帐户还必须有电子邮件地址和可用的电子邮件服务（例如，Exchange Online 或 Exchange Server）。

- 运行 Windows（最低配置为 Windows 7 Service Pack 1）并已安装 Office 2016、Office 2013 Service Pack 1 或 Office 2010 的计算机。 

- 如果你的组织中部署了 Active Directory Rights Management Services (AD RMS)：该计算机必须是以前未使用 AD RMS 的工作组计算机。 如果你想要保护文档，并确保计算机仅从 Azure 权限管理下载模板，则该条件是必需的。 不支持计算机同时连接到 AD RMS 和 Azure RMS。 如果你对迁移信息感兴趣，请参阅[从 AD RMS 迁移到 Azure 权限管理](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。   

让我们开始吧。

>[!div class="step-by-step"]
[&#187; 步骤 1](infoprotect-tutorial-step1.md)





<!--HONumber=Jul16_HO3-->


