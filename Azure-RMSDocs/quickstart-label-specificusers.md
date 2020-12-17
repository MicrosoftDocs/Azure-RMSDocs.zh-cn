---
title: 快速入门 - 为特定用户新建 Azure 信息保护标签 - AIP
description: 使用范围策略，创建和配置为一部分用户分类文档和电子邮件的新标签。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e706cd2ec04d60b1520839fb76c21105ebf95625
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386298"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>快速入门：为特定用户创建新的 Azure 信息保护标签

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 相关内容：*[适用于 Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

本快速入门介绍如何创建新的 Azure 信息保护标签：只有特定用户才能查看该标签并应用它来分类并保护文档和电子邮件。

此配置使用范围策略。

所需时间：在 10 分钟内即可完成此配置。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要具备以下条件：

|要求  |说明  |
|---------|---------|
|支持订阅     |  你需要包含 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection/)的订阅。 </br></br>如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。       |
|AIP 已添加到 Azure 门户    |  已将“Azure 信息保护”窗格添加到 Azure 门户，并确认已激活保护服务。 </br></br>有关详细信息，请参阅[快速入门：在 Azure 门户中开始](quickstart-viewpolicy.md)。       |
|Azure AD 中已启用电子邮件的组     | 你将需要 Azure AD 中已启用电子邮件的组，其中包含将查看和应用新标签的用户。 </br></br>如果你没有适当的组，请创建一个名为“销售团队”的组并至少添加一个用户。 |
|经典客户端已安装    |   若要测试新标签，需要在计算机上安装经典客户端。 </br></br>2021 年 3 月将弃用 Azure 信息保护经典客户端。 若要部署 AIP 经典客户端，请打开支持票证以获取下载访问权限。  |
| | |

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

## <a name="create-a-new-label"></a>创建新标签

首先，创建新标签。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](https://portal.azure.com)。 然后导航到“Azure 信息保护”窗格。

    例如，在资源、服务和文档的搜索框中，开始键入“信息”并选择“Azure 信息保护”。

    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

1. 在“分类”下，选择“标签”，然后单击“+ 添加新标签”。

1. 在“标签”窗格上，至少指定以下两个字段：

    |字段  |描述  |
    |---------|---------|
    |标签显示名称     |    用户将看到的新标签名称，用于标识内容的分类。 </br>例如：销售 - 受限    |
    |**描述**     |   工具提示，用于帮助用户确定何时选择此新标签。 </br> 例如：仅限销售团队的业务数据。     |
    | | | 

1. 请确保“已启用”设置为“开”（默认设置），然后选择“保存”![保存](media/qs-tutor/save-icon.png "保存")。

    选择右上角的 X，以关闭“新建标签”窗格。

## <a name="add-the-label-to-a-new-scoped-policy"></a>将标签添加到新范围策略

现在，将新创建的标签添加到新范围策略。

1. 在左侧的“分类”下，选择“策略”，然后单击“添加新策略”。

1. 在“策略名称”字段中，输入有意义的值，用于描述将看到你的新标签的用户。

    例如，“销售”。

1. 选择“选择获取此策略的用户或组”行以打开“AAD 用户和组”窗格。

1. 在“AAD 用户和组”窗格上，搜索并选择在先决条件中标识的组，如“销售团队”。

    单击“选择”以关闭窗格。

1. 返回到“策略”窗格，在“标签显示名称”下，单击“添加或删除标签”。

1. 在“策略:添加或删除标签”窗格上，选择已创建的标签，例如，“销售 - 受限”，然后选择“确定”。

1. 返回到“策略”窗格，选择“保存”![保存](media/qs-tutor/save-icon.png "保存")。

你的新标签现在仅向你指定的组的成员发布。

## <a name="test-your-new-label"></a>测试新标签

要测试此标签，至少需要两台计算机，因为 Azure 信息保护客户端不支持同一台计算机上的多个用户：

- 在第一台计算机上，以“销售团队”组的成员身份登录。 打开 Word，确认可以看到新标签。 如果 Word 已打开，请重新启动它以强制执行策略刷新。

- 在第二台计算机上，以非“销售团队”组的成员身份登录。 打开 Word，确认看不到新标签。 与前面一样，如果 Word 已打开，则重新启动它。

## <a name="clean-up-resources"></a>清理资源

如果不希望保留此标签和范围策略，请执行以下操作：

1. 从“分类” > “策略”区域中 ：在“Azure 信息保护 - 策略”窗格上，选择已创建的作用域内策略的上下文菜单（“...”）。 例如，“销售”。

1. 选择“删除策略”，如果系统提示你进行确认，请选择“确定”。

1. 从“分类” > “标签”区域中：在“Azure 信息保护 - 标签”窗格上，选择已创建的标签的上下文菜单（“...”）。  例如，“销售 - 受限”。

1. 选择“删除此标签”，如果系统提示你进行确认，请选择“确定”。

## <a name="next-steps"></a>后续步骤

本快速入门包含最少的选项，以便你可以使用经典客户端为特定用户快速创建新标签。 有关完整说明，请参阅以下文章：

- [如何创建新标签](configure-policy-new-label.md)

- [如何使用作用域内策略为特定用户配置策略](configure-policy-scope.md)

另外，如果你希望使用标签来保护内容，限制仅“销售团队”的成员可以打开该内容，需要配置标签以应用保护。 有关说明，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)。
