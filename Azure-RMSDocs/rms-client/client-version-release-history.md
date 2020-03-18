---
title: Azure 信息保护客户端-版本历史记录 & 支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能，并了解支持的生命周期策略。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 987e44dcd5d5c690f581fd47a4047b65260b71d9
ms.sourcegitcommit: 8c39347d9b7a120014120860fff89c5616641933
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79482832"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure 信息保护客户端：版本发行历史记录和支持策略


>*适用于： Active Directory Rights Management Services， [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*
>
> *适用于[Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

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
|1.48.204.0|04/16/2019|
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

使用以下信息可查看适用于 Windows 的 Azure 信息保护客户端的受支持版本的新增功能或更改内容。 最新版本会最先列出。

> [!NOTE]
> 小的修补程序不予列出，因此如果遇到 Azure 信息保护客户端相关问题，建议检查它是否已在最新 GA 版本中得到修复。 如果问题仍然存在，请检查当前预览版本（如果有）。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

## <a name="version-154590"></a>版本1.54.59。0

**发布**日期：12/02/2020

此版本仅包含修补程序。 

**修补程序**：

- 解决了在删除保护后，IQP 显示的、**恢复**和/或**另存为**选项所保护的文件的问题。 

- 许多产品功能工具提示文本经过改进，易于理解。 

- 解决使用受保护的 PDF 文件时的客户端稳定性问题。 

- 如果在电子邮件创建过程中将在电子邮件中删除标签，则现在会按预期删除保护标签。 

## <a name="version-154330"></a>版本1.54.33。0

**发布**日期：10/23/2019

支持，08/12/2020

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

## <a name="next-steps"></a>后续步骤

不确定是否安装了正确的客户端？  请参阅[选择要用于 Windows 计算机的标记客户端](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)。

有关安装和使用客户端的详细信息： 

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)
