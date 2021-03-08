---
title: 分类和标签的常见问题解答 - AIP
description: 使用 Azure 信息保护进行分类和设置标签时遇到问题？ 请查看此处是否有答案。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 22d655bc69fc5db7b4bad27eb09a826a1fde34b9
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446875"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>有关 Azure 信息保护中的分类和标签的常见问题

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关详细信息，请参阅仅适用于 [经典客户端的常见问题解答](faqs-classic.md)。 *

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

遇到有关 Azure 信息保护的专门与分类和标签有关的问题？  请查看此处是否有答案。 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>我应该安装哪个客户端来测试新功能？

建议安装 **Azure 信息保护统一标签客户端**。 统一标签客户端从以下管理中心之一下载标签和策略设置： 

- Office 365 安全与合规中心
- Microsoft 365 安全中心
- Microsoft 365 相容性中心。

此客户端现已正式发布，并且可能有一个预览版本，你可以在将来的版本中测试其他功能。

如果仍在尚未 [迁移到统一标签存储](configure-policy-migrate-labels.md)的 Azure 门户中配置标签，请改用 **Azure 信息保护经典客户端** 。

有关详细信息（包括功能和功能比较表），请参阅 [选择 Windows 标记解决方案](rms-client/use-client.md#choose-your-windows-labeling-solution)。

> [!TIP]
> 仅在 Windows 上支持 Azure 信息保护客户端。 
>
> 若要对 iOS、Android、macOS 和 web 上的文档和电子邮件进行分类和保护，请使用 [支持内置标签的 Office 应用](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)。 
> 

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>在哪里可以找到有关使用 Office 应用的敏感度标签的信息？

请参阅以下文档资源：

- [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) 

- [在 Office 应用中使用敏感度标签](/microsoft-365/compliance/sensitivity-labels-office-apps)

- [在 SharePoint 和 OneDrive 中为 Office 文件启用敏感度标签](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)

- [向 Office 中的文档和电子邮件应用敏感度标签](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

有关支持敏感度标签的其他方案的信息，请参阅 [敏感度标签的常见方案](/microsoft-365/compliance/get-started-with-sensitivity-labels#common-scenarios-for-sensitivity-labels)。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>如何防止他人删除或更改标签？

要防止用户删除或更改标签，内容必须已受到保护，并且保护权限不向用户授予导出或完全控制[使用权限](configure-usage-rights.md)。 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>标记一封电子邮件时，是否有任何附件会自动获得相同的标记？

不是。 标记有附件的电子邮件时，这些附件不会继承相同的标记。 附件仍不带标签，或者保留单独应用的标签。 不过，如果电子邮件的标签应用了保护配置，此保护配置也会应用于 Office 附件。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP 解决方案和其他应用如何与 Azure 信息保护相集成？

因为 Azure 信息保护将永久性元数据用于分类（包括明文标签），所以此信息可供 DLP 解决方案和其他应用程序读取。 

有关将此元数据与 Exchange Online 邮件流规则配合使用的示例，请参阅[配置 Azure 信息保护标签的 Exchange Online 邮件流规则](configure-exo-rules.md)。