---
title: "什么是 Azure 信息保护？"
description: "Azure 信息保护服务概述。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
ms.openlocfilehash: fc25cd11d950199f7ccd8e4e86e4d915c7fb6a95
ms.sourcegitcommit: f0402cf14506b4c61a156a2baf7e69b7b16883a1
translationtype: HT
---
# <a name="what-is-azure-information-protection"></a>什么是 Azure 信息保护？

>适用于：Azure 信息保护

Azure 信息保护是基于云的解决方案，可帮助组织对其文档和电子邮件进行分类、添加标签和保护。 这可以由定义规则和条件的管理员自动进行、由用户手动进行或是组合进行（在这种情况下会向用户提供建议）。 

下图显示实际操作中的 Azure 信息保护示例。 管理员配置了规则来检测敏感数据（在此例中是信用卡信息）。 当用户保存包含信用卡信息的 Word 文档时，她会看到一个自定义工具提示，建议她应用管理员配置的特定标签，该标签可对文档进行分类和（可选）保护。 

![用于 Azure 信息保护的建议分类示例](../media/info-protect-recommend-calloutsv2.png)

内容进行分类（以及保护（可选））之后，随后可以跟踪并控制其使用方式。 可以分析数据流以深入了解业务、检测危险行为和采取修正措施、跟踪对文档的访问、防止数据泄露或误用，等等。

## <a name="how-labels-apply-classification"></a>标签如何应用分类

可使用 Azure 信息保护标签对文档和电子邮件应用分类。 执行此操作时，分类在任何时候都是可识别的，无论数据的存储位置在哪或者与谁共享数据。 标签包括可视化标记，如页眉、页脚或水印。 元数据以明文形式添加到文件和电子邮件的标头，以便其他服务（如数据丢失防护解决方案）可以识别分类并执行相应的操作。 

例如，下面的电子邮件已分类为“内部”。 此标签作为页脚添加到电子邮件，用作所有收件人的可视指示器，旨在供内部使用，不应在组织外部发送。 此标签也嵌入在电子邮件标头中，以便电子邮件服务可以检查此值并且可以创建审核项或阻止在组织外部发送它。

![显示 Azure 信息保护分类的示例电子邮件页脚和标头](../media/example-email-footerv2.png)


## <a name="how-data-is-protected"></a>如何保护数据

保护技术使用 Azure Rights Management（通常缩写为 Azure RMS）。 此技术已与其他 Microsoft 云服务和应用程序（例如 Office 365 和 Azure Active Directory）集成。 它还可与你自己的业务线应用程序和软件供应商提供的信息保护解决方案搭配使用，无论这些应用程序和解决方案是在本地还是在云中。

此保护技术使用加密、标识和授权策略。 与应用的标签类似，使用权限管理能够始终为文档和电子邮件提供保护，而不受其位置的影响 – 不管是在组织、网络、文件服务器和应用程序的内部还是外部。 此信息保护解决方案让你可以始终控制你的数据，即使在这些数据与他人共享时也是如此。

例如，可以配置报告文档或销售预测电子表格，以便仅允许组织内人员进行访问，并且可以控制是否可以编辑该文档、是否将其限制为只读，以及是否禁止打印它。 同样，你也可以配置电子邮件，并且禁止转发电子邮件或使用“全部答复”选项。 这些保护任务可以使用权限管理模板来简化。

### <a name="rights-management-templates"></a>权限管理模板

激活 Azure Rights Management 服务之后，便会为你创建两个默认模板，仅限你组织内的用户才能访问数据。 可以使用这些模板立即帮助防止从你的组织泄露数据。 还可以通过配置应用更多限制性控件的你自己的自定义模板来补充这些默认模板。

这些模板可以是标签配置的一部分，以便当特定标签应用于文档（或电子邮件）时，数据进行分类并自动受保护。 这些模板也可以由用户或管理员在支持 Azure Rights Management 技术的产品和服务中进行选择。

此示例演示如何在从 Azure 门户配置 Azure 信息保护策略时为标签选择模板：

