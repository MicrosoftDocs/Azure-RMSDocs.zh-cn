---
title: "安装 Azure 信息保护客户端 | Azure 信息保护"
description: "有关安装客户端（将信息保护栏添加到 Office 应用程序）以便为文档和电子邮件选择分类标签的说明。"
manager: mbaldwin
ms.date: 09/13/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 2ecdfe905694b3d14727abdb5e6176d24f675d2e
ms.openlocfilehash: cd6684dd25a721272c073fcc972724a6b81c0c72


---

# 安装 Azure 信息保护客户端

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

若要使用 Azure 信息保护对文档和电子邮件进行分类，必须首先安装 Azure 信息保护客户端。 此安装将信息保护栏添加到 Office 应用程序（Word、Excel、PowerPoint、Outlook）以显示组织的分类标签，而且“**主页**”选项卡（Word、Excel、PowerPoint）上的新“**保护**”组具有名为“**保护**”的按钮：

下图显示了此信息保护栏和 [默认策略](configure-policy-default.md)(#默认策略) 中的标签：

![具有默认策略的 Azure 信息保护栏](../media/info-protect-bar-default.png)

从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)(#microsoft-下载中心) 下载 Azure 信息保护客户端。

安装客户端之前，请检查你具有所需的操作系统版本和应用程序：[Azure 信息保护要求](requirements-azure-infoprotect.md)(#azure-信息保护要求)。


## 手动安装 Azure 信息保护客户端

1. [下载客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)后，运行 **AzInfoProtection.exe** 并按照提示安装客户端。 此安装需要本地管理权限。

    如果无法连接到 Office 365 或 Azure Active Directory，但想要通过使用本地策略看到和体验 Azure 信息保护的客户端以用于演示目的，选择此选项以安装演示策略。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。 

2. 开始使用 Azure 信息保护客户端：如果计算机运行 Office 2010，请重新启动计算机。 对于其他版本的 Office，重新启动任何 Office 应用程序。

## 为用户安装 Azure 信息保护客户端

- 可以编写脚本，并通过使用命令行选项自动安装 Azure 信息保护客户端。 若要查看安装选项，请运行 `AzInfoProtection.exe /help`。

    例如，若要以无提示方式安装客户端，请执行以下操作： `AzInfoProtection.exe /passive | quiet`


## 卸载 Azure 信息保护客户端

可以使用以下任何选项：

- 使用控制面板卸载程序：单击“**Microsoft Azure 信息保护** > **卸载**”

- 重新运行 **AzInfoProtection.exe**，并从“修改安装程序”页上，单击“卸载”。 

- “运行” `AzInfoProtection.exe /uninstall`


## 验证安装、连接状态或报告问题

1. 打开 Office 应用程序，在“**主页**”选项卡的“**保护**”组中单击“**保护**”，然后单击“**帮助和反馈**”。

2. 在“**Microsoft Azure 信息保护**”对话框中，注意以下各项：

    - “**最后连接**”值，该值标识客户端最后一次连接到组织的 Azure 信息保护服务的时间。 当客户端连接到该服务时，如果它发现其当前策略中存在更改，它会自动下载最新的策略。 如果在显示时间后完成策略更改，关闭并重新打开 Office 应用程序。

    - 可标识帐户的所显示的用户名，用于针对 Azure 信息保护进行身份验证。 此用户名必须与用于 Office 365 或 Azure Active Directory 的帐户匹配。

    - Azure 信息保护客户端的版本。

    - “**发送反馈**”链接，可用于自动将客户端日志附加到电子邮件以发送到信息保护团队进行调查。

    - “**运行诊断**”链接：当前未实施此功能。

## Azure 信息保护栏的键盘快捷方式

若要使用键盘快捷方式访问 Azure 信息保护栏，请使用以下组合键：

- 按 **Ctrl** + **Shift** + **~** 

然后，使用 Tab 键选择标签和保护栏上的其他控件（“隐藏标签”图标和“删除标签”图标），按 Enter 键以将其选中。


## 文件位置

客户端文件：   

- 对于 64 位操作系统：**\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统：**\Program Files\Microsoft Azure Information Protection**

客户端日志文件和当前安装的策略文件：

- 对于 64 位和 32 位操作系统：**%localappdata%\Microsoft\MSIP**


## 后续步骤

若要更改信息保护栏上的标签，必须配置 Azure 信息保护策略。 有关详细信息，请参阅 [配置 Azure 信息保护策略](configure-policy.md)(#配置-azure-信息保护策略)。

有关如何自定义默认策略并在 Office 应用程序是查看所产生行为的示例，请尝试 [Azure 信息保护快速入门教程](infoprotect-quick-start-tutorial.md)(#azure-信息保护快速入门教程)。 



<!--HONumber=Sep16_HO2-->


