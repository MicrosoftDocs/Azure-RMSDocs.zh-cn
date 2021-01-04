---
title: 撤消文档访问-Azure 信息保护
description: 介绍最终用户如何使用 AIP 客户端撤消受保护文档的文档访问。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: f834aa10a522336067cc68ce9edd20284488b888
ms.sourcegitcommit: b9d7986590382750e63d9059206a40d28fc63eef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "97764095"
---
# <a name="user-guide-revoke-document-access-with-azure-information-protection-public-preview"></a>用户指南：使用 Azure 信息保护撤销文档访问 (公开预览版) 

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***相关的**： [仅限 AIP 统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [用户指南：使用 AIP 经典客户端时跟踪和撤销文档](client-track-revoke.md)。 *

本文介绍如何撤消 Microsoft Office 保护的文档的访问权限。

吊销受保护文档的访问权限可以防止其他用户访问该文档，即使您之前已向他们授予了访问权限。 有关详细信息，请参阅 [用户指南：通过 Azure 信息保护统一标签客户端对其进行分类和保护](clientv2-classify-protect.md)。

统一标签客户端的跟踪和撤销功能目前处于预览阶段。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 

## <a name="revoke-access-from-microsoft-office-apps"></a>撤消 Microsoft Office 应用的访问权限

若要撤消 Word、Excel 或 PowerPoint 中的访问权限：

1. 打开要撤消其访问权限的受保护文件。 这必须是已使用 *当前* 用户帐户 *应用了保护* 的文件。

    > [!TIP]
    > 如果你只是应用了标签和保护，则无法撤消同一会话中的访问权限。 如果需要撤消访问权限，请重新打开该文档。

1. 在 " **主页** " 选项卡上，单击 " **敏感度** " 按钮，然后选择 " **撤消访问权限**"：

    :::image type="content" source="../media/track-revoke-word.png" alt-text="选择 &quot;撤消 Microsoft Word 中的访问权限&quot;":::

    > [!NOTE]
    > 看不到此选项？ 有关详细信息，请参阅 [下面](#dont-see-the-revoke-access-option)的可能方案。
    >
 
1. 在出现的确认消息中，单击 **"是"** 以继续。

已吊销访问权限，其他用户将无法再访问该文档。 如果允许 [脱机访问](/microsoft-365/compliance/encryption-sensitivity-labels#assign-permissions-now) ，用户可以继续访问已撤消的文档，直到脱机策略期限过期。 

### <a name="dont-see-the-revoke-access-option"></a>看不到吊销访问权限选项？

如果在 "**敏感度**" 菜单中看不到 "**撤消访问权限**" 选项，则可能是下列方案之一：

- 你可能只是在此会话中应用了保护。 如果是这种情况，请关闭并重新打开文档，然后重试。

- 您可能正在查看未受保护的文档。 撤消访问权限仅适用于受保护的文档。

- 你可能没有安装最新的 AIP 统一标签客户端版本，或者你可能需要在安装后重新启动 Office 应用或计算机。 

    有关详细信息，请参阅 [用户指南：下载并安装 Azure 信息保护客户端](install-client-app.md)。

- 您的管理员可能已关闭组织中的 [跟踪功能](track-and-revoke-admin.md#turn-off-track-and-revoke-features-for-your-tenant) 。

## <a name="revoking-access-where-the-document-protection-has-been-changed-on-a-copy"></a>撤消对副本上的文档保护进行了更改的访问权限

如果其他用户已更改了该文档副本的标签或保护，则不会对该文档的副本 *撤销* 访问权限。 

这是因为跟踪和撤消访问是使用唯一的 Id 为值完成的，这将更改每次更改保护的时间。

> [!IMPORTANT]
> 如果你认为某个用户可能更改了文档的标签或保护级别，并且你需要撤消访问权限，请与系统管理员联系，以帮助你撤消对该文档副本的访问权限。
> 
## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅：

- [AIP 统一标签客户端用户指南](clientv2-user-guide.md)
- [AIP 统一标签客户端管理员指南](clientv2-admin-guide.md)
- [跟踪和撤销功能的已知问题](../known-issues.md#known-issues-for-track-and-revoke-features-public-preview)
