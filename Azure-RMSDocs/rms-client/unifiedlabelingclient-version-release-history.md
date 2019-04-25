---
title: Azure 信息保护统一标记客户端-版本发行历史记录和支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护统一标签客户端的发布信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 1262a2f1a70002686aed0bad47354cdc5ac23bac
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180879"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure 信息保护统一标记客户端-版本发行历史记录和支持策略

>适用范围：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> *说明：[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


您可以下载 Azure 信息保护统一标记的客户端从[Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

每个公开发行 (GA) 版本的 Azure 信息保护统一标记客户端支持最多六个月发布后的后续 GA 版本。 文档不包括关于不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

> [!NOTE]
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

### <a name="release-information"></a>发布信息

使用以下信息查看正式发布版本的 Azure 信息保护统一标记客户端支持的功能。

此客户端安装 Windows 计算机的 Office 加载项：文件资源管理器的扩展和 PowerShell 模块。 此客户端的[先决条件](../requirements.md)与从 Azure 下载策略的 Azure 信息保护客户端相同。

若要与 Azure 信息保护客户端比较特性和功能，请参阅[客户端功能比较](use-client.md#compare-the-clients)。

## <a name="version-20778"></a>版本 2.0.778

**发布日期**：04/16/2019

第一个公开上市版本的 Windows 的 Azure 信息保护统一标记客户支持以下功能： 

- 从 Azure 信息保护客户端升级。

- 手动、自动和建议标记：有关为此客户端配置自动和建议标签的详细信息，请参阅[将敏感度标签自动应用于内容](/Office365/SecurityCompliance/apply_sensitivity_label_automatically)。

- 文件资源管理器、用于分类和保护文件的右键单击操作、删除保护和应用自定义权限。

- 适用于受保护的文本和图像文件、受保护的 PDF 文件以及一般保护的文件的查看器。

- 用于实现以下目的的 PowerShell 命令：
    - [设置或删除文档上的标签](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [在检查文档内容后标记文档](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [读取应用于文档的标签信息](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [进行身份验证以支持无人参与的 PowerShell 会话](/powershell/module/azureinformationprotection/set-aipauthentication)

- 审核对中心报表使用的数据和终结点发现支持[Azure 信息保护分析](../reports-aip.md)。

- 以下标签和策略设置：
    - 视觉标记（页眉、页脚、水印）
    - 默认标签
    - 应用“不要转发”且仅在 Outlook 中显示的标签
    - 用户降低分类级别或删除标签的理由提示
    - 标签的颜色

- 管理中心中的策略刷新：
    - 在 Office 应用程序每次启动时刷新，每 4 小时刷新一次
    - 在右键单击以分类和保护文件或文件夹时刷新
    - 在运行 PowerShell cmdlet 以实现标记和保护时刷新

- “帮助和反馈”对话框，其中包括重置设置和导出日志。


## <a name="next-steps"></a>后续步骤

有关完整的详细信息，请参阅[比较表](use-client.md#compare-the-clients)。

有关如何安装和使用此客户端的详细信息： 

- 面向用户：[下载并安装客户端](install-unifiedlabelingclient-app.md)

- 面向管理员：[Azure 信息保护统一标记的客户端管理员指南](clientv2-admin-guide.md)

