---
title: 快速入门 - 为特定用户新建 Azure 信息保护标签 - AIP
description: 使用范围策略，创建和配置为一部分用户分类文档和电子邮件的新标签。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/28/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 3e69706b786227cd41e215bc48c6caf9fab250bb
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935361"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>快速入门：为特定用户创建新的 Azure 信息保护标签

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：  [适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

本快速入门介绍如何创建新的 Azure 信息保护标签：只有特定用户才能查看该标签并应用它来分类并保护文档和电子邮件。

此配置使用范围策略。

在 10 分钟内即可完成此配置。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要具备以下条件：

1. 包含 Azure 信息保护计划 1 或计划 2 的订阅。
    
    如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

2. 已将“Azure 信息保护”窗格添加到 Azure 门户，并确认已激活保护服务。

    如果在执行这些操作时需要帮助，请参阅[快速入门：在 Azure 门户中开始](quickstart-viewpolicy.md)。

3. Azure AD 中已启用电子邮件的组，其中包含将查看和应用新标签的用户。
    
    如果你没有适当的组，请创建一个名为“销售团队”  的组并至少添加一个用户。

4. 测试新的标签：Azure 信息保护客户端（经典）必须安装在 Windows 计算机上。 
    
    若要安装经典客户端，可以转到 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection.exe  。
     
    如果对经典客户端使用了不同的标签客户端，请参阅 Office 文档，以了解本教程的等效说明。 例如，[敏感度标签概述](/microsoft-365/compliance/sensitivity-labels)。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。
    
## <a name="create-a-new-label"></a>创建新标签

首先，创建新标签。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”  窗格。
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”  并选择“Azure 信息保护”  。
    
    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

2. 从“分类” > “标签”菜单选项中   ：在“Azure 信息保护 - 标签”窗格上，单击“添加新标签”   。

3. 在“标签”  窗格上，至少指定以下两项：
    
    - **标签显示名称**：用户将看到的新标签名称，用于标识内容的分类。 例如：`Sales - Restricted`。
    
    - **说明**：工具提示，用于帮助用户确定何时选择此新标签。 例如：`Business data that is restricted to the Sales Team.`

4. 请确保“已启用”  设置为“开”  （默认设置），然后选择“保存”  。

## <a name="add-the-label-to-a-new-scoped-policy"></a>将标签添加到新范围策略

现在，将新创建的标签添加到新范围策略。

1. 从“分类” > “策略”菜单选项中   ：在“Azure 信息保护 - 策略”窗格上，选择“添加新策略”   。 

2. 在“策略”  窗格上，对于“策略名称”  框，输入一个名称，用于标识哪组用户能够查看新创建的标签。 例如，`Sales` 。

3. 选中“选择哪些用户或组可以获取此策略”  选项。

4. 在“AAD 用户和组”  窗格上，选择“用户/组”  。 然后，在新的“用户/组”  窗格上，搜索并选择在先决条件中标识的组。 例如，“销售团队”  。 单击该窗格上的“选择”  ，然后单击“确定”  。

5. 重新回到“策略”  窗格，选择“添加或删除标签”  。

6. 在“策略:  添加或删除标签”窗格上，选择已创建的标签，例如，“销售 - 受限”  ，然后选择“确定”  。

7. 重新回到“策略”  窗格，选择“保存”  。 

你的新标签现在仅向你指定的组的成员发布。 

## <a name="test-your-new-label"></a>测试新标签

要测试此标签，至少需要两台计算机，因为 Azure 信息保护客户端不支持同一台计算机上的多个用户：

 - 在第一台计算机上，以“销售团队”组的成员身份登录。 打开 Word，确认可以看到新标签。 如果 Word 已打开，请重新启动它以强制执行策略刷新。

- 在第二台计算机上，以非“销售团队”组的成员身份登录。 打开 Word，确认看不到新标签。 与前面一样，如果 Word 已打开，则重新启动它。

## <a name="clean-up-resources"></a>清理资源

如果不希望保留此标签和范围策略，请执行以下操作：

1. 从“分类” > “策略”菜单选项中   ：在“Azure 信息保护 - 策略”  窗格上，选择刚刚创建的范围策略的上下文菜单（“...”  ）。 例如，“销售”  。

2. 选择“删除策略”  ，如果系统提示你进行确认，请选择“确定”  。

3. 从“分类”   > “标签”  菜单选项中：在“Azure 信息保护 - 标签”  窗格上，选择刚刚创建的标签的上下文菜单（“...”  ）。  例如，“销售 - 受限”  。

4.  选择“删除此标签”  ，如果系统提示你进行确认，请选择“确定”  。


## <a name="next-steps"></a>后续步骤

本快速入门包含最少的选项，可以为特定用户快速创建新标签。 有关完整说明，请参阅以下文章：

- [如何创建新标签](configure-policy-new-label.md)

- [如何使用作用域内策略为特定用户配置策略](configure-policy-scope.md)

另外，如果你希望使用标签来保护内容，限制仅“销售团队”的成员可以打开该内容，需要配置标签以应用保护。 有关说明，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)。