![在 Azure 门户中选择模板的示例](../media/info-protect-template-callout.png)

可以从 Exchange 管理中心选择相同模板，以配置支持 Azure Rights Management 技术的 Exchange Online 邮件流规则：

![为 Exchange Online 选择模板的示例](../media/templates-exchangeonline-callouts.png)

有关 Azure Rights Management 保护的详细信息，请参阅[什么是 Azure Rights Management？](what-is-azure-rms.md)

## <a name="integration-with-end-user-workflows"></a>与最终用户工作流的集成

安装 Azure 信息保护客户端时，Azure 信息保护会与最终用户的现有工作流集成。 此客户端会将信息保护栏安装到 Office 应用程序（如第一张图片所示）。 相同栏会添加到 Excel、PowerPoint 和 Outlook。 例如：

![Excel 中的 Azure 信息保护栏的示例](../media/excel2016-infoprotect-barv2.png)

此信息保护栏使最终用户可以方便地为正确分类选择标签，在需要时，这些标签还可以自动保护其文档和电子邮件。

若要对其他文件类型进行分类和保护，并想要一次性支持多个文件，用户可在 Windows 文件资源管理器中右键单击文件或文件夹：

![在文件资源管理器中，右键单击“使用 Azure 信息保护进行分类和保护”](../media/right-click-classify-protect-folder.png)

如果用户在文件资源管理器中选择“分类和保护”菜单选项，那么他们可以选择一个标签，操作方式类似于他们在 Office 桌面应用程序中使用信息保护栏。 如果需要，他们还可以设置自己的自定义权限。

高级用户（和管理员）可能会发现，针对管理和设置多个文件的分类和保护，使用 PowerShell 命令更有效。 虽然你也可以单独安装 PowerShell 模块，但完成此操作的 PowerShell 命令将自动包含在此客户端中。

文档受到保护后，用户和管理员可以使用文档跟踪站点监视访问这些文档的人员和时间。 如果他们怀疑存在误用，还可以撤销对这些文档的访问权限：

![撤销文档跟踪站点中的访问图标](../media/tracking-site-revoke-access-icon.png)


## <a name="resources-for-azure-information-protection"></a>Azure 信息保护的资源

- 公告：[Azure 信息保护现已推出正式版](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/04/azure-information-protection-is-now-generally-available/)

- 免费试用版：[企业移动性 + 安全性 E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- 下载客户端：[Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- 常见问题：[Azure 信息保护的常见问题](../get-started/faqs.md)

- Yammer：[Azure 信息保护](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- 视频：“信息保护的 5 大技巧”

    <iframe width="560" height="315" src="https://www.youtube.com/embed/GWcnZFMPcnE" frameborder="0" allowfullscreen></iframe>

    此外，Microsoft Ignite 2016 对 Azure 信息保护提供多个按需会话：

    - [BRK2127：采用综合标识驱动解决方案安全地保护和共享数据](https://myignite.microsoft.com/videos?q=BRK2127)
    
    - [THR2107：使用 Azure 信息保护进行安全协作](https://myignite.microsoft.com/videos?q=THR2107)
    
    - [THR2108：通过 Azure 信息保护确保全面保护数据](https://myignite.microsoft.com/videos?q=THR2108)
    
    - [BRK3095：了解分类、标记和保护如何提供持续的数据保护](https://myignite.microsoft.com/videos?q=BRK3095)
    
    - [BRK2128：利用 Microsoft Office 365 和 Azure 信息保护，向任何人发送安全电子邮件](https://myignite.microsoft.com/videos?q=BRK2128)


## <a name="next-steps"></a>后续步骤

阅读博客文章 [Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)（Azure 信息保护：准备、设置、保护！）

通过我们的 5 步骤 [Azure 信息保护快速入门教程](../get-started/infoprotect-quick-start-tutorial.md)，可为你自己配置和使用 Azure 信息保护。

或许你是通过其他名称了解的 Azure 信息保护或 Azure 权限管理。 请参阅[该服务的替代术语列表](azure-rms-aka.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]