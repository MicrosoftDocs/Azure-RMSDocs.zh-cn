---
title: 监视 Rights Management 连接器 - AIP
description: 帮助监视连接器和组织使用 Azure 信息保护中 Azure Rights Management 服务的信息。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8fc380b5d015ec055961b815117a0b5450c3661b
ms.sourcegitcommit: 373e05ff0c411d29cc5b61c36edaf5a203becc14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="monitor-the-azure-rights-management-connector"></a>监视 Azure Rights Management 连接器

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

安装并配置 RMS 连接器后，可以使用以下方法和信息，从而监视连接器和组织使用 Azure 信息保护中 Azure Rights Management 服务的情况。

## <a name="application-event-log-entries"></a>应用程序事件日志条目

RMS 连接器使用应用程序事件日志来记录 “Microsoft RMS 连接器”的条目。 

例如，信息事件如下所示：

- ID 1000：用于确认连接器服务是否已启动

- ID 1002：当服务器成功连接到 RMS 连接器

- ID 1004：每当授权帐户列表（列出所有帐户）下载到连接器时 

如果你还未将连接器配置为使用 HTTP，你应该会看到一个警告 ID 2002：客户正在使用不安全的 (HTTP) 连接。

如果连接器无法连接到 Azure Rights Management 服务，最有可能看到错误 3001。 例如，导致此连接故障发生的原因可能是 DNS 问题，或一个或多个运行 RMS 连接器的服务器无法连接 Internet。 

> [!TIP]
> RMS 连接器服务器无法连接到 Azure Rights Management 服务，通常是由 Web 代理配置引起的。

与所有事件日志条目一样，进一步查看消息，了解更多详细信息。

除了在首次部署连接器时检查事件日志以外，还应持续检查警告和错误。 连接器最初可能正常运行，但其他管理员可能会更改从属配置。 例如，另一个管理员更改了 Web 代理服务器配置以使 RMS 连接器服务器不能再访问 Internet（错误 3001）或从你指定为已授权使用连接器的组中删除计算机帐户（错误 2001）。

### <a name="event-log-ids-and-descriptions"></a>事件日志 ID 和说明

通过以下各节来识别可能的事件 ID、说明和任何附加信息。

-----

信息 **1000**

**Microsoft RMS 连接器 Web 服务已启动。**

当 RMS 连接器首次尝试启动时，将记录此事件。

----

信息 **1001**

**Microsoft RMS 连接器 Web 服务已停止。**

当 RMS 连接器因正常操作而停止时，将记录此事件。 例如，重新启动 IIS 或关闭计算机。 

----

信息 **1002**

**已允许授权服务器访问 Microsoft RMS 连接器。**

当本地服务器中的帐户首次连接到 RMS 连接器，而该帐户在 RMS 连接器管理员工具中由 Azure RMS 管理员授权之后，将记录此事件。 事件消息将包含 SID、帐户名称和建立连接的计算机名称。

----

信息 **1003**

**来自下列客户端的连接已从非安全 (HTTP) 连接切换为安全 (HTTPS) 连接。**

当本地服务器将其与 RMS 连接器的连接从 HTTP（安全级别较低）更改为 HTTPS（安全级别较高）时，将记录此事件。 事件消息将包含 SID、帐户名称和建立连接的计算机名称。

----

信息 **1004**

**已更新授权帐户列表。**

当 RMS 连接器下载了有权使用 RMS 连接器的帐户的最新列表（现有帐户及任何更改）时，将记录此事件。 此列表每 15 分钟下载一次，前提是 RMS 连接器可以与 Azure Rights Management 服务通信。

----

警告 **2000**

**HTTP 上下文中的用户主体丢失或无效，请验证 Microsoft RMS 连接器网站是否在 IIS 中禁用了匿名身份验证，而只启用了 Windows 身份验证。**

当 RMS 连接器无法唯一地标识尝试连接到 RMS 连接器的帐户时，将记录此事件。 这可能是由于为 IIS 错误地配置了匿名身份验证或者帐户来自不受信任的林。

----

警告 **2001**

**试图对 Microsoft RMS 连接器进行未经授权的访问。**

当帐户尝试连接到 RMS 连接器但失败时，将记录此事件。 导致此警告生成的最典型原因是，建立连接的帐户不在 RMS 连接器从 Azure Rights Management 服务下载的授权帐户列表中。 例如，最新列表尚未下载（此事件每 15 分钟发生一次），或在列表中找不到相应帐户。 

另一个原因可能是因为在配置为使用 RMS 连接器的同一服务器上安装了该连接器。 例如，在运行 Exchange Server 的服务器上安装 RMS 连接器，并授权 Exchange 帐户使用该连接器。 由于 RMS 连接器无法正确地标识试图进行连接的帐户，因此不支持此配置。

