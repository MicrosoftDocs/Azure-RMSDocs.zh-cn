---
title: Azure 信息保护客户端 - 版本发行历史记录和支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能，并了解支持的生命周期策略。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/09/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 1c41e1e6622dc76a2a2afe68a48d0761573ccf06
ms.sourcegitcommit: 6eab0086306a4e12cbcf7d8578cb5fd42abe1e66
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020594"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure 信息保护客户端：版本发行历史记录和支持策略

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

Azure 信息保护团队会定期更新 Azure 信息保护客户端，以提供修补程序和新功能。 

可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载最新正式版本和当前预览版（若有）。 Microsoft 更新目录（类别：“Azure 信息保护”）还随附正式版本，所以可利用 WSUS/Configuration Manager 或其他使用 Microsoft 更新的软件部署机制来升级客户端。

有关详细信息，请参阅[升级和维护 Azure 信息保护客户端](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

在发布新的通用版本 (GA) 前，原有的 Azure 信息保护客户端的支持期限最多为六个月。 此页面不包含不支持的客户端版本。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

### <a name="release-history"></a>版本历史

请查看以下信息，了解适用于 Windows 的 Azure 信息保护客户端受支持版本的新增功能或更改之处。 最新版本会最先列出。 

> [!NOTE]
> 小的修补程序不予列出，因此如果遇到 Azure 信息保护客户端相关问题，建议检查它是否已在最新 GA 版本中得到修复。 如果问题仍然存在，请检查当前预览版。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

## <a name="versions-later-than-12950"></a>高于 1.29.5.0 的版本

如果客户端版本高于 1.29.5.0，则这是用于测试和评估的预览内部版本。

此版本包括 RMS 客户端的 MSIPC 1.0.3557.524 版本。

**新增功能**： 

- 支持新的敏感信息类型，可帮助对包含个人信息的文档进行分类。 [详细信息](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- 对 Word、Excel 和 PowerPoint 文件中“Strict Open XML 文档”格式的标签支持。 有关 Open XML 格式的详细信息，请参阅 Office 博客文章[新 Office 中的新文件格式选项](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/)。 

- 通过配置新的[高级客户端配置](client-admin-guide-customizations.md#protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)，支持 PDF 加密 ISO 标准。 配置此选项后，受保护 PDF 文档的文件扩展名仍为. pdf（而不是更改为 .ppdf），并且可以通过支持此 ISO 标准的 PDF 阅读器打开。 

- 支持受 Secure Islands 保护的文件（PDF 和 Office 文档以外的文件）。 例如，受保护的文本和图片文件。 或者，文件扩展名为 .pfile 的文件。 此支持可实现新方案，例如 Azure 信息保护扫描程序可检查这些文件中的敏感信息，并自动为 Azure 信息保护重新标记它们。 [详细信息](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- 对于 Azure 信息保护扫描程序：

    - 新 cmdlet [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)：从版本 1.26.6.0 或更低版本升级后需要运行一次。
    
    - 新 cmdlet [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)：获取扫描程序服务的当前状态。  
    
    - 新 cmdlet [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)：当计划设置为手动时，指示扫描程序开始一次扫描周期。
    
    - 对于具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)的客户，支持 SharePoint Server 2010。
    
**修复程序**

- 对于 Azure 信息保护扫描程序：
    
    - 对于在 SharePoint 库中受保护的文档，如果未对数据存储库使用 DefaultOwner 参数，则 SharePoint 编辑器值现在用作默认值而不是“创建者”值。
    
    - 扫描程序报告包括 Office 文档的“上次修改者”。 

- 使用 PowerShell 或扫描程序进行分类和保护时，不会删除或加密 Office 文档元数据。

- 使用快速访问工具栏上的“下一项”和“上一项”箭头图标查看电子邮件时，将显示每封电子邮件的正确标签。

- 自定义权限支持包含撇号的收件人电子邮件地址。

- 通过打开存储在 SharePoint Online 中的受保护文档来启动此操作时，计算机环境可成功初始化（启动）。 

**其他更改**：
   
- 对于 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)：
    
    - Schedule 参数的值不再为“OneTime”、“Continuous”和“Never”，而是“Manual”和“Always”。
        
    - Type 参数已删除，因此在运行 [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration) 时也会从输出中删除该参数。 默认情况下，在首个扫描周期后，只检查新文件或经过修改的文件。 如果之前为了重新扫描所有文件将 Type 参数设置为 Full，现在使用 Reset 参数运行 [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)。 另外，还必须为扫描程序配置人工计划，这就需要使用 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) 将 Schedule 参数设置为 Manual。
    
- 对于扫描程序，默认排除列表现在包括 .rtf 文件。 [详细信息](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner)

- 策略版本更改为 1.4。 [配置断开连接的计算机](client-admin-guide-customizations.md#support-for-disconnected-computers)需要标识版本号。 


## <a name="version-12950"></a>版本 1.29.5.0 

**发布日期**：2018 年 6 月 26 日

此版本包括 RMS 客户端的 MSIPC 1.0.3403.1224 版本。

**修补程序**：

- 对于 Outlook 版本 16.0.9324.1000 及更高版本（即点即用），Azure 信息保护栏支持最新监视器显示选项，旧选项可能会导致栏显示在 Outlook 应用程序外面。

- [按 Office 应用程序类型](../configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)配置的视觉标记现在替换 Azure 信息保护标签应用的旧页眉或页脚。

- 如果 Excel 文件已有标签，当标签应用视觉标记时，新工作表现在也应用标签的视觉标记。

- 借助高级客户端设置[使用现有自定义属性来设置 Office 文档的标签](client-admin-guide-customizations.md#label-an-office-document-by-using-an-existing-custom-property)时，自动标签不会替代手动标签。

## <a name="version-127480"></a>版本 1.27.48.0

**发布日期**：2018 年 5 月 30 日

此版本包括 RMS 客户端的 MSIPC 1.0.3403.1224 版本。

**新增功能**： 

- 对于 Azure 信息保护扫描程序：
    
    - 你可以指定要列入扫描范围或者从扫描范围中排除的文件类型列表。 若要指定此列表，请使用 [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes)。 指定文件类型列表后，可以使用 [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes) 向列表添加新文件类型，并能使用 [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes) 从列表中删除文件类型。
    
    - 不通过应用默认标签来检查内容也可标记文件。 使用 [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) cmdlet，并将“MatchPolicy” 参数设置为“关闭” 
    
    - 无需配置用于自动分类的标签，也可发现具有敏感信息类型的文件。 使用 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet，并将“DiscoverInformationTypes”参数设置为“全部”
    
    - 默认情况下，只有 Office 文档类型会受到保护。 在注册表中定义其他文件类型时它们可以受到保护。 有关说明，请参阅开发人员指南中的[文件 API 配置](../develop/file-api-configuration.md)。
    
    - 默认情况下，扫描程序现以低完整性级别运行以获得更高安全性，以防你使用具有特权的帐户运行扫描程序。 当运行扫描程序的服务帐户只在[扫描程序先决条件](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner)中记录了权限时，低完整性级别不是必需的且不推荐使用，因为它会对性能产生负面影响。 你可以使用高级客户端设置禁用低完整性级别。 [详细信息](client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) 
    
- 对于 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/Get-AIPFileStatus)，输出现在包括 Rights Management 所有者和 Rights Management 颁发者以及内容受保护日期。
 
**其他更改**：

- 对于 Azure 信息保护扫描程序： 
    
    - 如果安装了旧版扫描程序，请在升级 Azure 信息保护客户端后，使用 [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) 重新运行扫描程序安装命令。 扫描程序和存储库的配置设置将会得到保留。 重新安装扫描程序会向扫描程序服务帐户授予对扫描程序数据库的删除权限，这是报表所必需的权限。    
    
    - [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) 的“ScanMode” 参数被重命名为“Enforce”其值为“Off”和“On”。
    
    - 若要使用默认标签，不再需要将默认标签配置为策略设置。 相反，只需通过存储库配置指定此默认标签。 

- 删除“祝贺你!” 欢迎页和“Azure 信息保护中的新增功能有哪些”页，首次使用时，Office 应用程序中会显示这些页面。

## <a name="version-12660"></a>版本 1.26.6.0

发布日期：2018/04/17

此版本包括 RMS 客户端的 MSIPC 1.0.3403.1224 版本。

**新增功能**：

- Azure 信息保护扫描程序：客户端附带的 PowerShell 模块包含新的 cmdlet，用于安装和配置扫描程序，以便可以发现本地数据存储上的文件并对其进行分类和保护。 有关说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](../deploy-aip-scanner.md)。 

- 现在可以通过在文本字符串中使用“If.App”变量语句并标识应用程序类型为 Word、Excel、PowerPoint 和 Outlook 设置不同的视觉标记。 [更多信息]configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- 支持[策略设置](../configure-policy-settings.md)“在 Office 应用中显示“信息保护”栏”。 此设置已关闭时，用户可以通过功能区上的“保护”按钮选择标签。

- 一个新的高级客户端设置（仍处于预览阶段），可以用于开启分类在后台继续运行。 在启用此设置时，对于 Office 应用，自动和建议分类持续在后台运行，而不是在保存文档时运行。 通过此行为更改，现在可以为存储在 SharePoint Online 中的文档应用自动和建议的分类。 [详细信息](client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)

- 这是一条新的高级客户端设置，使 Outlook 不会应用 Azure 信息保护策略中配置的默认标签。 相反，Outlook 可应用不同的默认标签，也可不应用标签。 [详细信息](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- 对于 Office 应用，当你指定自定义权限时，现在可以通过“通讯簿”图标浏览并选择用户。 使用文件资源管理器指定自定义权限时，此选项会将奇偶校验带到用户体验。

- 对于使用 PowerShell 但无法被授予**本地登录**权限的服务帐户，支持完全非交互式身份验证方法。 此身份验证方法需要对 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication) 使用新的 *Token* 参数，并将 PowerShell 脚本作为任务运行。 [详细信息](client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication) 的新参数 *IntegratedAuth*。 此参数支持 AD RMS 的服务器模式，AD RMS 需要处于该模式才能支持 Windows Server FCI。


**修补程序**：

修复了包括以下特定方案的稳定性：

- 对于 Office 16.0.8628.2010 版及更高版本（即点即用），Azure 信息保护栏支持以前可能会导致该栏显示在 Office 应用程序外部的最新监视器显示选项。

- 当两个组织使用 Azure 信息保护共享标记的文档和电子邮件时，将保留他们自己的标签，而不会替换为另一个组织的标签。

- 对于 Excel：
        
    - 支持更改 Office 主题或 Windows 主题，以前更改主题后会导致 Excel 不显示任何数据。
        
    - 支持包含交叉引用（以前会导致该单元格中的文本损坏）的单元格。
    
    - 支持键入日语、简体中文或韩语字符，这些字符以前会关闭窗口，因此无法选择这些字符。
    
    - 对注释的支持，之前在键入时关闭了注释。

- 对于 Powerpoint：支持共同编写，以前可能会导致数据丢失。

- 现在可以检查具有 .xml 文件扩展名的文件，以便进行建议或自动分类。

- 查看器现在可以打开大于 20 MB 的基于文本的受保护文件（.ptxt 和 .pxml）。 
- 使用 Outlook 提醒时，可防止 Outlook 挂起。

- 会以 Office 64 位成功启动，以便可以保护文档和电子邮件。

- 现在可以针对 Word、Excel、PowerPoint 和文件资源管理器为用户定义的权限配置标签，并能使用高级客户端设置隐藏自定义权限选项。 [详细信息](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users) 

- 如果为 Azure 信息保护策略中的视觉标记配置了客户端上未安装的字体名称，则将回退到宋体字体。

- 升级 Azure 信息保护客户端后，可防止 Office 崩溃。

- 对于 Office 应用，改进性能和内存占用率。

- 为用户定义的权限和 HYOK (AD RMS) 保护配置标签时，保护配置不再错误地使用 Azure Rights Management 服务。

- 为了获得更一致的管理体验，子标签不再继承其父标签的视觉标记和保护设置。

**其他更改**：

- 对于[客户端使用情况日志记录](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client )：将事件 ID 102 和 ID 103 替换为事件 ID 101。

## <a name="version-110560"></a>版本 1.10.56.0

发布日期：2017/09/18

此版本包括 RMS 客户端的 MSIPC 1.0.3219.0619 版本。

**新增功能**：

- 支持可为标签配置的新 Office 365 DLP 条件。 有关详细信息，请参阅[为 Azure 信息保护标签配置条件](../configure-policy-classification.md)。

- 支持为用户定义的操作配置的标签。 对于 Outlook，此标签自动应用 Outlook 的“不要转发”选项。 对于 Word、Excel、PowerPoint 和文件资源管理器，此标签提示用户指定自定义权限。 有关详细信息，请参阅[配置 Azure 信息保护标签以进行保护](../configure-policy-protection.md)。

- 标签支持多种语言。 自 2017 年 8 月 30 日起，[默认策略](../configure-policy-default.md)支持此版本客户端向用户显示的多种语言。 在此日期前用户若要查看默认策略中的首选语言标签以及配置的标签，请参阅[如何在 Azure 信息保护中配置不同语言的标签]configure-policy-languages.md)。

