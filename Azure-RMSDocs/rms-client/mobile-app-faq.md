---
title: 适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答
description: 一些常见问题，帮助你使用适用于 iOS 和 Android 的 Azure 信息保护应用
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/31/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: askipteam
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: fe86802c70276633439c1eaaa37160aa1dd0ff79
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252786"
---
# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题

适用于：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*

此页提供有关适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题的解答。

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>可以使用 Azure 信息保护应用做些什么？

如果电子邮件应用本机不支持权限管理数据保护，通过此应用可以查看权限保护的电子邮件消息 (.rpmsg files)。 通过此应用还可以查看权限保护的 PDF 文档、图片和文本文件。 

由于此应用是一个查看器，无法使用它来创建新的受保护电子邮件、对其进行答复、创建或编辑受保护文件。 此外，应用无法打开所查看文件的附件。 例如，受保护的 PDF 文档或受权限保护的电子邮件中的附件。

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>可以打开位于受保护的 SharePoint 库和 OneDrive for Business 中的 PDF 文件吗？

是的，你可以打开其他人通过 SharePoint 和 OneDrive for Business 与你共享的受保护的 PDF 文件。 点击该链接，然后选择此应用打开文件。 

此应用也可以打开 SharePoint 和 OneDrive for Business 以外的受保护 PDF 文件（受保护的 PDF 和 .ppdf 文件）。

## <a name="can-my-mobile-device-run-the-azure-information-protection-app"></a>我的移动设备是否可运行 Azure 信息保护应用？

Azure 信息保护应用要求最低版本为 **iOS 8** 或 **Android 4.4**。

如果具有这些版本或更高版本，可安装要在移动设备上运行的应用：

- 如果移动设备由 Microsoft Intune 管理，可能可以从公司门户安装 Azure 信息保护应用。

- 如果移动设备不受 Microsoft Intune 管理或公司门户不提供 Azure 信息保护应用，则可以直接从 iTunes 应用商店和 Google Play 应用商店安装应用，也可以通过在 [Azure 信息保护下载页面](https://portal.azurerms.com/#/download)中单击**移动设备**部分中的 iOS 或 Android 图标来安装应用。 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>如何开始使用查看器应用？

安装该应用后，你无需在该点再执行任何其他操作。 请等待，直到收到受保护的电子邮件或想要查看的文件，然后选择“AIP 查看器”以将其打开。 然后系统会提示使用工作或学校帐户登录，或提示选择一个证书。 对这些凭据进行身份验证后，便可以读取内容。

但是，如果不想等待，可以使用以下说明向自己发送受保护的电子邮件或文件来查看：[适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用入门](mobile-app-get-started.md) 

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>登录此应用应使用什么凭据？

如果你的组织已经具有本地 AD RMS（带有移动设备扩展名），或使用 Azure Rights Management 服务，则使用你的工作凭据进行登录。 

如果你的个人电子邮件地址用于保护该文件，则使用免费 [Microsoft 帐户](https://signup.live.com)的凭据进行登录。

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>可以使用个人电子邮件地址（如 Hotmail 或 Gmail 帐户）注册免费帐户吗？

可以，当你申请 Microsoft 帐户时，可以指定你的 Hotmail 或 Gmail 电子邮件地址或你拥有的任何其他电子邮件地址。 

但是，尽管此查看器可以打开受此帐户保护的文件，但是并非所有应用程序都可以在使用 Microsoft 帐户进行身份验证时打开受保护的内容。 [详细信息](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="which-file-extensions-can-i-open-with-this-app"></a>使用此应用可打开哪些文件扩展名？

可以打开 .rpmsg、.pdf、.ppdf、.pjpg、.pjpeg、.ptiff、.ppng、.ptxt、.pxml 以及几个其他的文本和图像文件格式。

有关文本和图像文件扩展名的完整列表，请参阅管理员指南中[分类和保护的支持文件类型](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)部分中的第一个表格。

##  <a name="how-do-i-provide-feedback-about-this-app"></a>如何提供有关此应用的反馈？

在应用中，转到“设置” > “发送反馈”。


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>我的问题没有得到相应解答 - 应采取何种操作？

请在我们的 [Yammer 网站](https://www.yammer.com/AskIPTeam)中发布问题。
