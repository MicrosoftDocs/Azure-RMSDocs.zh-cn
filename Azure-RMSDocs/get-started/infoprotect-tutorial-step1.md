---
title: "快速入门教程步骤 1 - AIP"
description: "快速试用 Azure 信息保护入门教程步骤 1 - 激活 Azure 权限管理服务。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 8ccf0ea41e9465e10408595a3b875704baca93d2
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="step-1-activate-the-rights-management-service"></a>步骤 1：激活权限管理服务
 
>*适用于：Azure 信息保护*

> [!NOTE]
>如果知道已为租户激活 Azure 权限管理服务，请直接转到“下一步”[](infoprotect-tutorial-step2.md)。 
>
>如果不确定是否已激活此服务，请使用此步骤中的说明进行检查。

如果已激活 Azure 权限管理服务，则可以保护组织最敏感的文档和电子邮件，并在将这些文档与其他人共享时跟踪受保护文档的使用状况。 激活此服务的方式有多种，包括使用 Windows PowerShell，以及使用管理门户。

在本教程中，将直接转到 Office 365 管理员管理门户中的“激活”页面。 该页面同时用于 Office 365 经典门户和 Office 365 管理中心预览。 

如果想要从 Office 365 管理门户导航到此页而不是直接转到此页，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md) 中的完整说明。 如果你有权访问 Azure 门户，但无权访问 Office 365 管理员门户，也可以使用这些完整说明。

## <a name="to-activate-the-rights-management-service"></a>激活 Rights Management 服务

1. 打开一个新的浏览器窗口并直接转到 Office 365 管理员的 [Rights Management 激活页](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系统提示登录，请使用 Office 365 的全局管理员帐户。

2. 在“Rights Management”页上，单击“激活”。 如果此按钮显示“停用”，则已激活该服务，可以直接转到“下一步”[](infoprotect-tutorial-step2.md)。 

    ![Azure 信息保护快速入门教程步骤 1 - 激活服务](../media/info-protect-activate.png)

3. 提示“是否要激活权限管理 ?”时，请单击“激活”以确认。

    你现在应该看到 **“权限管理已激活”** 以及停用选项（可能需要手动刷新该页）。

    此时请勿单击 **“高级功能”**。 单击该选项会将你转到可在其中配置自定义模板的 Azure 经典门户，这些模板不是本教程所必需的。 相反，你可以关闭此页面。

这就是完成本教程第一步所要执行的所有操作。 对于生产部署，你可能想要另外配置自定义模板，或者将自定义模板替代两个默认的 Azure 权限管理模板。 但本教程不需要使用自定义模板，因此你可以转到步骤 2。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于激活 Rights Management|[激活 Azure Rights Management](../deploy-use/activate-service.md)|
|关于默认模板以及如何创建新的自定义模板|[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; 简介](infoprotect-quick-start-tutorial.md)
[步骤 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
