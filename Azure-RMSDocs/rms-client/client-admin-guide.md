---
title: "Azure 信息保护客户端管理员指南"
description: "面向负责部署适用于 Windows 的 Azure 信息保护客户端的企业网络管理员的说明和信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: d442a9540243cd020b885f7dc2c13d999bbad868
ms.sourcegitcommit: 7b773ca5bf1abf30e527c34717ecb2dc96f88033
translationtype: HT
---
# <a name="azure-information-protection-client-administrator-guide"></a>Azure 信息保护客户端管理员指南

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7


如果你负责企业网络上的 Azure 信息保护客户端，或如果你想要获取除了 [Azure 信息保护客户端用户指南](client-user-guide.md)以外的更多技术信息，请使用以下信息。

Azure 信息保护客户端包括以下内容：

- 一个 Office 外接程序，可安装 Azure 信息保护栏以便用户选择分类标签；一个功能区上的“保护”按钮，可获取其他选项。

- Windows 文件资源管理器，便于用户将分类标签和保护应用到文件的右键单击选项。

- 一个查看器，可在本机应用程序无法将其打开时显示受保护的文件。

- 一个 PowerShell 模块，用于从文件应用和删除分类标签和保护。

- 权限管理客户端，可与 Azure 权限管理 (Azure RMS) 或 Active Directory Rights Management Services (AD RMS) 进行通信。

