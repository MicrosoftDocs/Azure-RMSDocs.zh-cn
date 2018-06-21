---
title: 快速入门教程步骤 5 - AIP
description: 快速试用 Azure 信息保护入门教程步骤 5 - 共享受保护的文件和跟踪文件。
keywords: ''
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/09/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4e59a3b3-f0f4-4535-8b96-cac68303d855
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7c6acb5a4b5c8f33193cbf5d8833201e0d68287e
ms.sourcegitcommit: 342b0bd8c57eb621714609ec28234dd07fe95d1e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "33946430"
---
# <a name="step-5-see-sharing-of-protected-files-in-action-and-track-your-document"></a>步骤 5：了解如何在实际操作中共享受保护的文件和如何跟踪文档 

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

在本教程的最后一步中，找到已创建的 Word 文档或 Excel 电子表格，将其发送到合作伙伴或同事。 就本教程来说，该文档实际包含什么文本并不重要，而之所以需要让其包含一些文本，是为了方便你确认所授权的收件人能够阅读它。

然后你就可以安全地通过电子邮件共享此文档。 

## <a name="to-safely-share-your-document-by-email"></a>通过电子邮件安全地共享你的文档

1. 在文件资源管理器中，右键单击文档，然后选择“分类和保护”。 “分类和保护 - Azure 信息保护”对话框将打开：

    ![Azure 信息保护快速入门教程步骤 5 - 右键单击“分类和保护”](../media/classify-protect-dialog.png)

2. 选择“使用自定义权限保护”，这将显示其他选项。

3. 对于“选择权限”，请保留默认值“查看器 - 仅查看”。

    使用此设置，收件人能够查看该文档，但不能进行编辑或打印。

4. 对于“选择用户”，请键入一个或多个企业电子邮件地址，如同将文档发送给与组织有业务往来的某人时的操作一样。 若要指定多个地址，请使用分号，或按 Enter。 

    请务必指定企业电子邮件地址，例如 janetm@contoso.com 或 p.dover@fabrikam.com，因为 Azure 信息保护目前不支持此方案的个人电子邮件地址。 

    或者，可单击“选择用户、组或组织”图标，选择同事的电子邮件地址：

    ![Azure 信息保护快速入门教程步骤 5 - 使用自定义权限保护](../media/protect-custom-permissions.png)  
    
    指定地址后，请将地址复制到剪贴板，因为我们将在稍后的步骤中用到它们。

5. 单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。

4. 返回文件资源管理器，再次右键单击你的文件，这次请选择“发送到” > “邮件收件人”。 此操作会将你的文档附加到电子邮件，我们将更改某些默认文本。

5. 更改默认文本之前，请将之前指定的电子邮件地址粘贴到“收件人”框。 

6. （可选）请在“主题”框中键入想要的主题，例如，“我正在共享受保护的文档”。 

7. 修改默认邮件描述，使其适合你的收件人。 但是，请添加以下文本：

    **我已使用 Microsoft Azure 信息保护对文件提供保护。若是首次使用，请参阅这些说明：https://aka.ms/rms-signup。** 

    ![Azure 信息保护快速入门教程步骤 5 — 通过电子邮件共享受保护的文档](../media/share-protected-emailv2.png)

    单击“发送”。

现在，你已发送受保护文档，你可以要求收件人等待该文档，在其到达后打开它。 

## <a name="ask-your-recipients-to-open-the-emailed-document"></a>要求收件人打开通过电子邮件发送的文档

收件人可以使用很多设备来阅读你以电子邮件附件形式发送的受保护文档。 这些设备包括 iPad、iPhone、Android 平板电脑和手机、Mac 计算机，以及 Windows 计算机。

要求他们阅读你发送的电子邮件。 如果这是他们第一次收到受 Rights Management 保护的附件，请要求他们单击说明链接。 然后他们将看到 Microsoft Azure 信息保护的“欢迎”页，该页将要求他们输入工作电子邮件地址。

如果他们单击“注册”，Azure 信息保护将检查他们的组织是否具有包含 Azure 权限管理数据保护服务的订阅。 如果没有，则可以申请一个免费帐户。

