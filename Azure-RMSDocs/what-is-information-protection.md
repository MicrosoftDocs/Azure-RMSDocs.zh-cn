---
title: 什么是 Azure 信息保护？ - AIP
description: Azure 信息保护服务的技术概述，此服务有助于组织标记文档和电子邮件，从而分类和保护数据（无论数据驻留在何处）。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/10/2019
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 1d65cbbe95b13bd86cdefe7360cdd46cd80ef0bc
ms.sourcegitcommit: 8499602fba94fbfa28d7682da2027eeed6583c61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83747138"
---
# <a name="what-is-azure-information-protection"></a>什么是 Azure 信息保护？

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

Azure 信息保护（有时也称为 AIP）是基于云的解决方案，有助于组织通过应用标签对其文档和电子邮件进行分类和有选择地保护。 标签可以由定义规则和条件的管理员自动应用、由用户手动应用或是二者组合应用（在这种情况下会向用户提供建议）。 

下图显示在用户计算机上实际操作中的 Azure 信息保护示例。 管理员已配置具有检测敏感数据的规则的标签，在我们的示例中，敏感数据是信用卡信息。 当用户保存包含信用卡号的 Word 文档时，她会看到一个自定义工具提示，建议她应用管理员配置的标签。 此标签将对文档进行分类并保护。 

![用于 Azure 信息保护的建议分类示例](./media/info-protect-recommend-calloutsv2.png)

###### <a name="screenshot-from-the-azure-information-protection-client-classic"></a>来自 [Azure 信息保护客户端（经典）](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的屏幕截图

内容进行分类（以及保护（可选））之后，随后可以跟踪并控制其使用方式。 可以分析数据流以深入了解业务、检测危险行为和采取修正措施、跟踪对文档的访问、防止数据泄露或误用，等等。

## <a name="how-labels-apply-classification"></a>标签如何应用分类

可使用 Azure 信息保护标签对文档和电子邮件应用分类。 执行此操作时，分类是可识别的，无论数据的存储位置在哪里或者与谁共享。 标签可包括视觉标记，如页眉、页脚或水印。 元数据以明文形式添加到文件和电子邮件标头。 明文形式确保其他服务（如数据丢失防护解决方案）可以识别分类并执行相应的操作。 

例如，下面的电子邮件已分类为“常规”。 标签已将“敏感度：常规”页脚添加到电子邮件。 此页脚是所有收件人的一个可视指示器，它用于一般业务数据，不应在组织外部发送。 该标签嵌入在电子邮件标头中，以便电子邮件服务可以检查此值，并且可以创建审核项或阻止在组织外部发送它。

![显示 Azure 信息保护分类的示例电子邮件页脚和标头](./media/example-email-footerv2.png)

###### <a name="screenshot-from-the-azure-information-protection-client-classic"></a>来自 [Azure 信息保护客户端（经典）](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的屏幕截图

## <a name="how-data-is-protected"></a>如何保护数据

保护技术使用 Azure Rights Management（通常缩写为 Azure RMS）。 此技术已与其他 Microsoft 云服务和应用程序（例如 Office 365 和 Azure Active Directory）集成。 它还可与你自己的业务线应用程序和软件供应商提供的信息保护解决方案搭配使用，无论这些应用程序和解决方案是在本地还是在云中。

此保护技术使用加密、标识和授权策略。 与应用的标签类似，使用权限管理能够始终为文档和电子邮件提供保护，而不受其位置的影响 – 不管是在组织、网络、文件服务器和应用程序的内部还是外部。 此信息保护解决方案让你可以始终控制你的数据，即使在这些数据与他人共享时也是如此。

例如，可以配置报告文档或销售预测电子表格，以便仅允许组织内人员进行访问，并且可以控制是否可以编辑该文档、是否将其限制为只读，以及是否禁止打印它。 同样，你也可以配置电子邮件，并禁止转发电子邮件或使用“全部答复”选项。 

这些保护设置可以是标签配置的一部分，这样用户就只需应用标签即可分类并保护文档和电子邮件。 不过，支持保护的应用程序和服务也可以使用相同的保护设置，但不能应用标签。 对于这些应用程序和服务，保护设置以 Rights Management 模板形式提供。

