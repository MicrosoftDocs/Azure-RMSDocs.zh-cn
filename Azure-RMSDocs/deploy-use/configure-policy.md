---
title: "配置 Azure 信息保护策略"
description: "若要配置分类、标记和保护，必须配置 Azure 信息保护策略。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 67d38d19408c67c5da8db188395e00a7d3f9d999
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="configuring-the-azure-information-protection-policy"></a>配置 Azure 信息保护策略

>适用于：Azure 信息保护

若要配置分类、标记和保护，必须配置 Azure 信息保护策略。 然后将此策略下载到已安装 [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)(#azure-信息保护客户端) 的计算机。

## <a name="subscription-support"></a>订阅支持

Azure 信息保护支持不同级别的订阅：

- Azure 信息保护 P2：支持所有分类、设置标签和保护功能。

- Azure 信息保护 P1：支持大多数分类、设置标签和保护功能，但不支持自动分类或 HYOK。

- 包括 Azure 权限管理服务的 Office 365：支持保护，但不支持分类和设置标签功能。

需要 Azure 信息保护 P2 订阅的选项在门户中进行标识。

如果贵组织拥有组合订阅，则你有责任确保用户不会使用其帐户未授权使用的功能。 Azure 信息保护客户端不会进行许可证检查以及强制执行。 在配置并非所有用户都具有相应许可证的选项时，请使用作用域内策略或注册表设置，以确保组织符合许可证：

- **当组织具备 Azure 信息保护 P1 和 Azure 信息保护 P2 的组合许可证时**：对于具有 P2 许可证的用户，请在配置需要 Azure 信息保护 P2 许可证的选项时创建并使用一个或多个[作用域内策略](configure-policy-scope.md)。 请确保全局策略不包含需要 Azure 信息保护 P2 许可证的选项。

- **当组织具有 Azure 信息保护订阅，但有些用户只有包含 Azure 权限管理服务的 Office 365 许可证时**：对于没有 Azure 信息保护许可证的用户，可在其计算机上编辑注册表，以防止他们下载 Azure 信息保护策略。 有关说明，请参阅管理员指南了解以下自定义项：[当组织具备组合许可证时，强制执行仅保护模式](../rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses)。

有关订阅的详细信息，请参阅 [需要为 Azure 信息保护准备哪个订阅，它包括哪些功能？](../get-started/faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

## <a name="signing-in-to-the-azure-portal"></a>登录到 Azure 门户

若要登录到 Azure 门户以配置和管理 Azure 信息保护：

- 使用以下链接：https://portal.azure.com

- 使用具有以下[管理员角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)之一的帐户：
    
    - **信息保护管理员**（当前为预览版）

    - **安全管理员**

    - **全局管理员/公司管理员**


## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>首次访问“Azure 信息保护”边栏选项卡

1. 登录到 Azure 门户。

2. 在中心菜单上，单击“创建资源”，然后从“MARKETPLACE”列表中选择“安全 + 标识”。 
    
3. 在“安全 + 标识”边栏选项卡上，从“特别推荐的应用”列表中选择“Azure 信息保护”。 然后，在“Azure 信息保护”边栏选项卡上，单击“创建”。
    
    此操作将为你的租户创建“Azure 信息保护”边栏选项卡，使你下次登录门户时，可以从中心的“所有服务”列表中选择此服务。 
    
    > [!TIP] 
    > 选择“固定到仪表板”以便在仪表板上创建“Azure 信息保护”磁贴，这样，下次登录到门户时，就可以跳过浏览到该服务。

4. 首次连接到该服务时，“快速入门”页会自动打开。 浏览建议的资源，或使用其他菜单选项。 要配置用户可选择的标签，请使用以下过程。

下次访问“Azure 信息保护”边栏选项卡时，将自动选择“策略” > “全局策略”选项，以便可为所有用户配置标签。 从“常规”菜单进行选择即可返回“快速入门”页。

## <a name="how-to-configure-the-azure-information-protection-policy"></a>如何配置 Azure 信息保护策略

1. 请确保使用以下管理角色之一登录到 Azure 门户：信息保护管理员、安全管理员或全局管理员。 请参阅[前述部分](#signing-in-to-the-azure-portal)了解有关这些管理角色的详细信息。

2. 如有必要，可导航到“Azure 信息保护”边栏选项卡：例如，在中心菜单上，单击“所有服务”并开始在“筛选”框中键入“信息保护”。 在结果中选择“Azure 信息保护”。 
    
    “Azure 信息保护 - 全局策略”边栏选项卡会自动打开，你可以查看和编辑所有用户获得的全局策略。 
    
    Azure 信息保护策略包含以下可配置的元素：
    
    - 让你和用户对文档和电子邮件进行分类的标签。
    
    - 用户在 Office 应用程序中看到的信息保护栏的标题和工具提示。
    
    - 在用户保存文档和发送电子邮件时强制执行分类的选项。
    
    - 将默认标签设置为对文档和电子邮件进行分类的起始点的选项。
    
    - 当用户选择比原始级别低的敏感度级别时提示用户提供相应原因的选项。
    
    - 用于自动标记电子邮件的选项（基于电子邮件附件）。
    
    - 为用户提供自定义帮助链接的选项。

Azure 信息保护附带[默认策略](configure-policy-default.md)，其中包含五个主要标签。 这些标签中有 2 个包含子标签，可根据需要提供子类别。 为子标签配置标签时，用户不能选择主标签，但必须选择一个子标签。

Azure 信息保护标签可用于组织常规创建和存储的数据，包括从最低等级的个人数据到最高等级的机密数据等各类数据。 

可以使用无更改的默认标签，或者你可以自定义它们，或删除它们，并可以创建新标签。 有关详细信息，请使用下一节中的链接来帮助你找到相关选项以及配置方法。

可以创建任意数量的标签。 但是，如果因标签数量过多而导致用户难以看见并选择正确的标签，可以创建作用域内策略，使用户仅看见相关的标签。 应用保护的标签具有数量上限（500 个）。

当在“Azure 信息保护”边栏选项卡上进行任何更改时，请单击“**保存**”以保存更改，或者单击“**放弃**”以返回到上一个保存的设置。

在完成所需更改后，单击“**发布**”。 

每当受支持的 Office 应用程序启动时，Azure 信息保护客户端都会检查是否有任何变化，并根据最新的 Azure 信息保护策略下载这些更改。 在客户端上刷新策略的其他触发器：

- 右键单击以分类和保护文件或文件夹。

- 运行 [PowerShell cmdlet](../rms-client/client-admin-guide-powershell.md) 以实现标签设置和保护（Get-AIPFileStatus、Set-AIPFileClassification 和 Set-AIPFileLabel）。

- 每 24 小时一次。

- [Azure 信息保护扫描程序](deploy-aip-scanner.md)：服务启动后，每小时一次。


>[!NOTE]
>客户端下载策略时，需要等待几分钟，它才能完全正常运行。 实际时间会因多种因素而异，例如策略配置的大小和复杂性以及网络连接。 如果标签生成的操作与最新更改不匹配，请等待最多 15 分钟，然后重试。

### <a name="configuring-your-organizations-policy"></a>配置组织的策略

使用以下信息来帮助你配置你的 Azure 信息保护策略：

- [默认信息保护策略](configure-policy-default.md)

- [如何配置策略设置](configure-policy-settings.md)

- [如何创建新标签](configure-policy-new-label.md)

- [如何删除或重排标签](configure-policy-delete-reorder.md)

- [如何更改或自定义现有标签](configure-policy-change-label.md)

- [如何配置标签以进行保护](configure-policy-protection.md)

- [如何配置标签以应用可视标记](configure-policy-markings.md)

- [如何为自动和建议分类配置条件](configure-policy-classification.md)

- [如何使用作用域内策略为特定用户配置策略](configure-policy-scope.md)

- [如何配置和管理模板](configure-policy-templates.md)

- [如何为不同语言配置标签](configure-policy-languages.md)

## <a name="next-steps"></a>后续步骤

有关如何自定义默认策略并在 Office 应用程序是查看所产生行为的示例，请尝试 [Azure 信息保护快速入门教程](../get-started/infoprotect-quick-start-tutorial.md)(#azure-信息保护快速入门教程)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
