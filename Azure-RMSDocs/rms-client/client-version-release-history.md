---
title: Azure 信息保护客户端 - 版本发行历史记录和支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能，并了解支持的生命周期策略。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/19/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ff9d6a4ce66deed8add68d7b1efc889ee9448f53
ms.sourcegitcommit: 5866509c17872e274720d3014fe218ed95e86ee3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure 信息保护客户端：版本发行历史记录和支持策略

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

Azure 信息保护团队会定期更新 Azure 信息保护客户端，以提供修补程序和新功能。 

可从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载最新的 GA 发行版和当前预览版。 这些版本还随附在 Microsoft 更新目录（类别：Azure 信息保护）中，可利用 WSUS/配置管理器或者使用 Microsoft 更新的其他软件部署机制来部署客户端。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

在发布新的通用版本 (GA) 前，原有的 Azure 信息保护客户端的支持期限最多为六个月。 此页面不包含不支持的客户端版本。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

### <a name="release-history"></a>版本历史

请查看以下信息，了解适用于 Windows 的 Azure 信息保护客户端受支持版本的新增功能或更改之处。 最新版本会最先列出。 

> [!NOTE]
> 小的修补程序不予列出，因此如果遇到 Azure 信息保护客户端相关问题，建议检查它是否已在最新 GA 版本中得到修复。 如果问题仍然存在，请检查当前预览版。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

## <a name="versions-later-than-110560"></a>1.10.56.0 以上版本

如果客户端版本高于 1.10.56.0，则这是用于测试和评估的预览内部版本。

当前的预览版本为 **1.21.203.0**，在客户端的最新正式版之后具有以下更改。

此版本包括 RMS 客户端的 MSIPC 1.0.3403.1224 版本。

**新增功能**：

- Azure 信息保护扫描程序：客户端附带的 PowerShell 模块包含新的 cmdlet，用于安装和配置扫描程序，以便可以发现本地数据存储上的文件并对其进行分类和保护。 有关说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](../deploy-use/deploy-aip-scanner.md)。 

- 对于 Office 应用，自动和建议分类持续在后台运行，而不是在保存文档时运行。 通过此行为更改，现在可以为存储在 SharePoint Online 中的文档应用自动和建议的分类。 [详细信息](../deploy-use/configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied) 

- 现在可以通过在文本字符串中使用“If.App”变量语句并标识应用程序类型为 Word、Excel、PowerPoint 和 Outlook 设置不同的视觉标记。 [详细信息](../deploy-use/configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- 支持[策略设置](../deploy-use/configure-policy-settings.md)“在 Office 应用中显示“信息保护”栏”。 此设置已关闭时，用户可以通过功能区上的“保护”按钮选择标签。

- 这是一条新的高级客户端设置，使 Outlook 不会应用 Azure 信息保护策略中配置的默认标签。 相反，Outlook 可应用不同的默认标签，也可不应用标签。 [详细信息](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- 对于 Office 应用，当你指定自定义权限时，现在可以通过“通讯簿”图标浏览并选择用户。 使用文件资源管理器指定自定义权限时，此选项会将奇偶校验带到用户体验。

- 对于使用 PowerShell 但无法被授予**本地登录**权限的服务帐户，支持完全非交互式身份验证方法。 此身份验证方法需要对 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication) 使用新的 *Token* 参数，并将 PowerShell 脚本作为任务运行。 [详细信息](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication) 的新参数 *IntegratedAuth*。 此参数支持 AD RMS 的服务器模式，AD RMS 需要处于该模式才能支持 Windows Server FCI。


**修补程序**：

修复了包括以下特定方案的稳定性：

- 对于 Office 16.0.8628.2010 版及更高版本（即点即用），Azure 信息保护栏支持以前可能会导致该栏显示在 Office 应用程序外部的最新监视器显示选项。

- 当两个组织使用 Azure 信息保护共享标记的文档和电子邮件时，将保留他们自己的标签，而不会替换为另一个组织的标签。

- 支持 Excel 中包含交叉引用（以前会导致该单元格中的文本损坏）的单元格。

- 支持更改 Office 主题或 Windows 主题，以前更改主题后会导致 Excel 不显示任何数据。

- 现在可以检查具有 .xml 文件扩展名的文件，以便进行建议或自动分类。

- 查看器现在可以打开大于 20 MB 的基于文本的受保护文件（.ptxt 和 .pxml）。 

- 使用 Outlook 提醒时，可防止 Outlook 挂起。

- 会以 Office 64 位成功启动，以便可以保护文档和电子邮件。

- 可以现在为 Word、Excel、PowerPoint 和文件资源管理器的用户定义权限配置标签，也可使用高级客户端设置隐藏自定义权限选项。 [详细信息](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users) 

- 如果为 Azure 信息保护策略中的视觉标记配置了客户端上未安装的字体名称，则将回退到宋体字体。

- 升级 Azure 信息保护客户端后，可防止 Office 崩溃。

- 对于 Office 应用，改进性能和内存占用率。

- 为用户定义的权限和 HYOK (AD RMS) 保护配置了标签时，该保护不再错误地使用 Azure Rights Management 服务。

- 为了获得更一致的管理体验，子标签不再继承其父标签的视觉标记和保护设置。


## <a name="version-110560"></a>版本 1.10.56.0

发布日期：2017/09/18

此版本包括 RMS 客户端的 MSIPC 1.0.3219.0619 版本。

**新增功能**：

- 支持可为标签配置的新 Office 365 DLP 条件。 有关详细信息，请参阅[为 Azure 信息保护标签配置条件](../deploy-use/configure-policy-classification.md)。

- 支持为用户定义的操作配置的标签。 对于 Outlook，此标签自动应用 Outlook 的“不要转发”选项。 对于 Word、Excel、PowerPoint 和文件资源管理器，此标签提示用户指定自定义权限。 有关详细信息，请参阅[配置 Azure 信息保护标签以进行保护](../deploy-use/configure-policy-protection.md)。

- 标签支持多种语言。 自 2017 年 8 月 30 日起，[默认策略](../deploy-use/configure-policy-default.md)支持此版本客户端向用户显示的多种语言。 用户若要查看此日期前默认策略首选语言中的标签以及配置的标签，请参阅[如何在 Azure 信息保护中配置不同语言的标签](../deploy-use/configure-policy-languages.md)。

- 除了在“信息保护”栏上显示外，Office 功能区上的“保护”按钮也会显示标签。 

- 对于以下 Visio 文件类型的本机保护：.vsdm、.vsdx、.vssm、.vssx、.vstm、.vstx

- 支持用户在 Azure 门户中配置的高级客户端配置。 这些配置包括：
    
    - [在 Outlook 中隐藏或显示“不转发”按钮](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [设置用户是否能够使用自定义权限选项](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [永久隐藏 Azure 信息保护栏](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
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

## <a name="next-steps"></a>后续步骤

有关安装和使用客户端的详细信息： 

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
