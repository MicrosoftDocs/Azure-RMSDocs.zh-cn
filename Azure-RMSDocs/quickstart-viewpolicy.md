---
title: 快速入门 - 在 Azure 门户中查看 Azure 信息保护 (AIP)
description: 如果你的组织刚刚开始使用 Azure 信息保护 (AIP)，请从此处开始将服务添加到 Azure 门户，确认已激活保护服务并发布标签和策略设置。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 0d3f289986688bab7e50f22bf9a9dc8c35f7ba5e
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807495"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>快速入门：在 Azure 门户中开始使用 Azure 信息保护

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 相关内容：*[适用于 Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

本快速入门包含以下内容：将 Azure 信息保护添加到 Azure 门户、确认保护服务已激活、创建默认标签（如果没有标签），并查看 Azure 信息保护经典客户端的策略设置。

所需时间：在 10 分钟内即可完成本快速入门。

## <a name="prerequisites"></a>先决条件

若要完成本快速入门，你需要：

- [Azure 门户](https://portal.azure.com/)帐户的访问权限。

- 包含 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection/)的订阅。

    如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

## <a name="add-azure-information-protection-to-the-azure-portal"></a>将 Azure 信息保护添加到 Azure 门户

即使你的订阅包含 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection/)，AIP 也不会自动在 Azure 门户中可用。

执行以下步骤以将 AIP 添加到 Azure 门户：

1. 使用租户的全局管理员帐户登录到 [Azure 门户](https://portal.azure.com)。

    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

1. 选择“+ 创建资源”。 在市场的搜索框中键入“Azure 信息保护”，然后选择“Azure 信息保护”。 在“Azure 信息保护”页上，选择“创建”，然后再次选择“创建”。

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="将 Azure 信息保护添加到 Azure 门户":::

    > [!TIP]
    > 如果这是你第一次执行此步骤，你将会在窗格名称旁看到“固定到仪表板”![固定到仪表板](media/qs-tutor/pin-to-dashboard.png "固定到仪表板图标")图标。 选择此图标可在仪表板上创建磁贴，以便你下一次可以直接导航到此处。

## <a name="confirm-that-the-protection-service-is-activated"></a>确认保护服务已激活

现在会自动为新客户激活保护服务。 确认立即激活还是之后激活，如下所示：

1. 在“Azure 信息保护”窗格上，选择“管理” > “保护激活”。

1. 确认是否已为租户激活保护。 例如：

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="确认 AIP 激活":::

    如果未在任何时间激活保护，则需要将其激活，方法是选择“激活”![激活 AIP](media/qs-tutor/activate.png "激活 AIP")。 激活完成后，信息栏将显示“激活已成功完成”。

## <a name="create-and-publish-labels"></a>创建和发布标签

你的组织可能已有标签，因为已为租户自动创建标签，或者因为 Office 365 安全与合规中心、Microsoft 安全中心或 Microsoft 合规中心具有敏感度标签。 我们一起来看一下：

1. 在“分类”下，选择“标签”。

    你可能已创建了默认标签。 下图显示了默认情况下使用 Azure 信息保护创建的标签：

    :::image type="content" source="media/info-protect-defaultlabels.png" alt-text="Azure 信息保护默认标签":::

    如果看不到默认标签或任何标签：

    如果看不到默认标签或任何标签，请选择“生成默认标签”来创建标签，以供在经典客户端中使用。

    如果在网格上方看不到“生成默认标签”按钮，请在“管理”下，选择“统一标记”。 如果“统一标记”的状态为“未激活”，请选择“激活”，然后返回到“分类” > “标签”窗格   。

    > [!NOTE]
    > 对于统一标记客户端，在 Microsoft M365 中管理标签。 有关详细信息，请参阅[通过敏感度标签应用加密，从而限制对内容的访问](/microsoft-365/compliance/encryption-sensitivity-labels)。
    >

1. 在 Azure 门户中发布标签，使其可用于 Azure 信息保护经典客户端：

    1. 打开“全局”策略。 在“分类”下，选择“策略” > “全局”。

    1. 选择“添加或删除标签”。

    1. 从“策略: 添加或删除标签”窗格中，选择所有标签，然后选择“确定”。

    1. 再从“策略:全局”窗格中，选择“保存”![保存](media/qs-tutor/save-icon.png "保存") 按钮。

        在提示符下，单击“确定”以发布所做的更改。

## <a name="view-your-labels"></a>查看标签

现在，你可以熟悉标签。

如果仍打开“全局”策略，请单击右上角的 X 关闭窗格。 在“分类”下，选择“标签”。

默认 Azure 信息保护分类标签是：

- 个人
- **常规**
- 机密
- 高度机密

默认情况下，某些标签已配置了视觉标记。 这些视觉标记可以是页脚、页眉和/或水印。 其他标记还配置了保护。

选择标签，并浏览以查看该标签的详细配置。

> [!TIP]
> 展开“高度机密”标签可以查看分类如何具有子类别的示例。
>

## <a name="view-your-policy-settings"></a>查看策略设置

首次从 Azure 门户连接到 Azure 信息保护服务时，将始终为你创建可供 Azure 信息保护客户端使用的默认策略设置。

- 经典客户端。 对于经典客户端，标签和策略设置均会下载到 Azure 信息保护策略中的客户端。

- 统一标记客户端。 对于统一标记客户端，只有标签会下载到该客户端。 从 Office 365 合规和安全中心、Microsoft 365 合规中心或 Microsoft 365 安全中心下载策略设置。 使用这些管理中心可以编辑标签和标签策略，而不是 Azure 门户。

    有关详细信息，请参阅 Microsoft 365 文档中的[了解敏感度标签](/microsoft-365/compliance/sensitivity-labels)。

经典客户端说明：

若要查看经典客户端的默认 Azure 信息保护策略设置，请执行以下操作：

1. 在“分类”下，选择“策略” > “全局”，以显示为租户创建的默认 Azure 信息保护策略设置。

1. 在“配置要对信息保护最终用户显示和应用的设置”部分中，策略设置显示在标签后面。 例如，未设置默认标签，文档和电子邮件无需具备标签，且用户在更改标签时无需提供理由：

    :::image type="content" source="media/defaultsettings-aip.png" alt-text="Azure 信息保护策略全局设置":::

1. 你现在可以在门户中关闭任何已打开的窗格。

## <a name="next-steps"></a>后续步骤

后续步骤将有所不同，具体取决于你使用的是经典客户端还是统一标记客户端。 不确定这些客户端之间有何区别？ 请参见[常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。

如果使用的是经典客户端：

- 在下一步中，你可能会发现以下教程有帮助：[编辑策略并为 Azure 信息保护创建新标签](infoprotect-quick-start-tutorial.md)。

- 或者，有关配置 Azure 信息保护策略的所有方面的详细说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

如果使用的是统一标记客户端：

请参阅 Microsoft 365 符合性文档中的[了解敏感度标签](/microsoft-365/compliance/sensitivity-labels)。