---
title: "快速入门教程步骤 3 - AIP"
description: "快速试用 Azure 信息保护入门教程步骤 3 - 安装客户端。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
ms.openlocfilehash: 0edde6cb304a4ad6b34d53ee798a5fbf7ede3b48
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="step-3-install-the-client"></a>步骤 3：安装客户端

>*适用于：Azure 信息保护*

在该步骤中，你将安装 Azure 信息保护客户端，因此刚配置的策略将下载到 Windows PC 上，并在 Office 应用中显示标签。


## <a name="install-the-azure-information-protection-client"></a>安装 Azure 信息保护客户端

1. 在已安装 Office 的 PC 上（当前未打开 Word），从 Microsoft 下载中心[下载 Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 

2. 运行 **AzInfoProtection.exe** 并按照提示安装客户端。

    在本教程中，无论是否选择安装演示策略都没有关系，因为将从 Azure 下载刚配置的策略，如果安装了演示策略，则将替换它。 但是，如果只想体验默认标签而无需连接到 Azure 信息保护，则可以使用演示策略选项。 

## <a name="verify-the-installation"></a>验证安装

通过打开 Word 和新的空白文档（此时不保存）验证安装是否成功。 如果提示你输入用户名和密码，请输入你的全局管理员帐户的详细信息。 

如果这是你第一次安装客户端，则会看到包含基本说明的“祝贺你”页面。 阅读完毕后，请点击“关闭”。

当文档加载后，你会看到两个新组件：

![Azure 信息保护快速入门教程步骤 3 - 已安装客户端](../media/word2016-calloutsv2.png)

- 在“主页”选项卡上，有一个新的**保护**组，其中有一个名为“保护”的按钮。

    依次单击“**保护**” > “**帮助和反馈**”，然后在“**Microsoft Azure 信息保护**”对话框中，确认客户端状态。 它应显示“连接为”和你的用户名。 此外，还应该看到上次连接的最近时间和日期以及信息保护策略的安装时间。 验证对于租户显示的用户名是否正确。

- 功能区下方有一个新栏：信息保护栏。 该栏的标题显示为“敏感级别”，以及为“常规”配置的默认标签。 

你现在已准备好查看运行中的 Azure 信息保护。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于安装 Azure 信息保护客户端|[下载并安装 Azure 信息保护客户端](../rms-client/install-client-app.md)|
|Azure 信息保护客户端的管理员说明|[Azure 信息保护客户端管理员指南](../rms-client/client-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; 步骤 2](infoprotect-tutorial-step2.md)
[步骤 4 &#187;](infoprotect-tutorial-step4.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]