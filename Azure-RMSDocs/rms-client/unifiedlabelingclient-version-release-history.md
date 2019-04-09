---
title: Azure 信息保护统一标签客户端 - 版本发布信息
description: 请参阅适用于 Windows 的 Azure 信息保护统一标签客户端的发布信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 7eb7ffd98651ed35be7ecd8043e49c1d15a65e8e
ms.sourcegitcommit: 8da0aa8f9bb9f91375580a703682d23a81a441bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58809703"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Azure 信息保护统一标签客户端：版本发布信息

>适用范围：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

> [!NOTE]
> 此客户端处于预览状态，随时可能更改。 客户端使用统一标签存储并从以下管理中心下载带有标签的策略：Office 365 安全与合规中心、Microsoft 365 安全中心和 Microsoft 365 合规中心。 [详细信息](/Office365/SecurityCompliance/sensitivity-labels)

可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=57440)下载最新预览版本的 Azure 信息保护统一标签客户端。

### <a name="release-information"></a>发布信息

使用以下信息以查看最新预览版本的 Azure 信息保护统一标签客户端所支持的功能。

此客户端安装 Windows 计算机的 Office 加载项：文件资源管理器的扩展和 PowerShell 模块。 此客户端的[先决条件](../requirements.md)与从 Azure 下载策略的 Azure 信息保护客户端相同。

若要与 Azure 信息保护客户端比较特性和功能，请参阅[客户端功能比较](use-client.md#feature-comparisons-for-the-clients)。

## <a name="current-preview-version"></a>当前的预览版本

**发布日期**：2019 年 2 月 25 日

此预览版的适用于 Windows 的 Azure 信息保护统一标签客户端支持以下功能： 

- 从 Azure 信息保护客户端升级。

- 手动、自动和建议标记：有关为此客户端配置自动和建议标签的详细信息，请参阅[将敏感度标签自动应用于内容](/Office365/SecurityCompliance/apply_sensitivity_label_automatically)。

- 文件资源管理器、用于分类和保护文件的右键单击操作、删除保护和应用自定义权限。

- 适用于受保护的文本和图像文件、受保护的 PDF 文件以及一般保护的文件的查看器。

- 用于实现以下目的的 PowerShell 命令：
    - [设置或删除文档上的标签](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [在检查文档内容后标记文档](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [读取应用于文档的标签信息](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [进行身份验证以支持无人参与的 PowerShell 会话](/powershell/module/azureinformationprotection/set-aipauthentication)

- 使用 [Azure 信息保护分析](../reports-aip.md)支持集中报告。

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

### <a name="features-that-do-not-work-in-this-preview-version-or-are-not-available"></a>在此预览版本中不起作用或不提供的功能

包括：

- 用于发现、标记和保护本地数据存储文件的扫描程序。

- 从 Azure 门户迁移并配置为 HYOK 保护的标签在发布时显示在客户端中，但这些标签不应用保护。

- AzureInformationProtection 模块中一组完整的 cmdlet 不可用，其中包括直接连接到保护服务的 cmdlet。 例如，用于批量取消文件保护的 Unprotect-RMSFile。

有关完整的详细信息，请参阅[比较表](use-client.md#feature-comparisons-for-the-clients)。

## <a name="instructions"></a>说明

1. 按照以下说明安装客户端：[用户指南：下载并安装 Azure 信息保护客户端（预览版）](install-unifiedlabelingclient-app.md) 

2. 像使用 Azure 信息保护客户端一样使用客户端，Office 应用程序的以下内容除外：
    - Office 功能区上的按钮命名为“敏感度”，而不是“保护”。
    - 默认情况下，管理员无法显示信息保护栏，但用户可通过从“敏感度”按钮选择“显示栏”来显示它。 
    - 不提供自定义权限
    - 不提供跟踪和撤销
    
    用户指令：
    
    - [对文件或电子邮件进行分类](client-classify.md) 
    
    - [对文件或电子邮件进行分类和保护](client-classify-protect.md)

3. 与我们分享你的体验： 
    
    - 要提供反馈或提出有关此预览版客户端的问题，请使用 [Azure 信息保护的 Yammer 站点](https://www.yammer.com/AskIPTeam)。
