---
title: Azure 信息保护统一标记客户端的版本历史记录和支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护统一标签客户端的发布信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 6f359c304080918713cee52667a1bedeb7b4ae07
ms.sourcegitcommit: 9628dcd88abde32f612896195f8d3d9a2c1d87bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2019
ms.locfileid: "67398734"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure 信息保护统一标记客户端-版本发行历史记录和支持策略

>适用对象：  Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> 说明： *[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


您可以下载 Azure 信息保护统一标记的客户端从[Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。

通常几周的一小段延迟后, 的最新正式发布版本还包括在产品名称为 Microsoft 更新目录**Microsoft Azure 信息保护** >  **Microsoft Azure 信息保护统一标记客户端**，和的分类**更新**。 此目录包含此内容意味着可利用 WSUS/Configuration Manager 或其他使用 Microsoft 更新的软件部署机制来升级客户端。

有关详细信息，请参阅[升级和维护 Azure 信息保护统一标记的客户端](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

每个公开发行 (GA) 版本的 Azure 信息保护统一标记客户端支持最多六个月发布后的后续 GA 版本。 文档不包括关于不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

> [!NOTE]
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

### <a name="release-information"></a>发布信息

使用以下信息查看正式发布版本的 Azure 信息保护统一标记客户端支持的功能。

此客户端安装 Windows 计算机的 Office 加载项：文件资源管理器的扩展和 PowerShell 模块。 此客户端的[先决条件](../requirements.md)与从 Azure 下载策略的 Azure 信息保护客户端相同。

若要比较的特性和功能使用 Azure 信息保护客户端，请参阅[比较客户端](use-client.md#compare-the-clients)。

## <a name="versions-later-than-207790"></a>2\.0.779.0 以上版本

**发布日期**：06/20/2019

如果必须晚于 2.0.779.0 的客户端的版本 2，它是用于测试和评估目的的预览版本。 

**新功能：**

- 为支持[高级设置](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)，使用 PowerShell 配置为安全与合规中心。
    
    这些高级的设置支持以下自定义：
     - [在 Office 应用程序中显示“信息保护”栏](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [在 Outlook 中启用建议的分类](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [为 Outlook 设置不同的默认标签](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [使用强制标签时，删除文档的“以后再说”](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [删除其他标记解决方案中的页眉和页脚](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [禁用在文件资源管理器中的自定义权限](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [对于受自定义权限保护的文件，始终在文件资源管理器中向用户显示自定义权限](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [为用户添加“报告问题”](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [禁用将在文档中发现的敏感信息发送到 Azure 信息保护 analytics](clientv2-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)
    - [禁止为一部分用户发送信息类型匹配项](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [从 Secure Islands 和其他标记解决方案迁移标签](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [应用标签时应用的自定义属性](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [将标签配置为在 Outlook 中应用 S/MIME 保护](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [指定父标签的默认子标签](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [指定标签的颜色](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- 为 Word、 Excel、 PowerPoint 和文件资源管理器用户定义权限配置的标签的支持：
    - 如果必须使用 Azure 门户中的此配置的标签，它们现在支持由统一标记客户端但目前在管理中心中没有等效的配置。
    - 当用户选择具有此配置的标签时，会提示他们选择用户和文档的保护设置。

- AzureInformationProtection 模块中的 PowerShell 更改：
    - 新 cmdlet:[新建 AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -替换新建-RMSProtectionLicense 创建自定义权限的临时策略
    - 新参数：
        -  *CustomPermissions*并*RemoveProtection* -添加到[Set-aipfilelabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)
        -  *通过使用 OnBeHalfOf* -添加到[Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)，而不是使用*令牌*的非交互式会话的参数
        -  *WhatIf*并*DiscoveryInfoTypes* -添加到[Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification)，因此，此 cmdlet 可以在发现模式下运行而不应用标签
    - 不推荐使用的 cmdlet:清除 RMSAuthentication、 Get-rmsfilestatus、 Get-rmsserver、 Get RMSServerAuthentication、 Get-rmstemplate、 保护 RMSFile、 Set-rmsserverauthentication、 取消保护 RMSFile


**修补程序：**

- 当配置自动标签时，标签将应用第一次保存文档。

- 默认标签支持子标签。

## <a name="version-207790"></a>版本 2.0.779.0

**发布日期**：05/01/2019

此版本包含一次修复，若要解决争用条件问题，有时，任何标签显示在 Office 应用程序或文件资源管理器中。

## <a name="version-207780"></a>版本 2.0.778.0

**发布日期**：04/16/2019

通过 11/01/2019年支持

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
    - 默认标签的当前限制为没有子标签的标签
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

