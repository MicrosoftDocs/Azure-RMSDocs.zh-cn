---
title: 快速入门 - 在 Azure 门户中开始使用 Azure 信息保护 - AIP
description: 如果你的组织刚刚开始使用 Azure 信息保护，请从此处开始将服务添加到 Azure 门户，确认已激活保护服务并查看策略。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/15/2018
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: 91a9a124c53d7c8f1aab31213595a8fc2f3627dd
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2019
ms.locfileid: "54393986"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>快速入门：在 Azure 门户中开始使用 Azure 信息保护

本快速入门介绍如何将 Azure 信息保护添加到 Azure 门户，确认已激活保护服务，并查看组织的默认策略。 

在 5 分钟内即可完成此快速入门。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要具备以下条件：

- 包含 Azure 信息保护计划 1 或计划 2 的订阅。
    
    如果没有上述任一订阅，可以为组织创建一个[免费](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

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

现在已为新租户自动激活保护服务，但最好确认它不需要手动激活。 

1. 在“Azure 信息保护”边栏选项卡上，选择“管理” > “保护激活”。

2. 确认是否已为租户激活保护： 
    
    - 如果保护已激活，会看到以下确认信息：
        
        ![Azure RMS 的 Azure 信息保护状态](./media/info-protect-azurerms-activated.png)
        
    - 如果保护未激活，会在状态信息中看到此反馈和激活选项：
        
        ![Azure RMS 的 Azure 信息保护状态](./media/info-protect-azurerms-deactivated.png)

3. 如果保护未激活，请选择“激活”。 

    激活完成后，信息栏将显示“激活已成功完成”。

## <a name="view-your-organizations-default-policy---labels-and-policy-settings"></a>查看组织的默认策略 - 标签和策略设置

使用 Azure 门户初次连接到 Azure 信息保护服务时，将创建该租户的默认策略。 默认策略包含可以按原样使用或自定义的标签和设置。

1. 选择“分类” > “策略” > “全局”，显示为租户创建的默认 Azure 信息保护策略。
    
2. 花几分钟时间了解显示的标签：
    
   - 用于分类的标签：“个人”、“公共”、“常规”、“机密”和“高度机密”。 最后两个标签展开可显示子标签，这提供了有关如何使分类具有子类别的示例：
    
   - 在默认配置中，某些标签未配置视觉标记。 视觉标记即页脚、页眉和水印。 某些标签可能设置了保护，具体取决于默认策略。 例如： 
    
     ![Azure 信息保护快速入门教程步骤 3 - 默认策略](./media/info-protect-policy-default-labelsv2.png)
    
3. “配置要对信息保护最终用户显示和应用的设置”部分中的标签后面还显示一些策略设置。 例如，未设置默认标签，文档和电子邮件无需具备标签，且用户在更改标签时无需提供理由：
    
    ![Azure 信息保护快速入门教程步骤 3 - 默认策略](./media/info-protect-policy-default-settings-quickstart.png) 

4. 由于只查看标签和设置，可以关闭已打开的任何边栏选项卡。

## <a name="next-steps"></a>后续步骤

现在可以在 Azure 门户中看到标签和策略设置，在下一步执行以下教程可能很有帮助：[编辑策略并为 Azure 信息保护创建新标签](infoprotect-quick-start-tutorial.md)。

或者，有关配置 Azure 信息保护策略的所有方面的详细说明，请参阅[配置 Azure 信息保护策略](configure-policy.md)。
