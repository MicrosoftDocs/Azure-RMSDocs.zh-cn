---
title: "配置 Azure 信息保护策略"
description: "若要配置分类、标记和保护，必须配置 Azure 信息保护策略。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 7a4922384a228457b683653e80afe4b8c8db6df2
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="configuring-azure-information-protection-policy"></a>配置 Azure 信息保护策略

>适用于：Azure 信息保护

若要配置分类、标记和保护，必须配置 Azure 信息保护策略。 然后将此策略下载到已安装 [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)(#azure-信息保护客户端) 的计算机。

## <a name="subscription-support"></a>订阅支持

Azure 信息保护策略支持不同级别的订阅：

- Azure 信息保护 P2：支持所有分类、设置标签和保护功能。

- Azure 信息保护 P1：支持大多数分类、设置标签和保护功能，但不支持自动分类或 HYOK。

- 包括 Azure 权限管理服务的 Office 365：支持保护，但不支持分类和设置标签功能。

现在，需要 Azure 信息保护 P2 订阅的选项在门户中进行标识。

如果你具有租户的用户混合订阅，则有责任确保用户下载的 Azure 信息保护策略不包含未授权给其帐户使用的配置选项。 配置并非所有用户都获许可使用的选项时，请使用作用域内策略，这样就不会将用户配置为使用他们不具有许可证的功能。

有关订阅的详细信息，请参阅 [需要为 Azure 信息保护准备哪个订阅，它包括哪些功能？](../get-started/faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

有关如何配置作用域内策略的详细信息，请参阅[如何使用作用域内策略为特定用户配置策略](configure-policy-scope.md)。

## <a name="how-to-configure-the-azure-information-protection-policy"></a>如何配置 Azure 信息保护策略

1. 在新浏览器窗口中，以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。

2. 导航到“Azure 信息保护”边栏选项卡：例如，在中心菜单上，单击“更多服务”并在“筛选”框中开始键入**信息保护**。 在结果中选择“Azure 信息保护”。 
    
    首次连接到服务时，“快速入门”页会自动打开。 要配置所有用户均可获取的策略，请单击“全局策略”以打开“策略: 全局”边栏选项卡。 此边栏选项卡自动打开，以便执行后续连接到服务的操作，方便你查看和编辑所有用户获取的全局策略。 
    
    Azure 信息保护策略包含以下可配置的元素：
    
    - 让你和用户对文档和电子邮件进行分类的标签。
    
    - 用户在 Office 应用程序中看到的信息保护栏的标题和工具提示。
    
    - 在用户保存文档和发送电子邮件时强制执行分类的选项。
    
    - 将默认标签设置为对文档和电子邮件进行分类的起始点的选项。
    
    - 当用户选择比原始级别低的敏感度级别时提示用户提供相应原因的选项。
    
    - 用于自动标记电子邮件的选项（基于电子邮件附件）。
    
    - 为用户提供自定义帮助链接的选项。

Azure 信息保护附带[默认策略](configure-policy-default.md)，其中包含五个主要标签。 这些标签可用于组织常规创建和存储的数据，包括从最低等级的个人数据到最高等级的机密数据等各类数据。 

可以使用无更改的默认标签，或者你可以自定义它们，或删除它们，并可以创建新标签。 有关详细信息，请使用下一节中的链接来帮助你找到相关选项以及配置方法。 

当在“Azure 信息保护”边栏选项卡上进行任何更改时，请单击“**保存**”以保存更改，或者单击“**放弃**”以返回到上一个保存的设置。 

在完成所需更改后，单击“**发布**”。 

每当受支持的 Office 应用程序启动时，Azure 信息保护客户端都会检查是否有任何变化，并根据最新的 Azure 信息保护策略下载这些更改。 在客户端上刷新策略的其他触发器：

- 右键单击以分类和保护文件或文件夹。

- 运行 [PowerShell cmdlet](../rms-client/client-admin-guide-powershell.md) 以实现标签设置和保护（Get-AIPFileStatus、Set-AIPFileClassification 和 Set-AIPFileLabel）。

- 每 24 小时一次。

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
