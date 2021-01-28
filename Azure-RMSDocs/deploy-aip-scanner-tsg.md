---
title: 排查本地扫描器部署问题
description: 有关排查统一标签本地扫描程序部署问题的说明
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/26/2021
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 46a994c5191e82d68f318e4900e0a5d45c1e176b
ms.sourcegitcommit: 3136ce04e185b93503585466b7ab4b5bb1df6827
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "98958068"
---
# <a name="troubleshooting-your-unified-labeling-on-premises-scanner-deployment"></a>排查您的统一标签本地扫描器部署问题

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***相关** 内容： [仅限 AIP 统一标签客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 *

使用本文中的内容来帮助你解决本地扫描程序部署问题。

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>使用扫描仪诊断工具进行故障排除

如果 Azure 信息扫描程序出现问题，请使用 [AIPScannerDiagnostics](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics) PowerShell 命令验证部署是否正常：

```powershell
Start-AIPScannerDiagnostics
```

诊断工具会检查以下详细信息，然后导出包含结果的日志文件：

- 数据库是否是最新的
- 网络 Url 是否可访问
- 是否存在有效的身份验证令牌和是否可以获取策略
- 配置文件是否在 Azure 门户中定义
- 脱机/联机配置是否存在并可获取
- 配置的规则是否有效

> [!TIP]
> 如果在不是扫描仪用户的用户下运行命令，请确保添加 **-OnBehalf** 参数。 
>

> [!NOTE]
> **AIPScannerDiagnostics** 命令不会运行完整的先决条件检查。 如果扫描程序出现问题，还请确保系统符合 [扫描器要求](deploy-aip-scanner-prereqs.md)，并确保 [扫描仪配置和安装](deploy-aip-scanner-configure-install.md) 已完成。
>

## <a name="troubleshooting-a-scan-that-timed-out"></a>排查超时的扫描问题

如果扫描程序意外停止并且未完成扫描存储库中的大量文件，则可能需要修改下列设置之一：

- **动态端口数**。 可能需要增加承载文件的操作系统的动态端口数。 SharePoint 的服务器强化可能是导致扫描程序超出允许的网络连接数并因此停止的一个原因。

    有关如何查看当前端口范围并增加范围的详细信息，请参阅 [可修改的设置以提高网络性能](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)。

- **列表视图阈值**。 对于大型 SharePoint 场，可能需要增加列表视图阈值。 默认情况下，列表视图阈值设置为 **5000**。

    有关详细信息，请参阅 [在 SharePoint 中管理大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。


## <a name="scanner-error-reference"></a>扫描仪错误引用

使用下列部分来了解扫描仪生成的特定错误消息，以及解决此问题的故障排除或解决方案操作：

|错误类型 |疑难解答  |
|---------|---------|
|**身份验证错误**     |  - [身份验证令牌不被接受](#authentication-token-not-accepted) <br>  - [缺少身份验证令牌](#authentication-token-missing)|
|**策略错误数**     |  - [缺少策略](#policy-missing) <br>- [策略不包括任何自动标记条件](#policy-doesnt-include-any-automatic-labeling-condition)      |
|**DB/架构错误**     |  - [数据库错误](#database-errors) <br> - [架构不匹配或已过时](#mismatched-or-outdated-schema)  |
|**其他错误**     |  - [基础连接已关闭](#underlying-connection-was-closed) <br> - [阻塞扫描进程](#stuck-scanner-processes) <br>- [无法连接到远程服务器](#unable-to-connect-to-remote-server) <br>- [发送请求时出错](#error-occurred-while-sending-the-request) <br>- [缺少内容扫描作业或配置文件](#missing-content-scan-job-or-profile) <br>- [未配置存储库](#no-repositories-configured) <br>- [找不到群集](#no-cluster-found)   |
|     |         |


<!--Authentication errors-->

### <a name="authentication-token-not-accepted"></a>身份验证令牌不被接受

**错误消息**

`Microsoft.InformationProtection.Exceptions.AccessDeniedException: The service didn't accept the auth token.`

**解决方案**

如果 [set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 命令失败，请确保在 Azure 门户中正确定义权限。

有关详细信息，请参阅 [创建和配置 set-aipauthentication 的 Azure AD 应用程序](rms-client/clientv2-admin-guide-powershell.md#create-and-configure-azure-ad-applications-for-set-aipauthentication)。

### <a name="authentication-token-missing"></a>缺少身份验证令牌

**错误消息**

下列类型作之一：

- `NoAuthTokenException: Client application failed to provide authentication token for HTTP request`

- `Microsoft.InformationProtection.Exceptions.NoAuthTokenException: Client application failed to provide authentication token for HTTP request. Failed with: System.AggregateException: One or more errors occurred. ---> Microsoft.IdentityModel.Clients.ActiveDirectory.AdalException: user_interaction_required: One of two conditions was encountered: 1. The PromptBehavior.Never flag was passed, but the constraint could not be honored, because user interaction was required. 2. An error occurred during a silent web authentication that prevented the http authentication flow from completing in a short enough time frame`

- `Failed to acquire a token using windows integrated authentication (No SSO)`

- 在 Azure 门户的 " **节点** " 页上： `Policy does not include any automatic labeling condition`

**解决方案**

为了使扫描程序以非交互方式运行，必须使用令牌进行身份验证。 

运行 [set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 命令时，请确保代表扫描器用户使用令牌参数。

例如：

```powershell
$pscreds = Get-Credential CONTOSO\scanner
Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
Acquired application access token on behalf of CONTOSO\scanner.
```

有关详细信息，请参阅 [获取扫描仪的 Azure AD 令牌](deploy-aip-scanner-configure-install.md#get-an-azure-ad-token-for-the-scanner)。

<!--Policy errors-->

### <a name="policy-missing"></a>缺少策略

**错误消息**

`Policy is missing`

**说明**

扫描仪找不到你的 Microsoft 信息保护 (MIP) 策略文件。

**解决方案**

若要验证策略文件是否按预期方式出现，请签入以下位置： **% localappdata% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.policies.sqlite3**

有关 MIP 标签和标签策略的详细信息，请参阅 Microsoft 365 文档中的 [创建和配置敏感度标签及其策略](/microsoft-365/compliance/create-sensitivity-labels) 。

### <a name="policy-doesnt-include-any-automatic-labeling-condition"></a>策略不包括任何自动标记条件

**错误**

错误表明标签策略缺少自动标记条件

**解决方案**

验证以下任何或所有问题：

|解决方案  |详细信息  |
|---------|---------|
|**检查内容扫描作业设置**     | 在 Azure 门户中执行以下操作： <br> <br>- [将要 **发现的信息类型** 设置为 **全部**](deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types)  <br>- [定义要在扫描时应用的默认标签](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository)      |
|**检查您的标签策略设置**     |  在标记管理中心（如 Microsoft 365 安全 & 相容性中心）中，执行以下操作： <br> <br>- [定义默认的敏感度标签](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)  <br> - [定义自动/建议标记规则](/microsoft-365/compliance/apply-sensitivity-label-automatically)       |
|**验证策略是否可访问**     | 如果设置按预期方式定义，则可能是策略文件本身丢失或无法访问，如 Microsoft 365 安全性 & 相容性中心出现超时。 <br>  <br>若要验证策略文件，请检查以下文件是否存在： **% localappdata% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.policies.sqlite3**        |
| | |

有关详细信息，请参阅 [什么是 Azure 信息保护统一标记扫描器？](deploy-aip-scanner.md) 和 [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels)。

<!--DB / Schema errors-->

### <a name="database-errors"></a>数据库错误

**错误消息**

`DB error`

**说明**

扫描仪可能无法连接到数据库。

**解决方案**

检查扫描仪计算机和数据库之间的网络连接。 

此外，请确保用于运行扫描程序的服务帐户具有访问数据库所需的任何权限。

### <a name="mismatched-or-outdated-schema"></a>架构不匹配或已过时

**错误消息**

下列类型作之一：

- `SchemaMismatchException`

- 在 Azure 门户的 " **节点** " 页上： `DB schema is not up to date. Run Update-AIPScanner command to update the DB schema` 或 `Error: DB schema is not up to date`

**解决方案**

运行 [install-aipscanner](/powershell/module/azureinformationprotection/Update-AIPScanner) 命令以重新同步你的架构，并确保它是最新的，并且具有最新的更改。


<!--Other errors-->

### <a name="underlying-connection-was-closed"></a>基础连接已关闭

**错误消息**

`System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IO.IOException: Authentication failed because the remote party has closed the transport stream.`

**解决方案**

此错误通常表示未启用 TLS 1.2。

有关详细信息，请参阅 [防火墙和网络基础结构](requirements.md#firewalls-and-network-infrastructure)。 

若要启用 TLS 1.2，请参阅如何在企业移动性 + 安全性文档中 [启用 tls 1.2](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client) 。

### <a name="stuck-scanner-processes"></a>阻塞扫描进程

**错误消息**

扫描仪正在处理的单个文件的时间比预期要长。 进程可能已停滞。

**解决方案**

查看详细报告以查看文件是否仍在增长。 

如果文件继续增长，这意味着扫描器仍在处理数据，并且您必须等待完成。

但是，如果该文件不再增长，请执行以下操作：

1. 执行下列一种或两种操作：

    - 运行 [AIPScannerDiagnostics](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics) cmdlet，对扫描仪运行诊断检查，并导出和 zip 日志文件以查找找到的任何错误。
    - 运行 [AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) cmdlet 以从 **%localappdata%\Microsoft\MSIP\Logs** 目录中导出和压缩日志文件。

1. 为 POLICY.MSIP Scanner 服务创建转储文件。 在 Windows 任务管理器中，右键单击 **Policy.msip 扫描器服务**，然后选择 " **创建转储文件**"。

1. 在 Azure 门户中，停止扫描。 

1. 在扫描仪计算机上，重新启动该服务。

1. 打开支持票证，并将转储文件附加到扫描程序进程。

有关详细信息，请参阅 [对超时的扫描进行故障排除](#troubleshooting-a-scan-that-timed-out)。 

### <a name="unable-to-connect-to-remote-server"></a>无法连接到远程服务器

**错误**

在 **% *localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog** 文件中，`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`    

> [!NOTE]
> 如果有多个日志，则压缩此文件。

**说明**

扫描仪超出了允许的网络连接数。

**解决方案**

增加承载文件的操作系统的动态端口数。

有关如何查看当前端口范围并增加范围的详细信息，请参阅 [可修改的设置以提高网络性能](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)。


另请参阅： [排查超时的扫描问题](#troubleshooting-a-scan-that-timed-out)。
### <a name="error-occurred-while-sending-the-request"></a>发送请求时出错

**错误消息**

`[System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IO.IOException: Unable to read data from the transport connection: An existing connection was forcibly closed by the remote host. ---> System.Net.Sockets.SocketException: An existing connection was forcibly closed by the remote host`

**解决方案**

此错误通常表示未启用 TLS 1.2。

有关详细信息，请参阅 [防火墙和网络基础结构](requirements.md#firewalls-and-network-infrastructure)。 

若要启用 TLS 1.2，请参阅如何在企业移动性 + 安全性文档中 [启用 tls 1.2](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client) 。


### <a name="missing-content-scan-job-or-profile"></a>缺少内容扫描作业或配置文件

**错误**

错误表明无法找到内容扫描作业或配置文件。

例如，" **节点** " 页上的 "Azure 门户中出现以下错误： `No content scan job found`

**解决方案**

在 Azure 门户中检查扫描程序配置。

有关详细信息，请参阅 [配置和安装 Azure 信息保护统一标记扫描器](deploy-aip-scanner-configure-install.md)。 

> [!NOTE]
> *配置文件* 是旧扫描程序术语，在较新版本的扫描程序中已被扫描程序群集和内容扫描作业替换。
> 
### <a name="no-repositories-configured"></a>未配置存储库

**错误消息**

在 Azure 门户的 " **节点** " 页上： `No repositories are configured`

**说明**

可能有一个内容扫描作业未配置存储库。 

**解决方案**

请检查你的内容扫描作业设置，并至少添加一个存储库。 

有关详细信息，请参阅 [创建内容扫描作业](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)。

### <a name="no-cluster-found"></a>找不到群集

**错误消息**

在 Azure 门户的 " **节点** " 页上： `No cluster found`

**说明**

找不到已定义的其中一个扫描仪群集的实际匹配项。

**解决方案**

验证群集配置，并根据自己的系统详细信息检查是否有打字和错误。

有关详细信息，请参阅 [创建扫描仪群集](deploy-aip-scanner-configure-install.md#create-a-scanner-cluster)。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅我们的博客，了解 [有关部署和使用 AIP UL 扫描器的最佳实践](https://techcommunity.microsoft.com/t5/microsoft-security-and/best-practices-for-deploying-and-using-the-aip-ul-scanner/ba-p/1878168)。