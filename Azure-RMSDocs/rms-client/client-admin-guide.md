---
title: "Azure 信息保护客户端管理员指南"
description: "面向负责部署适用于 Windows 的 Azure 信息保护客户端的企业网络管理员的说明和信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/10/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: e3910ecc2bed3f95660be86b6139e568815f24a0
ms.sourcegitcommit: ea03477312b64c0a846701e46d991fe2c85b3a1f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2017
---
# <a name="azure-information-protection-client-administrator-guide"></a>Azure 信息保护客户端管理员指南

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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

- 一个 Office 外接程序，可安装 Azure 信息保护栏以便用户选择分类标签；一个功能区上的“保护”按钮，可获取其他选项。

- Windows 文件资源管理器，便于用户将分类标签和保护应用到文件的右键单击选项。

- 一个查看器，可在本机应用程序无法将其打开时显示受保护的文件。

- 一个 PowerShell 模块，用于从文件应用和删除分类标签和保护。

- 权限管理客户端，可与 Azure 权限管理 (Azure RMS) 或 Active Directory Rights Management Services (AD RMS) 进行通信。

Azure 信息保护客户端最适合用于其 Azure 服务；Azure 信息保护及其数据保护服务（Azure 权限管理）。 不过，Azure 信息保护客户端也可用于本地版本的 Rights Management ( AD RMS)，只是存在一些限制。 有关 Azure 信息保护和 AD RMS 所支持功能的全面比较，请参阅[比较 Azure信息保护和 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。 

如果安装了 AD RMS，想迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。


## <a name="should-you-deploy-the-azure-information-protection-client"></a>你是否应该部署 Azure 信息保护客户端？

如果以下任一项适用，请部署 Azure 信息保护客户端：

- 想要通过从 Office 应用程序（Word、Excel、PowerPoint、Outlook）中选择标签对文档和电子邮件进行分类（或保护）。

- 想要通过使用文件资源管理器（支持其他文件类型、多选和文件夹）对文档和电子邮件进行分类（或保护）。

- 想要通过使用 PowerShell 命令运行对文档进行分类（或保护）的脚本。

- 想要在本机应用程序显示未安装文件或无法打开这些文档时查看受保护的文档。

- 只想通过使用文件资源管理器或使用 PowerShell 命令保护文件。

- 想要用户和管理员能够跟踪和撤销受保护的文档。

- 想要从文件和容器（取消保护）批量删除加密，以进行数据恢复。

- 运行 Office 2010 并且想要通过使用 Azure 权限管理服务保护文档和电子邮件。

示例显示了 Office 应用程序中的 Azure 信息保护客户端外接程序、组织的分类标签，以及功能区上的新“保护”按钮：

![具有默认策略的 Azure 信息保护栏](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>如何为用户安装 Azure 信息保护客户端

安装客户端之前，请检查计算机是否具有 Azure 信息保护所需的操作系统版本和应用程序：[Azure 信息保护要求](../get-started/requirements-azure-rms.md)。 

检查 Azure 信息保护客户端可能需要的其他先决条件。

### <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的其他先决条件

- Microsoft .NET Framework 4.6.2
    
    默认情况下，完整安装的 Azure 信息保护客户端要求至少有 Microsoft .NET Framework 4.6.2；如果没有，那么安装程序会尝试下载并安装此系统必备。 在客户端安装过程中安装此必备项后，将重启计算机。 可以使用[自定义安装参数](#more-information-about-the-downgradedotnetrequirement-installation-parameter)忽略此系统必备，尽管不建议这样做。

- Microsoft .NET Framework 4.5.2
    
    如果单独安装 Azure 信息保护查看器，则要求的最低版本为 Microsoft .NET Framework 4.5.2，如果缺少此版本，安装程序会尝试下载并安装它。

- Windows PowerShell 版本 4.0
    
    客户端的 PowerShell 模块需要 Windows PowerShell 4.0 版本，此版本可能需要在旧版操作系统上安装。 有关详细信息，请参阅[如何：安装 Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)。 安装程序不会为你检查或安装此必备项。 若要确认正在运行的 Windows PowerShell 的版本，请在 PowerShell 会话中键入 `$PSVersionTable`。

- Microsoft Online Services 登录助手 7.250.4303.0
    
    运行 Office 2010 的计算机需要安装 Microsoft Online Services 登录助手版本 7.250.4303.0。 此版本包含在客户端安装中。 如果已安装登录助手的更高版本，请先将其卸载，然后再安装 Azure 信息保护客户端。 例如，通过使用“控制面板” > “程序和功能” > “卸载或更改程序”来检查版本和卸载登录助手。

- KB 2533623
    
    运行 Windows 7 Service Pack 1 的计算机需要 KB 2533623。 有关此更新的详细信息，请参阅 [Microsoft 安全公告：不安全的库加载可能允许远程执行代码](https://support.microsoft.com/en-us/kb/2533623)。 可以直接安装此更新，也可以使用为你安装的另一个更新代替此更新。
    
    如果需要此更新且未安装，则客户端安装将警告你必须安装此更新。 可以在安装客户端后安装此更新，但某些操作将被阻止并再次显示该信息。  

> [!IMPORTANT]
> 安装 Azure 信息保护客户端需要本地管理权限。

### <a name="options-to-install-the-azure-information-protection-client-for-users"></a>为用户安装 Azure 信息保护客户端的选项

为用户安装客户端有三个选项：

**Windows 更新**：Microsoft 更新目录中包含 Azure 信息保护客户端，因此可以利用使用该目录的任何软件更新服务来安装和更新此客户端。

**运行客户端的可执行文件 (.exe) 版本**：建议的安装方式，以交互方式或无提示方式运行。 此方法非常灵活，建议使用，因为安装程序会检查多个必备组件，并且可以自动安装缺少的必备组件。 [说明](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

**部署客户端的 Windows Installer (.msi) 版本**：仅支持使用集中部署机制的无提示安装，如组策略、Configuration Manager 和 Microsoft Intune。 对于由 Intune 和移动设备管理 (MDM) 管理的 Windows 10 电脑而言，这是必要的方法，因为这些计算机不支持安装可执行文件。 但是，使用此安装方法时，必须手动检查并安装或卸载可执行文件的安装程序为每台计算机执行时依赖的软件。 [说明](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>使用可执行安装程序安装 Azure 信息保护客户端

如果在使用 Microsoft Update 目录，或使用 Intune 之类的集中部署方法部署 .msi，请使用以下说明安装客户端。

1. 从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载可执行版本 Azure 信息保护客户端。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 

2. 对于默认安装，只需运行可执行文件，例如 **AzInfoProtection.exe**。 但是，若要查看安装选项，请先使用 **/help** 运行可执行文件：`AzInfoProtection.exe /help`

    有关无提示安装客户端的示例：`AzInfoProtection.exe /quiet`
    
    有关无提示仅安装 PowerShell cmdlet 的示例：`AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    帮助屏幕中未列出的其他参数：
    
    - **ServiceLocation**：如果要在运行 Office 2010 的计算机上安装客户端，且你的用户不是其计算机上的本地管理员，或者你不希望系统会向他们发出提示，请使用此参数。 [详细信息](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**：使用此参数可以不遵守一定要有 Microsoft Framework .NET 版本 4.6.2 的要求。 [详细信息](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0**：使用此参数来禁用安装选项“通过向 Microsoft 发送使用情况统计信息来帮助改进 Azure 信息保护”。 
    
3. 如果以交互方式安装，并且无法连接到 Office 365 或 Azure Active Directory，但出于演示目的，想要通过本地策略看到和体验 Azure 信息保护客户端，请选择此选项安装**演示策略**。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。
    
4. 若要完成安装： 

    - 如果计算机运行的是 Office 2010，请重新启动计算机。 
        
        如果未使用 ServiceLocation 参数安装客户端，首次打开一个使用 Azure 信息保护栏的 Office 应用程序（如 Word）时，必须确认是否有任何要求首次使用时更新注册表的提示。 利用[服务发现](../rms-client/client-deployment-notes.md#rms-service-discovery)功能填充注册表项。 
    
    - 对于其他版本的 Office，请重启任一 Office 应用程序和文件管理器的所有实例。 
        
5. 可以查看默认在 %temp% 文件夹中创建的安装日志文件来确认安装是否成功。 可以使用 **/log** 安装参数更改此位置。 
 
    此文件具有以下命名格式：`Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例如：**Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    在此日志文件中搜索以下字符串：**Product: Microsoft Azure Information Protection -- Installation completed successfully**（产品：Microsoft Azure 信息保护 - 已成功完成安装）。 如果安装失败，此日志文件包含有助于标识并解决任何问题的详细信息。

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>详细了解 ServiceLocation 安装参数

如果为具有 Office 2010 的用户安装客户端，并且他们没有本地管理权限，请指定用于 Azure 权限管理服务的 ServiceLocation 参数和 URL。 此参数和值将创建和设置以下注册表项：

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

使用以下过程标识要为 ServiceLocation 参数指定的值。 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>若要标识要为 ServiceLocation 参数指定的值

1. 对于 PowerShell 会话，请先运行 [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice)，并指定要连接到 Azure 权限管理服务的管理员凭据。 然后运行 [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration)。 
 
    如果尚未安装适用于 Azure 权限管理服务的 Windows PowerShell 模块，请参阅[安装适用于 Azure 权限管理的 Windows PowerShell](../deploy-use/install-powershell.md)。

2. 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

    示例：**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. 在该值中，将 **/_wmcs/licensing** 从此字符串删除。 例如：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    剩余字符串就是要为 ServiceLocation 参数指定的值。

有关为 Office 2010 和 Azure RMS 无提示安装客户端的示例：`AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>详细了解 DowngradeDotNetRequirement 安装参数

为了使用 Windows 更新支持自动更新，并与 Office 应用程序可靠集成，Azure 信息保护客户端使用 Microsoft .NET Framework 版本 4.6.2。 默认情况下，安装程序会检查是否有此版本；如果没有，则会尝试进行安装。 然后，安装程序要求重启计算机。

如果安装这一 Microsoft .NET Framework 更高版本不可行，可以在安装客户端时使用 **DowngradeDotNetRequirement=True** 参数和值，这样就可以在已安装 Microsoft .NET Framework 版本 4.5.1 的情况下忽略这项要求。

例如： `AzInfoProtection.exe DowngradeDotNetRequirement=True`

建议谨慎使用此参数。还请注意，将 Azure 信息保护客户端与旧版 Microsoft .NET Framework 结合使用时，Office 应用程序存在报告的尚未解决的问题。 如果确实遇到了尚未解决的问题，请先升级到建议的版本，然后再尝试其他故障排除解决方案。 

此外，还请注意，如果使用 Windows 更新来不断更新 Azure 信息保护客户端，还需要使用另一软件部署机制，才能将客户端升级到更高版本。

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>使用 .msi 安装程序安装 Azure 信息保护客户端

对于集中部署，请使用以下特定于 Azure信息保护客户端 .msi 安装版本的信息。 

如果将 Intune 用于软件部署方法，请将这些说明与[使用 Microsoft Intune 添加应用](/intune/deploy-use/add-apps)一起使用。

1. 从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载 Azure 信息保护客户端的 .msi 版本。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 

2. 对于运行 .msi 文件的每台计算机，必须确保以下软件依赖项已经就绪。 例如，将这些依赖项与客户端 .msi 版本一起打包，或只部署到满足这些依赖关系的计算机上：
    
    |Office 版本|操作系统|软件|操作|
    |--------------------|--------------|----------------|---------------------|
    |Office 2013|所有支持的版本|[KB 3054941](https://www.microsoft.com/en-us/download/details.aspx?id=49337)<br /><br /> 文件名中包含的版本号：v3|安装|
    |Office 2010|所有支持的版本|[Microsoft Online Services 登录助手](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> 版本：2.1|安装|
    |Office 2010|Windows 8.1 和 Windows Server 2012 R2|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB 2843630 或 KB 2919355，则进行安装|
    |Office 2010|Windows 8 和 Windows Server 2012|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|安装|
    |Office 2010|Windows 7|[KB 2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB 3125574，则进行安装|
    |不适用|Windows 7|KB 2627273 <br /><br /> 文件名中包含的版本号：v4|卸载|

3. 对于默认安装，将 .msi 与 /quiet/ 一起运行，例如，`AzInfoProtection.msi /quiet`。 但是，你可能需要指定[可执行安装程序说明](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)中记录的其他安装参数。  

## <a name="additional-checks-and-troubleshooting"></a>其他检查和故障排除

使用“**帮助和反馈**”选项打开“**Microsoft Azure 信息保护**”对话框：

- 在 Office 应用程序中：在“**开始**”选项卡上的“**保护**”组中，依次选择“**保护**”和“**帮助和反馈**”。

- 在文件资源管理器中：右键单击选择一个/多个文件或文件夹，然后依次选择“**分类和保护**”和“**帮助和反馈**”。 

### <a name="help-and-feedback-section"></a>“**帮助和反馈**”部分

默认情况下，“提供详细信息”链接转到 [Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection)网站，但也可以根据 Azure 信息保护策略中的一项[策略设置](../deploy-use/configure-policy-settings.md)，将其配置为转到自定义 URL。

使用“**给我们发送反馈**”链接可以向信息保护团队发送建议或请求。 对于技术支持，请勿将此选项，而是参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)。 

“导出日志”自动收集并附加 Azure 信息保护客户端的日志文件，如果必须将日志文件发送给 Microsoft 支持人员的话。 最终用户也可以使用此选项，将这些日志文件发送给你的支持人员。

若要获取诊断信息并重置客户端，请选择“**运行诊断**”。 诊断测试完成后，单击“**复制结果**”，将信息粘贴到电子邮件中，以便你可以发送给 Microsoft 支持人员，或者最终用户可以发送给你的支持人员。 测试完成后，还可以重置客户端。

有关“重置”选项的详细信息：

- 不是本地管理员也能使用此选项，并且不会在事件查看器中记录此操作。 

- 除非文件被锁定，否则此操作将删除 **%localappdata%\Microsoft\MSIPC** 中的所有文件，该路径用于存储客户端证书和权限管理模板。 此操作不会删除 Azure 信息保护策略或客户端日志文件，也不会注销用户。

- 会删除以下注册表项和设置：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**。 如果配置了此注册表项的设置，则必须在重置客户端后重新配置注册表设置。 例如，由于要从 AD RMS 迁移并且网络上仍有服务连接点，因此配置了用于重定向到 Azure 信息保护租户的设置。

- 重置客户端后，必须重新初始化用户环境，下载客户端证书和最新模板。 为了执行此操作，请关闭 Office 的所有实例，然后重新启动 Office 应用程序。 此操作还检查是否已下载最新的 Azure 信息保护策略。 完成此操作之前，请勿再次运行诊断测试。


### <a name="client-status-section"></a>“**客户端状态**”部分

使用“**连接身份**”值来确认显示的用户名是否是要用于 Azure 信息保护身份验证的帐户。 此用户名必须与用于 Office 365 或 Azure Active Directory 的帐户匹配。 帐户还必须属于为 Azure 信息保护配置的租户。

如果需要以与显示用户名不同的用户身份登录，请参阅[以其他用户身份登录](client-admin-guide-customizations.md#sign-in-as-a-different-user)自定义项。

“最后连接”显示客户端最后一次连接到组织的 Azure 信息保护服务的时间。 可以将此信息与信息保护策略安装日期和时间结合，以确认 Azure 信息保护策略上次安装或更新的时间。 当客户端连接服务时，如果它发现与其当前策略有差异，则会自动下载最新策略，频率同样也是每 24 小时。 如果在显示时间后完成策略更改，关闭并重新打开 Office 应用程序。

如果看到**此客户端未获许可使用 Office Professional Plus**：Azure 信息保护客户端检测到安装的 Office 版本不支持应用 Rights Management 保护。 执行此检测时，便会发现应用保护的标签未显示在 Azure 信息保护栏上。

使用“**版本**”信息可以确认安装的是哪个版本的客户端。 可以单击“**最近更新**”链接来查看客户端的“[版本发行历史记录](client-version-release-history.md)”，检查是否为最新发行版本以及相应的修补程序和新功能。


## <a name="to-uninstall-the-azure-information-protection-client"></a>卸载 Azure 信息保护客户端

可以使用以下任何选项：

- 使用控制面板卸载程序：单击“**Microsoft Azure 信息保护** > **卸载**”

- 重新运行可执行文件（如 **AzInfoProtection.exe**），并从“修改安装程序”页上，单击“卸载”。 

- 使用 **/uninstall** 运行可执行文件。 例如： `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>后续步骤
现在你已安装 Azure 信息保护客户端，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
