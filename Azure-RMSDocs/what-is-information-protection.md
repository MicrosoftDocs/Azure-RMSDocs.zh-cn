---
title: 什么是 Azure 信息保护 (AIP)？
description: Azure 信息保护 (AIP) 是一项服务，可帮助组织标记文档和电子邮件。 无论数据保存在哪里，AIP 都能对其进行分类和保护。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/23/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 9330feb804a4991fd73f6e0895db69e401089e49
ms.sourcegitcommit: 24c97b58849af4322d3211b8d3165734d5ad6c88
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91427910"
---
# <a name="what-is-azure-information-protection"></a>什么是 Azure 信息保护？

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

Azure 信息保护 (AIP) 是一种基于云的解决方案，可帮助组织通过应用标签来对文档和电子邮件进行分类和保护。 标签可以：

- 由使用规则和条件的管理员自动应用
- 由用户手动应用
- 由组合（其中管理员定义向用户显示的建议）应用

例如，你的管理员可能配置了一个具有检测敏感数据（例如信用卡信息）的规则的标签。 在这种情况下，在 Word 文件中保存信用卡信息的所有用户都可能在文档顶部看到一个工具栏，其中建议他们应用针对此场景的相关标签。

标签可以对文档进行[分类](#how-labels-apply-classification-with-aip)和（可选）[保护](#how-aip-protects-your-data)，使你能够：

- 跟踪和控制使用内容的方式
- 分析数据流以深入了解业务 - 检测有风险的行为并采取纠正措施 
- 跟踪文档访问，防止数据泄漏或不当使用
- 以及更多...

## <a name="how-labels-apply-classification-with-aip"></a>标签如何使用 AIP 应用分类

使用 Azure 信息保护对文档和电子邮件应用分类标签。

标记内容包括：

- 无论数据存储在哪里或与谁共享都能检测到的分类。
- 视觉标记，例如标头、页脚或水印。
- 以明文形式添加到文件和电子邮件标头的元数据。 明文形式的元数据可确保其他服务能够识别分类并执行相应的操作

例如在下图中，标记服务使用[统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)将电子邮件分类为“常规”：

:::image type="content" source="media/example-email-footerv2.png" alt-text="显示 Azure 信息保护分类的示例电子邮件页脚和标头":::

在此示例中，标记还：

- 向电子邮件添加了“敏感度:***常规”的页脚*** 。 该页脚是显示给所有收件人的一个可视指示器，用于不得在组织外部发送的一般业务数据。
- 电子邮件标头中嵌入的元数据。 通过标头数据，电子邮件服务可检测标签，从理论上说可创建审核条目或阻止它发送到组织外部。

## <a name="how-aip-protects-your-data"></a>AIP 如何保护数据

Azure 信息保护使用 [Azure Rights Management 服务](what-is-azure-rms.md) (Azure RMS) 来保护数据。 

Azure RMS 已与其他 Microsoft 云服务和应用程序（例如 Microsoft 365 和 Azure Active Directory）集成，它还可用于你自己或第三方应用程序和信息保护解决方案。 Azure RMS 同时适用于本地和云解决方案。

Azure RMS 使用加密、标识和授权策略。 与 AIP 标签类似，无论文档或电子邮件位于何处，使用 Azure RMS 应用的保护都保留在文档和电子邮件中，从而确保你始终控制你的内容，即使与其他人共享也是如此。

保护设置可以：

- 并入标签配置中，让用户只需应用标签即可对文档和电子邮件进行分类和保护。 
- 通过支持保护但不标记的应用程序和服务自行使用。 

    对于只支持保护的应用程序和服务，保护设置用作[权限管理模板](#rights-management-templates)。

例如，你可能想要配置一个报表或销售预测电子表格，以便它只能供你组织中的人员访问。 在这种情况下，你要应用保护设置来控制是可编辑该文档、将文档限制为只读，还将阻止打印文档。

电子邮件可具有类似的保护设置，来防止被转发或使用“全部答复”选项。

### <a name="rights-management-templates"></a>权限管理模板

在激活 Azure Rights Management 服务之后，便会为你提供两个默认权限管理模板，用于将数据访问权限限制为你组织内的用户。 可立即使用这些模板，也可配置你自己的保护设置，在新模板中应用更严格的控制。

权限管理模板可用于支持 Azure 权限权利的任何应用程序或服务。

下图显示了 Exchange 管理中心的一个示例，其中你可配置 Exchange Online 邮件流规则来使用 RMS 模板：

:::image type="content" source="media/templates-exchangeonline-callouts.png" alt-text="显示 Azure 信息保护分类的示例电子邮件页脚和标头":::

> [!NOTE]
> 创建包含保护设置的 AIP 标签时，还将创建一个相应的权限管理模板，它可独立于标签单独使用。 
>  

有关详细信息，请参阅[什么是 Azure 权限管理？](what-is-azure-rms.md)

## <a name="aip-and-end-user-integration-for-documents-and-emails"></a>文档和电子邮件的 AIP 和最终用户集成

AIP 客户端会向 Office 应用程序安装“信息保护”栏，让最终用户能够将 AIP 集成到他们的文档和电子邮件中。

例如，在 Excel 中使用[统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)：

![Excel 中的 Azure 信息保护栏的示例](./media/excelproplus-infoprotect-bar.png)

虽然标签可自动应用于文档和电子邮件，从而免除用户的猜测并符合组织策略，但最终用户可使用“信息保护”栏自行选择标签和应用分类。

此外，通过 AIP 客户端，用户可使用 Windows 文件资源管理器中的右键单击菜单来分类和保护其他文件类型，或者一次性地分类和保护多个文件。 例如：

:::image type="content" source="media/right-click-classify-protect-folder.png" alt-text="显示 Azure 信息保护分类的示例电子邮件页脚和标头":::

“分类和保护”菜单选项的工作方式与 Office 应用程序汇总的“应用保护”栏类似，用户可选择标签或设置自定义权限。

> [!TIP]
> 高级用户或管理员可能会发现，PowerShell 命令可用来更高效地管理和设置多个文件的分类和保护。 客户端中有[相关的 PowerShell 命令](https://docs.microsoft.com/powershell/module/azureinformationprotection)，它们也可单独安装。

用户和管理员可使用文档跟踪站点来监视受保护的文档、查看谁何时访问了这些文档。 如果他们怀疑存在误用，则还可以撤消对这些文档的访问权限。 例如：

![撤销文档跟踪站点中的访问图标](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>其他电子邮件集成

将 AIP 与 Exchange Online 结合使用可带来额外的好处，可将受保护的电子邮件发送给任意用户并保证他们可在任意设备上阅读这些邮件。

例如，你可能需要将敏感信息发送到使用 Gmail、Hotmail 或 Microsoft 帐户的个人电子邮件地址，或者发送给在 Microsoft 365 或 Azure AD 中没有帐户的用户  。 这些电子邮件应静态加密并在传输中加密，且只有原始收件人才能阅读。

此方案需要 [Office 365 消息加密功能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)。 如果收件人在本机电子邮件客户端中无法打开受保护的电子邮件，可以使用一次性密码，通过浏览器阅读敏感信息。

例如，Gmail 用户可能会在收到的电子邮件中看到以下提示：

:::image type="content" source="media/ome-message.png" alt-text="显示 Azure 信息保护分类的示例电子邮件页脚和标头":::

对于发送电子邮件的用户，他们需要与将受保护的电子邮件发送到自己的组织中的用户时执行相同的操作。 例如，选择“请勿转发”按钮，使 AIP 客户端可添加到 Outlook 功能区。 

或者，“请勿转发”功能可集成到标签中，用户可选择它来向该电子邮件同时应用分类和保护。 例如，在[统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)中：

![选择配置为“不转发”的标签](./media/recipients-only-label2.png)

管理员也可配置要应用权限保护的邮件流规则，为用户自动提供保护。

附加到这些电子邮件的任何 Office 文档页将自动受到保护。

## <a name="scanning-for-existing-content-to-classify-and-protect"></a>扫描现有内容来进行分类和保护

理想情况是，你在创建文档和电子邮件时对它们进行标记。 但是，你可能已在本地或云端存储很多文档，而你也想要对这些文档进行分类和保护。

使用下述方法之一对现有内容进行分类和保护：

- **本地存储**：请使用 [Azure 信息保护扫描程序](deploy-aip-scanner.md)来发现网络共享和 Microsoft SharePoint Server 站点及库中的文档，并对其进行分类和保护。

    扫描程序将作为一项服务在 Windows Server 上运行，它使用同一套策略规则来检测敏感信息并对文档应用特定标签。 

    或者，使用扫描程序向数据存储库中的所有文档应用默认标签，这样就无需检查文件内容。 仅在报告模式下使用扫描程序，来发现你可能不知道的敏感信息。

- **云数据存储**：请使用 [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/azip-integration) 将标签应用于 Box、SharePoint 和 OneDrive 中的文档。 要查看教程，请参阅[自动应用 Azure 信息保护分类标签](https://docs.microsoft.com/cloud-app-security/use-case-information-protection) 

## <a name="latest-labeling-updates-for-microsoft-365"></a>Microsoft 365 的最新标签更新

查看最新信息，了解 Azure 信息保护如何使用 Microsoft 365 来帮助你发现、分类、保护和监视位于任何位置的敏感信息：

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

有关详情，请参阅：

- [Microsoft 365 管理中心的新增功能](https://docs.microsoft.com/microsoft-365/admin/whats-new-in-preview)
- [SharePoint 管理中心的新增功能](https://docs.microsoft.com/sharepoint/what-s-new-in-admin-center)

## <a name="additional-azure-information-protection-resources"></a>其他 Azure 信息保护资源

- 免费试用版：[企业移动性 + 安全性 E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- 订阅选项和定价：[Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)

- 下载客户端：[Azure 信息保护客户端](https://www.microsoft.com/download/details.aspx?id=53018)

- 下载可自定义的最终用户指南：[Azure 信息保护最终用户采用指南](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- 常见问题解答：[Azure 信息保护的常见问题](faqs.md)

- Yammer：[Azure 信息保护](https://www.yammer.com/AskIPTeam)

- Twitter 源文档：[https://twitter.com/docsmsft](https://twitter.com/docsmsft)

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

在[快速入门](quickstart-viewpolicy.md)和[教程](infoprotect-quick-start-tutorial.md)的帮助下，自行配置和使用 Azure 信息保护。 

如果已准备好为组织部署该服务，请转到[操作方法指南](how-to-guides.md)。
