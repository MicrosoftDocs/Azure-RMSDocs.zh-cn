---
title: Azure 信息保护统一标签客户端 - 版本发布信息
description: 请参阅适用于 Windows 的 Azure 信息保护统一标签客户端的发布信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/23/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 939ae3e367b14f722c38be023c70d9dcce21004f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254826"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Azure 信息保护统一标签客户端：版本发布信息

>适用于：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

> [!NOTE]
> 此客户端处于预览状态，随时可能更改。 客户端使用统一标签存储并从 Office 365 安全与合规中心下载带有标签的策略。 [详细信息](/Office365/SecurityCompliance/sensitivity-labels)

可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=57440)下载最新预览版本的 Azure 信息保护统一标签客户端。

### <a name="release-information"></a>发布信息

使用以下信息以查看最新预览版本的 Azure 信息保护统一标签客户端所支持的功能。 

此客户端作为 Windows 计算机的 Office 加载项安装，并且具有与从 Azure 下载策略的 Azure 信息保护客户端相同的[先决条件](../requirements.md)。

## <a name="current-preview-version"></a>当前的预览版本

**发布日期**：2018 年 10 月 16 日

此预览版的适用于 Windows 的 Azure 信息保护统一标签客户端支持以下功能： 

- 从 Azure 信息保护客户端升级

- 将分类和保护应用于 Word、Excel、PowerPoint 和 Outlook 的手动标签。

- 视觉标记（页眉、页脚、水印）

- 默认标签 

- 应用“不可转发”的标签

- 如果用户降低敏感度级别，系统提示说明理由

- “帮助和反馈”对话框，其中包括重置设置和导出日志

- 每个 Office 应用每 4 小时刷新一次安全与合规中心策略。

此预览版不提供以下功能：

- 自动分类和建议分类

- “自定义权限”

- 适用于受保护的文本和图像文件、受保护的 PDF 文件以及一般保护的文件的查看器

- 文件资源管理器，右键单击操作以对文件进行分类和保护

- PowerShell 命令，用于对命令行中的文件进行分类和保护

- 用于发现、标记和保护本地数据存储文件的扫描仪

- 支持除英语以外的语言

## <a name="instructions"></a>说明

1. 按照以下说明安装客户端：[用户指南：下载并安装 Azure 信息保护客户端（预览版）](install-unifiedlabelingclient-app.md) 

2. 像使用 Azure 信息保护客户端一样使用 Office 应用中的客户端，但 Office 功能区中的按钮名为“敏感度”而非“保护”：
    
    - [对文件或电子邮件进行分类](client-classify.md) 
    
    - [对文件或电子邮件进行分类和保护](client-classify-protect.md)

3. 与我们分享你的体验： 
    
    - 要提供反馈或提出有关此预览版客户端的问题，请使用 [Azure 信息保护的 Yammer 站点](https://www.yammer.com/AskIPTeam)。
    
    - 要报告此预览版客户端的问题，请使用功能区上“敏感度”按钮中的“帮助和反馈”选项。 将日志从对话框中导出，然后将这些日志文件附加到使用“报告问题”选项创建的电子邮件中。 

