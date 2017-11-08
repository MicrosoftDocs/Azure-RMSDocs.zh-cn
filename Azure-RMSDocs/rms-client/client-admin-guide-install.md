---
title: "为用户安装 Azure 信息保护客户端"
description: "面向管理员的说明和信息，介绍如何在企业网络中部署适用于 Windows 的 Azure 信息保护客户端。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 675afc962da542a03b90bea2dcb5d004829e361a
ms.sourcegitcommit: 832d3ef5f9c41d6adb18a8cf5304f6048cc7252e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2017
---
# <a name="admin-guide-install-the-azure-information-protection-client-for-users"></a>管理员指南：为用户安装 Azure 信息保护客户端

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

在企业网络中安装 Azure 信息保护客户端之前，请检查计算机是否具有 Azure 信息保护所需的操作系统版本和应用程序：[Azure 信息保护要求](../get-started/requirements-azure-rms.md)。 

然后检查 Azure 信息保护客户端可能需要的其他先决条件（如下一部分所述）。 安装程序不会检查所有先决条件。

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的其他先决条件

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

- 请勿为 Office 应用程序禁用“Microsoft Azure 信息保护”加载项
    
    如果已配置组策略设置“托管加载项列表”，请通过为 Azure 信息保护指定以下编程标识符 (ProgID) 来添加 Office 应用程序的 Microsoft Azure 信息保护加载项，并将选项设置为“1：始终启用加载项”。
    
    - 对于 Outlook：`MSIP.OutlookAddin`
    
    - 对于 Word：`MSIP.WordAddin`
    
    - 对于 Excel：`MSIP.ExcelAddin`
    
    - 对于 PowerPoint：`MSIP.PowerPointAddin`
    
    即使尚未配置“托管加载项列表”组策略设置，如果收到报告称将禁用“Microsoft Azure 信息保护”加载项，也可能需要对其进行配置。 禁用此加载项后，Office 应用程序中将不会显示“Azure 信息保护”栏。
    
    有关此组策略设置的详细信息，请参阅 [Office 2013 和 Office 2016 程序的组策略设置导致未加载任何加载项](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)。

> [!IMPORTANT]
> 安装 Azure 信息保护客户端需要本地管理权限。


## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>为用户安装 Azure 信息保护客户端的选项

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
    |Office 2016|所有支持的版本|64 位：[KB317866](https://www.microsoft.com/en-us/download/details.aspx?id=55073)<br /><br />32 位：[KB317866](https://www.microsoft.com/en-us/download/details.aspx?id=55058)<br /><br /> 版本：1.0|安装|
    |Office 2013|所有支持的版本|64 位：[KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 位：[KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />版本：1.0|安装|
    |Office 2010|所有支持的版本|[Microsoft Online Services 登录助手](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> 版本：2.1|安装|
    |Office 2010|Windows 8.1 和 Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB2843630 或 KB2919355，则进行安装|
    |Office 2010|Windows 8 和 Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|安装|
    |Office 2010|Windows 7|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB3125574，则进行安装|
    |不适用|Windows 7|KB2627273 <br /><br /> 文件名中包含的版本号：v4|卸载|
    

3. 对于默认安装，将 .msi 与 /quiet/ 一起运行，例如，`AzInfoProtection.msi /quiet`。 但是，你可能需要指定[可执行安装程序说明](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)中记录的其他安装参数。  


## <a name="how-to-install-the-azure-information-protection-scanner"></a>如何安装 Azure 信息保护扫描程序

当前的 Azure 信息保护客户端预览版包括 Azure 信息保护扫描程序。 客户端包括的 PowerShell 模块具有用于安装和配置扫描程序的 cmdlet。

要安装客户端以获取扫描程序，请按照前面部分中的相同说明进行操作。 注意，如果不需要所有客户端组件（例如，Office 加载项和查看器），可只安装 PowerShell 模块。 例如，可使用 `PowerShellOnly=true /quiet` 运行可执行文件。

安装客户端后，即可开始安装扫描程序。 有关说明，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](../deploy-use/deploy-aip-scanner.md)。


## <a name="next-steps"></a>后续步骤
现在你已安装 Azure 信息保护客户端，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
