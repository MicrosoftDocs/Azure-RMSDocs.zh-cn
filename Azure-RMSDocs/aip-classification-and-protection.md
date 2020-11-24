---
title: Azure 信息保护 (AIP) 标签、分类和保护
description: 了解 Azure 信息保护如何 (AIP) 如何为文档和电子邮件添加标签来分类和保护数据。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 450cf34997f676e1033856e14adfc3e792fb1e04
ms.sourcegitcommit: 1086cf04a29bb12cdb25c1fd8429f93d423bcc69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2020
ms.locfileid: "95566500"
---
# <a name="azure-information-protection-aip-labeling-classification-and-protection"></a>Azure 信息保护 (AIP) 标签、分类和保护

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

Azure 信息保护 (AIP) 是一种基于云的解决方案，可帮助组织通过应用标签来对文档和电子邮件进行分类和保护。 

例如，你的管理员可能配置了一个具有检测敏感数据（例如信用卡信息）的规则的标签。 在这种情况下，在 Word 文件中保存信用卡信息的所有用户都可能在文档顶部看到一个工具栏，其中建议他们应用针对此场景的相关标签。

标签可以对文档进行[分类](#how-labels-apply-classification-with-aip)和（可选）[保护](#how-aip-protects-your-data)，使你能够：

- 跟踪和控制使用内容的方式
- 分析数据流以深入了解业务 - 检测有风险的行为并采取纠正措施 
- 跟踪文档访问，防止数据泄漏或不当使用
- 以及更多...

## <a name="how-labels-apply-classification-with-aip"></a>标签如何使用 AIP 应用分类

用 AIP 标记你的内容包括：

- 无论数据存储在哪里或与谁共享都能检测到的分类。
- 视觉标记，例如标头、页脚或水印。
- 以明文形式添加到文件和电子邮件标头的元数据。 明文形式的元数据可确保其他服务能够识别分类并执行相应的操作

例如在下图中，标记服务使用[统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)将电子邮件分类为“常规”：

:::image type="content" source="media/example-email-footerv2.png" alt-text="显示 Azure 信息保护分类的示例电子邮件页脚和标头":::

在此示例中，标记还：

- 向电子邮件添加了“敏感度:***常规”的页脚*** 。 该页脚是显示给所有收件人的一个可视指示器，用于不得在组织外部发送的一般业务数据。
- 电子邮件标头中嵌入的元数据。 通过标头数据，电子邮件服务可检测标签，从理论上说可创建审核条目或阻止它发送到组织外部。

管理员可以使用规则和条件、用户手动应用标签，也可以使用管理员定义向用户显示的建议的组合。

## <a name="how-aip-protects-your-data"></a>AIP 如何保护数据

Azure 信息保护使用 [Azure Rights Management 服务](what-is-azure-rms.md) (Azure RMS) 来保护数据。 

Azure RMS 已与其他 Microsoft 云服务和应用程序（例如 Office 365 和 Azure Active Directory）集成，它还可用于你自己或第三方应用程序和信息保护解决方案。 Azure RMS 同时适用于本地和云解决方案。

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

:::image type="content" source="media/templates-exchangeonline-callouts.png" alt-text="为 Exchange Online 选择模板的示例":::

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

:::image type="content" source="media/right-click-classify-protect-folder.png" alt-text="在文件资源管理器中，右键单击“使用 Azure 信息保护进行分类和保护”":::

“分类和保护”菜单选项的工作方式与 Office 应用程序汇总的“应用保护”栏类似，用户可选择标签或设置自定义权限。

> [!TIP]
> 高级用户或管理员可能会发现，PowerShell 命令可用来更高效地管理和设置多个文件的分类和保护。 客户端中有[相关的 PowerShell 命令](https://docs.microsoft.com/powershell/module/azureinformationprotection)，它们也可单独安装。

用户和管理员可使用文档跟踪站点来监视受保护的文档、查看谁何时访问了这些文档。 如果他们怀疑存在误用，则还可以撤消对这些文档的访问权限。 例如：

![撤销文档跟踪站点中的访问图标](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>其他电子邮件集成

将 AIP 与 Exchange Online 结合使用可带来额外的好处，可将受保护的电子邮件发送给任意用户并保证他们可在任意设备上阅读这些邮件。

例如，你可能需要将敏感信息发送到使用 Gmail、Hotmail 或 Microsoft 帐户的个人电子邮件地址，或者发送给在 Office 365 或 Azure AD 中没有帐户的用户  。 这些电子邮件应静态加密并在传输中加密，且只有原始收件人才能阅读。

此方案需要 [Office 365 消息加密功能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)。 如果收件人在本机电子邮件客户端中无法打开受保护的电子邮件，可以使用一次性密码，通过浏览器阅读敏感信息。

例如，Gmail 用户可能会在收到的电子邮件中看到以下提示：

:::image type="content" source="media/ome-message.png" alt-text="OME 和 AIP 的 Gmail 收件人体验":::

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


## <a name="next-steps"></a>后续步骤

在[快速入门](quickstart-viewpolicy.md)和[教程](infoprotect-quick-start-tutorial.md)的帮助下，自行配置和使用 Azure 信息保护。 

如果已准备好为组织部署该服务，请转到[操作方法指南](how-to-guides.md)。
