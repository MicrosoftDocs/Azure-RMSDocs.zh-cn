---
title: Azure 信息保护经典客户端-版本历史记录 & 支持策略
description: 了解 Azure 信息保护经典客户端版本的新增功能或更改的内容，并了解支持的生命周期策略。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: def8ba403e961f6e64b0bd34eb5c7ac5bd50632a
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807061"
---
# <a name="azure-information-protection-classic-client-version-release-history-and-support-policy"></a>Azure 信息保护经典客户端：版本发行历史记录和支持策略


>***适用于**： Active Directory Rights Management Services， [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，Windows 8，Windows Server 2019，Windows Server 2016，windows Server 2012 R2，windows server 2012 *
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标记客户端，请参阅 [统一标签客户端版本历史记录](unifiedlabelingclient-version-release-history.md)。 *

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

若要部署 AIP 经典客户端，请提交支持票证以获取下载访问权限。

有关详细信息，请参阅[升级和维护 Azure 信息保护客户端](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

在发布新的通用版本 (GA) 前，原有的 Azure 信息保护客户端的支持期限最多为六个月。 除了此部分，文档不包含有关不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>不再支持的常规可用性版本：

|客户端版本|发布日期|
|--------------|-------------|
|1.54.33.0 | 2019/10/23|
|1.53.10|07/15/2019|
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

此页上使用的日期格式为 *月/日/年*。

从6/2/2019 开始，Azure 信息保护的标记服务需要使用 TLS 1.2 的连接。

1.4.21.0 发行的所有客户端版本03/15/2017 支持 TLS 1.2。 客户端版本 **1.3.155.2**、 **1.2.4.0** 和 **1.1.23.0** 不使用 TLS 1.2，因此无法再下载 Azure 信息保护策略。

### <a name="release-history"></a>版本历史记录

使用以下信息可查看受支持版本的 Azure 信息保护适用于 Windows 的 Azure 信息保护客户端的新增功能或更改的内容。 最新版本会最先列出。

所述的 Azure 信息保护功能目前以预览版提供。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 

> [!NOTE]
> 小的修补程序不予列出，因此如果遇到 Azure 信息保护客户端相关问题，建议检查它是否已在最新 GA 版本中得到修复。 如果问题仍然存在，请检查当前预览版本 (（如果有）) 。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

## <a name="version-154590"></a>版本1.54.59。0

**发布** 日期：02/12/2020

此版本仅包含修补程序。 

**修补程序**：

- 解决了在删除保护后，IQP 显示的、 **恢复** 和/或 **另存为** 选项所保护的文件的问题。 

- 许多产品功能工具提示文本经过改进，易于理解。 

- 解决使用受保护的 PDF 文件时的客户端稳定性问题。 

- 如果在电子邮件创建过程中将在电子邮件中删除标签，则现在会按预期删除保护标签。 

## <a name="next-steps"></a>后续步骤

不确定是否安装了正确的客户端？  请参阅 [选择 Windows 标记解决方案](use-client.md#choose-your-windows-labeling-solution)。

有关安装和使用客户端的详细信息： 

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)
