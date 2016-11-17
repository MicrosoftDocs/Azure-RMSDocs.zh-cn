---
title: "有关适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题 | Azure 信息保护"
description: 
keywords: "一些常见问题，帮助你使用适用于 iOS 和 Android 的 Azure 信息保护应用"
author: cabailey
manager: mbaldwin
ms.date: 11/03/2016
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2f1930f4657278d25ef6dd369866f16e4ba71644
ms.openlocfilehash: 1cafa88ded2bf951f8af93e4b27cc526735d19e8


---

# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题

*适用于：Active Directory Rights Management Services、Azure 信息保护*

此页提供有关适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题的解答。

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>可以使用 Azure 信息保护应用做些什么？

如果电子邮件应用本机不支持权限管理数据保护，通过此应用可以查看权限保护的电子邮件消息 (.rpmsg files)。 通过此应用还可以查看权限保护的 PDF 文件、图片和文本文件。 目前，无法使用此应用创建新的受保护电子邮件、对其进行答复、创建或编辑受保护文件。

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>可以打开位于受保护的 SharePoint 库和 OneDrive For Business 中的 PDF 文件吗？

是的，你可以打开其他人通过 SharePoint 和 OneDrive for Business 与你共享的受保护的 PDF 文件。 点击该链接，然后选择此应用打开文件。 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>如何开始使用查看器应用？

在移动设备上，需访问该应用支持的其中一个文件来查看操作中的查看器。 例如：

- **.rpmsg 文件**：此为权限保护的电子邮件消息，当移动设备上的电子邮件应用本机不支持权限数据保护时，会在电子邮件中以附件形式存在。 
    
    使用另一台设备可向自己发送权限保护的电子邮件消息，用户可从自己的移动设备访问。 例如，在 Windows 计算机使用 Outlook。 有关本机支持权限管理的电子邮件客户端列表，请参阅[支持 Azure Rights Management 数据保护的应用程序](../get-started/requirements-applications.md)中的“电子邮件”列。

- **权限保护的 PDF 文件**：在本机支持权限管理的 Windows 计算机或 PDF 应用程序上，使用 Rights Management 共享应用程序通过电子邮件以附件方式向自己发送权限保护的 PDF 文件。 或者，使用电子邮件地址将 PDF 文件上传到 SharePoint 保护的库，然后共享。

- **.ptxt、.pjpg 或.ppng**：在 Windows 计算机上使用 Rights Management 共享应用程序和[共享保护](sharing-app-protect-by-email.md)选项以电子邮件附件形式向自己发送受保护的文件。 有关可用于测试的文件类型的完整列表，请参阅 Rights Management 共享应用程序管理员指南中的[支持的文件类型和文件扩展名](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)部分中的第一个表。 

若要在 Azure 信息保护查看器应用中查看这些文件，请点击此电子邮件附件或链接。 系统提示选择一个应用来打开文件时，请选择“AIP 查看器”应用。 然后系统会提示登录到工作或学校帐户。 身份验证成功后，Azure 信息保护应用会显示电子邮件或文件以供阅读。

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>登录此应用应使用什么凭据？

如果你的组织已经具有本地 AD RMS（带有移动设备扩展名），或使用 Azure Rights Management 服务，则可以使用你的凭据进行登录。 如果没有，则可以使用 [Azure 信息保护页](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)注册一个免费的新帐户。

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>可以使用个人电子邮件地址（如 Hotmail 或 Gmail 帐户）注册免费帐户吗？

不行。 现在，只能使用业务电子邮件地址（工作或学校帐户）注册。 我们正致力于研究对个人单子邮件地址的支持，会在其可用时更新此项。

## <a name="which-file-extensions-can-i-open-with-this-app"></a>使用此应用可打开哪些文件扩展名？

可以打开 .rpmsg、.pdf、.ppdf、.pjpg、.ptxt 以及几个其他的文本和图像文件格式。

##  <a name="how-do-i-provide-feedback-about-this-app"></a>如何提供有关此应用的反馈？

在应用中，转到“设置” > “发送反馈”。


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>我的问题没有得到相应解答 - 应采取何种操作？

将你的问题发布到我们的 [Yammer 站点](http://www.yammer.com/AskIPTeam)，或[发送电子邮件到信息保护团队](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app)。



<!--HONumber=Nov16_HO1-->


