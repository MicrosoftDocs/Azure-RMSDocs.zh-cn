---
title: 安装 Azure 信息保护统一标记用户的客户端
description: 说明和管理员可以部署 Azure 信息保护统一标记上的客户端的 Windows 企业网络的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: c54754c5ec016aaaa54874b2be5bd0ac2d112e90
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183666"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>管理员指南：安装 Azure 信息保护统一标记用户的客户端

>适用范围：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> *说明：[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

在企业网络上安装 Azure 信息保护统一标记客户端之前，请检查计算机具有所需的操作系统版本和 Azure 信息保护的应用程序：[Azure 信息保护的要求](../requirements.md)。 

下一节中所述，然后检查 Azure 信息保护统一标记客户端，可能需要的其他先决条件。 安装程序不会检查所有先决条件。

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>针对 Azure 信息保护统一标记客户端的其他先决条件

- Microsoft .NET Framework 4.6.2
    
    Azure 信息保护统一标记的客户端默认情况下，完整安装需要 Microsoft.NET Framework 4.6.2 的最小版本，如果缺少此，从可执行安装程序安装向导尝试下载并安装此客户端必备组件。 在客户端安装过程中安装此必备项后，将重启计算机。 可以使用[自定义安装参数](#more-information-about-the-downgradedotnetrequirement-installation-parameter)在使用安装向导时忽略此系统必备，尽管不建议这样做。
    
    当你使用可执行安装程序、Windows 更新或 Windows 安装程序无提示安装客户端时，不会自动安装此系统必备。 对于这些情况，如果需要，你必须单独安装此系统必备，否则安装将失败。 你可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53344)下载 Microsoft .NET Framework 4.6.2（脱机安装程序）。

- Microsoft .NET Framework 4.5.2
    
    如果单独安装 Azure 信息保护查看器，则要求的最低版本为 Microsoft .NET Framework 4.5.2，如果缺少此版本，可执行安装程序不会下载并安装它。

- Windows PowerShell 版本 4.0
    
    客户端的 PowerShell 模块需要 Windows PowerShell 4.0 版本，此版本可能需要在旧版操作系统上安装。 有关详细信息，请参阅[如何：安装 Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)。 安装程序不会为你检查或安装此必备项。 若要确认正在运行的 Windows PowerShell 的版本，请在 PowerShell 会话中键入 `$PSVersionTable`。

- 屏幕分辨率大于 800 x 600
    
    当右键单击文件资源管理器中的文件或文件夹时，分辨率 800x600 及以下无法完全显示“分类和保护 - Azure信息保护”对话框。


- Microsoft Online Services 登录助手 7.250.4303.0
    
    运行 Office 2010 的计算机需要安装 Microsoft Online Services 登录助手版本 7.250.4303.0。 此版本包含在客户端安装中。 如果登录助手的更高版本，将在安装 Azure 信息保护统一标记客户端之前将其卸载。 例如，通过使用“控制面板” > “程序和功能” > “卸载或更改程序”来检查版本和卸载登录助手。

- KB 4482887
    
    仅适用于 Windows 10 版本 1809，操作系统内部版本早于 17763.348，安装 [2019 年 3 月 1 日—KB4482887 (OS 内部版本 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) 以确保信息保护栏在 Office 应用程序中正确显示。 如果已有 Office 365 1902 或更高版本，则不需要此更新。

- KB 2533623
    
    运行 Windows 7 Service Pack 1 的计算机需要 KB 2533623。 有关此更新的详细信息，请参阅 [Microsoft 安全顾问：不安全的库加载可能允许远程执行代码](https://support.microsoft.com/en-us/kb/2533623)。 可以直接安装此更新，也可以使用为你安装的另一个更新代替此更新。
    
    如果需要此更新且未安装，则客户端安装将警告你必须安装此更新。 可以在安装客户端后安装此更新，但某些操作将被阻止并再次显示该信息。  

- Visual C++ Redistributable for Visual Studio 2015（32 位版）
    
    对于运行 Windows 7（含 Service Pack 1）的计算机，请从以下下载页面安装 vc_redist.x86.exe：[Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
    
    客户端安装不会检查此必备项，但它所需的 Azure 信息保护统一标记的客户端进行分类和保护的 PDF 文件。

- 配置组策略，以免 Azure 信息保护加载项被禁用
    
    对于 Office 2013 及更高版本，配置组策略以确保始终为 Office 应用程序启用 Microsoft Azure 信息保护加载项。 如果没有此配置，则可能禁用 Microsoft Azure 信息保护加载项，并且用户无法在其 Office 应用程序中标记其文档和电子邮件。
    
    - 对于 Outlook:使用记录在 Office 文档中的[系统管理员对加载项的控制](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins)中的组策略设置。
    
    - 对于 Word、Excel 和 PowerPoint：使用[由于 Office 2013 和 Office 2016 程序的组策略设置没有加载任何加载项](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)中记录的组策略设置“托管加载项列表”。 
        
        为 Azure 信息保护指定以下编程标识符 (ProgID)，并将此选项设置为“1: 始终启用加载项”。
        
        对于 Word：`MSIP.WordAddin`
        
        对于 Excel：`MSIP.ExcelAddin`
        
        对于 PowerPoint：`MSIP.PowerPointAddin`

> [!IMPORTANT]
> 安装 Azure 信息保护统一标记客户端需要本地管理权限。


## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>若要安装 Azure 信息保护统一标记用户的客户端的选项

为用户安装客户端有两个选项：

**运行客户端的可执行文件 (.exe) 版本**：可以通过交互方式或无提示方式运行的建议的安装方式。 此方法非常灵活，建议使用，因为安装程序会检查多个必备组件，并且可以自动安装缺少的必备组件。 [说明](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**部署客户端的 Windows Installer (.msi) 版本**：仅支持使用集中部署机制的无提示安装，如组策略、Configuration Manager 和 Microsoft Intune。 对于由 Intune 和移动设备管理 (MDM) 管理的 Windows 10 电脑而言，这是必要的方法，因为这些计算机不支持安装可执行文件。 但是，使用此安装方法时，必须手动检查并安装或卸载可执行文件的安装程序为每台计算机执行时依赖的软件。 [说明](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

安装 Azure 信息保护统一标记客户端后，可以通过重复你选中的安装的方法，更新此客户端或使用 Windows 更新来保持客户端自动升级。 有关升级的详细信息，请参阅[升级和维护 Azure 信息保护客户端](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)部分。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>若要安装 Azure 信息保护统一标记的客户端通过使用可执行安装程序

如果在使用 Microsoft Update 目录，或使用 Intune 之类的集中部署方法部署 .msi，请使用以下说明安装客户端。

1. 从下载 Azure 信息保护统一标记客户 （AzInfoProtection_UL 文件名称） 的可执行文件版本[Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 

2. 对于默认安装中，只需运行可执行文件，例如， **AzInfoProtection_UL.exe**。 但是，若要查看安装选项，请先使用 **/help** 运行可执行文件：`AzInfoProtection_UL.exe /help`

    有关无提示安装客户端的示例：`AzInfoProtection_UL.exe /quiet`
    
    有关无提示仅安装 PowerShell cmdlet 的示例：`AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    帮助屏幕中未列出的其他参数：
    
    - **Servicelocation**：如果要在运行 Office 2010 的计算机上安装客户端，并且你的用户不是其计算机上的本地管理员，或者你不希望系统向他们发出提示，请使用此参数。 [详细信息](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**：使用此参数以绕过 Microsoft Framework .NET 版本 4.6.2 的要求。 [详细信息](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry = 0**：使用此参数来禁用安装选项“通过向 Microsoft 发送使用情况统计信息来帮助改进 Azure 信息保护”。 

3. 若要完成安装： 

    - 如果计算机运行的是 Office 2010，请重新启动计算机。 
        
        如果客户端未使用 ServiceLocation 参数，当你首次打开一个 Office 应用程序使用 Azure 信息保护统一客户端 (如 Word) 的安装，必须确认任何提示此更新注册表首次使用。 利用[服务发现](client-deployment-notes.md#rms-service-discovery)功能填充注册表项。 
    
    - 对于其他版本的 Office，请重启任一 Office 应用程序和文件管理器的所有实例。 
        
5. 可以查看默认在 %temp% 文件夹中创建的安装日志文件来确认安装是否成功。 可以使用 **/log** 安装参数更改此位置。 
 
    此文件具有以下命名格式：`Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例如：**Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    在此日志文件中搜索以下字符串：**Product:Microsoft Azure Information Protection -- Installation completed successfully**。 如果安装失败，此日志文件包含有助于标识并解决任何问题的详细信息。

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>详细了解 ServiceLocation 安装参数

如果为具有 Office 2010 的用户安装客户端，并且他们没有本地管理权限，请指定用于 Azure 权限管理服务的 ServiceLocation 参数和 URL。 此参数和值将创建和设置以下注册表项：

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

使用以下过程标识要为 ServiceLocation 参数指定的值。 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>若要标识要为 ServiceLocation 参数指定的值

1. 对于 PowerShell 会话，请先运行 [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice)，并指定要连接到 Azure 权限管理服务的管理员凭据。 然后运行 [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration)。 
 
    如果尚未安装适用于 Azure Rights Management 服务的 PowerShell 模块，请参阅[安装 AADRM PowerShell 模块](../install-powershell.md)。

2. 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

    例如：LicensingIntranetDistributionPointUrl： https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

3. 在该值中，将 **/_wmcs/licensing** 从此字符串删除。 例如：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    剩余字符串就是要为 ServiceLocation 参数指定的值。

有关为 Office 2010 和 Azure RMS 无提示安装客户端的示例：`AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>详细了解 DowngradeDotNetRequirement 安装参数

若要支持自动升级，通过使用 Windows 更新，并与 Office 应用程序可靠集成，Azure 信息保护统一标记客户端，请使用 Microsoft.NET Framework 版本 4.6.2。 默认情况下，使用可执行安装程序的交互安装会检查是否有此版本；如果没有，则会尝试进行安装。 然后，安装程序要求重启计算机。

如果安装这一 Microsoft .NET Framework 更高版本不可行，可以在安装客户端时使用 **DowngradeDotNetRequirement=True** 参数和值，这样就可以在已安装 Microsoft .NET Framework 版本 4.5.1 的情况下忽略这项要求。

例如：`AzInfoProtection_UL.exe DowngradeDotNetRequirement=True`

我们建议你使用此参数，谨慎使用，并使用与 Office 应用程序挂起此较旧版本的 Microsoft.NET 中使用 Azure 信息保护统一标记客户端时报告问题的知识框架。 如果确实遇到了尚未解决的问题，请先升级到建议的版本，然后再尝试其他故障排除解决方案。 

此外请记住，是否使用 Windows 更新来不断更新 Azure 信息保护统一标记客户，你必须具有另一个软件部署机制，才能升级到更高版本的客户端。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>若要安装 Azure 信息保护统一标记的客户端使用.msi 安装程序

对于集中部署，使用以下特定于 Azure 信息保护统一标记客户端的.msi 安装版本的信息。 

如果将 Intune 用于软件部署方法，请将这些说明与[使用 Microsoft Intune 添加应用](/intune/deploy-use/add-apps)一起使用。

1. 从下载的 Azure 信息保护统一标记客户 (AzInfoProtection_UL).msi 版本[Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 

2. 对于运行 .msi 文件的每台计算机，必须确保以下软件依赖项已经就绪。 例如，将这些依赖项与客户端 .msi 版本一起打包，或只部署到满足这些依赖关系的计算机上：
    
    |Office 版本|操作系统|软件|操作|
    |--------------------|--------------|----------------|---------------------|
    |Office 365 1902 或更高版本之外的所有版本|仅限于 Windows 10 版本 1809，操作系统内部版本早于 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|安装|
    |Office 2016|所有支持的版本|64 位：[KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 位：[KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> 版本：1.0|安装|
    |Office 2013|所有支持的版本|64 位：[KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 位：[KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />版本：1.0|安装|
    |Office 2010|所有支持的版本|[Microsoft Online Services 登录助手](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> 版本：2.1|安装|
    |Office 2010|Windows 8.1 和 Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB2843630 或 KB2919355，则进行安装|
    |Office 2010|Windows 8 和 Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|安装|
    |Office 2010|Windows 7 和 Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB3125574，则进行安装|
    |“不适用”|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|安装|
    |“不适用”|Windows 7|KB2627273 <br /><br /> 文件名中包含的版本号：v4|“卸载”|

3. 对于默认安装，将 .msi 与 /quiet/ 一起运行，例如，`AzInfoProtection_UL.msi /quiet`。 但是，你可能需要指定[可执行安装程序说明](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)中记录的其他安装参数。  


## <a name="next-steps"></a>后续步骤
至此，已安装 Azure 信息保护统一标记客户端，请参阅以下可能需要支持此客户端的其他信息：

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)

