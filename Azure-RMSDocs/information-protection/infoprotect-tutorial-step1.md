---
title: "Azure 信息保护快速入门教程 1 | Azure 信息保护"
description: "入门教程第 1 步，该教程用于快速试用适合你组织的 Microsoft Azure 信息保护，只需 4 个步骤，所需时间不到 15 分钟。"
author: cabailey
manager: mbaldwin
ms.date: 07/291/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: 96b5d2e53d2d1460a97a87f4037cab79b8586244


---

# 步骤 1：激活权限管理服务
 
>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

> [!NOTE]
>如果你只想对数据进行分类而不使用 Azure 权限管理进行保护，或者如果你已为租户激活 Azure 权限管理，请直接跳转到[下一步](infoprotect-tutorial-step2.md)。 

激活 Azure 权限管理之后，你可以在对最敏感文档和文件进行分类之后对其进行保护。 若要激活 Azure 权限管理，你可以使用 Office 365 管理中心或 Azure 经典门户：

-   如果你有一个包含 Azure Rights Management 的 Office 365 订阅，或者虽然你的 Office 365 订阅不包含 Azure Rights Management，但你有一个包含 Azure RMS Premium 的订阅，则可执行以下操作：**使用 Office 365 管理中心**。

-   如果没有 Office 365 订阅：**使用 Azure 经典门户**。

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

此时请勿单击 **“高级功能”**。 单击该选项会将你转到可在其中配置自定义模板的 Azure 经典门户，这些模板不是本教程所必需的。 与之相反，你可以关闭 Office 365 管理中心。

### 从 Azure 经典门户激活 Rights Management

1.  转到 [Azure 经典门户](http://go.microsoft.com/fwlink/p/?LinkID=275081)，并使用 Azure Active Directory 全局管理员帐户登录。

2.  在左窗格中，单击“ACTIVE DIRECTORY” 。

3.  在 **“Active Directory”** 页中，单击 **“权限管理”**。

4.  选择要进行 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的待管理目录，单击“激活”，然后确认你的操作。

**“权限管理状态”** 现在应该显示 **“活动”** ，而 **“激活”** 选项将替换为 **“停用”**。

虽然你可以在门户中配置 Rights Management 的其他选项，但这些选项不是本教程所必需的，因此可关闭 Azure 经典门户。

这就是第一步所要执行的所有操作。 已激活 Azure 权限管理服务，因此稍后在本教程中，你可以选择一个默认 Azure 权限管理模板，用于保护归类为“机密”的文档和电子邮件。

对于生产部署，你可能想要另外配置自定义模板，或者将自定义模板替代两个默认的 Azure 权限管理模板。 但本教程不需要使用自定义模板，因此你可以转到步骤 2。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于激活 Rights Management|[激活 Azure 权限管理](../deploy-use/activate-service.md)|
|关于默认模板以及如何创建新的自定义模板|[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; 简介](infoprotect-quick-start-tutorial.md)
[步骤 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Sep16_HO1-->


