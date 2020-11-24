---
title: Azure 信息保护统一标签客户端管理员指南
description: 适用于企业网络（负责部署适用于 Windows 的 Azure 信息保护统一标签客户端）的管理员的说明和信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2af1d3fad0e831032d8c7f6aa2a312cdfb7a9558
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566184"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Azure 信息保护统一标记客户端管理员指南

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP For Windows And office 版本中的扩展支持](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。*
>
> 说明：[用于 Windows 的 Azure 信息保护统一标记客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

如果你负责企业网络上的 Azure 信息保护统一标签客户端，或者如果你想要获得比 [Azure 信息保护统一标签客户端用户指南](clientv2-user-guide.md)中的更多技术信息，请使用本指南中的信息。 

例如：

- 了解此客户端的不同组件以及是否应安装这些组件

- 如何为用户安装客户端，以及有关先决条件、安装选项和参数及验证检查的信息

- 查找客户端文件和使用情况日志

- 确定客户端支持的文件类型

- 将客户端与 PowerShell 结合用于命令行控制

**是否有本文档未解决的问题？** 请访问 [Azure 信息保护 Yammer 站点](https://www.yammer.com/AskIPTeam)。 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Azure 信息保护统一标签客户端技术概述

Azure 信息保护统一标签客户端包括以下各项：

- Office 外接程序，可在功能区上安装 " **敏感度** " 按钮，使用户能够选择敏感度标签，并提供显示 Azure 信息保护栏以获得更好的标签可见性的选项。

- Windows 文件资源管理器，便于用户将分类标签和保护应用到文件的右键单击选项。

- 一个查看器，可在本机应用程序无法将其打开时显示受保护的文件。

- 一个 PowerShell 模块，用于发现文件中的敏感信息，应用或删除分类标签和保护文件。 
    
    客户端包括用于安装和配置在 Windows Server 上作为服务运行的 [Azure 信息保护扫描程序](../deploy-aip-scanner.md) 的 cmdlet。 此服务允许你发现、分类和保护数据存储中的文件，例如网络共享和 SharePoint 服务器库

- 与保护服务通信的 Rights Management 客户端 (Azure Rights Management) 以加密和保护文件。

除查看器外，Azure 信息保护统一标签客户端不能与直接与保护服务或 Active Directory Rights Management Services 通信的应用程序和服务一起使用。

如果安装了 AD RMS，想迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../migrate-from-ad-rms-to-azure-rms.md)。


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>是否应部署 Azure 信息保护统一标签客户端？

如果要在 Microsoft 365 中使用 [敏感标签](/microsoft-365/compliance/sensitivity-labels) ，请部署 Azure 信息保护统一标签客户端，以下内容适用：

- 你需要通过在 Windows 计算机上的 Office 应用 (Word、Excel、PowerPoint、Outlook) 中选择标签来对 (和) 文档和电子邮件进行分类。

- 想要通过使用文件资源管理器（支持除 Office、多选和文件夹支持的文件类型以外的其他文件类型）对文件进行分类（或保护）。

- 想要通过使用 PowerShell 命令运行对文档进行分类（或保护）的脚本。

- 你需要测试可发现、分类 (的服务，还可以选择保护本地存储的) 文件。

- 想要在本机应用程序显示未安装文件或无法打开这些文档时查看受保护的文档。

示例显示 Azure 信息保护统一标签客户端的 Office 加载项，并显示功能区上的 "新建 **敏感度** " 按钮和可选的 "Azure 信息保护" 栏：

![具有默认策略的 Azure 信息保护栏](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>安装和支持 Azure 信息保护统一标签客户端

可以使用可执行文件或 Windows installer 文件来安装 Azure 信息保护统一标签客户端。 有关每个选项的详细信息和说明，请参阅为 [用户安装 Azure 信息保护统一标签客户端](clientv2-admin-guide-install.md)。  

使用以下部分获取有关安装客户端的支持信息。 

### <a name="installation-checks-and-troubleshooting"></a>安装检查和疑难解答

安装客户端后，请使用“帮助和反馈”选项打开“Microsoft Azure 信息保护”对话框：

- 从 Office 应用程序：在 " **主页** " 选项卡上的 " **敏感度** " 组中，选择 " **敏感度**"，然后选择 " **帮助和反馈**"。

- 在文件资源管理器中：右键单击选择一个/多个文件或文件夹，然后依次选择“**分类和保护**”和“**帮助和反馈**”。 

#### <a name="help-and-feedback-section"></a>“**帮助和反馈**”部分

默认情况下，" **告诉我详细** 信息" 链接转到 [Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection) 网站。 你可以配置自己的 URL 链接，该链接将作为你的标签管理中心中的策略设置之一转到自定义帮助页： Office 365 Security & 相容性中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。

仅当指定 [高级设置](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)时，才会显示 "**报告问题**" 链接。 配置此设置时，指定 HTTP 链接，例如支持人员的电子邮件地址。 

如果要求将这些日志文件发送到 Microsoft 支持部门，则 **导出日志** 会自动收集并附加 Azure 信息保护统一标签客户端的日志文件。 最终用户也可使用此选项将这些日志文件发送给你的支持人员。 或者，可以使用 [AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) PowerShell cmdlet。

**重置设置** 将注销用户，删除当前下载的敏感度标签和标签策略，并重置 Azure Rights Management 服务的用户设置。

> [!NOTE]
> 如果客户端出现技术问题，请参阅 [支持选项和社区资源](../information-support.md#support-options-and-community-resources)。

##### <a name="more-information-about-the-reset-settings-option"></a>有关“重置设置”选项的详细信息

- 不是本地管理员也能使用此选项，并且不会在事件查看器中记录此操作。 

- 除非文件被锁定，否则此操作将删除以下位置中的所有文件。 这些文件包括客户端证书、保护模板、标签管理中心的敏感标签和策略，以及缓存的用户凭据。 不会删除客户端日志文件。
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\mip\\*\<ProcessName.exe\>*
    
    - %LocalAppData%\Microsoft\MSIP\AppDetails
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- 将删除以下注册表项和设置。 如果以下任意注册表项具有自定义值，则必须在重置客户端后重新对其进行配置。
    
    对于企业网络，通常使用组策略配置这些设置，在这种情况下，在计算机上刷新组策略时，将自动重新应用这些设置。 但是，某些设置可能通过脚本一次性配置，或手动配置。 在这些情况下，必须执行其他步骤来重新配置这些设置。 例如，由于要从 AD RMS 迁移并且网络上仍有服务连接点，因此计算机要运行一次脚本才能配置用于重定向到 Azure 信息保护的设置。 重置客户端后，计算机必须再次运行此脚本。
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC

- 当前登录的用户已注销。

#### <a name="client-status-section"></a>“**客户端状态**”部分

使用“**连接身份**”值来确认显示的用户名是否是要用于 Azure 信息保护身份验证的帐户。 此用户名必须与用于 Microsoft 365 或 Azure Active Directory 的帐户相匹配。 此帐户还必须属于在标记管理门户中为敏感度标签配置的 Microsoft 365 租户。

如果需要以不同的用户身份登录到所显示的用户，请参阅 [以其他用户身份登录](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user) 。

使用“**版本**”信息可以确认安装的是哪个版本的客户端。 您可以通过阅读客户端的 [版本信息](unifiedlabelingclient-version-release-history.md) 来检查这是否是最新的发行版和相应的修补程序和新功能。

## <a name="support-for-multiple-languages"></a>支持多种语言

Azure 信息保护统一标签客户端支持 Office 365 支持的相同语言。 有关这些语言的列表，请参阅 Office 中的 [国际可用性](https://products.office.com/business/international-availability) 页面。

对于这些语言，菜单选项、对话框和来自 Azure 信息保护的消息，统一标签客户端以用户的语言显示。 只有单个安装程序可检测语言，因此，无需额外配置即可安装不同语言的 Azure 信息保护统一标签客户端。 

但是，在标签中心配置标签时，不会自动翻译指定的标签名称和说明。 要使用户查看其首选语言的标签，请提供自己的翻译，并通过使用 Office 365 Security & 相容性 PowerShell 并使用 [集标签](/powershell/module/exchange/policy-and-compliance/set-label)的 *LocaleSettings* 参数为标签配置它们。 视觉标记未翻译，且不支持多种语言。

## <a name="post-installation-tasks"></a>安装后任务

安装 Azure 信息保护统一标签客户端之后，请确保为用户提供有关如何标记文档和电子邮件的说明，以及针对特定方案选择哪些标签的指南。 例如：

- 联机用户说明： [Azure 信息保护统一标签用户指南](clientv2-user-guide.md)

- 下载可自定义的用户指南：[Azure 信息保护最终用户采用指南](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

## <a name="installing-the-azure-information-protection-scanner"></a>安装 Azure 信息保护扫描程序

统一标签客户端的扫描程序已正式发布。 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)安装最新版本的统一标签客户端。

如果是首次在计算机上安装扫描程序，请下载并安装此客户端，然后按照 [部署 Azure 信息保护扫描程序中的说明自动对文件进行分类和保护](../deploy-aip-scanner.md)。

如果要从 Azure 信息保护客户端 (经典) 或以前版本的统一标签客户端升级扫描程序，请参阅 [升级 Azure 信息保护扫描程序](#upgrading-the-azure-information-protection-scanner) 部分了解相关说明。

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>升级和维护 Azure 信息保护统一标签客户端

> [!NOTE]
> Azure 信息保护统一标签客户端支持 (经典) 升级 Azure 信息保护客户端，以及从以前版本的 Azure 信息保护统一标签客户端升级。

Azure 信息保护团队会定期更新 Azure 信息保护统一标签客户端，以提供新功能和修补程序。 公告会发布到团队的 [Yammer 网站](https://www.yammer.com/AskIPTeam)。

如果使用 Windows 更新，则 Azure 信息保护的统一标签客户端将自动升级此客户端的常规可用性版本，而不考虑客户端的安装方式。 新客户端版本会在发布后的几周内发布到目录中。

也可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载新版本，手动升级客户端。 然后，安装新版本来升级客户端。 如果要从 Azure 信息保护客户端升级 (经典) ，则必须使用此方法升级预览版。

如果要从 Azure 信息保护客户端 (经典) 在 Windows 7 上进行升级，则在客户端升级过程中，任何 Office 应用程序都将自动重启。 此自动重启不适用于更高版本的操作系统，或者，如果要从统一标签客户端的较旧版本升级。

手动升级时，只有当要更改安装方法时，才需要先卸载旧版本。 例如，从客户端的可执行文件 (.exe) 版本更改为客户端的 Windows 安装程序 (.msi) 版本。 或当需要安装旧版客户端时。 例如，你安装了预览版本用于测试，现在需要恢复到当前的正式发行版。

使用 [版本发行历史记录和支持策略](unifiedlabelingclient-version-release-history.md) 来了解 Azure 信息保护统一标签客户端的支持策略、当前支持的版本以及支持的版本的新增功能和更改功能。 

### <a name="upgrading-the-azure-information-protection-scanner"></a>升级 Azure 信息保护扫描程序

用于升级扫描程序的说明取决于你是从 Azure 信息保护统一标签客户端中的扫描程序的早期版本升级，还是从 Azure 信息保护客户端升级 (经典) 。

#### <a name="to-upgrade-the-scanner-from-an-earlier-version-of-the-unified-labeling-client"></a>从统一标签客户端的早期版本升级扫描程序

1. 在扫描程序计算机上，停止扫描程序服务“Azure 信息保护扫描程序”。

2.    从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载并安装最新版本的统一标签客户端，以便升级 Azure 信息保护统一标签客户端。

3. 在 PowerShell 会话中，使用扫描程序的配置文件运行 Update-AIPScanner 命令。 例如： `Update-AIPScanner –Profile Europe`

4. 重启 Azure 信息保护扫描程序服务“Azure 信息保护扫描程序”。

你现在可以使用 [部署 Azure 信息保护扫描程序中的其余说明自动分类和保护文件，并](../deploy-aip-scanner.md)忽略安装扫描程序的步骤。 由于已经安装了扫描仪，因此没有理由再次安装。

#### <a name="to-upgrade-the-scanner-from-the-classic-client"></a>从经典客户端升级扫描程序

如果当前正在从 Azure 信息保护客户端 (经典) 使用 Azure 信息保护扫描程序，则可以将其升级，以使用从 Office 365 安全 & 符合性中心发布的敏感信息类型和敏感度标签 (或 Microsoft 365 安全中心或 Microsoft 365 符合性中心) 。

如何升级扫描程序取决于当前正在运行的经典客户端版本：

- [从版本1.48.204.0 和更高版本升级](#upgrade-from-the-azure-information-protection-client-classic-version-1482040-and-later-versions-of-this-client)

- [从早于1.48.204.0 的版本升级](#upgrade-from-the-azure-information-protection-client-classic-versions-earlier-than-1482040)

升级会创建一个名为 " **AIPScannerUL_ \<profile_name>**" 的新数据库，并保留以前版本的扫描数据库。 如果确信不需要以前的扫描程序数据库，则可以将其删除。 由于升级会创建一个新数据库，因此在首次运行时，扫描程序会重新扫描所有文件。

##### <a name="upgrade-from-the-azure-information-protection-client-classic-version-1482040-and-later-versions-of-this-client"></a>从此客户端 (经典) 版本1.48.204.0 和更高版本升级 Azure 信息保护客户端

如果使用统一标签客户端的预览版本升级扫描仪，则不需要再次运行这些说明。

1. 在扫描程序计算机上，停止扫描程序服务“Azure 信息保护扫描程序”。

2. 通过从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载和安装统一的标签客户端，升级到 Azure 信息保护统一的标签客户端。

3. 在 PowerShell 会话中，使用扫描程序的配置文件运行 Update-AIPScanner 命令。 例如：`Update-AIPScanner –Profile Europe`。
    
    此步骤创建一个名为的新数据库 **AIPScannerUL_ \<profile_name>**

4. 重启 Azure 信息保护扫描程序服务“Azure 信息保护扫描程序”。

你现在可以使用 [部署 Azure 信息保护扫描程序中的其余说明自动分类和保护文件，并](../deploy-aip-scanner.md)忽略安装扫描程序的步骤。 由于已经安装了扫描仪，因此没有理由再次安装。

##### <a name="upgrade-from-the-azure-information-protection-client-classic-versions-earlier-than-1482040"></a>从 Azure 信息保护客户端升级 (早于1.48.204.0 的经典) 版本

> [!IMPORTANT]
> 对于平滑升级路径，请不要在运行扫描程序的计算机上安装 Azure 信息保护统一标签客户端，作为升级扫描仪的第一步。 请改用以下升级说明。

从版本1.48.204.0 开始，扫描器使用配置文件从 Azure 门户获取其配置设置。 升级扫描程序包括指示扫描器使用此联机配置，为统一标签客户端提供脱机配置，不支持扫描程序的脱机配置。

1. 使用 Azure 门户创建新的扫描程序配置文件，其中包含扫描程序和数据存储库的设置及其所需的任何设置。 有关此步骤的帮助，请参阅从扫描程序部署说明 [在 Azure 门户中配置扫描器](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal) 。

2. 在扫描程序计算机上，停止扫描程序服务“Azure 信息保护扫描程序”。

3. 通过从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载和安装统一的标签客户端，升级到 Azure 信息保护统一的标签客户端。

4. 在 PowerShell 会话中，使用你在步骤 1 中指定的相同配置文件名称运行 Update-AIPScanner 命令。 例如： `Update-AIPScanner –Profile Europe`

5. 重启 Azure 信息保护扫描程序服务“Azure 信息保护扫描程序”。

你现在可以使用 [部署 Azure 信息保护扫描程序中的其余说明自动分类和保护文件，并](../deploy-aip-scanner.md)忽略安装扫描程序的步骤。 由于已经安装了扫描仪，因此没有理由再次安装。

###### <a name="upgrading-in-a-different-order-to-the-recommended-steps"></a>按照建议步骤的不同顺序进行升级

从早于1.48.204.0 的版本升级时，如果在运行 Update-AIPScanner 命令之前未在 Azure 门户中配置扫描仪，则没有指定用于标识升级过程的扫描程序配置设置的配置文件名称。 

在这种情况下，当在 Azure 门户中配置扫描程序时，必须指定与运行 Update-AIPScanner 命令时使用的完全相同的配置文件名称。 如果名称不匹配，则不会为设置配置扫描程序。 

> [!TIP]
> 若要识别具有此错误配置的扫描仪，请使用 Azure 门户中的 " **Azure 信息保护-节点** " 窗格。
>  
> 对于具有 internet 连接的扫描仪，它们使用 Azure 信息保护客户端的正式版本号显示其计算机名称，但没有配置文件名称。 只有版本号为1.41.51.0 的扫描仪才能在此窗格中显示 "配置文件名称"。 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>卸载 Azure 信息保护统一标签客户端

可使用以下任一选项卸载客户端：

- 使用 "控制面板" 卸载程序：单击 **Microsoft Azure 信息保护**  >  **卸载**

- 重新运行可执行文件 (例如 **AzInfoProtection_UL.exe**) ，并从 " **修改安装程序** " 页上单击 " **卸载**"。 

- 使用 **/uninstall** 运行可执行文件。 例如： `AzInfoProtection_UL.exe /uninstall`

## <a name="next-steps"></a>后续步骤
若要安装客户端，请参阅为 [用户安装 Azure 信息保护统一标签客户端](clientv2-admin-guide-install.md)。

若已安装客户端，要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)