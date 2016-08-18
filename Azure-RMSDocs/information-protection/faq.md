---
title: "Azure 信息保护预览版常见问题 | Azure 信息保护"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d17bacf8e148622db0e2393f40d3fd37c8f086eb
ms.openlocfilehash: c61e299cac50069afc119d37fd461cda88a2afd3


---

# Azure 信息保护预览版的常见问题

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

对 Azure 信息保护的预览版有疑问？  请查看此处是否有答案。 

随着一些信息被移至主文档，以及我们将添加来自客户的新问题，该列表将得到频繁更新。 

## Azure 信息保护的预览版本有哪些功能，以及当前存在哪些限制？

该预览版在 Microsoft Office 应用中添加了一个信息保护栏，你可以使用该栏查看并修改指定给数据的分类标签。 可以手动完成分类，或者向你推荐特定分类，或者自动应用分类。 对于你指定的分类，可使用 Azure 权限管理模板保护数据。  

在 Azure 门户中配置分类标签和行为。 你可以使用默认的内置策略非常快速地评估 Azure 信息保护，或完全自定义你自己的策略。 你可以更改用户使用的分类标签的颜色、名称和顺序。 你还可以配置工具提示和诸如页眉、页脚或水印等分类可视化标记。

请尝试学习我们的快速入门教程，以便在数分钟内了解相关功能：[《Quick start tutorial for Azure Information Protection》](infoprotect-quick-start-tutorial.md)（Azure 信息保护快速入门教程）。

请注意，预览版允许你尝试新的**高级 P2 服务计划**，而一些高级功能，例如自动和推荐的标签，在正式发布的当前计划中可能无法供你使用。 有关其他服务计划（Azure 信息保护高级 P1 和 Azure 信息保护高级 P2）的信息，请参阅以下博客帖子：[Introducing Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/07/introducing-enterprise-mobility-security/)（企业移动性 + 安全性简介）。

该预览版具有以下限制。 有关其他特性和功能何时可用的信息，请留意[企业移动性和安全性博客](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)和 [Yammer 站点](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)上的公告：

- 对于分类和标签没有任何集中式日志记录。

- 标签名称和工具提示仅支持一种语言。

- 自动分类的条件必须是短语或模式。

- 无法在 Windows 文件资源管理器中对文件进行分类。

- 暂不支持适用于移动设备（iOS 和 Android） Mac 计算机的 Office 应用和 Office web 应用（Office Online）。

- 未集成 Exchange Online 或 SharePoint Online。

- 适用于合作伙伴和开发人员的 SDK 不可用。

## 需要什么订阅才可以尝试 Azure 信息保护？

对于预览版本，你可以使用包含 Azure 权限管理的任何订阅。 Azure 信息保护在所有区域中可用。 有关免费试用版的可用订阅和链接的详细信息，请参阅[《Azure RMS requirements: Cloud subscriptions that support Azure RMS》](../get-started/requirements-subscriptions.md)（Azure RMS 要求：支持 Azure RMS 的云订阅）。