Azure 信息保护客户端最适合用于其 Azure 服务；Azure 信息保护及其数据保护服务（Azure 权限管理）。 不过，Azure 信息保护客户端也可用于本地版本的 Rights Management ( AD RMS)，只是存在一些限制。 有关 Azure 信息保护和 AD RMS 所支持功能的全面比较，请参阅[比较 Azure信息保护和 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。 

如果安装了 AD RMS，想迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

**是否有本文档未回答的问题？** 请访问 [Azure 信息保护 Yammer 站点](https://www.yammer.com/AskIPTeam)。 


## <a name="should-you-deploy-the-azure-information-protection-client"></a>你是否应该部署 Azure 信息保护客户端？

如果以下任一项适用，请部署 Azure 信息保护客户端：

- 想要通过从 Office 应用程序（Word、Excel、PowerPoint、Outlook）中选择标签对文档和电子邮件进行分类（或保护）。

- 想要通过使用文件资源管理器（支持其他文件类型、多选和文件夹）对文档和电子邮件进行分类（或保护）。

- 想要通过使用 PowerShell 命令运行对文档进行分类（或保护）的脚本。

- 想要在本机应用程序显示未安装文件或无法打开这些文档时查看受保护的文档。

- 只想通过使用文件资源管理器或使用 Powershell 命令保护文件。

- 想要用户和管理员能够跟踪和撤销受保护的文档。

- 想要从文件和容器（取消保护）批量删除加密，以进行数据恢复。

- 运行 Office 2010 并且想要通过使用 Azure 权限管理服务保护文档和电子邮件。

示例显示了 Office 应用程序中的 Azure 信息保护客户端外接程序、组织的分类标签，以及功能区上的新“保护”按钮：

![具有默认策略的 Azure 信息保护栏](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>如何为用户安装 Azure 信息保护客户端

安装客户端之前，请检查是否具有 Azure 信息保护客户端所需的操作系统版本和应用程序：[Azure 信息保护要求](../get-started/requirements-azure-rms.md)。 

Azure 信息保护客户端的其他先决条件：

- 默认情况下，完整安装的 Azure 信息保护客户端要求至少有 Microsoft .NET Framework 4.6.2；如果没有，那么安装程序会尝试下载并安装此系统必备。 在客户端安装过程中安装此必备项后，将重启计算机。 可以使用自定义安装参数忽略此系统必备，尽管不建议这样做。

- 如果单独安装 Azure 信息保护查看器，则要求的最低版本为 Microsoft .NET Framework 4.5.2，如果缺少此版本，安装程序会尝试下载并安装它。

- PowerShell 模块需要 Windows PowerShell 4.0 版本，此版本可能需要在旧版操作系统上安装。 有关详细信息，请参阅[如何：安装 Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)。 安装程序不会为你检查或安装此必备项。 若要确认正在运行的 Windows PowerShell 的版本，请在 PowerShell 会话中键入 **$PSVersionTable**。

- 运行 Windows 7 Service Pack 1 的计算机需要 KB 2533623。 有关此更新的详细信息，请参阅 [Microsoft 安全公告：不安全的库加载可能允许远程执行代码](https://support.microsoft.com/en-us/kb/2533623)。 可以直接安装此更新，也可以使用为你安装的另一个更新代替此更新。
    
    如果需要此更新且未安装，则客户端安装将警告你必须安装此更新。 可以在安装客户端后安装此更新，但某些操作将被阻止并再次显示该信息。  

> [!NOTE]
> 安装需要本地管理权限。

Microsoft 更新目录中也包含 Azure 信息保护客户端，因此可以利用使用该目录的任何软件更新服务来安装和更新客户端。 

1. 从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)(#microsoft-下载中心) 下载 Azure 信息保护客户端。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 

2. 对于默认安装，只需运行可执行文件，例如 **AzInfoProtection.exe**。 但是，若要查看安装选项，请先使用 **/help** 运行可执行文件：`AzInfoProtection.exe /help`

    有关无提示安装客户端的示例：`AzInfoProtection.exe /quiet`
    
    有关无提示仅安装 PowerShell cmdlet 的示例：`AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    帮助屏幕中未列出的其他参数：
    
    - **ServiceLocation**：如果要在运行 Office 2010 的计算机上安装客户端，且你的用户不是其计算机上的本地管理员，或者你不希望系统会向他们发出提示，请使用此参数。 [详细信息](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**：使用此参数可以不遵守一定要有 Microsoft Framework .NET 版本 4.6.2 的要求。 [详细信息](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

3. 如果以交互方式安装，并且无法连接到 Office 365 或 Azure Active Directory，但出于演示目的，想要通过本地策略看到和体验 Azure 信息保护客户端，请选择此选项安装**演示策略**。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。
    
4. 若要完成安装： 

    - 如果计算机运行的是 Office 2010，请重新启动计算机。 
        
        如果未使用 ServiceLocation 参数安装客户端，首次打开一个使用 Azure 信息保护栏的 Office 应用程序（如 Word）时，必须确认是否有任何要求首次使用时更新注册表的提示。 利用[服务发现](../rms-client/client-deployment-notes.md#rms-service-discovery)功能填充注册表项。 
    
    - 对于其他版本的 Office，请重启任一 Office 应用程序和文件管理器的所有实例。 
        
5. 可以查看默认在 %temp% 文件夹中创建的安装日志文件来确认安装是否成功。 可以使用 **/log** 安装参数更改此位置。 
 
    此文件具有以下命名格式：`Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例如：**Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    在此日志文件中搜索以下字符串：**Product: Microsoft Azure Information Protection -- Installation completed successfully**（产品：Microsoft Azure 信息保护 - 已成功完成安装）。 如果安装失败，此日志文件包含有助于标识并解决任何问题的详细信息。

### <a name="more-information-about-the-servicelocation-installation-parameter"></a>详细了解 ServiceLocation 安装参数

如果为具有 Office 2010 的用户安装客户端，并且他们没有本地管理权限，请指定用于 Azure 权限管理服务的 ServiceLocation 参数和 URL。 此参数和值将创建和设置以下注册表项：

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

使用以下过程标识要为 ServiceLocation 参数指定的值。 

#### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>若要标识要为 ServiceLocation 参数指定的值

1. 对于 PowerShell 会话，请先运行 [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice)，并指定要连接到 Azure 权限管理服务的管理员凭据。 然后运行 [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration)。 
 
    如果尚未安装适用于 Azure 权限管理服务的 Windows PowerShell 模块，请参阅[安装适用于 Azure 权限管理的 Windows PowerShell](../deploy-use/install-powershell.md)。

2. 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

    示例：**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. 在该值中，将 **/_wmcs/licensing** 从此字符串删除。 例如：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    剩余字符串就是要为 ServiceLocation 参数指定的值。

有关为 Office 2010 和 Azure RMS 无提示安装客户端的示例：`AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>详细了解 DowngradeDotNetRequirement 安装参数

为了使用 Windows 更新支持自动更新，并与 Office 应用程序可靠集成，Azure 信息保护客户端使用 Microsoft .NET Framework 版本 4.6.2。 默认情况下，安装程序会检查是否有此版本；如果没有，则会尝试进行安装。 然后，安装程序要求重启计算机。

如果安装这一 Microsoft .NET Framework 更高版本不可行，可以在安装客户端时使用 **DowngradeDotNetRequirement=True** 参数和值，这样就可以在已安装 Microsoft .NET Framework 版本 4.5.1 的情况下忽略这项要求。

例如： `AzInfoProtection.exe DowngradeDotNetRequirement=True`

建议谨慎使用此参数。还请注意，将 Azure 信息保护客户端与旧版 Microsoft .NET Framework 结合使用时，Office 应用程序存在报告的尚未解决的问题。 如果确实遇到了尚未解决的问题，请先升级到建议的版本，然后再尝试其他故障排除解决方案。 

此外，还请注意，如果使用 Windows 更新来不断更新 Azure 信息保护客户端，还需要使用另一软件部署机制，才能将客户端升级到更高版本。

## <a name="additional-checks-and-troubleshooting"></a>其他检查和故障排除

使用“**帮助和反馈**”选项打开“**Microsoft Azure 信息保护**”对话框：

- 在 Office 应用程序中：在“**开始**”选项卡上的“**保护**”组中，依次选择“**保护**”和“**帮助和反馈**”。

- 在文件资源管理器中：右键单击选择一个/多个文件或文件夹，然后依次选择“**分类和保护**”和“**帮助和反馈**”。 

### <a name="help-and-feedback-section"></a>“**帮助和反馈**”部分

默认情况下，“**提供详细信息**”链接转到 [Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection)网站，但也可以根据 Azure 信息保护策略中的一项[策略设置](../deploy-use/configure-policy-settings.md)，将其配置为转到自定义 URL。

使用“**给我们发送反馈**”链接可以向信息保护团队发送建议或请求。 对于技术支持，请勿将此选项，而是参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)。 

**导出日志**用于自动收集并附加 Azure 信息保护客户端的日志文件，如果你必须将日志文件发送给 Microsoft 支持人员的话。 最终用户也可以使用此选项，将这些日志文件发送给你的支持人员。

若要获取诊断信息并重置客户端，请选择“**运行诊断**”。 诊断测试完成后，单击“**复制结果**”，将信息粘贴到电子邮件中，以便你可以发送给 Microsoft 支持人员，或者最终用户可以发送给你的支持人员。 测试完成后，还可以重置客户端。

有关“重置”选项的详细信息：

- 不是本地管理员也能使用此选项，并且不会在事件查看器中记录此操作。 

- 除非文件被锁定，否则此操作将删除 **%localappdata%\Microsoft\MSIPC** 中的所有文件，该路径用于存储客户端证书和权限管理模板。 此操作不会删除 Azure 信息保护策略或客户端日志文件，也不会注销用户。

- 会删除以下注册表项和设置：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**。 如果为此注册表项配置设置（例如，由于要从 AD RMS 迁移并且网络上仍有服务连接点，因此配置用于重定向到 Azure 信息保护租户的设置），那么重置客户端后必须重新配置注册表设置。

- 重置客户端后，必须重新初始化用户环境，下载客户端证书和最新模板。 为了执行此操作，请关闭 Office 的所有实例，然后重新启动 Office 应用程序。 此操作还会检查是否已下载最新的 Azure 信息保护策略。 完成此操作之前，请勿再次运行诊断测试。


### <a name="client-status-section"></a>“**客户端状态**”部分

使用“**连接身份**”值来确认显示的用户名是否是要用于 Azure 信息保护身份验证的帐户。 此用户名必须与用于 Office 365 或 Azure Active Directory 的帐户一致，并与为 Azure 信息保护所配置的租户中的帐户一致。

如果需要以与显示用户名不同的用户身份登录，请参阅此页上的[以其他用户身份登录](#sign-in-as-a-different-user)部分。

“**上次连接时间**”显示客户端最后一次连接组织的 Azure 信息保护服务的时间，并且可与“**信息保护策略安装日期和时间**”结合使用，从而确认 Azure 信息保护策略上次安装或更新的时间。 当客户端连接服务时，如果它发现与其当前策略有差异，则会自动下载最新策略，频率同样也是每 24 小时。 如果在显示时间后完成策略更改，关闭并重新打开 Office 应用程序。

如果看到**此客户端未获许可使用 Office Professional Plus**：Azure 信息保护客户端检测到安装的 Office 版本不支持应用 Rights Management 保护。 执行此检测时，便会发现应用保护的标签未显示在 Azure 信息保护栏上。

使用“**版本**”信息可以确认安装的是哪个版本的客户端。 可以单击“**最近更新**”链接来查看客户端的“[版本发行历史记录](client-version-release-history.md)”，检查是否为最新发行版本以及相应的修补程序和新功能。

## <a name="custom-configurations"></a>自定义配置

使用以下高级配置的相关信息，你可能需要将其用于特定方案或用户子集。 

### <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

在生产环境中，如果用户使用的是 Azure 信息保护客户端，则通常不需要以其他用户身份登录。 但是，如果拥有多个租户，则可能需要以管理员身份执行此操作。 例如，除了拥有组织使用的 Office 365 或 Azure 租户外，还拥有一个测试租户。

可以使用“Microsoft Azure 信息保护”对话框验证当前登录的帐户身份：打开 Office 应用程序，在“主页”选项卡上的“保护”组中，单击“保护”，然后单击“帮助和反馈”。 帐户名称会显示在“客户端状态”部分中。

特别是在使用管理员帐户时，请务必检查所显示的登录帐户的域名。 例如，如果在两个不同的租户中都拥有“admin”帐户，则很容易忽略登录的帐户名正确但域错误的情况。 出现此情况可能导致下载 Azure 信息保护策略失败，或无法看到期望的标签或行为。

以其他用户身份登录：

1. 使用注册表编辑器，导航到“HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP”并删除“TokenCache”值（及其关联的值数据）。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果在 Office 应用程序中没有看到登录到 Azure 信息保护服务的提示，请返回“Microsoft Azure信息保护”对话框，然后从更新的“客户端状态”部分中单击“登录”。

此外：

- 如果使用的是单一登录，则需要在编辑注册表后注销 Windows，然后使用其他用户帐户登录。 Azure 信息保护客户端会使用当前登录的用户帐户自动进行身份验证。

- 如果要重新初始化 Azure Rights Management 服务的环境（也称为引导），可以使用 [RMS Analyzer工具](https://www.microsoft.com/en-us/download/details.aspx?id=46437)中的“重置”选项进行此操作。

- 如果要删除当前下载的 Azure 信息保护策略，可以从 **%localappdata%\Microsoft\MSIP** 文件夹中删除 **Policy.msip** 文件。

### <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>隐藏 Windows 文件资源管理器中的“分类和保护”菜单选项

如果你具有 1.3.0.0 或更高版本的 Azure 信息保护客户端，可以通过编辑注册表配置此高级配置。 

创建以下 DWORD 值名称（以及任何数值数据）：

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

### <a name="support-for-disconnected-computers"></a>对断开连接的计算机的支持

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务，以下载最新的 Azure 信息保护策略。 如果你知道你的计算机在一段时间无法内连接到 Internet，可以通过编辑注册表阻止客户端尝试连接到该服务。 

找到以下值名称并将值数据设置为 **0**：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

确保客户端在 **%localappdata%\Microsoft\MSIP** 文件夹中具有一个名为 **Policy.msip** 的有效策略文件。 如有必要，可以从 Azure 门户中导出策略，并将导出的文件复制到客户端计算机。 此外，还可以使用此方法将已过时的策略文件替换为已发布的最新策略。

## <a name="to-uninstall-the-azure-information-protection-client"></a>卸载 Azure 信息保护客户端

可以使用以下任何选项：

- 使用控制面板卸载程序：单击“**Microsoft Azure 信息保护** > **卸载**”

- 重新运行可执行文件（如 **AzInfoProtection.exe**），并从“修改安装程序”页上，单击“卸载”。 

- 使用 **/uninstall** 运行可执行文件。 例如： `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>后续步骤
现在你已安装 Azure 信息保护客户端，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
