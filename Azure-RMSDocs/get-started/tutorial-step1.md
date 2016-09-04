---
title: "Azure RMS 快速入门教程 - 步骤 1 | Azure RMS"
description: "使用本教程的第一步，可以快速试用适合你的组织的 Microsoft Azure Rights Management，只需执行 5 个步骤，所需时间不到 15 分钟。"
keywords: 
author: Cabailey
manager: mbaldwin
ms.date: 06/29/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.assetid: 7c4798e6-34a0-4c3f-a47f-505764ddf322
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: c00264e6c8b99d95e8eedf9b91781484611880c3


---



# Azure RMS 快速启动步骤 1：激活 Rights Management 服务

>*适用于：Azure Rights Management、Office 365*


跳转到： 
> [!div class="op_single_selector"]
- [简介](quick-start-tutorial.md)
- [步骤 1：激活 Azure RMS](tutorial-step1.md)
- [步骤 2：安装 RMS 共享应用](tutorial-step2.md)
- [步骤 3：通过电子邮件发送机密文档](tutorial-step3.md)
- [步骤 4：收件人读取文档](tutorial-step4.md)
- [步骤 5：跟踪你的文档](tutorial-step5.md)


![Azure RMS 快速入门教程步骤 1](../media/AzRMS_QuickStartSteps1.PNG)

即使你的订阅支持 Azure 权限管理，该服务在默认情况下也是禁用的。 你可以使用 Office 365 管理中心或 Azure 经典门户来激活它：

-   如果你有一个包含 Azure Rights Management 的 Office 365 订阅，或者虽然你的 Office 365 订阅不包含 Azure Rights Management，但你有一个包含 Azure RMS Premium 的订阅，则可执行以下操作：**使用 Office 365 管理中心**。

-   如果没有 Office 365 订阅：**使用 Azure 经典门户**。

![教程步骤 1 屏幕截图](../media/AzRMS_Tutorial_1_Screenshots.png)

### 从 Office 365 经典管理中心激活 Rights Management

> [!NOTE]
> 如果你使用的是 **Office 365 管理中心预览版**，而不是 Office 365 经典管理中心，则可以使用[如何从 Office 365 管理中心预览版激活 Azure Rights Management](../deploy-use/activate-office365-preview.md) 中的说明，或切换到经典版以使用下列说明。 若要进行切换，请在登录后，单击“主页”上的“转到旧管理中心”。

1.  转到 [Office 365 门户](https://portal.office.com/)，并使用 Office 365 全局管理员帐户登录。

2.  如果未自动显示 Office 365 管理中心，请选择左上方的“应用启动程序”图标，然后选择“管理”。 “管理”  磁贴只会向 Office 365 管理员显示。

    > [!TIP]
    > 有关管理中心的帮助，请参阅 [关于 Office 365 管理中心 - 管理员帮助](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)。

3.  在左窗格中，单击“服务设置” 。

4.  单击“权限管理” 。

5.  在 **“权限管理”** 页上，单击 **“管理”**。

6.  在“Rights Management”页上，单击“激活”。

7.  当提示 **“是否要激活权限管理?”**时，请单击 **“激活”**。

你现在应该看到 **“权限管理已激活”** 以及停用选项（可能需要手动刷新该页）。

此时请勿单击**高级功能**。 单击该选项会将你转到可在其中配置模板的 Azure 经典门户，这些模板不是本教程所必需的。 与之相反，你可以关闭 Office 365 管理中心。

### 从 Azure 经典门户激活 Rights Management

1.  转到 [Azure 经典门户](http://go.microsoft.com/fwlink/p/?LinkID=275081)，并使用 Azure Active Directory 全局管理员帐户登录。

2.  在左窗格中，单击“ACTIVE DIRECTORY” 。

3.  在 **“Active Directory”** 页中，单击 **“权限管理”**。

4.  选择要进行 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的待管理目录，单击“激活”，然后确认你的操作。

**“权限管理状态”** 现在应该显示 **“活动”** ，而 **“激活”** 选项将替换为 **“停用”**。

虽然你可以在门户中配置 Rights Management 的其他选项，但这些选项不是本教程所必需的，因此可关闭 Azure 经典门户。

此第一步只需执行这些操作。 激活此服务后，你组织中的所有用户就可以对重要的和敏感的文档进行保护。 在生产环境中，你可能需要对谁能在开始的时候执行此操作进行限制，以方便分阶段部署。 不过，本教程不需要这样。

进行生产部署时，你可能还需要配置自定义模板，当然本教程不包含此部分内容。 在需要对文件进行保护时，用户可以使用模板更快速、轻松地应用正确的设置。 激活权限管理时，你将自动获得 2 个默认的模板，而在生产环境中，你可能需要使用自己的自定义模板对这些模板进行补充。 但本教程不需要模板，因此你可以转到下一步。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于激活 Rights Management 和控制激活该服务后对文件和电子邮件提供保护的人|[激活 Azure 权限管理](../deploy-use/activate-service.md)|
|关于默认模板以及如何创建新的自定义模板|[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)|


>[!div class="step-by-step"]
[« 简介](quick-start-tutorial.md)
[步骤 2 »](tutorial-step2.md)


<!--HONumber=Aug16_HO4-->


