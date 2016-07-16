---
title: "Azure RMS 快速入门教程 - 步骤 3 | Azure RMS"
description: "使用本教程的第三步，可以快速试用适合你的组织的 Microsoft Azure Rights Management，只需执行 5 个步骤，所需时间不到 15 分钟。"
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c604e749-8918-40e8-8148-6bd000cb2be2
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: efe389db839f3f70e9cdb9138f6749e2bd2e029f


---


# Azure RMS 快速启动步骤 3：通过电子邮件发送要保护的文档

*适用于：Azure Rights Management、Office 365*


跳转到： 
> [!div class="op_single_selector"]
- [简介](quick-start-tutorial.md)
- [步骤 1：激活 Azure RMS](tutorial-step1.md)
- [步骤 2：安装 RMS 共享应用](tutorial-step2.md)
- [步骤 3：通过电子邮件发送机密文档](tutorial-step3.md)
- [步骤 4：收件人读取文档](tutorial-step4.md)
- [步骤 5：跟踪你的文档](tutorial-step5.md)


就这一步来说，首先请使用 Word 创建并保存一个文档，该文档表示你想要保护的文档，可以将其命名为 **Confidential.docx**。 就本教程来说，该文档实际包含什么文本并不重要，而之所以需要让其包含一些文本，是为了方便你确认所授权的收件人能够阅读它。 例如，你可以键入： **如果你可以阅读电子邮件附件中的此内容，则说明发件人已通过 Azure RMS 成功共享了受保护的文件。**

然后你就可以安全地通过电子邮件共享此文档。

![Azure RMS 快速入门教程步骤 3](../media/AzRMS_Tutorial_3_Screenshots.png)

### 通过电子邮件安全地共享你的文档

1.  使用 Outlook 创建一封新邮件，然后将你刚创建的文件添加到附件中。

2.  在 **“收件人”** 框中，键入一个或多个业务电子邮件地址。 请务必指定业务电子邮件地址，例如 **janetm@contoso.com** 或 **p.dover@fabrikam.com**，因为 Azure Rights Management 目前不支持 Internet 提供商提供的可以在家里使用的个人电子邮件地址。 请不要担心你向其发送电子邮件的人是否也有 Azure 权限管理。

3.  键入一个主题，例如  **“机密文档”** ，然后键入简短的电子邮件内容，例如 **“请阅读此机密文档，不要与其他人共享。”**

4.  然后，在 **“RMS”** 组的 **“消息”** 选项卡中，单击 **“共享保护项”** ，然后再次单击 **“共享保护项”** ：

5.  在 **“共享保护项”** 对话框中，执行以下操作：

    1.  选择 **“查看者 – 仅查看”**。

        这意味着收件人能够查看该文档，但不能进行编辑或打印。

    2.  选择 **“当有人尝试打开这些文档时，给我发电子邮件”**。

        每次收件人尝试打开该附件时，你都会收到电子邮件通知。另外，如果其他人尝试打开该附件（例如，收件人将电子邮件转发给同事），你也会收到电子邮件通知。 在最后这种情况中，你会看到访问被拒绝，你可以根据用户详细信息来决定是否向该人发送一份允许其打开的文档。

    3.  选择 **“允许我立即撤消对这些文档的访问权限”**。

        此选项要求收件人每次打开该附件时都要有 Internet 连接，但好处是，如果你在以后撤销该文档，则收件人下次将无法打开它。 如果你不选择此选项，则收件人在没有 Internet 连接的情况下也可以打开该文档，但坏处是，如果你在以后撤销该文档，则可能需要延迟一段时间才能生效。

    4.  单击 **“立即发送”**。

        将向你所指定的电子邮件地址发送带附件的电子邮件。 除了你的电子邮件，他们还会看到有关如何阅读受 Azure 权限管理保护的附加文档的说明。

现在，你已发送受保护文档，你可以要求收件人等待该文档，在其到达后打开它。 但请勿关闭 Outlook，因为我们需要在最后一步再次使用它来跟踪该附件。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|有关保护通过电子邮件进行共享的文件的完整说明和替代方法|[使用 Rights Management 共享应用程序保护通过电子邮件共享的文件](../rms-client/sharing-app-protect-by-email.md)|
|关于“共享保护项”对话框中的选项|[权限管理共享应用程序的的对话框选项](../rms-client/sharing-app-dialog-box.md)|


>[!div class="step-by-step"]
[« 步骤 2](tutorial-step2.md)
[步骤 4 »](tutorial-step4.md)


<!--HONumber=Jun16_HO4-->


