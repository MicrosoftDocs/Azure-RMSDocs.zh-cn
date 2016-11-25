---
title: "快速入门教程步骤 5 | Azure 信息保护"
description: "入门教程第 5 步，快速试用适合组织的 Microsoft Azure 信息保护，所需时间大概 30 分钟。"
keywords: 
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4e59a3b3-f0f4-4535-8b96-cac68303d855
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 5844ddd3f675cdc5a88de3abc3170d7e8a89aee9


---


# <a name="step-5-see-sharing-of-protected-files-in-action-and-track-your-document"></a>步骤 5：了解如何在实际操作中共享受保护的文件和如何跟踪文档 

>适用于：Azure 信息保护

在本教程的最后一步中，找到已创建的 Word 文档，将其发送到合作伙伴或同事。 就本教程来说，该文档实际包含什么文本并不重要，而之所以需要让其包含一些文本，是为了方便你确认所授权的收件人能够阅读它。

然后你就可以安全地通过电子邮件共享此文档。 

## <a name="to-safely-share-your-document-by-email"></a>通过电子邮件安全地共享你的文档

1.  在 Word 中打开文档。 可以看到再次自动应用了默认标签**内部**。 

2.  在“主页”选项卡上的“RMS”组中，单击“共享受保护文档”，然后在菜单中单击“共享受保护文档”：

    ![Azure 信息保护快速入门教程步骤 5 — 共享受保护文档](../media/share-protected-callout.png)

    可看到“共享受保护文档”对话框，类似于此图片：

    ![Azure 信息保护快速入门教程步骤 5 — 共享受保护文档对话框](../media/example-share-protected-dialog.png)

3. 在“用户”框中，键入一个或多个企业电子邮件地址，如同将文档发送给与组织有业务往来的某人时的操作一样。 或者，指定同事的电子邮件地址。 请务必指定企业电子邮件地址，例如 **janetm@contoso.com** 或 **p.dover@fabrikam.com**，因为 Azure 信息保护目前不支持个人电子邮件地址。 

    请不要担心接收电子邮件的人是否也使用 Azure 信息保护。

4. 选择 **“查看者 – 仅查看”**。

    这意味着收件人能够查看该文档，但不能进行编辑或打印。

5. 选择 **“当有人尝试打开这些文档时，给我发电子邮件”**。

    每次收件人尝试打开该附件时，你都会收到电子邮件通知。另外，如果其他人尝试打开该附件（例如，收件人将电子邮件转发给同事），你也会收到电子邮件通知。 如果文档被转发，会看到访问被拒绝，并且可以根据用户详细信息来决定是否向此人发送一份允许其打开的文档。

6. 选择 **“允许我立即撤消对这些文档的访问权限”**。

    此选项要求收件人每次打开该附件时都要有 Internet 连接，但好处是，如果你在以后撤销该文档，则收件人下次将无法打开它。 

4.  单击“发送”可查看要发送给指定收件人的电子邮件，其中包含默认的说明文本。 例如：

    ![共享受保护文档时的示例电子邮件](../media/example-email-share-protected.png)
    
    **注意**：如果安装 Azure 信息保护客户端时 Outlook 为打开状态，则看不到上面图片中的信息保护栏：该信息保护栏并不专门用于演示共享受保护文档的步骤中，因此不需要关闭并重新打开 Outlook 来完成本教程。 如果安装 Azure 信息保护客户端后打开 Outlook，会看到类似于初次打开时的 Word 文档的电子邮件，由于 Azure 信息保护策略中配置的全局设置，该邮件默认应用了**内部**标签。
    
    你会注意到有两个附件：原始的 Word 文档和名称相同但具有 **.ppdf** 文件扩展名的文件。 .ppdf 版本是一个由 Rights Management 共享应用程序自动创建的受保护的 PDF 文件，用于预防收件人不具备支持受保护的文档的 Office 版本的情况。 此附加文件使收件人可通过使用随 Rights Management 共享应用程序一同安装的查看器来阅读受保护的文档。

    在电子邮件中单击“发送”。

现在，你已发送受保护文档，你可以要求收件人等待该文档，在其到达后打开它。 但请勿关闭 Word，因为需要在最后一步中再次使用它来跟踪共享的文档。

## <a name="ask-your-recipients-to-open-the-emailed-document"></a>要求收件人打开通过电子邮件发送的文档

收件人可以使用很多设备来阅读你以电子邮件附件形式发送的受保护文档。 这些设备包括 iPad、iPhone、Android 平板电脑和手机、Mac 计算机，以及 Windows 计算机。