### <a name="instructions-for-recipient-to-view-the-protected-document-attachment"></a>收件人说明：查看受保护的文档附件

1. 在已安装 Office 的电脑或移动设备上，打开附件以阅读该文档。  

2.  如果系统提示你输入用户名和密码，请在输入用户名时采用与发送电子邮件和附件时所用电子邮件地址相同的格式。 例如，**janetm@contoso.com** 或 **p.dover@fabrikam.com**。至于密码，请键入注册个人 RMS 时提供的密码。 或者，如果组织有诸如 Office 365 等云服务，或使用 Azure，请输入平时使用的工作密码。

3. 打开后请阅读文档内容。 由于该文档为只读文档，因此无法更改其内容。

收件人可能将电子邮件转发给原始电子邮件中未指定的其他人。 这些人无法打开附件。 当系统要求他们提供用户名时，将会拒绝其对文档的访问。

现在，收件人已打开该附件并选择性地将其转发给他人，你可以跟踪文档。

## <a name="to-track-your-protected-document"></a>跟踪受保护文档

1.  打开保护和共享的文档。 信息横幅将确认你指定的自定义保护设置：

    ![自定义保护的信息横幅](../media/information-banner-custom-protection.png)

2.  在“**开始**”选项卡中，依次单击“**保护**” > “**跟踪和撤销**”：

    ![跟踪使用情况选项](../media/track-usage-calloutv3.png)

    该操作可转到文档跟踪站点。

2.  如果你看到**按你的方式保护和共享**页，请单击**登录**，然后再次提供用户名和密码。

3.  在“你的共享文档”页上，可看到共享的文档名称。 此时，该文档是唯一显示的文件，但当你共享更多的受保护文档时，此列表会扩大。

    在此页上，你会看到你何时共享了该文档（何时发送了带受保护附件的电子邮件）、其当前状态（活动、撤销或过期），以及你向其发送电子邮件的收件人的名称。 单击文档名可获取更多详细信息。

4.  在新页（包含你所单击的文件的名称）上，你只会看到该文档的摘要详细信息，以及可供文档使用的其他选项的列表（**“列表”**、 **“时间线”**、 **“映射”**、 **“设置”**）。

    单击每个选项，了解如何使用不同的方式来跟踪受保护文档。 此外，你也可以在 **“摘要”** 页上单击 **“在 Excel 中打开”** 以将信息导出到电子表格，或者单击 **“撤消访问权限”** 以停止共享该文档。

你可以返回此站点来跟踪受保护文档的更多活动，或者根据需要撤消访问权限。 你甚至可以通过移动设备或平板电脑来访问该站点，只需使用浏览器访问以下链接即可： [文档跟踪](http://go.microsoft.com/fwlink/?LinkId=529562)



|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|有关保护之后可安全共享的文件的完整说明|[对文件或电子邮件进行分类和保护](../rms-client/client-classify-protect.md)|
|关于供其他用户注册的免费帐户|[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|关于文档跟踪站点的使用|[跟踪和撤消文档](../rms-client/client-track-revoke.md)


## <a name="next-steps"></a>后续步骤

现在你已经了解了默认的 Azure 信息保护策略和如何自定义该策略，以及如何在 Word 文档中使用标签，你可以尝试一些其他设置，了解在支持 Azure 信息保护的其他 Office 应用中是如何使用这些设置的：Excel、PowerPoint、Outlook。 如果在安装 Azure 信息保护客户端时这些应用已打开，请关闭并重新打开它们，然后再尝试将它们与 Azure 信息保护结合使用。

尝试共享更多的文档，跟踪文档的使用情况，以及确认文档撤销的方式。

然后你会发现以下一系列操作很有用处：返回到 Azure 门户的“快速入门”页，阅读 Azure 信息保护的一些[常见问题](faqs.md)并浏览一些其他文档文章。 但是，如果已准备好开始为组织部署 Azure 信息保护，那么下一步应为 [Azure 信息保护部署路线图](../plan-design/deployment-roadmap.md)。 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]