---
title: "Azure 信息保护的仅保护模式"
description: "此信息适用于以仅保护模式运行 Azure 信息保护客户端的用户。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 51dcca7823321defba2ffe45cde3e544ea16662a
ms.sourcegitcommit: 832d3ef5f9c41d6adb18a8cf5304f6048cc7252e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2017
---
# <a name="user-guide-protection-only-mode-for-the-azure-information-protection-client"></a>用户指南：Azure 信息保护客户端的仅保护模式

当 Azure 信息保护客户端没有用于对文档和电子邮件进行分类的标签，它将在仅保护模式下运行。 例如，在此模式中，当使用 Windows 文件资源管理器，右键单击“分类和保护”，可能会看到以下项：

![仅保护模式](../media/protection-only-mode.png)

仅保护模式将在以下情况下运行：

- 贵组织未订阅包含分类和标签功能的 Azure 信息保护，但是订阅了包含使用 Azure 权限管理服务进行数据保护的 Office 365。 
    
    - 可以使用 Azure 信息保护客户端保护文件和查看受保护的文件。 无法对文档和电子邮件进行分类或添加标签。

- 贵组织仅为部分用户订阅了 Azure 信息保护：
    
    - 对于此组合订阅，管理员有责任确保仅部分用户可以使用分类和标签功能。 其余用户应在仅保护模式下运行 Azure 信息保护客户端。 

- 你的组织已订阅 Azure 信息保护，但是你无法下载 Azure 信息保护策略。 
    
    - 这可能是因为配置不正确，也可能因为你没有成功登录。 请联系技术支持或管理员，但在此期间，你可以使用 Azure 信息保护客户端保护文件和查看受保护的文件。

## <a name="limitations-for-protection-only-mode"></a>仅保护模式的限制

- 在 Office 应用程序中，Azure 信息保护栏将不显示。 单击“保护” > “显示栏”时，此菜单选项将不可用。

- 在文件资源管理器中使用“分类和保护 - Azure 信息保护”对话框时，不会看到分类标签。 相反，如上图所示，你将看到一个用于选择 Rights Management (RMS) 模板的选项。 

## <a name="supported-tasks-for-protection-only-mode"></a>仅保护模式支持的任务

- 通过使用 Office 信息权限管理 (IRM) 功能，保护（和取消保护）Office 应用程序中的文档和电子邮件：例如，单击“文件” > “信息” > “保护文档” > “限制访问”。 有关详细信息，请参阅[在 Office 365、Office 2016 或 Office 2013 中使用信息保护](../deploy-use/help-users.md)。

- 通过使用 Windows 文件资源管理器保护（和取消保护）文件：右键单击单个文件、多个文件或文件夹 >“分类和保护”。 若要应用管理员已配置的保护，请在“分类和保护 - Azure 信息保护”对话框中，单击“选择模版”，然后选择任一可用模板。

- 通过使用 Azure 信息保护查看器查看受保护的文件。

- 从 Office 应用程序访问文档跟踪站点。 但是，必须具有用于跟踪和撤销来自此站点的文档的有效订阅。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
