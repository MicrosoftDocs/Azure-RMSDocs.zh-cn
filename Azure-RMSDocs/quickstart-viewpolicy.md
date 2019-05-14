---
title: 快速入门 - 在 Azure 门户中查看 Azure 信息保护 - AIP
description: 如果你的组织刚刚开始使用 Azure 信息保护，请从此处开始将服务添加到 Azure 门户，确认已激活保护服务并查看标签和策略设置。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/25/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 099d35d7d4862aff3006b1d6cc57423b898234c4
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767891"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>快速入门：在 Azure 门户中开始使用 Azure 信息保护

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

本快速入门包含以下内容：将 Azure 信息保护添加到 Azure 门户、确认保护服务已激活、创建默认标签（如果没有标签），并查看 Azure 信息保护的策略设置。

在 10 分钟内即可完成本快速入门。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要具备以下条件：

- 包含 Azure 信息保护计划 1 或计划 2 的订阅。
    
    如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

## <a name="add-azure-information-protection-to-the-azure-portal"></a>将 Azure 信息保护添加到 Azure 门户

Azure 门户中不会自动包含 Azure 信息保护。 必须添加它。

1. 使用租户的全局管理员帐户登录到 [Azure 门户](https://portal.azure.com)。 
    
    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

2. 在中心菜单上，选择“创建资源”，然后在市场的搜索框中键入“Azure 信息保护”。 
    
3. 在结果列表中选择“Azure 信息保护”。 然后在“Azure 信息保护”边栏选项卡中，单击“创建”。
    
    > [!TIP] 
    > （可选）选择“固定到仪表板”以便在仪表板上创建“Azure 信息保护”磁贴，这样，下次登录到门户时，就可以跳过浏览到该服务。
    
    再次单击“创建”。

## <a name="confirm-the-protection-service-is-activated"></a>确认保护服务已激活

现在已为新客户自动激活保护服务，但最好确认它不需要手动激活。 

1. 在“Azure 信息保护”边栏选项卡上，选择“管理” > “保护激活”。

2. 确认是否已为租户激活保护： 
    
    - 如果保护已激活，会看到以下确认信息：
        
        ![Azure RMS 的 Azure 信息保护状态 - 已激活](./media/info-protect-azurerms-activated.png)
        
    - 如果保护未激活，会在状态信息中看到此反馈和激活选项：
        
        ![Azure RMS 的 Azure 信息保护状态 - 未激活](./media/info-protect-azurerms-deactivated.png)

3. 如果保护未激活，请选择“激活”。 

    激活完成后，信息栏将显示“激活已成功完成”。

## <a name="create-labels---if-necessary"></a>创建标签（如有必要）

你的组织可能已有标签，因为已为租户自动创建标签，或者因为 Office 365 安全与合规中心、Microsoft 安全中心或 Microsoft 合规中心具有敏感度标签。 我们一起来看一下：

1. 选择“分类” > “标签”：
    
    如果你看到选项“生成默认标签”，表明你还没有任何标签：
    
     ![Azure 信息保护无默认标签](./media/info-protect-nodefaultlabels.png)
    
    如果看不到用于生成默认标签的此选项，表明你已有标签，它们可能类似于下图中 Azure 信息保护的默认标签：
    
    ![Azure 信息保护默认标签](./media/info-protect-defaultlabels.png)

2. 如果你已有标签，请转到下一节以查看标签。 如果还没有标签，请选择“生成默认标签”选项。

4. 然后，若要为所有用户发布标签，请从“分类” > “策略” > “全局”中：
    
    a. 选择“添加或删除标签”。
    
    b. 从“策略: 添加或删除标签”边栏选项卡中，选择所有标签，然后选择“确定”。
    
    c. 再从“策略:全局”边栏选项卡上，选择“保存”。

## <a name="view-your-labels"></a>查看标签

选择“分类” > “标签”，并花一些时间熟悉“Azure 信息保护 - 标签”边栏选项卡上显示的标签。

如果它们不与上一节图中的标签类似，说明你使用的不是 Azure 信息保护中的默认标签，而是从 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 合规中心创建的标签。

> [!TIP]
> 如果不需要使用自定义标签，但要使用 Azure 信息保护中的默认标签，请执行以下操作： 
> - 删除自定义标签，然后会将在“标签”边栏选项卡中看到用于生成默认标签的选项，如[上一节](#create-labels---if-necessary)中所述。 

从“Azure 信息保护 - 标签”边栏选项卡上：

- 用于分类的默认标签包括：“个人”、“公共”、“常规”、“机密”和“高度机密”。 最后两个标签展开可显示子标签，这提供了有关如何使分类具有子类别的示例。

- 从“MARKING”和“PROTECTION”列中，可以看到某些标签已配置视觉标记。 视觉标记即页脚、页眉和水印。 某些标签可能还设置了保护。 

例如： 

![默认标签的 Azure 信息保护快速入门概述](./media/info-protect-policy-default-labelsv2.png)

如果选择一个标签，将在新的边栏选项卡上看到该标签配置的详细信息。

## <a name="view-your-policy-settings"></a>查看策略设置

首次使用 Azure 门户连接到 Azure 信息保护服务时，将始终为你创建可供 Azure 信息保护客户端使用的默认策略设置。 对于此客户端，我们查看的策略设置和标签会下载到 Azure 信息保护策略中的客户端。

如果使用 Azure 信息保护统一标记客户端，那么此客户端不会使用这些策略设置。 相反，此客户端从 Office 365 合规和安全中心、Microsoft 365 合规中心或 Microsoft 365 安全中心下载标签和策略设置。

若要查看默认的 Azure 信息保护策略设置，请执行以下操作：

1. 选择“分类” > “策略” > “全局”，以显示为租户创建的默认 Azure 信息保护策略设置。
    
2. 在“配置要对信息保护最终用户显示和应用的设置”部分中的标签后面，你将看到策略设置。 例如，未设置默认标签，文档和电子邮件无需具备标签，且用户在更改标签时无需提供理由：
    
    ![Azure 信息保护策略全局设置](./media/info-protect-policy-default-settingsv3.png)

3. 由于只查看设置，因此可以在门户中关闭已打开的任何边栏选项卡。

## <a name="next-steps"></a>后续步骤

现在可以在 Azure 门户中看到默认标签和策略设置，在下一步中，以下教程可能很有帮助：[编辑策略并为 Azure 信息保护创建新标签](infoprotect-quick-start-tutorial.md)。

或者，有关配置 Azure 信息保护策略的所有方面的详细说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。
