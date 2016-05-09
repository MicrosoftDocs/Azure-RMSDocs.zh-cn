---
# required metadata

title: Azure RMS 快速入门教程 - 步骤 4 | Azure RMS
description: 使用本教程的第四步，可以快速试用适合你的组织的 Microsoft Azure Rights Management，只需执行 5 个步骤，所需时间不到 15 分钟。
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: f8340056-87a1-4daa-8b63-3d95fc381b9c

# optional metadata

ROBOTS: 
audience:
ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm:
ms.technology:
ms.custom:

---


# Azure RMS 快速启动步骤 4：请收件人打开通过电子邮件发送的文档

跳转到： 
> [!div class="op_single_selector"]
- [简介](quick-start-tutorial.md)
- [步骤 1：激活 Azure RMS](tutorial-step1.md)
- [步骤 2：安装 RMS 共享应用](tutorial-step2.md)
- [步骤 3：通过电子邮件发送机密文档](tutorial-step3.md)
- [步骤 4：收件人读取文档](tutorial-step4.md)
- [步骤 5：跟踪你的文档](tutorial-step5.md)


![](../media/AzRMS_QuickStartSteps4.PNG)

收件人可以使用很多设备来阅读你以电子邮件附件形式发送的受保护文档。 这些设备包括 iPad、iPhone、Android 平板电脑和手机、Mac 计算机，以及 Windows 计算机。

要求他们阅读你发送的电子邮件。 他们会看到你的电子邮件，而在此之前，他们会看到以下文本：

**发件人已使用 Microsoft RMS 保护了附件。必须**[登录](http://aka.ms/rms)
      **才能打开它们。**

当他们单击此链接时，会显示相关说明，告知他们如何安装 RMS 共享应用程序，以及如何在必要时注册免费的帐户。 该免费帐户提供个人 RMS 订阅，因此可确保被授权的用户始终能够阅读受保护的文档，即使其组织没有 Azure RMS。 然后，他们就可以根据以下说明阅读受保护的附件。

![](../media/AzRMS_Tutorial_4_Screenshots.png)

### 查看受保护的文档附件

1.  由于 Azure 权限管理对 Word 文档进行了保护，因此该电子邮件有两个附件。 这实际上是同一文件的两个版本，仅文件扩展名不同。 打开文件扩展名为 **.ppdf** 的版本 (**Confidential.ppdf**)。

    如果[设备上具有支持 Rights Management 的 Office 版本](https://technet.microsoft.com/library/dn655136.aspx)，则可以打开该文件 (**Confidential.docx**) 的其他版本，让其在 Word 中打开。

2.  如果系统提示你输入用户名和密码，请在输入用户名时采用与发送电子邮件和附件时所用电子邮件地址相同的格式。 例如，**janetm@contoso.com** 或 **p.dover@fabrikam.com**。 至于密码，请键入注册个人 RMS 时提供的密码。 如果你的组织有 Azure RMS，则也可输入通常的工作密码。

此时该文档会打开，你可以阅读其内容。 例如，文档内容可能是：**如果你可以阅读电子邮件附件中的此内容，则说明发件人已通过 Azure RMS 成功共享了受保护的文件。** 由于该文档为只读文档，因此无法更改其内容。

你也可以要求收件人将电子邮件转发给没有包括在你的原始电子邮件中的其他人，此为可选步骤。 即使这些其他人所工作的组织有 Azure 权限管理，或者这些人申请了自己的个人 RMS 订阅，他们也无法打开该附件。 当系统要求他们提供用户名时，将会拒绝其对文档的访问。

现在，收件人已打开该附件并选择性地将其转发给他人，因此正常情况下你会获得电子邮件通知，该通知会报告此活动。 不过，时间越长，电子邮件越不容易查找，因此若要跟踪谁访问了你的文档，更好的方法是使用文档跟踪站点，这会在最后一步进行介绍。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于如何查看受 Azure Rights Management 保护的文件的完整说明|[查看和使用受权限管理保护的文件](../rms-client/sharing-app-view-use-files.md)|
|关于免费订阅：个人 RMS|[个人 RMS 和 Azure 权限管理](../understand-explore/rms-for-individuals.md)|
|关于你所看到的两个版本的电子邮件附件文件|[自动创建的 .ppdf 文件是什么文件？](../rms-client/sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)|


>[!div class="step-by-step"]
[« 步骤 3](tutorial-step3.md)
[步骤 5 »](tutorial-step5.md)

<!--HONumber=Apr16_HO3-->