### <a name="rights-management-templates"></a>Rights Management 模板

在激活 Azure Rights Management 服务之后，便会为你提供两个默认模板，用于将数据访问权限限制为你组织内的用户。 可以使用这些模板立即帮助防止从你的组织泄露数据。 你还可以通过配置应用更多限制性控件的自己的保护设置来补充这些默认模板。

事实上，针对包含保护设置的 Azure 信息保护创建标签时，此操作会创建相应的 Rights Management 模板。 然后，还可将该模板用于支持 Azure Rights Management 的应用程序和服务。

例如，可从 Exchange 管理中心配置 Exchange Online 邮件流规则来使用这些模板：

![为 Exchange Online 选择模板的示例](./media/templates-exchangeonline-callouts.png)

有关 Azure Rights Management 保护的详细信息，请参阅[什么是 Azure Rights Management？](what-is-azure-rms.md)

## <a name="integration-with-end-user-workflows-for-documents-and-emails"></a>与文档和电子邮件的最终用户工作流集成

安装 Azure 信息保护客户端时，Azure 信息保护会与最终用户的现有工作流集成。 此客户端会将信息保护栏安装到 Office 应用程序（如在 Word 中显示此栏的第一张图片所示）。 相同的信息保护栏会添加到 Excel、PowerPoint 和 Outlook。 例如：

