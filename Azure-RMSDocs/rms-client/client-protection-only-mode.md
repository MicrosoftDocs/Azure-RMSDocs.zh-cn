---
title: "Azure 信息保护客户端的仅保护模式"
description: "此信息适用于以仅保护模式运行 Azure 信息保护客户端的用户。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ffed64826982756072456be18cced0226b6bb6cc
ms.openlocfilehash: bc81b8587e999e6cbb036942e1c5d37e1e2b319b


---

# <a name="protection-only-mode-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的仅保护模式

不使用 Azure 信息保护策略运行 Azure 信息保护客户端时，它将显示为处于“仅保护”模式。 例如，使用 Windows 文件资源管理器时，右键单击“分类和保护”：

![仅保护模式](../media/protection-only-mode.png)

 此模式将在以下情况下运行：

- 你的组织未订阅 Azure 信息保护（用于数据的分类和保护），但是订阅了 Azure 权限管理服务（用于通过 Office 365 保护数据）。 
    - 这是受支持的方案，你可以使用 Azure 信息保护客户端保护文件和查看受保护的文件。

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



<!--HONumber=Feb17_HO2-->


