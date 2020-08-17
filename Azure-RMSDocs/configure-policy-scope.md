---
title: 为 Azure 信息保护配置作用域内策略 - AIP
description: 若要为特定的用户配置不同的设置和标签，必须配置用于 Azure 信息保护的作用域内策略。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6c7ab059ff19cc7f8b41bc345521e9e1798e7769
ms.sourcegitcommit: 325bb21a2210069f6d838ca7a875d7082c5e02a6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88264355"
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>如何使用作用域内策略为特定用户配置 Azure 信息保护策略

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）  和标签管理  将于 2021 年 3 月 31 日  弃用  。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

当 Azure 信息保护策略下载到已安装了 Azure 信息保护客户端的计算机时，所有用户都从默认策略或你为全局策略配置的更改获取设置和标签。 如果要使用不同的设置和标签为特定用户补充此配置，则必须创建为这些用户配置的 **作用域内策略** 。

## <a name="how-scoped-policies-work"></a>作用域内策略的工作方式

对于支持 Azure 信息保护客户端的应用程序，所有用户都会收到全局策略，其中包含信息保护栏标题和工具提示、全局设置以及全局标签。 如果为特定用户配置了作用域内策略，则那些用户还会收到那些附加设置和标签。 

请注意，除支持 Azure 信息保护客户端的 Office 桌面应用程序外，PowerShell 和 Azure 信息保护扫描程序也支持标签。 也就是说，可以为运行 Powershell 命令或扫描程序的帐户创建和配置范围内策略。 

与标签一样，作用域内策略也排列在 Azure 门户中。 如果为某个用户配置了多个作用域，则会首先为该用户计算有效策略，然后再下载该策略。 根据策略的顺序，将应用最后一个策略设置。 用户看到的标签是来自全局策略的标签和来自用户所属的作用域内策略的任何附加标签。

当你的租户中的用户打开标记的文档或电子邮件且此用户不在标签的作用域内时例外。 在此情况下，用户会看到标签集的名称，但标签不会显示为可供选择。  

因为作用域内策略始终从全局策略继承标签和设置，因此，在创建或编辑作用域内策略时会显示来自全局策略的标签。 不过，在编辑作用域内策略时，无法编辑来自全局策略的标签。 但是，可以向这些继承的标签添加子标签。

例如，如果全局策略中有一个名为**机密**的标签，则所有用户都会看到此标签。 无法使用作用域内策略删除或重排标签。 但是，你可能希望为市场营销部创建一个作用域内策略来向“机密”添加一个新的子标签，以便用户可以看到**机密\促销**。 你还可以为销售部创建另一个作用域内策略来向“机密”添加一个新的子标签，以便用户可以看到**机密\合作伙伴**。 然后，可以针对不同的设置配置每个子标签，并且只有相应部门中的用户才能看到子标签。

## <a name="configure-a-scoped-policy"></a>配置作用域内策略

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”窗格。

    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 从 "**分类**  >  **策略**" 菜单选项：在 " **Azure 信息保护-策略**" 窗格中，选择 "**添加新策略**"。 然后，你会看到 " **策略** " 窗格，其中显示了你的现有全局策略，你现在可以在其中配置新的作用域内策略。

3. 指定只有管理员才能在 Azure 门户中看到的策略名称和说明。 该名称在你的租户中必须是唯一的。 然后选择 " **指定获取此策略的用户/组**"，然后在后续窗格中，可以搜索和选择此策略的用户和组。 在此作用域内策略中配置的标签和设置将仅应用于这些用户。
    
    出于性能原因，将[缓存](prepare.md#group-membership-caching-by-azure-information-protection)作用域内策略的组成员关系。

    > [!NOTE]
    > 最多选择200个用户或组。 如果需要的用户数超过200，请创建新组，将相关用户添加到组，然后将策略范围设置为新组。 

4. 现添加新标签或配置作用域内策略设置。 全局策略始终首先应用，因此，你可以为全局策略补充新标签并且可以覆盖全局设置。 例如，全局策略可能没有指定默认标签，并且你在不同的作用域内策略中为特定部门配置了不同的默认标签。

    如果在配置标签或设置时需要帮助，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy) 部分中的链接。

6. 就像编辑全局策略时一样，当你在 "Azure 信息保护" 窗格中进行任何更改时，请单击 " **保存** " 以保存更改，或者单击 " **放弃** " 以还原到上次保存的设置。 

7. 对此作用域内策略完成所需更改后，在初始 " **Azure 信息保护-策略** " 窗格上，确保此作用域内策略按您希望的顺序应用。 为多个作用域内策略选择了同一用户时，这很重要。 若要更改顺序，请选择上下文菜单 (**...**) 并选择“上移”**** 或“下移”****。 

每次启动受支持的 Office 应用程序或打开文件资源管理器时，Azure 信息保护客户端都会检查是否进行了任何更改。 客户端会下载对全局策略或应用于该用户的作用域内策略所做的任何更改。

## <a name="next-steps"></a>后续步骤

有关如何自定义默认策略并在 Office 应用程序中查看所产生行为的示例，请尝试学习[编辑策略并创建新标签](infoprotect-quick-start-tutorial.md)教程。
