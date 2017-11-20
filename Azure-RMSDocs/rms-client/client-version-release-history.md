---
title: "Azure 信息保护客户端&colon; 版本发行历史记录和支持策略"
description: "请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能，并了解支持的生命周期策略。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e107d796ebda1b1942e19ede8c794f79defbf64e
ms.sourcegitcommit: fd3932ab19a00229b56efc3e301abaf9cff3f70b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure 信息保护客户端：版本发行历史记录和支持策略

>*适用于：Azure 信息保护*

Azure 信息保护团队会定期更新 Azure 信息保护客户端，以提供修补程序和新功能。 

可从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载最新的 GA 发行版和当前预览版。 这些版本还随附在 Microsoft 更新目录（类别：Azure 信息保护）中，可利用 WSUS/配置管理器或者使用 Microsoft 更新的其他软件部署机制来部署客户端。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

Azure 信息保护客户端的正式发布 (GA) 版本自发行之日期可获取 6 个月的支持。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

### <a name="release-history"></a>版本历史

请查看以下信息，了解适用于 Windows 的 Azure 信息保护客户端受支持版本的新增功能或更改之处。 最新版本会最先列出。 


> [!NOTE]
> 小的修补程序不予列出，因此如果遇到 Azure 信息保护客户端相关问题，建议检查它是否已在最新 GA 版本中得到修复。 如果问题仍然存在，请检查当前预览版。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

## <a name="versions-later-than-110560"></a>1.10.56.0 以上版本

如果客户端版本高于 1.10.56.0，则这是用于测试和评估的预览内部版本。 

要了解自上次推出正式发布版客户端以来，当前预览版中新增或更改的内容，请参阅[下载页面](https://www.microsoft.com/en-us/download/details.aspx?id=53018)中的“详细信息”部分。 

## <a name="version-110560"></a>版本 1.10.56.0

发布日期：2017/09/18

此版本包括 RMS 客户端的 MSIPC 1.0.3219.0619 版本。

**新增功能**：

- 支持可为标签配置的新 Office 365 DLP 条件。 有关详细信息，请参阅[为 Azure 信息保护标签配置条件](../deploy-use/configure-policy-classification.md)。

- 支持为用户定义的操作配置的标签。 对于 Outlook，此标签自动应用 Outlook 的“不要转发”选项。 对于 Word、Excel、PowerPoint 和文件资源管理器，此标签提示用户指定自定义权限。 有关详细信息，请参阅[配置 Azure 信息保护标签以进行保护](../deploy-use/configure-policy-protection.md)。

- 除了在“信息保护”栏上显示外，Office 功能区上的“保护”按钮也会显示标签。 

- 对于以下 Visio 文件类型的本机保护：.vsdm、.vsdx、.vssm、.vssx、.vstm、.vstx

- 支持用户在 Azure 门户中配置的高级客户端配置。 这些配置包括：
    
    - [在 Outlook 中隐藏“不要转发”按钮](../rms-client/client-admin-guide-customizations.md#hide-the-do-not-forward-button-in-outlook)
    
    - [使“自定义权限”选项对用户不可见](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
    - [永久隐藏 Azure 信息保护栏](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
    - [在 Outlook 中启用建议的分类](../rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- 对于 PowerShell，支持通过使用新的PowerShell cmdlet、[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 和 [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication)，以非交互式方式标记文件。 有关如何使用这些 cmdlet 的详细信息，请参阅管理员指南的 [PowerShell 部分](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

- 对于 PowerShell cmdlet、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 和 [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)，新参数为：Owner 和 PreserveFileDetails。 这些参数允许用户为 Owner 自定义属性指定电子邮件地址，并使标记的文档的日期保持不变。

**修补程序**：

修复了包括以下特定方案的稳定性：

- 支持以常规方式保护大文件，此前该方式可能会导致大于 1 GB 的文件损坏。 现在，文件大小仅受可用硬盘空间和可用内存限制。 有关文件大小限制的详细信息，请参阅管理员指南中的[支持保护的文件大小](client-admin-guide-file-types.md#file-sizes-supported-for-protection)。

- Azure 信息保护客户端查看器以只读方式打开受保护的 PDF (.ppdf) 文件。

- 支持标记和保护存储在 SharePoint Server 上的文件。

- 水印现在支持多行。 此外，视觉标记现在[仅在第一次保存时](../deploy-use/configure-policy-markings.md#when-visual-markings-are-applied)（而不是每次保存文档时）应用于文档。

- “帮助和反馈”对话框中的“运行诊断”选项被替换为“重置设置”。 此操作的行为已更改为包括注销用户和删除 Azure 信息保护策略。 有关详细信息，请参阅管理员指南中的[有关“重置设置”选项的详细信息](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option)。

- 支持代理身份验证。

添加了修补程序以提供更好的用户体验，包括：

- 用户指定自定义权限时的电子邮件验证。 此外，现在可以通过按 Enter 指定多个电子邮件地址。

- 当父标签的所有子标签都配置为保护，并且客户端没有支持保护的 Office 版本时，不会显示父标签。 

## <a name="version-172100"></a>版本 1.7.210.0

**发布日期**：2017/06/06

此版本包括 RMS 客户端的 MSIPC 1.0.2217.1 版本。

**新增功能**：

- 新的 PowerShell cmdlet：[Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification)。 运行此 cmdlet 时，它会检查文件内容，并根据你在 Azure 信息保护策略中指定的条件自动将标签应用到未标记的文件。

**修补程序**：

- 未连接到 Internet 但具备有效 Azure 信息保护策略的计算机现在支持所有标记和分类 cmdlet。

- 为保持一致性，[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) cmdlet 的输出参数从英式英语 (IsLabelled) 更改为美式英语 (IsLabeled)。 如果你有用于查找此参数的脚本或自动化进程，请更新此参数的拼写。

- 稳定性的常规修复包括：

    - 对于 Outlook：修复崩溃、高内存消耗和菜单显示问题。
    
    - 对于 Word、Excel 和 PowerPoint：修复 CPU 使用率过高、保存大型 Excel 文件时的显示问题或应用程序停止响应等问题。 
    
    此外，对于这些应用程序，若要提高使用 SharePoint Online 和 OneDrive for Business 的 Office 2016 性能，请在文件关闭而不是保存时（自动保存或用户选择保存）应用自动和建议标记。 同样，如果设置“所有文档和电子邮件都必须具有一个标签”处于启用状态，那么在该文件关闭之前，系统不会提示用户选择标签。 Word 2016 和 Excel 2016 为例外情况，用户选择“另存为”选项。 然后，此操作触发这些标记行为（如果已配置）。 

## <a name="next-steps"></a>后续步骤

有关安装和使用客户端的详细信息： 

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
