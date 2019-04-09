---
title: Azure 信息保护客户端 - 版本发行历史记录和支持策略
description: 请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能，并了解支持的生命周期策略。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d6ffbce2dfba5a2d835808a21857eb396cfc1eb5
ms.sourcegitcommit: 8da0aa8f9bb9f91375580a703682d23a81a441bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58809856"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure 信息保护客户端：版本发行历史记录和支持策略

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

Azure 信息保护团队会定期更新 Azure 信息保护客户端，以提供修补程序和新功能。 

可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载最新正式版本和当前预览版（若有）。 经过短暂的延迟后（通常是几周的时间），最新的正式发布版本也会包含在 Microsoft 更新目录中（类别：Azure 信息保护）。 此目录包含此内容意味着可利用 WSUS/Configuration Manager 或其他使用 Microsoft 更新的软件部署机制来升级客户端。

有关详细信息，请参阅[升级和维护 Azure 信息保护客户端](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)。

### <a name="servicing-information-and-timelines"></a>维护信息和日程表

在发布新的通用版本 (GA) 前，原有的 Azure 信息保护客户端的支持期限最多为六个月。 文档不包括关于不支持的客户端版本的信息。 修补程序和新功能始终应用于最新 GA 版，且不适用于较旧的 GA 版。

不应在生产网络上为最终用户部署预览版本。 而是使用最新预览版来查看和试用即将在下一 GA 版本中推出的新功能或修补程序。 仅支持当前预览版。

### <a name="release-history"></a>版本历史

请查看以下信息，了解适用于 Windows 的 Azure 信息保护客户端受支持版本的新增功能或更改之处。 最新版本会最先列出。 