![Excel 中的 Azure 信息保护栏的示例](./media/excelproplus-infoprotect-bar.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-client"></a>来自 [Azure 信息保护统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的屏幕截图 

此信息保护栏使最终用户能够轻松选择用于正确分类的标签。 如有需要，还可以自动应用标签以避免用户猜测，或者用于遵循组织策略。

若要对其他文件类型进行分类和保护，并想要一次性支持多个文件，用户可在 Windows 文件资源管理器中右键单击文件或文件夹：

![在文件资源管理器中，右键单击“使用 Azure 信息保护进行分类和保护”](./media/right-click-classify-protect-folder.png)

如果用户在文件资源管理器中选择“分类和保护”菜单选项，那么他们可以选择一个标签，操作方式类似于他们在 Office 桌面应用程序中使用信息保护栏。 如果需要，他们还可以设置自己的自定义权限。

高级用户（和管理员）可能会发现，针对管理和设置多个文件的分类和保护，使用 PowerShell 命令更有效。 虽然也可以单独安装 PowerShell 模块，但完成这些操作的 PowerShell 命令会自动包含在此客户端中。

文档受到保护后，用户和管理员可以使用文档跟踪站点监视访问这些文档的人员和时间。 如果他们怀疑存在误用，还可以撤销对这些文档的访问权限：

![撤销文档跟踪站点中的访问图标](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>其他电子邮件集成

将 Azure 信息保护与 Exchange Online 一起使用时，用户将获得额外的好处：可以将受保护的电子邮件发送给任何用户，并确保他们可以在任意设备上阅读该电子邮件。

例如，用户需要将敏感信息发送到使用 Gmail、Hotmail 或 Microsoft 帐户的个人电子邮件地址  。 或者，向在 Office 365 或 Azure AD 中没有帐户的用户发送敏感信息。 这些电子邮件应静态加密并在传输中加密，且只有原始收件人才能阅读。

此方案需要[ Office 365 邮件加密中的新功能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)。 如果收件人在本机电子邮件客户端中无法打开受保护的电子邮件，可以使用一次性密码，通过浏览器阅读敏感信息。

例如，Gmail 用户在电子邮件中看到以下信息：

![OME 和 AIP 的 Gmail 收件人体验](./media/ome-message.png)

对于发送电子邮件的用户，他们的工作流与将受保护电子邮件发送到其组织内的用户相同。 例如，他们可以选择“不要转发”按钮，Azure 信息保护客户端可以将该按钮添加到 Outlook 功能区。 或者，此“不要转发”功能可以集成到用户选择的标签，使电子邮件分类并受到保护。 例如：

![选择配置为“不转发”的标签](./media/recipients-only-label2.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-client"></a>来自 [Azure 信息保护统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的屏幕截图

或者，可以通过使用应用权限保护的邮件流规则，为用户自动提供保护。 

将 Office 文档附加到这些电子邮件时，这些文档也会自动受到保护。

## <a name="classifying-and-protecting-existing-documents"></a>对现有文档进行分类和保护

理想情况下，在首次创建文档和电子邮件时，就对其进行标记。 但是，你可能在数据存储中已经有很多文档，并且希望对这些文档也进行分类和保护。 这些文档存储可能是在本地，也可能是在云中。

对于你的本地数据存储，请使用 Azure 信息保护扫描程序，以发现本地文件夹、网络共享及 Microsoft SharePoint Server 站点和库中的文档，并对其进行分类和保护。 扫描程序在 SharePoint Server 上将作为服务运行。 可在策略中使用同一规则，以检测敏感信息，并向文档应用特定标签。 或者，也可以向数据存储库中的所有文档应用默认标签，无需检查文件内容。 此外，也可以仅在报告模式下使用扫描程序，以帮助你发现可能不知道的敏感信息。 

有关部署和使用扫描程序的详细信息，请参阅[部署 Azure 信息保护扫描程序，以自动对文件进行分类和保护](deploy-aip-scanner.md)。

对于你的云数据存储，请使用 Microsoft Cloud App Security 将你的标签应用于 Box、SharePoint 和 OneDrive 中的文档。 有关详细信息，请参阅[自动应用 Azure 信息保护分类标签](/cloud-app-security/use-case-information-protection)和 [Azure 信息保护集成](/cloud-app-security/azip-integration)。

## <a name="latest-labeling-updates-for-microsoft-365"></a>Microsoft 365 的最新标签更新

请参阅有关 Azure 信息保护如何帮助你发现、分类、保护和监视敏感信息的最新信息，无论该敏感信息位于何处：

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

## <a name="resources-for-azure-information-protection"></a>Azure 信息保护的资源

- 免费试用版：[企业移动性 + 安全性 E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- 订阅选项和定价：[Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)

- 下载客户端：[Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- 下载可自定义的用户指南：[Azure 信息保护最终用户采用指南](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- 常见问题解答：[Azure 信息保护的常见问题](faqs.md)

- Yammer：[Azure 信息保护](https://www.yammer.com/AskIPTeam)

- 文档中记录的新变化：[Azure 信息保护技术博客](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/bg-p/AzureInformationProtectionBlog/label-name/Docs)

其他资源：[Azure 信息保护的信息和支持](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

在奥兰多，Microsoft Ignite 2019 取得了巨大成功！ 会上提供了与 Azure 信息保护相关的大量精彩资讯，其中包括最新更新和改进功能。 如果你未能参与，我们录制有会议视频供你日后观看。

请参阅以下列表，了解我们推荐的前 5 项会议：

- [BRK2119 - 保护你的敏感数据！了解最新的 Microsoft 信息保护功能](https://myignite.techcommunity.microsoft.com/sessions/81172?source=sessions)
 
- [THR3067 - 了解你的数据：五个热门提示和技巧，让你更好地了解敏感数据格局](https://myignite.techcommunity.microsoft.com/sessions/81183)

- [BRK3103 - 保护敏感文件和数据并非易事。选择可以平衡安全性和工作人员效率的适当数据保护方式](https://myignite.techcommunity.microsoft.com/sessions/81177?source=sessions)

- [BRK2120 - 已拥有 Azure 信息保护？导航统一的标签、策略配置、客户端和分析](https://myignite.techcommunity.microsoft.com/sessions/81178?source=sessions)

- [BRK2121 - 借助 Microsoft 信息保护 SDK 将敏感度标签和保护功能扩展到自己的应用和 ISV 解决方案](https://myignite.techcommunity.microsoft.com/sessions/81179?source=sessions)

最新博客文章：[了解敏感数据所在的位置，并通过 Microsoft 365 智能地对其进行保护](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Understand-where-your-sensitive-data-is-located-and/ba-p/960465)


## <a name="next-steps"></a>后续步骤

可通过观看我们的[快速入门教程](quickstart-viewpolicy.md)和[教程](infoprotect-quick-start-tutorial.md)，自行配置和使用 Azure 信息保护。 或者，如果已准备好部署组织的此项服务，请转到[操作方法指南](how-to-guides.md)。
