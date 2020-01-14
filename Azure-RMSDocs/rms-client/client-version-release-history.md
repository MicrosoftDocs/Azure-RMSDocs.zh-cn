---
title: Azure 信息保护客户端-版本历史记录 & 支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能，并了解支持的生命周期策略。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/05/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 021919bbc683c47edd778b98a2a5685419515b8e
ms.sourcegitcommit: 2d75192e7cd2e322ab422fc2115aa063e8dda18b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75913345"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure 信息保护客户端：版本发行历史记录和支持策略


>*适用于： Active Directory Rights Management Services， [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012，windows Server 2008 r2*
>
> *适用于[Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*



可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载最新正式版本和当前预览版（若有）。 

在通常几周的短暂延迟后，最新的正式发行版还会包含在 Microsoft 更新目录中，其中产品名称为**Microsoft Azure 信息保护** > **Microsoft Azure 信息保护客户端**和**更新**分类。 此目录包含此内容意味着可利用 WSUS/Configuration Manager 或其他使用 Microsoft 更新的软件部署机制来升级客户端。

有关详细信息，请参阅[升级和维护 Azure 信息保护客户端](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)。

> [!TIP]
> 对使用 Azure 信息保护统一标签客户端感兴趣，因为标签是从 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 符合性中心发布的？ 从 Microsoft 下载中心下载并安装统一标签客户端时，可以将 Azure 信息保护客户端升级到[统一的标签客户端](unifiedlabelingclient-version-release-history.md)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

在发布新的通用版本 (GA) 前，原有的 Azure 信息保护客户端的支持期限最多为六个月。 除了此部分，文档不包含有关不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>不再支持的常规可用性版本：

|客户端版本|发布日期|
|--------------|-------------|
|1.41.51.0|2018 年 11 月 27 日|
|1.37.19.0|2018 年 09 月 17 日|
|1.29.5.0|2018 年 06 月 26 日|
|1.27.48.0|2018 年 05 月 30 日|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|2017/03/15|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|2016/10/27|
|1.1.23.0|10/01/2016|

此页上使用的日期格式为*月/日/年*。

从6/2/2019 开始，Azure 信息保护的标记服务需要使用 TLS 1.2 的连接。

1\.4.21.0 发行的所有客户端版本03/15/2017 支持 TLS 1.2。 客户端版本**1.3.155.2**、 **1.2.4.0**和**1.1.23.0**不使用 TLS 1.2，因此无法再下载 Azure 信息保护策略。

### <a name="release-history"></a>版本历史

请查看以下信息，了解适用于 Windows 的 Azure 信息保护客户端受支持版本的新增功能或更改之处。 最新版本会最先列出。

> [!NOTE]
> 小的修补程序不予列出，因此如果遇到 Azure 信息保护客户端相关问题，建议检查它是否已在最新 GA 版本中得到修复。 如果问题仍然存在，请检查当前预览版本（如果有）。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。


## <a name="version-154330"></a>版本1.54.33。0

**发布**日期：10/23/2019

此版本包括 RMS 客户端的 MSIPC 版本1.0.4008.0813。

此版本提供了一般的稳定性和性能修复。

## <a name="version-153100"></a>版本1.53.10。0

**发布**日期：07/15/2019

支持，04/23/2020

此版本包括 RMS 客户端的 MSIPC 版本1.0.3889.0419。

**新功能：**

- 新的高级客户端设置若要从策略设置 "**所有文档和电子邮件**" 中免除 Outlook 邮件，必须具有标签。 [详细信息](client-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)

- 新的高级客户端设置，用于进一步自定义在 Outlook 中实现弹出消息的设置，警告、调整或阻止发送电子邮件。 使用这一新的高级设置，你可以为不带附件的电子邮件设置不同的操作。 [详细信息](client-admin-guide-customizations.md#to-specify-a-different-action-for-email-messages-without-attachments)

**修补程序**：

- 使用文件资源管理器时，右键单击以标记单独应用了保护的文件，将保留该保护。 例如，用户对文件应用了自定义权限。

- 如果将具有为用户定义的权限配置的标签的电子邮件线程上的 "不转发" 选项替换为 "不转发"，则原始收件人仍可打开电子邮件。

- 在下面的方案中，用户将不再在标签工具提示中看到标签自动设置的内容：用户接收附加了未标记但自动保护的文档的受保护电子邮件。 当发件人来自同一组织的用户打开文档时，保护设置的相应标签将应用到该文档。

- 运行[protect-rmsfile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 的最小[使用权限](../configure-usage-rights.md#usage-rights-and-descriptions)现在为**另存为、导出**（导出），而不是**复制**（提取）。

## <a name="version-1482040"></a>版本1.48.204。0

**发布**日期：04/16/2019

支持，01/15/2020

此版本包括 RMS 客户端的 MSIPC 1.0.3592.627 版本。

**新功能：**

- Azure 信息保护扫描程序现在是从 Azure 门户配置的，而不是使用 PowerShell 进行配置。
    
    如果要从扫描程序的正式发布版本升级，则升级过程与以前的版本不同，因此请务必阅读[升级 Azure 信息保护扫描程序](client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。

- 在指定配置文件名称时，扫描器现在支持同一 SQL server 实例上的多个配置数据库。

- 支持以下有助于识别文档和电子邮件中的凭据的敏感信息类型：
    - Azure 服务总线连接字符串
    - Azure IoT 连接字符串
    - Azure 存储帐户
    - Azure IAAS 数据库连接字符串和 Azure SQL 连接字符串
    - Azure Redis 缓存连接字符串
    - Azure SAS
    - SQL Server 连接字符串
    - Azure DocumentDB 身份验证密钥
    - Azure 发布设置密码
    - Azure 存储帐户密钥（通用）

- 终结点发现支持[Azure 信息保护分析](../reports-aip.md)，用于报告用户首次保存 Office 文档时找到的敏感信息（使用适用于 Word、Excel 和 PowerPoint 的桌面应用程序）：
    - 若要发现此信息，无需标记文档。
    - 敏感信息由预定义的和自定义的信息类型标识。
    - 如果你不希望将敏感信息类型发送到 Azure 信息保护分析，你可以使用[高级客户端设置](client-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)禁用终结点发现。

- 新的高级客户端设置，在 Outlook 中实现弹出消息，可以针对正在发送的电子邮件发出警告、进行验证或阻止。 [详细信息](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    
    请注意，如果为预览版本配置了 OutlookCollaborationTrustedDomains 的 "高级客户端" 属性，则此设置现在将被三个新设置替换，因此，每个操作都可以免除域： OutlookWarnTrustedDomains、OutlookJustifyTrustedDomains 和 OutlookBlockTrustedDomains。

- 如果使用 [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) cmdlet 标记和保护文件，则可以使用 *EnableTracking* 参数将文件注册到文档跟踪站点。 [详细信息](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- 用于[Azure 信息保护分析](../reports-aip.md)的新高级客户端设置，用于在 Azure 门户中选中此复选框，以使用户能够更深入地分析敏感数据，从而防止为一部分用户发送信息类型匹配项。 此设置适用于客户端和扫描仪。 [详细信息](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)

- 仅在将策略设置配置为不显示自定义权限时适用的新高级客户端设置：当存在使用自定义权限保护的文件时，在文件资源管理器中显示 "自定义权限" 选项，以便用户可以查看并更改它们（如果他们有权更改保护设置）。 [详细信息](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)


**修补程序**：

- 当发送操作系统区域设置为英语时，路径和文件名不会在 Azure 信息保护分析中显示问号 (?) 来代替非 ASCII 字符。

- 用户将新部分添加到 Word 文档，然后重新标记文档时，将一致地应用新的视觉标记。

- Azure 信息保护客户端正确地删除对受 Rights Management 共享应用程序保护的 PDF 文档的保护。

- 为用户定义的权限配置父标签时，PowerShell 和扫描程序会正确应用子标签。

- Azure 信息保护客户端正确显示已由[支持统一标签的客户端](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)应用的标签。

- 在文件资源管理器删除保护并右键单击 PowerShell 和扫描程序后，文档在 Office 中正确打开，而没有恢复消息。

- 当使用高级客户端设置设置一个 [Outlook 默认标签](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook)时，可以应用一个具有子标签的父标签，当为用户禁用所有这些子标签时，可使用父标签。

- 当你为带有附件的电子邮件使用[策略设置](../configure-policy-settings.md)时 **，将应用与这些附件的最高分类匹配的标签**，并使用为用户定义的权限配置最高分类的标签，以前的结果是标签已应用到电子邮件，但保护不是。 现在：
    - 如果标签的用户定义权限包括 Outlook （不要转发）：应用该标签，并且它不会将保护转发到电子邮件。
    - 如果标签的用户定义权限仅适用于 Word、Excel、PowerPoint 和文件资源管理器：请不要应用标签，也不要将任何保护应用于电子邮件。

**其他变化：**

- 为建议或自动分类配置的标签[不再支持](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client)以下敏感信息类型：
    - 欧盟电话号码
    - 欧盟 GPS 坐标

- 由于 Azure 信息保护扫描程序从 Azure 门户配置，因此以下 cmdlet 现已弃用，且不能用于配置数据存储库或文件类型列表：
    - Add-AIPScannerRepository
    - Add-AIPScannerScannedFileTypes
    - Get-AIPScannerRepository
    - Remove-AIPScannerRepository
    - Remove-AIPScannerScannedFileTypes
    - Set-AIPScannerRepository
    - Set-AIPScannerScannedFileTypes

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) 是一个新的 PowerShell cmdlet，用于 Azure 信息保护扫描程序无法从 Azure 门户下载其配置的情况。

- 默认情况下，Azure 信息保护扫描程序不再排除 .zip 文件。 若要检查和标记 .zip 文件，请参阅管理员指南的[检查 .zip 文件](client-admin-guide-file-types.md#to-inspect-zip-files)部分。

- [policy setting](../configure-policy-settings.md) **用户必须提供理由以设置较低的分类标签、删除标签或删除保护**不再适用于扫描仪。 当**你在 scanner 配置文件中配置**设置 "重新**标记文件**"，然后选中 "**允许标签降级**" 复选框时，扫描程序会执行这些操作。

## <a name="next-steps"></a>后续步骤

不确定是否安装了正确的客户端？  请参阅[选择要用于 Windows 计算机的标记客户端](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)。

有关安装和使用客户端的详细信息： 

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)