要求他们阅读你发送的电子邮件。 如果这是他们第一次收到受 Rights Management 保护的附件，请要求他们单击说明链接。 之后他们看到[欢迎使用 Microsoft RMS！](https://portal.azurerms.com/#/rmshelp) 页面，其中显示了如何安装 RMS 共享应用程序的说明，以及如何在必要时注册免费的帐户。 然后他们就可以阅读受保护的附件。

### <a name="instructions-for-recipient-to-view-the-protected-document-attachment"></a>收件人说明：查看受保护的文档附件

1. 打开其中一个附件来阅读此文档：
    
    - 如果设备上安装了支持 Rights Management 的 Office 版本：
    
        -  打开文件扩展名为 **.docx** 的文档。
        
    - 如果没有安装支持 Rights Management 的 Office 版本，或者不确定，又或者只是想要尝试 Rights Management 共享应用程序中的查看器，那么： 
    
        - 打开文件扩展名为 **.ppdf** 的文档。

2.  如果系统提示你输入用户名和密码，请在输入用户名时采用与发送电子邮件和附件时所用电子邮件地址相同的格式。 例如，**janetm@contoso.com** 或 **p.dover@fabrikam.com**。 至于密码，请键入注册个人 RMS 时提供的密码。 或者，如果组织有诸如 Office 365 等云服务，或使用 Azure，请输入平时使用的工作密码。

3. 打开后请阅读文档内容。 由于该文档为只读文档，因此无法更改其内容。

收件人可能将电子邮件转发给原始电子邮件中未指定的其他人。 这些人无法打开附件。 当系统要求他们提供用户名时，将会拒绝其对文档的访问。

现在，收件人已打开该附件并选择性地将其转发给他人，因此正常情况下你会获得电子邮件通知，该通知会报告此活动。 不过，时间越长，电子邮件越不容易查找，因此若要跟踪谁访问了你的文档，更好的方法是使用文档跟踪站点，这会在最后一步进行介绍。

## <a name="to-track-your-protected-document"></a>跟踪受保护文档

1.  返回到 Word，在“主页”选项卡的“RMS”组中，单击“共享受保护文档”，然后在菜单中单击“跟踪使用情况”：

    ![跟踪使用情况选项](../media/track-usage-callout.png)

    该操作可转到文档跟踪站点。

2.  如果你看到**按你的方式保护和共享**页，请单击**登录**，然后再次提供用户名和密码。

3.  在“你的共享文档”页上，可看到共享的文档名称。 此时，该文档是唯一显示的文件，但当你共享更多的受保护文档时，此列表会扩大。

    在此页上，你会看到你何时共享了该文档（何时发送了带受保护附件的电子邮件）、上次活动的日期，以及你向其发送电子邮件的收件人的名称。 单击文档名可获取更多详细信息。

4.  在新页（包含你所单击的文件的名称）上，你只会看到该文档的摘要详细信息，以及可供文档使用的其他选项的列表（**“列表”**、 **“时间线”**、 **“映射”**、 **“设置”**）。

    单击每个选项，了解如何使用不同的方式来跟踪受保护文档。 此外，你也可以在 **“摘要”** 页上单击 **“在 Excel 中打开”** 以将信息导出到电子表格，或者单击 **“撤消访问权限”** 以停止共享该文档。

你可以返回此站点来跟踪受保护文档的更多活动，或者根据需要撤消访问权限。 你甚至可以通过移动设备或平板电脑来访问该站点，只需使用浏览器访问以下链接即可： [文档跟踪](http://go.microsoft.com/fwlink/?LinkId=529562)



|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|有关保护通过电子邮件进行共享的文件的完整说明和替代方法|[使用 Rights Management 共享应用程序保护通过电子邮件共享的文件](../rms-client/sharing-app-protect-by-email.md)|
|关于“共享保护项”对话框中的选项|[Rights Management 共享应用程序的对话框选项](../rms-client/sharing-app-dialog-box.md)|
|关于供其他用户注册的免费帐户|[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|关于文档跟踪站点的使用|[跟踪和撤消文档](../rms-client/sharing-app-track-revoke.md)


## <a name="next-steps"></a>后续步骤

现在你已经了解了默认的 Azure 信息保护策略和如何自定义该策略，以及如何在 Word 文档中使用标签，你可以尝试一些其他设置，了解在支持 Azure 信息保护的其他 Office 应用中是如何使用这些设置的：Excel、PowerPoint、Outlook。 如果在安装 Azure 信息保护客户端时这些应用已打开，请关闭并重新打开它们，然后再尝试将它们与 Azure 信息保护结合使用。

尝试共享更多的文档，跟踪文档的使用情况，以及确认文档撤销的方式。

你会发现阅读 Azure 信息保护的一些[常见问题](faqs.md)和浏览其他一些文档文章很有用处。 但是，如果已准备好开始为组织部署 Azure 信息保护，那么下一步应为 [Azure 信息保护部署路线图](../plan-design/deployment-roadmap.md)。 


<!--HONumber=Nov16_HO2-->


