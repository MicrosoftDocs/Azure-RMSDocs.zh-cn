---
title: "Azure 信息保护快速入门教程 - 步骤 3 | Azure 权限管理"
description: "入门教程第 3 步，该教程用于快速试用适合你组织的 Microsoft Azure 信息保护，只需 4 个步骤，所需时间不到 15 分钟。"
author: cabailey
manager: mbaldwin
ms.date: 07/11/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 7f85c673cd1e8055d6a27dcc49b5da18a7e12f98
ms.openlocfilehash: 41ebf56c55d94e9aecf9538d474c8fa2c77ae83e


---

# 步骤 3：安装 Azure 信息保护客户端 

*适用于：Azure 信息保护预览版*

在该步骤中，你将安装 Azure 信息保护客户端，因此刚配置的策略将下载到 Windows PC 上，并在 Office 应用中显示标签。 

1. 在已安装 Office 的 PC 上（当前未打开 Word），从 Microsoft 下载中心[下载 Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 

2. 运行 **AZInfoProtection.exe** 并按照提示安装客户端。

    在本教程中，无论是否选择安装演示策略都没有关系，因为将从 Azure 下载刚配置的策略，如果安装了演示策略，则将替换它。 但是，如果只想体验默认标签而无需连接到 Azure 信息保护，则可以使用演示策略选项。 

3. 通过打开 Word 和新的空白文档（此时不保存）验证是否已安装客户端。 如果提示你输入用户名和密码，请输入你的全局管理员帐户的详细信息。 当文档加载后，你会看到两个新组件：

    - 在“主页”选项卡上，有一个新的**保护**组，其中有一个标记为“保护”的按钮。

        单击“保护” > “帮助和反馈”，然后在“Microsoft Azure 信息保护”对话框中，确认客户端状态。 应显示“已安装信息保护策略”和最新的连接时间。 验证对于租户显示的用户名是否正确。

    - 在功能区下方显示一个新栏：信息保护栏。 该栏的标题显示为“敏感度”，默认标签为我们配置的“供内部使用”。 


![Azure 信息保护快速入门教程步骤 3 - 已安装客户端](../media/word2013-callouts.png)

你可以进行最后一步，以查看分类、设置标签和保护的实际操作。

>[!div class="step-by-step"]
[&#171; 步骤 2](infoprotect-tutorial-step2.md)
[步骤 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Jul16_HO3-->


