---
title: "Azure 信息保护的常见问题解答"
description: "有关 Azure 信息保护及其数据保护服务 Azure Rights Management (Azure RMS) 的一些常见问题。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ebdbb045a60e30a78b8a5536415302e912995791
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Azure 信息保护的常见问题

>*适用于：Azure 信息保护、Office 365*

是否有关于 Azure 信息保护或 Azure Rights Management 服务 (Azure RMS) 的问题？ 请查看此处是否有答案。

定期更新这些常见问题页，其中新添加的内容在 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services)（企业移动性和安全性博客）上的每月文档更新公告中列出。

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure 信息保护和 Azure Rights Management 之间有何不同？

Azure 信息保护对组织的文档和电子邮件进行分类、标记和保护。 该保护技术使用 Azure Rights Management 服务；现在该服务是 Azure 信息保护的一个组件。

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>需要为 Azure 信息保护准备哪个订阅，以及它包括哪些功能？
请参阅 Azure 信息保护网站上的[订阅信息](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)和[功能列表](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)。 

如果你的 Office 365 订阅包含权限管理，请从“功能”页下载 [Azure 信息保护授权数据表](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure 信息保护是否支持本地和混合方案？

是。 尽管 Azure 信息保护是基于云的解决方案，但它可对存储在本地和云中的文档和电子邮件进行分类、标签设置和保护。

如果具有 Exchange Server、SharePoint Server 和 Windows 文件服务器，则可部署[权限管理连接器](../deploy-use/deploy-rms-connector.md)，便于这些本地服务器可使用 Azure 权限管理服务保护电子邮件和文档。 你还可以使用 [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/)，将 Active Directory 域控制器与 Azure AD 同步和联合，为用户提供更为契合的身份验证体验。

Azure 权限管理服务根据需要自动生成并管理 XrML 证书，因此它不使用本地 PKI。 有关 Azure Rights Management 如何使用证书的详细信息，请参阅 [Azure RMS 的工作原理](../understand-explore/how-does-it-work.md)一文中的 [Azure RMS 工作演练：首次使用、内容保护、内容使用](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)。

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>听说很快将发布新版 Azure 信息保护 — 何时发布？

本技术文档不包含即将发布的版本的相关信息。 有关此类信息和发布公告，请查看 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services)（企业移动性和安全性博客）并从 Twitter 上的 [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) 获取最新更新。 如果你对 Office 版本感兴趣，还请务必查看 [Office 博客](https://blogs.office.com/)。

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>在何处可以找到 Azure 信息保护的支持信息 — 例如法律、合规性和 SLA？

请参阅 [Azure 信息保护的合规性和支持信息](../understand-explore/compliance.md)。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>如何针对 Azure 信息保护报告问题或发送反馈？

若要获取技术支持，请使用标准支持渠道或[联系 Microsoft 支持](information-support.md#to-contact-microsoft-support)。

若要提供反馈（例如，针对改进功能或新功能提出建议）：请在 Office 应用程序的“开始”选项卡的“保护”组中，单击“保护”，然后单击“帮助和反馈”。 在“Microsoft Azure 信息保护”对话框中，单击“发送反馈”。 将向信息保护团队发送电子邮件，并自动附加电脑中的日志文件。 

我们还邀请你加入我们的工程团队：[Azure 信息保护 Yammer 站点](https://www.yammer.com/askipteam/)。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>如果我的问题不在这里，我该如何操作？

首先，查看特定于分类和标签，或特定于数据保护的常见问题。 Azure 权限管理服务 (Azure RMS) 为 Azure 信息保护提供数据保护技术，Azure RMS 可与或者不与分类和标签结合使用： 

- [分类和标签的常见问题解答](faqs-infoprotect.md)

- [数据保护的常见问题解答](faqs-rms.md)

如果问题没有回复，请使用 [Azure 信息保护的信息和支持](information-support.md)中列出的链接和资源。

此外，我们还为最终用户制作了常见问题解答：

- [适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](../rms-client/mobile-app-faq.md)

- [适用于 Mac 计算机和 Windows Phone 的 RMS 共享应用常见问题解答](https://technet.microsoft.com/dn451248)

- [FAQ for Rights Management Sharing Application for Windows](https://technet.microsoft.com/dn467883)（适用于 Windows 的 Rights Management 共享应用程序常见问题解答）


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

