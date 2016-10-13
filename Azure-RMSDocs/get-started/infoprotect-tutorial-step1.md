---
title: "快速入门教程步骤 1 | Azure 信息保护"
description: "入门教程第 1 步，该教程用于快速试用适合你组织的 Microsoft Azure 信息保护，所需时间大概 30 分钟。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: b23022c5fbec3d4f6f19ab5017ecf9badf01a9e7
ms.openlocfilehash: 247ab8dd5a47f9370f03fbd5badd7c78784d20b5


---

# 步骤 1：激活权限管理服务
 
>*适用于：Azure 信息保护*

> [!NOTE]
>如果已为你的租户激活 Azure Rights Management 服务 - 请直接转到[下一步](infoprotect-tutorial-step2.md)。 

当已激活 Azure Rights Management 服务时，你可以保护组织最敏感的文档和电子邮件，并在将其与其他人共享时跟踪其使用方式。 激活此服务的方式有多种，包括使用 Windows PowerShell，以及通过管理门户导航。

对于本教程，我们将直接转到 Office 365 管理员的激活页，这也是与 Office 365 经典门户和 Office 365 管理中心预览相同的页面。 

如果想要从 Office 365 管理门户导航到此页而不是直接转到此页，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md) 中的完整说明。 如果你有权访问 Azure 门户，但无权访问 Office 365 管理员门户，也可以使用这些完整说明。

## 激活 Rights Management 服务

1. 打开一个新的浏览器窗口并直接转到 Office 365 管理员的 [Rights Management 激活页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系统提示登录，请使用 Office 365 的全局管理员帐户。

2. 在“Rights Management”页上，单击“激活”。

3. 当提示 **“是否要激活权限管理?”**时，请单击 **“激活”**。

    你现在应该看到 **“权限管理已激活”** 以及停用选项（可能需要手动刷新该页）。

    此时请勿单击 **“高级功能”**。 单击该选项会将你转到可在其中配置自定义模板的 Azure 经典门户，这些模板不是本教程所必需的。 相反，你可以关闭此页面。

这就是完成本教程第一步所要执行的所有操作。 对于生产部署，你可能想要另外配置自定义模板，或者将自定义模板替代两个默认的 Azure 权限管理模板。 但本教程不需要使用自定义模板，因此你可以转到步骤 2。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于激活 Rights Management|[激活 Azure 权限管理](../deploy-use/activate-service.md)|
|关于默认模板以及如何创建新的自定义模板|[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; 简介](infoprotect-quick-start-tutorial.md)
[步骤 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Sep16_HO4-->


