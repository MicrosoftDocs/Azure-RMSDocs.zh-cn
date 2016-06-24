---
# required metadata

title: 监视 Azure Rights Management 连接器 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 监视 Azure Rights Management 连接器

*适用于：Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

安装并配置 RMS 连接器后，你可以使用以下方法和信息以帮助你监视连接器和 Azure RMS 组织的使用。

## 应用程序事件日志条目

RMS 连接器使用应用程序事件日志来记录 “Microsoft RMS 连接器”的条目。 

例如，信息事件 ID 1000 确认连接器服务已启动，ID 1002 确认服务器成功连接到 RMS 连接器，ID 1004 确认每次已授权的帐户列表（列出每个帐户）被下载到连接器。 

如果你还未将连接器配置为使用 HTTP，你应该会看到一个警告 ID 2002：客户正在使用不安全的 (HTTP) 连接。

如果连接器无法连接到 Azure RMS，你将很有可能看到错误 3001。 例如，这可能是 DNS 问题或一个或多个运行 RMS 连接器的服务器缺少 Internet 访问的结果。 

> [!TIP] RMS 连接器服务器无法连接到 Aure RMS 通常是由 Web 代理配置引起的。

对于所有事件日志条目，进一步查看消息以了解更多详细信息。

除了在首次部署连接器时检查事件日志以外，还应持续检查警告和错误。 例如，连接器可能最初按预期方式工作，但是其他管理员可能会更改从属配置。 例如，另一个管理员更改了 Web 代理服务器配置以使 RMS 连接器服务器不能再访问 Internet（错误 3001）或从你指定为已授权使用连接器的组中删除计算机帐户（错误 2001）。

## 性能计数器

当你安装 RMS 连接器时，它将自动创建 “Microsoft Rights Management 连接器”性能计数器，你可能会发现这很有用，可以帮助你监视通过连接器使用 Azure RMS 的性能。 

例如，如果保护文档或电子邮件时，或打开受保护的文档或电子邮件时定时经历延迟，性能计数器可以帮助你确定该延迟是由连接器上的处理时间、来自 Azure RMS 的处理时间还是网络延迟所引起的。 若要帮助你识别出现延迟的位置，请查找包含“连接器处理时间”、“服务响应时间”和“连接器响应时间”的平均计数的计数器。 例如：“授权成功批处理请求平均连接器响应时间”。

如果你最近添加了新的服务器帐户以使用连接器，你可以检查计数器“上次授权策略更新后的时间”来确认在你对其更新后，连接器已经下载了列表，或者你是否需要等待稍长的时间（最多 15 分钟）。

## RMS 分析工具

你可以使用 Rights Management Services 分析工具来帮助你监视连接器的运行状况并确定配置问题。

如果你尚未下载该工具，可以从[下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=46437)进行下载，然后在任何可以访问 Internet 和可以连接到 RMS 连接器的计算机上安装该工具。 运行该工具，在“欢迎”页面上，选择“Azure RMS 连接器”选项。

有关其他信息和说明，请参阅下载页面上的“详细信息”和“安装说明”。

## Logging

使用情况日志记录可帮助你识别电子邮件和文档何时受到保护以及何时使用。 通过使用 RMS 连接器完成此操作后，日志中的用户 ID 字段包含安装 RMS 连接器时自动生成的服务主体名称。

有关详细信息，请参阅[记录和分析 Azure Rights Management 使用情况](log-analyze-usage.md)。

如果你需要有关诊断用途的更详细的日志记录，可以使用 Windows Sysinternals 的 [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277)，并通过修改 ISS 中默认网站的 web.config 文件来启用 RMS 连接器的跟踪。 为此，请执行以下操作：

1. 在“%programfiles%\Microsoft Rights Management connector\Web Service”中找到 web.config 文件。

2. 找到以下行：

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. 使用以下内容来替换该行：

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  停止和启动 IIS 以激活跟踪。 

5.  当你捕获了所需的跟踪时，还原步骤 3 的行，并再次停止和启动 IIS。



<!--HONumber=Jun16_HO2-->