- 除了在“信息保护”栏上显示外，Office 功能区上的“保护”按钮也会显示标签。 

- 对于以下 Visio 文件类型的本机保护：.vsdm、.vsdx、.vssm、.vssx、.vstm、.vstx

- 支持用户在 Azure 门户中配置的高级客户端配置。 这些配置包括：
    
    - [在 Outlook 中隐藏或显示“不转发”按钮](client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [设置用户是否能够使用自定义权限选项](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [永久隐藏 Azure 信息保护栏](client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
    - [在 Outlook 中启用建议的分类](client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- 对于 PowerShell，支持通过使用新的PowerShell cmdlet、[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 和 [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication)，以非交互式方式标记文件。 有关如何使用这些 cmdlet 的详细信息，请参阅管理员指南的 [PowerShell 部分](client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)。

- 对于 PowerShell cmdlet、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) 和 [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)，新参数为：Owner 和 PreserveFileDetails。 这些参数允许用户为 Owner 自定义属性指定电子邮件地址，并使标记的文档的日期保持不变。

**修补程序**：

修复了包括以下特定方案的稳定性：

- 支持以常规方式保护大文件，此前该方式可能会导致大于 1 GB 的文件损坏。 现在，文件大小仅受可用硬盘空间和可用内存限制。 有关文件大小限制的详细信息，请参阅管理员指南中的[支持保护的文件大小](client-admin-guide-file-types.md#file-sizes-supported-for-protection)。

- Azure 信息保护客户端查看器以只读方式打开受保护的 PDF (.ppdf) 文件。

- 支持标记和保护存储在 SharePoint Server 上的文件。

- 水印现在支持多行。 此外，视觉标记现在[仅在第一次文档保存时]configure-policy-markings.md#when-visual-markings-are-applied)应用于文档，而不是每次文档保存都应用。

- “帮助和反馈”对话框中的“运行诊断”选项被替换为“重置设置”。 此操作的行为已更改为包括注销用户和删除 Azure 信息保护策略。 有关详细信息，请参阅管理员指南中的[有关“重置设置”选项的详细信息](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option)。

- 支持代理身份验证。

添加了修补程序以提供更好的用户体验，包括：

- 用户指定自定义权限时的电子邮件验证。 此外，现在可以通过按 Enter 指定多个电子邮件地址。

- 当父标签的所有子标签都配置为保护，并且客户端没有支持保护的 Office 版本时，不会显示父标签。 

## <a name="next-steps"></a>后续步骤

有关安装和使用客户端的详细信息： 

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)