> [!NOTE]
> 小的修补程序不予列出，因此如果遇到 Azure 信息保护客户端相关问题，建议检查它是否已在最新 GA 版本中得到修复。 如果问题仍然存在，请检查当前预览版。
>  
> 有关技术支持，请参阅[支持选项和社区资源](../information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

## <a name="versions-later-than-141510"></a>高于 1.41.51.0 的版本

如果客户端之一的版本高于 1.41.51.0，则这是用于测试和评估的预览内部版本。  

> [!TIP]
> 由于你的标记是从 Office 365 安全与合规中心、Microsoft 365 安全中心或 Microsoft 365 合规中心发布的，因此是否对评估 Azure 信息保护统一标签客户端感兴趣？ 请参阅 [Azure 信息保护统一标签客户端：版本发布信息](unifiedlabelingclient-version-release-history.md)。

**发布日期**：2019 年 3 月 5 日

此版本包括 RMS 客户端的 MSIPC 1.0.3592.627 版本。

**新功能：**

- Azure 信息保护扫描程序现在从 Azure 门户（而不是使用 PowerShell）进行配置：
    
    - 如果要从扫描程序的正式发布版本升级，则升级过程与以前的版本不同，因此请务必阅读[升级 Azure 信息保护扫描程序](client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。
    
    - 如果是首次安装扫描程序，而不是升级，请参阅[部署 Azure 信息保护扫描程序的预览版本以自动分类和保护文件](../deploy-aip-scanner-preview.md)。

- 如果使用 [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) cmdlet 标记和保护文件，则可以使用 *EnableTracking* 参数将文件注册到文档跟踪站点。 [详细信息](client-admin-guide-document-tracking.md#using-powershell-to-register-labeled-documents-with-the-document-tracking-site)

- 指定配置文件名称时，Azure 信息保护扫描程序现在支持同一 SQL Server 实例上的多个配置数据库。

- 支持以下有助于识别文档和电子邮件中的凭据的敏感信息类型：
    - Azure 服务总线连接字符串
    - Azure IoT 连接字符串
    - Azure 存储帐户
    - Azure IAAS 数据库连接字符串和 Azure SQL 连接字符串
    - Azure Redis 缓存连接字符串
    - Azure SAS
    - SQL Server 连接字符串
    - Azure DocumentDB 身份验证密钥
    - Azure 发布设置密码
    - Azure 存储帐户密钥（通用）

- 新的高级客户端设置，在 Outlook 中实现弹出消息，可以针对正在发送的电子邮件发出警告、进行验证或阻止。 [详细信息](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)

- 新的高级客户端设置，仅当将策略设置配置为不显示自定义权限时才适用：当有一个文件受自定义权限保护时，请在文件资源管理器中显示自定义权限选项，以便用户可以查看和更改它们（如果他们具有更改保护设置的权限）。 [详细信息](client-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)

- Azure 信息保护分析的新高级客户端设置，用于当你已在 Azure 门户中选中此复选框以收集内容匹配项时阻止为一部分用户发送信息类型匹配项。 [详细信息](client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)

**修补程序**：

- 用户将新部分添加到 Word 文档，然后重新标记文档时，将一致地应用新的视觉标记。

- Azure 信息保护客户端正确地删除对受 Rights Management 共享应用程序保护的 PDF 文档的保护。

- 当发送操作系统区域设置为英语时，路径和文件名不会在 Azure 信息保护分析中显示问号 (?) 来代替非 ASCII 字符。

- 为用户定义的权限配置父标签时，PowerShell 和扫描程序会正确应用子标签。

- Azure 信息保护客户端正确显示已由[支持统一标签的客户端](../configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)应用的标签。

- 在文件资源管理器删除保护并右键单击 PowerShell 和扫描程序后，文档在 Office 中正确打开，而没有恢复消息。

- 当使用高级客户端设置设置一个 [Outlook 默认标签](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook)时，可以应用一个具有子标签的父标签，当为用户禁用所有这些子标签时，可使用父标签。

- 如果使用[策略设置](../configure-policy-settings.md) 对于带有附件的电子邮件消息，会应用与这些附件的最高级别分类匹配的标签，并且将具有最高级别分类的标签配置为用户定义的权限，之前的结果是将标签应用于电子邮件，但没有应用保护。 现在：
    - 当标签的用户定义权限包括 Outlook 时（不要转发）：将该标签及其“不要转发”保护应用于电子邮件。
    - 标签的用户定义权限仅适用于 Word、Excel、PowerPoint 和文件资源管理器：请勿应用标签，也不对电子邮件应用任何保护。

**其他变化：**

- 为推荐或自动分类配置的标签不再支持以下敏感信息类型：
    - 欧盟电话号码
    - 欧盟 GPS 坐标

- 由于 Azure 信息保护扫描程序从 Azure 门户配置，因此以下 cmdlet 现已弃用，且不能用于配置数据存储库或文件类型列表：
    - Add-AIPScannerRepository
    - Add-AIPScannerScannedFileTypes
    - Get-AIPScannerRepository
    - Remove-AIPScannerRepository
    - Remove-AIPScannerScannedFileTypes
    - Set-AIPScannerRepository
    - Set-AIPScannerScannedFileTypes

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) 是一个新的 PowerShell cmdlet，用于 Azure 信息保护扫描程序无法从 Azure 门户下载其配置的情况。

- 默认情况下，Azure 信息保护扫描程序不再排除 .zip 文件。 若要检查和标记 .zip 文件，请参阅管理员指南的[检查 .zip 文件](client-admin-guide-file-types.md#to-inspect-zip-files)部分。

- [策略设置](../configure-policy-settings.md)“用户必须提供设置较低分类标签、删除标签或删除保护的理由”不再适用于扫描程序。 在扫描程序配置文件中将设置“重新标记文件”配置为“启用”时，扫描程序会执行这些操作。

## <a name="version-141510"></a>版本 1.41.51.0

**发布日期**：2018 年 11 月 27 日

此版本包括 RMS 客户端的 MSIPC 1.0.3592.627 版本。

**新功能：**

- 现在 Azure 信息保护客户端默认为使用 PDF 加密 ISO 标准保护 PDF 文件。 之前需要使用高级客户端设置启用此支持。
    
    若想要将客户端还原为使用 .ppdf 文件扩展名保护 PDF 文件，请使用相同的[高级客户端设置](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)，但指定“False”。

- Microsoft Ignite 中宣布支持 Azure 信息保护分析功能的[中心报告](../reports-aip.md)。

- Excel 现在还支持使用不同颜色的[视觉标记](../configure-policy-markings.md)。

- 对于现有 S/MIME 部署，新增了以下高级客户端设置：将标签配置为在 Outlook 中自动应用 S/MIME 保护。 [详细信息](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- 新增了高级客户端设置，作为通过编辑注册表来阻止对[已断开连接计算机](client-admin-guide-customizations.md#support-for-disconnected-computers)显示 Azure 信息保护服务登录提示的替代方法。

- 新增了高级客户端设置，用于在使用以下策略设置时[支持子标签的顺序](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)：
    - **对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签**

**修补程序**：

- Azure 信息保护客户端不再对文件资源管理器（右键单击）和 PowerShell 命令排除 .msg、.rar 和 .zip 文件扩展名。 不过，扫描程序仍默认排除这些文件扩展名。 

- 当你使用文件资源管理器（右键单击）时，Azure 信息保护客户端可以取消保护多个文件（选择多个文件或一个包含受保护文件的文件夹）。

- 对于 Excel：
    
    - 如果你在编辑单元格时保存电子表格，系统现在会应用视觉标记。
    
    - Excel 2010：如果是使用共同创作[权限级别](../configure-usage-rights.md#rights-included-in-permissions-levels)来保护电子表格的，现在可以在右键单击文件并选择“分类和保护”时使用“删除标签”按钮。

- 可以[从其他标记解决方案中删除页眉和页脚](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)的高级客户端设置现在支持自定义布局。

**其他变化：**

- 如果扫描程序的日程安排设置为“始终”，两次扫描之间现在有 30 秒延迟。

- 当扫描程序标记的文件已受到保护时，它不再更改该文件的 Rights Management 所有者。

## <a name="version-137190"></a>版本 1.37.19.0

**发布日期**：2018 年 09 月 17 日

此版本包括 RMS 客户端的 MSIPC 1.0.3592.627 版本。

**新增功能**： 

- 通过配置新的[高级客户端配置](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)，支持 PDF 加密 ISO 标准。 此选项设置为“True”时，受保护 PDF 文档的文件扩展名仍为. pdf（而不是更改为 .ppdf），并且可以通过支持此 ISO 标准的 PDF 阅读器打开。 目前，必须指示用户通过使用 Azure 信息保护查看器来手动打开这些受保护的 PDF。 若要帮助用户实现此操作，当他们打开这些受保护的 PDF 之一时，他们将看到含有图标的页面，让他们针对其操作系统进行选择。

- 支持新的敏感信息类型，可帮助对包含个人信息的文档进行分类。 [详细信息](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- 如果已为用户分配 Azure 权限管理（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证，应用保护的标签现在显示在 Office 365 商业版或 Microsoft 365 商业版中的 Office 365 应用内。

- 对 Word、Excel 和 PowerPoint 文件中“Strict Open XML 文档”格式的标签支持。 有关 Open XML 格式的详细信息，请参阅 Office 博客文章[新 Office 中的新文件格式选项](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/)。 

- 支持受 Secure Islands 保护的文件（PDF 和 Office 文档以外的文件）。 例如，受保护的文本和图片文件。 或者，文件扩展名为 .pfile 的文件。 此支持可实现新方案，例如 Azure 信息保护扫描程序可检查这些文件中的敏感信息，并自动为 Azure 信息保护重新标记它们。 [详细信息](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- 用以删除其他标记解决方案已将其应用到文档中的页眉和页脚的新高级客户端设置。 [详细信息](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- 对于 Azure 信息保护扫描程序：

    - 新 cmdlet，[Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)：从之前的正式发布版本 (1.29.5.0) 或更早版本升级后需要运行一次。
    
    - 新 cmdlet，[Get AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)：获取扫描程序服务的当前状态。  
    
    - 新 cmdlet，[Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)：当计划设置为手动时，指示扫描程序开始一次扫描周期。
    
    - 将 ISO 标准用于 PDF 加密时，PDF 文档现在会默认受到保护。
    
    - 对于具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)的客户，支持 SharePoint Server 2010。
    
- 支持 Azure 门户中的新“Azure 信息保护 - 节点(预览)”边栏选项卡，让你能够从一个中心位置管理扫描程序。 部署的扫描程序连接 Azure 后每 5 分钟更新一次信息。 可以从此边栏选项卡执行以下操作：启动扫描程序进行一次性扫描、重新扫描所有文件、查看扫描程序的状态，以及查看扫描速度。

**修复程序**

- 对于 Azure 信息保护扫描程序：
    
    - 对于在 SharePoint 库中受保护的文档，如果未对数据存储库使用 DefaultOwner 参数，则 SharePoint 编辑器值现在用作默认值而不是“创建者”值。
    
    - 扫描程序报告包括 Office 文档的“上次修改者”。
    
    - 如[编辑扫描程序的注册表](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner)一节中所述，现在可以通过在编辑注册表时使用 `*` 通配符来保护所有文件类型。

- 使用快速访问工具栏上的“下一项”和“上一项”箭头图标查看电子邮件时，将显示每封电子邮件的正确标签。

- 如果你使用文件资源管理器、PowerShell 或扫描程序进行分类和保护，系统不会删除或加密 Office 文档元数据。

- 自定义权限支持包含撇号的收件人电子邮件地址。

- 通过打开存储在 SharePoint Online 中的受保护文档来启动此操作时，计算机环境可成功初始化（启动）。

- 当你将客户端用于文件资源管理器、PowerShell 或扫描程序的右键单击时，将阻止对 WebDav 位置的文件进行标记，因为这是不受支持的方案。

- 当你配置“所有文档和电子邮件必须具有标签”的[“策略设置”](../configure-policy-settings.md)时，“删除标签”图标不会在客户端应用（Word、Excel、PowerPoint 和 Outlook）中显示。

**其他更改**：

- 对于 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)：
    
    - Schedule 参数的值不再为“OneTime”、“Continuous”和“Never”，而是“Manual”和“Always”。
        
    - Type 参数已删除，因此在运行 [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration) 时也会从输出中删除该参数。 默认情况下，在首个扫描周期后，只检查新文件或经过修改的文件。 如果之前为了重新扫描所有文件将 Type 参数设置为 Full，现在使用 Reset 参数运行 [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)。 另外，还必须为扫描程序配置人工计划，这就需要使用 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) 将 Schedule 参数设置为 Manual。
    
- 客户端和扫描程序的默认排除列表现在包括 .msg、.rar 和 .zip 文件。 扫描程序还会排除 .rtf 文件。 [详细信息](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- 策略版本更改为 1.4。 [配置断开连接的计算机](client-admin-guide-customizations.md#support-for-disconnected-computers)需要标识版本号。

- “帮助和反馈”对话框中的“给我们发送反馈”链接会被删除。 它将被暂时替换为“报告问题”，默认情况下，会向 Microsoft 发送一封电子邮件。 从 2018 年 12 月起，默认不会显示“报告问题”选项，但可以使用在其中为链接指定 HTTP 字符串的[高级客户端设置](client-admin-guide-customizations.md#add-report-an-issue-for-users)进行添加。 例如，为用户报告问题设置的自定义 Web 页面，或者发送给支持人员的电子邮件地址。 


## <a name="next-steps"></a>后续步骤

有关安装和使用客户端的详细信息： 

- 面向用户：[下载并安装客户端](install-client-app.md)

- 面向管理员：[Azure 信息保护客户端管理员指南](client-admin-guide.md)
