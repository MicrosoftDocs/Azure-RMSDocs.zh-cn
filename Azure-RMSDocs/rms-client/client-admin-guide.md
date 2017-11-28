---
title: "Azure 信息保护客户端管理员指南"
description: "面向负责部署适用于 Windows 的 Azure 信息保护客户端的企业网络管理员的说明和信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/20/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: c338fe4258d6d8b20a4d8c285bc821981810b409
ms.sourcegitcommit: f1d0b899e6d79ebef3829f24711f947316bca8ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="azure-information-protection-client-administrator-guide"></a>Azure 信息保护客户端管理员指南

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

如果你负责企业网络上的 Azure 信息保护客户端，或如果你想要获取除了 [Azure 信息保护客户端用户指南](client-user-guide.md)以外的更多技术信息，请使用本指南中的信息。 

例如：

- 了解此客户端的不同组件以及是否应安装这些组件

- 如何为用户安装客户端，以及有关先决条件、安装选项和参数及验证检查的信息

- 如何适应通常需要编辑注册表的自定义配置

- 查找客户端文件和使用情况日志

- 确定客户端支持的文件类型

- 为用户配置和使用文档跟踪站点

- 将客户端与 PowerShell 结合用于命令行控制

**是否有本文档未解决的问题？** 请访问 [Azure 信息保护 Yammer 站点](https://www.yammer.com/AskIPTeam)。 

## <a name="technical-overview-of-the-azure-information-protection-client"></a>Azure 信息保护客户端的技术概述

Azure 信息保护客户端包括以下内容：

- 一个 Office 加载项，可安装 Azure 信息保护栏以便用户选择分类标签；一个功能区上的“保护”按钮，可获取其他选项。 对于 Outlook，在功能区上还可以使用“不转发”按钮。

- Windows 文件资源管理器，便于用户将分类标签和保护应用到文件的右键单击选项。

- 一个查看器，可在本机应用程序无法将其打开时显示受保护的文件。

- 一个 PowerShell 模块，用于从文件应用和删除分类标签和保护。 
    
    此模块包括的 cmdlet 可用于安装和配置 [Azure 信息保护扫描程序](../deploy-use/deploy-aip-scanner.md)（当前为预览版），该扫描程序在 Windows Server 上作为服务运行。 借助此服务，可发现和保护数据存储（例如，网络共享和 SharePoint Server 库）中的文件并对其进行分类。

- 权限管理客户端，可与 Azure 权限管理 (Azure RMS) 或 Active Directory Rights Management Services (AD RMS) 进行通信。

Azure 信息保护客户端最适合用于其 Azure 服务；Azure 信息保护及其数据保护服务（Azure 权限管理）。 不过，Azure 信息保护客户端也可用于本地版本的 Rights Management ( AD RMS)，只是存在一些限制。 有关 Azure 信息保护和 AD RMS 所支持功能的全面比较，请参阅[比较 Azure信息保护和 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。 

如果安装了 AD RMS，想迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。


## <a name="should-you-deploy-the-azure-information-protection-client"></a>你是否应该部署 Azure 信息保护客户端？

如果以下任一项适用，请部署 Azure 信息保护客户端：

- 想要通过从 Office 应用程序（Word、Excel、PowerPoint、Outlook）中选择标签对文档和电子邮件进行分类（或保护）。

- 想要通过使用文件资源管理器（支持其他文件类型、多选和文件夹）对文档和电子邮件进行分类（或保护）。

- 想要通过使用 PowerShell 命令运行对文档进行分类（或保护）的脚本。

- 想要运行一项服务来发现（或保护）存储在本地的文件并对其进行分类。 此扫描程序服务当前以预览版提供。

- 想要在本机应用程序显示未安装文件或无法打开这些文档时查看受保护的文档。

- 只想通过使用文件资源管理器或使用 PowerShell 命令保护文件。

- 想要用户和管理员能够跟踪和撤销受保护的文档。

- 想要从文件和容器（取消保护）批量删除加密，以进行数据恢复。

- 运行 Office 2010 并且想要通过使用 Azure 权限管理服务保护文档和电子邮件。

示例显示了 Office 应用程序中的 Azure 信息保护客户端加载项、组织的分类标签，以及功能区上新的“保护”按钮：

![具有默认策略的 Azure 信息保护栏](../media/word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-client"></a>安装和支持 Azure 信息保护客户端

可通过使用 Windows 更新、可执行文件或 Windows Installer 文件来安装 Azure 信息保护客户端。 如需详细了解每个选项和说明，请参阅[为用户安装 Azure 信息保护客户端](client-admin-guide-install.md)。  

使用以下部分获取有关安装客户端的支持信息。 

### <a name="installation-checks-and-troubleshooting"></a>安装检查和疑难解答

安装客户端后，请使用“帮助和反馈”选项打开“Microsoft Azure 信息保护”对话框：

- 在 Office 应用程序中：在“**开始**”选项卡上的“**保护**”组中，依次选择“**保护**”和“**帮助和反馈**”。

- 在文件资源管理器中：右键单击选择一个/多个文件或文件夹，然后依次选择“**分类和保护**”和“**帮助和反馈**”。 

#### <a name="help-and-feedback-section"></a>“**帮助和反馈**”部分

默认情况下，“提供详细信息”链接转到 [Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection)网站，但也可以根据 Azure 信息保护策略中的一项[策略设置](../deploy-use/configure-policy-settings.md)，将其配置为转到自定义 URL。

使用“**给我们发送反馈**”链接可以向信息保护团队发送建议或请求。 对于技术支持，请勿将此选项，而是参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)。 

“导出日志”自动收集并附加 Azure 信息保护客户端的日志文件，如果必须将日志文件发送给 Microsoft 支持人员的话。 最终用户也可以使用此选项，将这些日志文件发送给你的支持人员。

“重置设置”会注销用户、删除当前下载的 Azure 信息保护策略，并重置 Azure Rights Management 服务的用户设置。

##### <a name="more-information-about-the-reset-settings-option"></a>有关“重置设置”选项的详细信息

- 不是本地管理员也能使用此选项，并且不会在事件查看器中记录此操作。 

- 除非文件被锁定，否则此操作将删除以下位置中的所有文件。 这些文件包括客户端证书、Rights Management 模板、Azure 信息保护策略和缓存的用户凭据。 不会删除客户端日志文件。
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- 将删除以下注册表项和设置。 如果以下任意注册表项具有自定义值，则必须在重置客户端后重新对其进行配置。 
    
    对于企业网络，通常使用组策略配置这些设置，在这种情况下，在计算机上刷新组策略时，将自动重新应用这些设置。 但是，某些设置可能通过脚本一次性配置，或手动配置。 在这些情况下，必须执行其他步骤来重新配置这些设置。 例如，由于要从 AD RMS 迁移并且网络上仍有服务连接点，因此计算机要运行一次脚本才能配置用于重定向到 Azure 信息保护的设置。 重置客户端后，计算机必须再次运行此脚本。
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- 当前登录的用户已注销。

#### <a name="client-status-section"></a>“**客户端状态**”部分

使用“**连接身份**”值来确认显示的用户名是否是要用于 Azure 信息保护身份验证的帐户。 此用户名必须与用于 Office 365 或 Azure Active Directory 的帐户匹配。 帐户还必须属于为 Azure 信息保护配置的租户。

如果需要以与显示用户名不同的用户身份登录，请参阅[以其他用户身份登录](client-admin-guide-customizations.md#sign-in-as-a-different-user)自定义项。

“最后连接”显示客户端最后一次连接到组织的 Azure 信息保护服务的时间。 可以将此信息与信息保护策略安装日期和时间结合，以确认 Azure 信息保护策略上次安装或更新的时间。 当客户端连接服务时，如果它发现与其当前策略有差异，则会自动下载最新策略，频率同样也是每 24 小时。 如果在显示时间后完成策略更改，关闭并重新打开 Office 应用程序。

如果看到**此客户端未获许可使用 Office Professional Plus**：Azure 信息保护客户端检测到安装的 Office 版本不支持应用 Rights Management 保护。 执行此检测时，便会发现应用保护的标签未显示在 Azure 信息保护栏上。

使用“**版本**”信息可以确认安装的是哪个版本的客户端。 可以单击“**最近更新**”链接来查看客户端的“[版本发行历史记录](client-version-release-history.md)”，检查是否为最新发行版本以及相应的修补程序和新功能。

## <a name="support-for-multiple-languages"></a>支持多种语言

Azure 信息保护客户端支持 Office 365 支持的同种语言。 有关这些语言的列表，请参阅 Office [国际可用性](https://products.office.com/business/international-availability)页面的 Office 365、Exchange Online Protection 和 Power BI 部分。

对于这些语言，Azure 信息保护客户端中的菜单选项、对话框和消息将以用户的语言显示。 由于有一个安装程序可检测语言，因此不需要进行额外配置即可安装不同语言的 Azure 信息保护客户端。 

但是，在 Azure 信息保护策略中配置标签时，不会自动翻译指定的标签名称和说明。 从 2017 年 8 月 30 日起，当前的[默认政策](../deploy-use/configure-policy-default.md)包含对部分语言的支持。 若要以用户首选语言向其显示标签，必须提供你的翻译并将 Azure 信息保护策略配置为使用这些翻译。 有关详细信息，请参阅[如何在 Azure 信息保护中配置不同语言的标签](../deploy-use/configure-policy-languages.md)。 视觉标记未翻译，且不支持多种语言。

## <a name="uninstalling-the-azure-information-protection-client"></a>卸载 Azure 信息保护客户端

可使用以下任一选项卸载客户端：

- 使用控制面板卸载程序：单击“**Microsoft Azure 信息保护** > **卸载**”

- 重新运行可执行文件（如 **AzInfoProtection.exe**），并从“修改安装程序”页上，单击“卸载”。 

- 使用 **/uninstall** 运行可执行文件。 例如： `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>后续步骤
要安装客户端，请参阅[为用户安装 Azure 信息保护客户端](client-admin-guide-install.md)。

若已安装客户端，要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
