---
title: "Azure 信息保护客户端&colon;版本发行历史记录"
description: "请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 28b7c2f8bbd058251f4edfd93b2fee181bd4d339
ms.sourcegitcommit: ebf396cbe8eabed720b317f131884fe9f23b8691
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2017
---
# <a name="azure-information-protection-client-version-release-history"></a>Azure 信息保护客户端：版本发行历史记录

>*适用于：Azure 信息保护*

Azure 信息保护团队会定期更新 Azure 信息保护客户端，以提供修补程序和新功能。 客户端包含在 Microsoft 更新目录（类别：**Azure 信息保护**）中，还可以随时从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载最新正式发布版 (GA) 和即将发布的版本（预览版本）。

不应在生产网络上为最终用户部署预览版本。 而应使用预览版本来查看和尝试在下一正式发布版中将出现的新功能或修补程序。 

使用以下信息查看正式发布版中的新增内容或更改的内容。 最新版本会最先列出。 有关当前预览版本的信息，请参阅下载页上的信息。

> [!NOTE]
> 不会列出小修补程序，因此，如果 Azure 信息保护客户端遇到问题，请先检查它是否是最新正式发布版的问题。 如果是，则检查当前预览版本。
>  
> 如果仍有问题，请参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。


## <a name="version-172100"></a>版本 1.7.210.0

**发布日期**：2017/06/06

此版本包括 RMS 客户端的 MSIPC 1.0.2217.1 版本。

**修补程序**：

- 未连接到 Internet 但具备有效 Azure 信息保护策略的计算机现在支持所有标记和分类 cmdlet。

- 为保持一致性，[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) cmdlet 的输出参数从英式英语 (IsLabelled) 更改为美式英语 (IsLabeled)。 如果你有用于查找此参数的脚本或自动化进程，请更新此参数的拼写。

- 稳定性的常规修复包括：

    - 对于 Outlook：修复崩溃、高内存消耗和菜单显示问题。
    
    - 对于 Word、Excel 和 PowerPoint：修复 CPU 使用率过高、保存大型 Excel 文件时的显示问题或应用程序停止响应等问题。 
    
    此外，对于这些应用程序，若要提高使用 SharePoint Online 和 OneDrive for Business 的 Office 2016 性能，请在文件关闭而不是保存时（自动保存或用户选择保存）应用自动和建议标记。 同样，如果设置“所有文档和电子邮件都必须具有一个标签”处于启用状态，那么在该文件关闭之前，系统不会提示用户选择标签。 Word 2016 和 Excel 2016 为例外情况，用户选择“另存为”选项。 然后，此操作触发这些标记行为（如果已配置）。 

**新增功能**：

- 新的 PowerShell cmdlet：[Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification)。 运行此 cmdlet 时，它会检查文件内容，并根据你在 Azure 信息保护策略中指定的条件自动将标签应用到未标记的文件。


## <a name="version-14210"></a>版本 1.4.21.0

**发布时间**：2017 年 3 月 15 日

**要求变化：**

旧版新增了完整客户端的 Microsoft .NET Framework 4.6.2 系统必备。 可以使用自定义安装参数 **DowngradeDotNetRequirement** 忽略此系统必备，尽管不建议这样做。 有关详细信息，请参阅管理员指南中的[客户端安装部分](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users)。


**修补程序**：

- 支持使用映射驱动器分类和保护文件。

- 查看器支持大型文件 (>250MB)。 

- 配置 HYOK 后，Outlook 可以应用已配置为使用 Azure Rights Management 模板或 AD RMS 模板的标签。


**新增功能**：

- 能够在 Office 应用程序中设置自定义权限，从而可以为你自己、外部组或另一组织中的所有用户设置保护。 有关详细信息，请参阅用户指南中的[设置文档的自定义权限](client-classify-protect.md#set-custom-permissions-for-a-document)。
    
- PDF 文件现支持仅应用分类的标签。

- 对于 PDF 文件，查看器现支持搜索、缩放和旋转等选项。 若要使用这些选项，请右键单击查看器中显示的文件。


## <a name="version-131552"></a>版本 1.3.155.2

**发布日期**：2017/02/08

**新要求**：

Microsoft .NET Framework

- 此版本的 Azure 信息保护客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装它。 Azure 信息保护客户端完成安装后，可能需要重启计算机。

- 如果单独安装 Azure 信息保护查看器，则要求的最低版本为 Microsoft .NET Framework 4.5.2，如果缺少此版本，安装程序会尝试下载并安装它。

**新增功能**：

- 一个新的统一客户端，它将适用于 Windows 的 Rights Management 共享应用程序中的功能与 Azure 信息保护客户端组合在一起。 包括：
    
    - 与 Windows 文件资源管理器集成（右键单击）以应用标签和保护。 支持其他文件格式和多个文件选择。
    - 适用于受保护文档的查看器（包括用于 SharePoint 的受保护 PDF）。
    - PowerShell cmdlet，可用于获取和设置存储在本地或存储在网络共享上的文件的标签。 这些 cmdlet 与 RMS 保护工具（RMSProtection 模块）之前随附的 cmdlet 一起安装。
    - 客户端使用情况日志，记录应用的标签、应用方式、应用者等信息。

此客户端版本是 2016 年 12 月首次发布的预览版客户端的[公开发行版本](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/)。 有关此版本的客户端的详细信息，请参阅以下指南：

- [Azure 信息保护客户端管理员指南](client-admin-guide.md)

- [Azure 信息保护用户指南](client-user-guide.md)


## <a name="version-1240"></a>版本 1.2.4.0

**发布日期**：2016/10/27

**修补程序**：

- 禁用 Windows 更新服务时，客户端安装完成。

- 在 Office 2016 中，在保存文档并且为页眉或页脚配置应用的标签时，光标不会跳转到页眉或页脚。

- 在 Word 中，自动分类适用于捆绑文本框中的文本。

**新功能**：

- 安装 Azure 信息保护客户端后，用户可从 Office 应用程序运行的诊断测试和重置选项：在“开始”选项卡的“保护”组中，单击“保护”、“帮助和反馈”，然后单击“运行诊断”。 

    若要详细了解此选项，请参阅管理员指南中的[其他检查和故障排除](client-admin-guide.md#additional-checks-and-troubleshooting)部分。

## <a name="version-11230"></a>版本 1.1.23.0

**发布日期**：2016/10/01

正式发布。

## <a name="next-steps"></a>后续步骤

有关安装和使用客户端的详细信息：

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]