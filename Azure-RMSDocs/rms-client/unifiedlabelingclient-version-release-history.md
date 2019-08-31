---
title: Azure 信息保护统一标签客户端版本历史记录 & 支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护统一标签客户端的发布信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/06/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b38a46f02812e93f936d5e62276d34c10bdbb19d
ms.sourcegitcommit: d3ac12c51b41bd1ec4ce4009303d124efc95353b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180619"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure 信息保护统一标签客户端-版本发行历史记录和支持策略

>适用范围： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> 说明： *[适用于 Windows 的 Azure 信息保护统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


你可以从[Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载 Azure 信息保护统一标签客户端。

在通常几周的短暂延迟后, 最新的正式发行版也包含在 Microsoft 更新目录中, 产品名称为**Microsoft Azure 信息保护** > **Microsoft Azure 信息保护统一标签客户端**和**更新**分类。 此目录包含此内容意味着可利用 WSUS/Configuration Manager 或其他使用 Microsoft 更新的软件部署机制来升级客户端。

有关详细信息, 请参阅[升级和维护 Azure 信息保护统一标签客户端](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

Azure 信息保护统一标签客户端的每个正式发行版 (GA) 在发布后续版本后, 最多可支持六个月。 文档不包括关于不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

> [!NOTE]
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

### <a name="release-information"></a>发布信息

使用以下信息可查看 Windows 的支持版本的 Azure 信息保护统一标签客户端的新增功能或更改的内容。 最新版本会最先列出。 

> [!NOTE]
> 不会列出小修补程序, 因此, 如果你遇到与统一标签客户端有关的问题, 我们建议你检查是否已通过最新的 GA 版本修复了此问题。 如果问题仍然存在, 请检查当前预览版本 (如果有)。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

此客户端正在替换 Azure 信息保护客户端 (经典)。 若要将特性和功能与经典客户端进行比较, 请参阅[比较客户端](use-client.md#compare-the-clients)。

## <a name="version-22190"></a>版本2.2.19。0

**发布日期**：08/06/2019

**纠正**

- 客户端可以成功地下载其策略并显示当前的敏感度标签。 从以前的版本升级后, 如果未在标签中心配置任何自定义信息类型, 则需要此修补程序。

- 一般的性能和稳定性方面的改进。

## <a name="version-22140"></a>版本2.2.14。0

**发布日期**：07/15/2019

支持, 04/06/2020

**新功能：**

- 支持在 PowerShell 中为安全与合规中心配置的[高级设置](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)。
    
    这些高级设置支持以下自定义:
     - [在 Office 应用程序中显示“信息保护”栏](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [使 Outlook 邮件免于强制标记](clientv2-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)
    - [在 Outlook 中启用建议的分类](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [为 Outlook 设置不同的默认标签](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [使用强制标签时，删除文档的“以后再说”](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [删除其他标记解决方案中的页眉和页脚](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [在文件资源管理器中禁用自定义权限](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [为用户添加“报告问题”](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [禁止将文档中发现的敏感信息发送到 Azure 信息保护分析](clientv2-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)
    - [禁止为一部分用户发送信息类型匹配项](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [从 Secure Islands 和其他标记解决方案迁移标签](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [应用标签时应用自定义属性](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [将标签配置为在 Outlook 中应用 S/MIME 保护](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [为父标签指定默认子标签](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [指定标签的颜色](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- 支持为 Word、Excel、PowerPoint 和文件资源管理器的用户定义权限配置的标签:
    - 如果在 Azure 门户中具有此配置的标签, 则统一标签客户端现在支持这些标签, 尽管管理中心当前没有等效的配置。
    - 当用户选择具有此配置的标签时, 系统将提示他们选择文档的用户和保护设置。

- AzureInformationProtection 模块中的 PowerShell 更改:
    - 新 cmdlet:[AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -替换 RMSProtectionLicense, 为自定义权限创建即席策略
    - 新参数:
        -  *CustomPermissions*和*RemoveProtection* -添加到[set-aipfilelabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *OnBeHalfOf* -已添加到[set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication), 用于代替非交互式会话的*令牌*参数
        -  *WhatIf*和*DiscoveryInfoTypes*已添加到[set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification), 因此此 cmdlet 可以在发现模式下运行, 而无需应用标签
    - 直接连接到保护服务的不推荐使用的 cmdlet:清除-RMSAuthentication、Get-rmsfilestatus、RMSServer、Set-rmsserverauthentication、Get-rmstemplate、protect-rmsfile、set-rmsserverauthentication、protect-rmsfile、取消保护-


**纠正**

- 支持通过*DiscoveryInfoTypes*参数进行分析和[set-aipfileclassification](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipfileclassification?view=azureipps)的[内容匹配](../reports-aip.md#content-matches-for-deeper-analysis)。

- 更改为 Windows 中的备用区域设置后, 仍然可以将具有保护功能的标签应用于 PDF 文档。

- 从内容中删除标签时, 仅当将其作为标签配置的一部分应用时, 才会删除保护。 如果与标签分开应用保护, 则会保留该保护。 例如, 用户对文件应用了自定义权限。

- 当配置自动标签时, 标签会在首次保存文档时应用。

- 默认标记支持子标签。

## <a name="version-207790"></a>版本2.0.779。0

**发布日期**：05/01/2019

支持, 02/15/2020

此版本提供单个修补程序来解决争用情况问题, 有时, Office 应用程序或文件资源管理器中不显示标签。

## <a name="version-207780"></a>版本2.0.778。0

**发布日期**：04/16/2019

支持, 11/01/2019

适用于 Windows 的 Azure 信息保护统一标签客户端的第一个通用版本支持以下功能: 

- 从 Azure 信息保护客户端升级。

- 手动、自动和建议标记：有关为此客户端配置自动和建议标签的详细信息，请参阅[将敏感度标签自动应用于内容](/Office365/SecurityCompliance/apply-sensitivity-label-automatically)。

- 文件资源管理器、用于分类和保护文件的右键单击操作、删除保护和应用自定义权限。

- 适用于受保护的文本和图像文件、受保护的 PDF 文件以及一般保护的文件的查看器。

- 用于实现以下目的的 PowerShell 命令：
    - [设置或删除文档上的标签](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [在检查文档内容后标记文档](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [读取应用于文档的标签信息](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [进行身份验证以支持无人参与的 PowerShell 会话](/powershell/module/azureinformationprotection/set-aipauthentication)

- 使用[Azure 信息保护分析](../reports-aip.md)审核数据和终结点发现支持。

- 以下标签和策略设置：
    - 视觉标记（页眉、页脚、水印）
    - 默认标记-当前限制为不带子标签的标签
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

有关安装和使用该客户端的详细信息: 

- 面向用户：[下载并安装客户端](install-unifiedlabelingclient-app.md)

- 面向管理员：[Azure 信息保护统一标签客户端管理员指南](clientv2-admin-guide.md)