若要在 Azure 门户中配置 Azure 信息保护策略，必须具有 Azure 订阅。 如果你还没有你组织的 Azure 订阅，则可以通过注册免费试用版来获取订阅：转到 [Azure 入门](https://account.windowsazure.com/organization)页并按照说明进行操作。

对订阅要求的任何更改将在[企业移动性和安全性博客](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)上公布。

## 是否需要是全局管理员才能试用 Azure 信息保护预览版？

仅对于预览版，任何由 Azure 进行身份验证的用户都可以在 Azure 门户中查看并配置其租户的 Azure 信息保护分类和标记策略。 但是，若要配置标签以应用 Azure 权限管理模板，则必须以 Azure Active Directory 全局管理员的身份进行登录。

如果在安装 [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)时选择安装演示策略，那么你甚至不需要登录门户来试用预览版。 演示策略在本地安装 Azure 信息保护的默认策略，因此你可以尝试为文档和电子邮件设置标签，但是，在未登录 Azure 门户的情况下你将无法更改或添加新标签。 

如果你想要保护你对其进行分类和设置标签的文档和电子邮件，但是尚未激活 Azure 权限管理，那么激活过程将需要专门的管理员权限。 有关详细信息，请参阅[是否必须是全局管理员才能配置 Azure RMS？我可以委派给其他管理员吗？](../get-started/faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators)


## Azure 信息保护是否支持本地和混合方案？

Azure 信息保护是一个基于云的解决方案。 如果你对在混合方案中部署 Azure 信息保护感兴趣，请发送电子邮件到 askipteam@microsoft.com 来联系信息保护团队。

## Azure 信息保护支持哪些客户端平台和应用程序？

该问题的答案已在[《Requirements for Azure Information Protection》](requirements-azure-infoprotect.md)（Azure 信息保护要求）中记录并将得到更新。


## 计算机如何从 Azure 信息保护中获取策略信息，以及这些信息多长时间刷新一次？

每次用户打开 Office 应用程序时，Azure 信息保护客户端就会检查是否存在更新版本的 Azure 信息保护策略。 如果有更新版本，客户端将使用 HTTPS 链接来下载它以保护数据。 

如果在发布新的 Azure 信息保护策略时加载 Office 应用程序的多个实例，必须关闭所有实例以获取策略的最新版本。 例如，你有两个 Word 文档打开，并且想要在一个文档中测试更新后的 Azure 信息保护策略：关闭两个 Word 文档，并重新打开你想要使用最新策略的文档。

## 文件存储在什么位置才可以使用 Azure 信息保护？ 

由于 Azure 信息保护向文件和电子邮件应用永久性标签和保护，因此文件存储在什么位置并没有关系。

## 是否只能对新数据进行分类，还是也可以对现有数据进行分类？

对于新内容和现有内容的更改，Azure 信息保护策略操作将在文档已保存和电子邮件已发送时生效。 

如果你已保存想要分类的文件，只需在 Office 应用程序中打开并保存它们。 

目前，无法批量扫描并应用分类，必须在 Office 应用程序中打开并保存每个文档。 

## 是否可以仅将 Azure 信息保护用于分类，而不进行强制加密和限制使用权限？

是。 你可以将 Azure 信息保护策略配置为仅应用标签。 事实上，我们预计在只需要保护要求特殊数据管理的一部分文档或电子邮件的网络部署中，这会是一个绝大多数的情况。

## 自动分类是如何工作的？

在 Azure 门户中，可以使用预定义的模式，如“信用卡号”或“美国社会保障号”。 或者，你可以定义自定义字符串或模式作为自动分类的条件。

你可以在[《Quick start tutorial for Azure Information Protection》](infoprotect-quick-start-tutorial.md)（Azure 信息保护的快速入门教程）中看到该示例。 

分类的准确性取决于配置基于条件的分类规则的方式。 目前，条件支持文本模式和正则表达式。 有关预览期间可用的每个选项的说明以及测试的建议示例，请参见 [如何针对 Azure 信息保护的自动和建议分类配置条件](configure-policy-classification.md)(#如何针对-azure-信息保护的自动和建议分类配置条件)。 保存了文档或发送了电子邮件之后，将运行检测。

若要获取最佳用户体验并确保业务连续性，我们建议你从用户建议操作开始，而不是完全自动化操作。 这可以使你的用户能够接受标签或保护操作，或者覆盖这些建议。   

## Azure 信息保护是否能够提示用户亲自对文件进行分类，而不是使用自动分类？ 

是。 使用 Azure 门户配置是使用自动分类还是对用户做出建议，此处将选项“选择如何应用标签: 自动还是向用户推荐”设为“推荐”。

你可以在[《Quick start tutorial for Azure Information Protection》](infoprotect-quick-start-tutorial.md)（Azure 信息保护的快速入门教程）中看到该示例。  

## 可以强制对所有文档进行分类吗？

是。 如果你要求用户对他们保存的所有文件进行分类，请在 Azure 门户中将选项“所有文档和电子邮件都必须有标签”设为“开”。 

## 我可以删除文件的分类吗？

是。 若要删除文件的分类，请在 Office 应用程序中打开该文件，单击信息保护栏中的“编辑标签”图标，单击“删除标签”图标，然后单击“确定”来确认你的操作。 


## 我是否可以提示用户说明他们更改分类级别的原因？

是。 若要确保用户说明他们更改分类的原因，请在 Azure 门户中，将选项“当降低敏感度级别时用户必须提供理由”设为“开”。 当他们这样做时，将在其本地 Windows 事件日志中记录他们的操作和理由：“应用程序” > “Microsoft Azure 信息保护”。

## 如何自动保护已分类的内容？

在 Azure 门户中，可以根据你指定的分类级别，选择 Azure 权限管理模板来自动保护内容。

你可以在[《Quick start tutorial for Azure Information Protection》](infoprotect-quick-start-tutorial.md)（Azure 信息保护的快速入门教程）中看到该示例。 有关详细信息，请参阅 [如何配置标签以应用权限管理保护](configure-policy-protection.md)(#如何配置标签以应用权限管理保护)。

## 一个文件是否可以有两个不同的分类？

如有必要，你可以为特定敏感度标签创建子标签，以便更好地描述子类别。 例如，主体标签 **Secret** 可能包含子标签，如 **Secret – Legal** 和 **Secret – Finance**。 你随后可对不同的子标签应用不同的分类可视化标记和不同的权限管理模板。

虽然当前可在两个级别上设置可视化标记、保护和条件，但是当使用子级别时，请只在子级别上配置这些设置。 如果在父标签及其子级别上配置相同的设置，那么子级别上的设置具有更高优先级。

## DLP 解决方案和其他应用如何与 Azure 信息保护相集成？

因为 Azure 信息保护将永久性元数据用于分类，其中包括明文标签，所以该信息可以被 DLP 解决方案和其他应用读取。 对于文件，该元数据存储在自定义属性中；对于电子邮件，该信息存储在电子邮件标头中。

## 在 Azure 信息保护中如何使用文档跟踪和撤销？

对使用 Azure 信息保护进行分类和保护的文件的文档跟踪方式与目前对 Azure 权限管理和 RMS 共享应用程序的文档跟踪方式一样。 你也可以使用 Azure 信息保护客户端（1.0.233 版或更高版本）来访问文档跟踪站点： 

- 在 Office 应用程序的“主页”选项卡的“保护”组中，单击“保护” > “跟踪使用情况”。 

有关详细信息，请参阅[《Track and revoke your documents when you use the RMS sharing application》](../rms-client/sharing-app-track-revoke.md)（使用 RMS 共享应用程序跟踪和撤销文档）。

## Azure 信息保护如何实施我配置的策略？

如果使用 Azure 权限管理模板保护文档，则首先对用户进行身份验证以确保她有权限访问该文档，随后由应用程序实施使用权限策略。 

## Azure 信息保护如何使用 Azure Active Directory？

Azure 信息保护将 Azure Active Directory 用于用户身份验证。

## 是否可以控制哪些用户可以使用 Azure 信息保护对内容进行分类并保护？

你可以通过控制 Azure 信息保护客户端的分布来限制哪些用户可以对数据进行分类并保护。 

不管是否安装了 Azure 信息保护客户端，任何用户都可以使用或编辑由 Azure 信息保护分类的文件和电子邮件。 

## 如何针对此预览版报告问题或发送反馈？

如果在使用此预览版本时发现问题，请在 Office 应用的“主页”选项卡的“保护”组中，单击“保护”，然后单击“帮助和反馈”。 在“Microsoft Azure 信息保护”对话框中，单击“发送反馈”。 将向信息保护团队发送电子邮件，并自动附加 PC 中的日志文件以帮助诊断问题。 

如果你有任何问题或反馈，请使用 [Azure 信息保护 Yammer 站点](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)。 

## 如果我的问题不在这里，我该如何操作？

首先，请确认你的问题不包括在企业移动性和安全性博客上的 [Azure 信息保护预览版通告](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/)中。

然后，请访问我们的 [Yammer 站点](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)查看是否其他人已提出相同的问题。 如果没有，请发布你的问题。







<!--HONumber=Aug16_HO2-->


