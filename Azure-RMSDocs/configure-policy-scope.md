---
title: 为 Azure 信息保护配置作用域内策略 - AIP
description: 若要为特定用户配置不同的设置和标签，必须为 Azure 信息保护配置作用域内策略。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4082ffeb2a2410f132c0542d0fb770163c5b5f4c
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559525"
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>如何使用作用域内策略为特定用户配置 Azure 信息保护策略

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> *适用于[Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

将 Azure 信息保护策略下载到安装了 [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)的计算机时，所有用户都会从默认策略或为全局策略配置的更改中获取设置和标签。 如果要使用不同的设置和标签为特定用户补充此配置，则必须创建为这些用户配置的**作用域内策略**。

## <a name="how-scoped-policies-work"></a>作用域内策略的工作方式

对于支持 Azure 信息保护客户端的应用程序，所有用户都会收到全局策略，其中包含信息保护栏标题和工具提示、全局设置以及全局标签。 如果已为特定用户配置了作用域内策略，这些用户会收到这些附加设置和标签。 

请注意，除支持 Azure 信息保护客户端的 Office 桌面应用程序外，PowerShell 和 Azure 信息保护扫描程序也支持标签。 也就是说，可以为运行 Powershell 命令或扫描程序的帐户创建和配置范围内策略。 

作用域内策略与标签相似，都会在 Azure 门户中排序。 如果为用户配置了多个作用域，则会在下载之前为用户计算有效策略。 根据策略的顺序，将应用最后一个策略设置。 用户看到的标签来自全局策略，而其他标签来自用户所属的作用域内策略。

当你的租户中的用户打开标记的文档或电子邮件且此用户不在标签的作用域内时例外。 在此情况下，用户会看到标签集的名称，但标签不会显示为可供选择。  

由于作用域内策略始终继承全局策略中的标签和设置，因此在创建或编辑作用域内策略时会显示全局策略中的标签。 但是，编辑作用域内策略时，无法从全局策略中编辑标签。 但可将子标签添加到这些继承的标签中。

例如，如果全局策略中有一个名为 **Confidential** 的标签，则所有用户都会看到此标签。 无法使用作用域内策略删除或重排标签。 但是你可能想为市场营销部创建一个作用域内策略，它会将新的子标签添加到 Confidential，以便这些用户可以查看 **Confidential\Promotions**。 还可为销售部创建另一个作用域内策略，它会将新的子标签添加到 Confidential，以便这些用户可以查看 **Confidential\Partners**。 每个子标签随后可以针对不同设置进行配置，子标签仅对各自部门的用户可见。

## <a name="configure-a-scoped-policy"></a>配置作用域内策略

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到 " **Azure 信息保护**" 窗格。

    例如，在 "资源"、"服务" 和 "文档" 的 "搜索" 框中，开始键入**信息**并选择 " **Azure 信息保护**"。

2. 从 "**分类**" > **策略**"菜单选项：在" **Azure 信息保护-策略**"窗格中，选择"**添加新策略**"。 然后，你会看到 "**策略**" 窗格，其中显示了你的现有全局策略，你现在可以在其中配置新的作用域内策略。

3. 在 Azure 门户中指定仅管理员可见的策略名称和说明。 该名称对租户来说必须是唯一的。 然后选择 "**指定获取此策略的用户/组**"，然后在后续窗格中，可以搜索和选择此策略的用户和组。 在此作用域内策略中配置的标签和设置将仅应用于这些用户。
    
    出于性能原因，作用域策略的组成员身份会进行[缓存](prepare.md#group-membership-caching-by-azure-information-protection)。

4. 现添加新标签或配置作用域内策略设置。 始终优先应用全局策略，以便使用新标签补充全局策略，并可以覆盖全局设置。 例如，全局策略可能没有指定的默认标签，并且你为特定部门在不同作用域内策略中配置不同的默认标签。

    如果在配置标签或设置时需要帮助，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。

6. 就像编辑全局策略时一样，当你在 "Azure 信息保护" 窗格中进行任何更改时，请单击 "**保存**" 以保存更改，或者单击 "**放弃**" 以还原到上次保存的设置。 

7. 对此作用域内策略完成所需更改后，在初始 " **Azure 信息保护-策略**" 窗格上，确保此作用域内策略按您希望的顺序应用。 为多个作用域内策略选择了相同用户时，这一点很重要。 要更改顺序，请选择上下文菜单（“...”），然后选择“上移”或“下移”。 

启动受支持的 Office 应用程序或打开文件资源管理器时，Azure 信息保护客户端会检查任何更改。 客户端会将所有更改都下载到适用于该用户的全局策略或作用域内策略中。

## <a name="next-steps"></a>后续步骤

有关如何自定义默认策略并在 Office 应用程序中查看所产生行为的示例，请尝试学习[编辑策略并创建新标签](infoprotect-quick-start-tutorial.md)教程。
