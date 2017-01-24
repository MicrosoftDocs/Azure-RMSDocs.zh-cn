---
title: "Rights Management 共享应用程序用户指南 | Azure 信息保护"
description: "适用于 Windows 的 Microsoft Rights Management (RMS) 共享应用程序可帮助你防止外人查看重要文档和图片，保护文档和图片的安全，即使你通过电子邮件发送它们或将其保存到另一台设备也是如此。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: eaf6d02c-aa36-4915-856e-49bb71ab1484
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 8acc80758eb27cfbe537b705342220418c22fa96


---

# <a name="rights-management-sharing-application-user-guide"></a>权限管理共享应用程序用户指南

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、具有 SP1 的 Windows 7、Windows 8、Windows 8.1*

适用于 Windows 的 Microsoft Rights Management (RMS) 共享应用程序可帮助你防止外人查看重要文档和图片，保护文档和图片的安全，即使你通过电子邮件发送它们或将其保存到另一台设备也是如此。 你还可以通过此应用程序，打开并使用其他人已通过使用相同的 Rights Management 保护技术保护的文件。

你只需一台至少运行 Windows 7 with Service Pack 1 的计算机即可。 然后从 Microsoft [下载并安装](http://go.microsoft.com/fwlink/?LinkId=303970) 这款免费的应用程序。

如果你的疑问在本指南中没有相应解答，请参阅 [适用于 Windows 的 Microsoft Rights Management 共享应用程序常见问题](http://go.microsoft.com/fwlink/?LinkId=303971)。 此页还提供了一些故障排除信息，如果你遇到了问题，可用作参考。

## <a name="examples-for-using-the-rms-sharing-application"></a>使用 RMS 共享应用程序的示例
下面只是一些示例，演示了如何使用 RMS 共享应用程序来帮助你保护文件。

|我想要…|如何实现|
|----------------|------------------|
|**…与我信任的、在另一个组织工作的人员安全地共享财务信息**<br /><br />你与合作伙伴公司协作，并且想要通过电子邮件向他们发送包含预期销售额的 Excel 电子表格。 你希望他们能够查看数字但不能进行更改。|使用 Excel 中功能区上的“共享保护项”  按钮，键入合作伙伴公司中与你合作的两名人员的电子邮件地址，选择“查看者 - 仅查看” ，然后单击“发送” 。<br /><br />当该电子邮件到达合作伙伴公司时，只有该电子邮件中的收件人才可以查看该电子表格，但是他们无法保存、编辑、打印或转发它。<br /><br />分步指南：[使用 Rights Management 共享应用程序，保护你通过电子邮件共享的文件](sharing-app-protect-by-email.md)。|
|**…通过电子邮件将文档安全地发送给使用 iOS 设备的人员**<br /><br />你想要通过电子邮件将高度机密的 Word 文档发送给某位同事，你知道该同事会定期在其 iOS 设备上检查电子邮件。|使用文件资源管理器右键单击该文件，然后选择“共享保护项” 以将该文件作为附件发送给你的同事。<br /><br />收件人在其 iOS 设备上接收电子邮件。 因为她没有 iPad 和 iPhone 版 Office，所以单击该电子邮件中的链接（该链接会告知如何下载共享应用程序），安装适用于 iOS 设备的版本，然后查看文档¹。<br /><br />分步指南：[使用 Rights Management 共享应用程序，保护你通过电子邮件共享的文件](sharing-app-protect-by-email.md)。|
|**…查看是谁在何时打开了我的受保护文档，并撤消访问权限（如有必要）**<br /><br />你已安全地与潜在供应商共享了机密设计文档，现在你想要查看哪些人员在何时从何处访问了它。 然后，当其中一个供应商获得业务时，你想要撤消对原始文档的访问权限，以使与你共享它的人员无法再读取它。|通过电子邮件共享文档之后，转到 [文档跟踪站点](http://go.microsoft.com/fwlink/?LinkId=529562) 来检查哪位人员在何时访问了它。 当你需要停止共享它时，可以选择撤消访问的选项。<br /><br />分步指南：[使用 RMS 共享应用程序跟踪和撤销文档](sharing-app-track-revoke.md)。|
|**…阅读在包含安全共享文件附件的电子邮件中收到的附件，但是因为我的公司不使用 Rights Management，所以我无法阅读**<br /><br />电子邮件发件人是你信任的人，因为你过去曾与他们有业务往来，你猜想他们可能向你发送了有关潜在新业务机会的信息。|照电子邮件中的说明，单击链接注册 Microsoft Rights Management。 Microsoft 将确认你的组织没有 Azure 信息保护等订阅，并向你发送一封电子邮件以完成免费注册过程，然后你便可以使用新帐户登录。 单击电子邮件中的第二个链接来安装 Rights Management 共享应用，然后可以打开电子邮件附件，阅读有关新业务机会的信息。<br /><br />分步指南：[查看和使用受 Rights Management 保护的文件](sharing-app-view-use-files.md)。|
|**…保护我的笔记本电脑上的公司机密文件，以防止非公司人员访问它们**<br /><br />你经常出差，经常使用笔记本电脑访问和更新文件夹中的文件，必须保护该文件夹以阻止未经授权的访问。|你的笔记本电脑上已安装 RMS 共享应用程序。 通过使用可快速保护文件的模板，你可以使用文件资源管理器来保护这些文件。 如果你的笔记本电脑被盗，你大可放心，任何非公司人员都无法访问这些文档。<br /><br />分步指南：[使用 Rights Management 共享应用程序保护设备上的文件&#40;就地保护&#41;](sharing-app-protect-in-place.md)。|
¹ 由 Foxit 提供技术支持的 PDF Rendering。 Foxit Corporation 版权所有 © 2003–2014。

## <a name="what-do-you-want-to-do"></a>要执行什么操作？
> [!NOTE]
> 有关详细的技术信息（例如[支持的文件类型](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)以及[如何在企业网络上安装此应用程序](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)），请参阅[《Rights Management sharing application administrator guide》](sharing-app-admin-guide.md)（Rights Management 共享应用程序管理员指南）。

- [下载并安装共享应用程序](install-sharing-app.md)

- [保护设备上的文件（就地保护）](sharing-app-protect-in-place.md)

- [保护通过电子邮件共享的文件](sharing-app-protect-by-email.md)

- [更改受保护文件的权限](sharing-app-reprotect-files.md)

- [跟踪和撤消文档](sharing-app-track-revoke.md)

- [查看和使用受保护的文件](sharing-app-view-use-files.md)

- [移除对文件的保护](sharing-app-remove-protection.md)

- [使用键盘快捷方式](sharing-app-keyboard-shortcuts.md)

- [在对话框中指定设置](sharing-app-dialog-box.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


