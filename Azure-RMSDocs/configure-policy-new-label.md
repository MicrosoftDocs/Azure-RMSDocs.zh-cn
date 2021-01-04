---
title: 新的 Azure 信息保护标签 - AIP
description: 尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建用户可在信息保护栏中看到的自己的标签。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 0a191dbdba3ceb2408757284847e4565d9338950
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806577"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>如何创建 Azure 信息保护的标签

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标签客户端，请参阅 Microsoft 365 文档中的 " [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) "。 *

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

尽管 Azure 信息保护附带了可以自定义的默认标签，你还可以创建自己的标签。

可以添加新标签，或在需要更高级别的分类时将新子标签添加到现有标签。 例如，[默认策略](configure-policy-default.md)中的最后一个标签包含子标签。

创建标签的首个子标签时，用户不能再选择原始父标签。 如有必要，请新建子标签来重新创建父标签设置，让用户能够应用相同的设置。

使用以下说明添加一个新标签，随后可以将其添加到 Azure 信息保护策略。

## <a name="to-create-a-new-label"></a>创建新标签

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”窗格。
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 从 "**分类**  >  **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，执行以下操作之一：
    
    - 创建新的标签：单击“**添加新的标签**”。
    
    - 若要创建新的子标签：右键单击或选择要为其创建子标签的标签的上下文菜单 (**...** ") ，然后单击" **添加子标签**"。

3. 在 " **标签** " 或 " **子标签** " 窗格中，选择此新标签所需的选项，然后单击 " **保存**"。
    
    指定显示名称时，禁止指定一些字符（如反斜杠和 & 号），因为并非所有使用 Azure 信息保护的服务和应用程序都支持这些字符。 除了阻止的字符以外，请不要指定 **#** 字符。    
    
    请注意，新标签将自动分配为黑色。 从颜色列表中选择一种可区分的颜色，或者输入颜色的红色、绿色和蓝色 (RGB) 组成的十六进制三元色代码。 例如，#DAA520。 如果需要这些代码的参考，可从 MSDN web 文档的页面找到一个有用的表格 [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) 。你还可以在许多应用程序中找到这些代码，以便你编辑图片。 例如，通过 Microsoft 画图，从调色板中选择自定义颜色，系统将自动显示 RGB 值，该值可供复制。

4. 向用户提供新标签：从 "**分类**  >  **策略**" 菜单选项中，选择要包含新标签的策略。 选择“添加或删除标签”。 从 " **策略：添加或删除标签** " 窗格中选择标签，选择 **"确定"**，然后选择 " **保存**"。
    
    >[!TIP]
    >对于新标签，请考虑首先将它们添加到用于测试的作用域内策略。 如果对结果满意，则从该测试范围删除标签，然后将标签添加到在生产中使用的策略。     
    
    有关添加标签的详细信息，请参阅[如何添加或删除标签](configure-policy-add-remove-label.md)。
    
    更改将会自动提供给用户和服务。 不再提供单独发布选项。

5. 如果希望以不同的语言为用户显示此新标签名称和说明：请按照 [如何为不同语言配置标签](configure-policy-languages.md)中的过程进行操作。 

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。  


