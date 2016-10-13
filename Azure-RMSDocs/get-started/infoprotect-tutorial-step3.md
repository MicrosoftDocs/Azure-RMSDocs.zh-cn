---
title: "快速入门教程步骤 3 | Azure 信息保护"
description: "入门教程第 3 步，该教程用于快速试用适合你组织的 Microsoft Azure 信息保护，所需时间大概 30 分钟。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: b5c87669c965d1e67b47dcfbd8ba97f1da41d104
ms.openlocfilehash: 042e168452d2b5cbc1eeec4fc06a3b0f137a5caf


---

# 步骤 3：安装客户端和应用程序 

>*适用于：Azure 信息保护*

在该步骤中，你将首先安装 Azure 信息保护客户端，因此刚配置的策略将下载到 Windows PC 上，并在 Office 应用中显示标签。

其次，你将安装 Rights Management 共享应用程序，以便可以安全地通过电子邮件共享文档，然后跟踪其使用情况。 

这两个安装都可与 Office 应用程序集成，当前你必须单独安装它们。


## 安装 Azure 信息保护客户端

1. 在已安装 Office 的 PC 上（当前未打开 Word），从 Microsoft 下载中心[下载 Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 

2. 运行 **AzInfoProtection.exe** 并按照提示安装客户端。

    在本教程中，无论是否选择安装演示策略都没有关系，因为将从 Azure 下载刚配置的策略，如果安装了演示策略，则将替换它。 但是，如果只想体验默认标签而无需连接到 Azure 信息保护，则可以使用演示策略选项。 

## 安装权限管理共享应用程序 

1. 转到 Microsoft 网站上的 [Microsoft 权限管理](http://go.microsoft.com/fwlink/?LinkId=303970) 页。

2. 在 **“计算机”** 部分，单击 **“适用于 Windows 的 RMS 应用程序”** 图标，然后保存用于安装 Microsoft 权限管理共享应用程序的 **Setup.exe** 文件。

3. 在 **“安装 Microsoft RMS”** 页上，单击 **“下一步”**，然后等待安装完成。 然后单击“重新启动”（如果系统提示你重新启动计算机），或单击“关闭”完成安装。


## 验证安装

通过打开 Word 和新的空白文档（此时不保存）验证这些安装是否成功。 如果提示你输入用户名和密码，请输入你的全局管理员帐户的详细信息。 

当文档加载后，你应看到三个新组件：

- 在“主页”选项卡上，有一个新的**保护**组，其中有一个标记为“保护”的按钮。

    单击“保护” > “帮助和反馈”，然后在“Microsoft Azure 信息保护”对话框中，确认客户端状态。 应显示“已安装信息保护策略”和最新的连接时间。 验证对于租户显示的用户名是否正确。

- 在“主页”选项卡上，还有一个新的“RMS”组，其中有一个标记为“共享保护项”的按钮。

- 功能区下方有一个新栏：信息保护栏。 该栏的标题显示为“敏感度”，默认标签为我们配置的“供内部使用”。 
    
    ![Azure 信息保护快速入门教程步骤 3 - 已安装客户端](../media/word2013-callouts2.png)

你现在已准备好查看运行中的 Azure 信息保护。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于安装 Azure 信息保护客户端|[安装 Azure 信息保护客户端](../rms-client/info-protect-client.md)|
|关于安装 Rights Management 共享应用程序和用户说明|[权限管理共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)|
|关于适用于 Windows 的 Rights Management 共享应用程序的脚本化安装以及更多技术信息|[保护级别 – 本机和常规](../rms-client/sharing-app-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; 步骤 2](infoprotect-tutorial-step2.md)
[步骤 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Sep16_HO4-->