事件消息包含尝试连接到 RMS 连接器的帐户和计算机的相关信息：

- 如果尝试连接到 RMS 连接器的帐户是有效帐户，则使用 RMS 连接器管理员工具将其添加到授权帐户列表中。 有关必须对哪些帐户授权的详细信息，请参阅[将服务器添加到允许服务器列表](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers)。 

- 如果尝试连接到 RMS 连接器的帐户来自与 RMS 连接器服务器相同的计算机，请在单独的服务器上安装连接器。 有关连接器必备组件的详细信息，请参阅 [RMS 连接器的必备组件]( deploy-rms-connector.md#prerequisites-for-the-rms-connector)。

----

警告 **2002**

**来自下列客户端的连接正在使用非安全 (HTTP) 连接。**

当本地服务器成功连接到 RMS 连接器，但连接使用 HTTP（安全级别较低），而不是 HTTPS （安全级别较高）时，将记录此事件。 每个帐户（而非每个连接）记录一个事件。 如果帐户成功地切换为使用 HTTPS，但又还原为 HTTP，则将再次触发此事件。

事件消息包含帐户 SID、帐户名称和连接到 RMS 连接器的计算机名称。

有关如何将 RMS 连接器配置为使用 HTTPS 连接的信息，请参阅[将 RMS 连接器配置为使用 HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)。

----

警告 **2003**

**授权列表为空。在填充连接器的授权用户和组列表之前，服务将不可用。**

当 RMS 连接器没有授权帐户列表，从而导致任何本地服务器都无法连接到它时，将记录此事件。 RMS 连接器从 Azure RMS 每 15 分钟下载一次列表。 

若要指定帐户，请使用 RMS 连接器管理员工具。 有关详细信息，请参阅[授权服务器使用 RMS 连接器]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)。 

----

错误 **3000**

**Microsoft RMS 连接器中发生未经处理的异常。**

每次 RMS 连接器遇到意外错误时都将记录此事件，且错误详细信息包含在事件消息中。

事件消息中的文本“请求失败，出现了空响应”可识别一个可能的原因。 如果你看到此文本，则可能是因为你有一个网络设备在对本地服务器与 RMS 连接器服务器之间的数据包进行 SSL 检查。 Azure Rights Management 服务不支持此配置，导致通信失败，并生成此事件日志消息。

----

错误 **3001**

**下载授权信息时出现异常。**

如果 RMS 连接器无法下载有权使用 RMS 连接器的帐户的最新列表，将记录此事件。 事件消息中列出了错误详细信息。



----

## <a name="performance-counters"></a>性能计数器

安装 RMS 连接器后，它将自动创建 Microsoft Rights Management 连接器性能计数器，有助于监视并改进使用 Azure Rights Management 服务的性能。 

例如，当文档或电子邮件受到保护时，经常会经历延迟。 或者，当打开受保护文档或电子邮件时，也会经历延迟。 对于这些情况，性能计数器有助于确定延迟是由于连接器处理时间、Azure Rights Management 服务处理时间还是网络延迟所致。 

若要帮助你识别出现延迟的位置，请查找包含“连接器处理时间”、“服务响应时间”和“连接器响应时间”的平均计数的计数器。 例如：“授权成功批处理请求平均连接器响应时间”。

如果你最近添加了新的服务器帐户以使用连接器，你可以检查计数器“上次授权策略更新后的时间”来确认在你对其更新后，连接器已经下载了列表，或者你是否需要等待稍长的时间（最多 15 分钟）。

## <a name="logging"></a>Logging

使用情况日志记录可帮助你识别电子邮件和文档何时受到保护以及何时使用。 当 RMS 连接器用于保护和使用内容时，日志中的用户 ID 字段包含 Aadrm_S-1-7-0 的服务主体名称。 此名称是自动为 RMS 连接器创建。

有关使用情况日志记录的详细信息，请参阅[记录和分析 Azure 权限管理服务的使用情况](log-analyze-usage.md)。

如果需要更详细的日志记录以供诊断使用，可以使用 Windows Sysinternals 中的 [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277)。 在 IIS 中修改默认网站的 web.config 文件，启用对 RMS 连接器的跟踪：

1. 在“%programfiles%\Microsoft Rights Management connector\Web Service”中找到 web.config 文件。

2. 找到以下行：

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. 将上一行代码替换为以下文本：

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  停止和启动 IIS 以激活跟踪。 

5.  当你捕获了所需的跟踪时，还原步骤 3 的行，并再次停止和启动 IIS。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
