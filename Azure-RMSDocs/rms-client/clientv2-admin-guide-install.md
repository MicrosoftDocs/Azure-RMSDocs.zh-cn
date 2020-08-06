---
title: 为用户安装 Azure 信息保护统一标签客户端
description: 管理员用于在企业网络上部署 Azure 信息保护统一标签客户端的说明和信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 010471368d219cc2ba45d24744a17c09ca83b85d
ms.sourcegitcommit: dec5df81b569283a72f0a983d3f53b82cbbc562c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2020
ms.locfileid: "87802311"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>管理员指南：为用户安装 Azure 信息保护统一标签客户端

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*
>
> **对于 Windows 7 和 Office 2010，具有扩展 Microsoft 支持的客户也可以获得这些版本的 Azure 信息保护支持。请咨询你的支持联系人了解完整的详细信息。*
>
> *适用于以下内容的说明： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

在企业网络上安装 Azure 信息保护统一标签客户端之前，请检查计算机是否具有 Azure 信息保护所需的操作系统版本和应用程序： [Azure 信息保护的要求](../requirements.md)。 

然后检查 Azure 信息保护统一标签客户端可能需要的其他先决条件，如下一节中所述。 安装程序不会检查所有先决条件。

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Azure 信息保护统一标签客户端的其他先决条件

除了[Azure 信息保护要求](../requirements.md)中列出的项目外，AIP 统一标签客户端还需要满足以下先决条件。

|要求  |说明  |
|---------|---------|
|**Microsoft .NET 框架4.6。2**     | 默认情况下，默认情况下，Azure 信息保护统一标签客户端完全安装需要 Microsoft .NET Framework 4.6.2 的最低版本。 </br></br>如果缺少此框架，则可执行安装程序中的安装向导将尝试下载并安装此必备组件。 在客户端安装过程中安装此必备项后，将重启计算机。 </br></br>**注意：** 尽管不建议这样做，但当你使用[自定义安装参数](#more-information-about-the-downgradedotnetrequirement-installation-parameter)来使用安装向导时，可以绕过此先决条件。        |
|**Microsoft .NET Framework 4.5.2**     | 如果 Azure 信息保护查看器是单独安装的，则查看器应用程序需要 Microsoft .NET Framework 4.5.2 的最低版本。 </br></br>**重要提示：** 如果查看器缺少此框架，则可执行安装*程序不会下载或*安装该框架。        |
|**Windows PowerShell 最低版本4。0**     |   客户端的 PowerShell 模块需要最低版本的 Windows PowerShell 4.0，这些版本可能需要安装在较早的操作系统上。 </br></br>有关详细信息，请参阅[如何：安装 Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)。 </br></br>**重要提示：** 安装*程序不会检查或*安装此必备组件。 若要确认正在运行的 Windows PowerShell 的版本，请在 PowerShell 会话中键入 `$PSVersionTable`。      |
|**屏幕分辨率大于 800 x 600**    |     当右键单击文件资源管理器中的文件或文件夹时，分辨率 800x600 及以下无法完全显示“分类和保护 - Azure信息保护”**** 对话框。    |
|**Microsoft Online Services 登录助手 7.250.4303.0**     |   运行 Office 2010 的计算机需要 Microsoft Online Services 登录助手版本7.250.4303.0，此版本包含在客户端安装中。 </br></br>如果有登录助手的更高版本，请先卸载它，然后再安装 Azure 信息保护统一标签客户端。 </br></br>例如，通过使用 **"控制面板" "**  >  **程序和功能**"  >  **卸载或更改程序**来检查版本并卸载登录助手。      |
|**KB 4482887**     | 仅适用于 Windows 10 版本 1809，操作系统内部版本早于 17763.348，安装 [2019 年 3 月 1 日—KB4482887 (OS 内部版本 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) 以确保信息保护栏在 Office 应用程序中正确显示。 </br></br>如果已有 Office 365 1902 或更高版本，则不需要此更新。        |
|**管理员权限**| 安装 Azure 信息保护统一标签客户端需要本地管理权限。| 
|   |  |
        
### <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>配置组策略以阻止禁用 AIP

对于 Office 版本2013及更高版本，建议配置组策略，以确保始终启用适用于 Office 应用程序的**Microsoft Azure 信息保护**外接程序。  如果没有此外接程序，用户将无法在 Office 应用程序中标记其文档或电子邮件。   

- **对于 Outlook：** 使用[系统管理员对外接程序的控制](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins)中所述的组策略设置。
- **对于 Word、Excel 和 PowerPoint：** 使用[由于 Office 2013 和 office 2016 程序的组策略设置而未加载加载项](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)中所述的**托管外**接程序的组策略设置列表。 . 

    为 AIP 指定 (ProgID) 的以下编程标识符，并将选项设置为**1：始终启用外接程序**。

    |应用  |ProgID  |
    |---------|---------|
    |Word     |     `MSIP.WordAddin`    |
    |Excel     |  `MSIP.ExcelAddin`       |
    |PowerPoint     |   `MSIP.PowerPointAddin`      |
    | | | 

## <a name="applications"></a>应用程序

Azure 信息保护统一标签客户端可以使用 Office 应用程序的 Word、Excel、PowerPoint 和 Outlook 通过以下任一 Office 版本来标记和保护文档和电子邮件：

- Office 应用最低版本 1805，Office 365 商业版或 Microsoft 365 商业版中的内部版本 9330.2078，前提是已为用户分配了 Azure Rights Management（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证
- Office 365 ProPlus
- Office 专业增强版 2019
- Office Professional Plus 2016
- Office Professional Plus 2013 Service Pack 1
- Office Professional Plus 2010 Service Pack 2

其他版本 (例如，Office 的**标准**) 无法使用 Rights Management 服务来保护文档和电子邮件。 对于这些版本，仅支持 Azure 信息保护以便进行**标记**。 因此，应用保护的标签不会向用户显示 Azure 信息保护敏感度按钮或栏。

有关支持保护服务的 Office 版本的信息，请参阅[支持 Azure Rights Management 数据保护的应用程序](https://docs.microsoft.com/azure/information-protection/requirements-applications)。

### <a name="office-features-and-capabilities-not-supported"></a>不支持的 Office 功能

Azure 信息保护统一标签客户端不支持在同一台计算机上或在 Office 中切换用户帐户的多个版本的 Office。

Azure 信息保护功能不支持 Office 邮件合并功能。

## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>为用户安装 Azure 信息保护统一标签客户端的选项

为用户安装客户端有两个选项：

**运行客户端的可执行文件 (.exe) 版本**：建议的安装方式，以交互方式或无提示方式运行。 此方法非常灵活，建议使用，因为安装程序会检查多个必备组件，并且可以自动安装缺少的必备组件。 [说明](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**部署客户端的 Windows Installer (.msi) 版本**：仅支持使用集中部署机制的无提示安装，如组策略、Configuration Manager 和 Microsoft Intune。 对于由 Intune 和移动设备管理 (MDM) 管理的 Windows 10 电脑而言，这是必要的方法，因为这些计算机不支持安装可执行文件。 但是，使用此安装方法时，必须手动检查并安装或卸载可执行文件的安装程序为每台计算机执行时依赖的软件。 [说明](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

安装 Azure 信息保护统一标签客户端之后，你可以通过重复所选的安装方法来更新此客户端，或者使用 Windows 更新来保持客户端自动升级。 有关升级的详细信息，请参阅[升级和维护 Azure 信息保护客户端](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)部分。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>使用可执行安装程序安装 Azure 信息保护统一标签客户端

如果在使用 Microsoft Update 目录，或使用 Intune 之类的集中部署方法部署 .msi，请使用以下说明安装客户端。

1. 从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载 Azure 信息保护统一标签客户端 (文件名 AzInfoProtection_UL) 的可执行版本。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 

2. 对于默认安装，只需运行可执行文件，例如**AzInfoProtection_UL.exe**。 但是，若要查看安装选项，请先通过 **/help**运行可执行文件：`AzInfoProtection_UL.exe /help`

    有关无提示安装客户端的示例：`AzInfoProtection_UL.exe /quiet`
    
    有关无提示仅安装 PowerShell cmdlet 的示例：`AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    帮助屏幕中未列出的其他参数：
    
    - **ServiceLocation**：如果要在运行 Office 2010 的计算机上安装客户端，且你的用户不是其计算机上的本地管理员，或者你不希望系统会向他们发出提示，请使用此参数。 [详细信息](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**：使用此参数可以不遵守一定要有 Microsoft Framework .NET 版本 4.6.2 的要求。 [详细信息](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0**：使用此参数来禁用安装选项“通过向 Microsoft 发送使用情况统计信息来帮助改进 Azure 信息保护”****。 

3. 若要完成安装： 

    - 如果计算机运行的是 Office 2010，请重新启动计算机。 
        
        如果未使用 ServiceLocation 参数安装客户端，则在首次打开使用 Azure 信息保护统一客户端 (（例如，Word) ）的某个 Office 应用程序时，必须在首次使用时确认要更新注册表的任何提示。 利用[服务发现](client-deployment-notes.md#rms-service-discovery)功能填充注册表项。 
    
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

1. 在 PowerShell 会话中，首先运行[AipService](https://docs.microsoft.com/powershell/module/aipservice/connect-aipservice)并指定管理员凭据以连接到 Azure Rights Management 服务。 然后运行[AipServiceConfiguration](https://docs.microsoft.com/powershell/module/aipservice/get-aipserviceconfiguration)。 
 
    如果尚未安装 Azure Rights Management 服务的 PowerShell 模块，请参阅[安装 AIPService PowerShell 模块](../install-powershell.md)。

2. 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

    例如：LicensingIntranetDistributionPointUrl：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. 该值中，将 **/_wmcs/licensing** 从此字符串删除。 例如：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    剩余字符串就是要为 ServiceLocation 参数指定的值。

有关为 Office 2010 和 Azure RMS 无提示安装客户端的示例：`AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>详细了解 DowngradeDotNetRequirement 安装参数

为支持使用 Windows 更新进行自动升级，并与 Office 应用程序可靠集成，Azure 信息保护统一标签客户端使用 Microsoft .NET Framework 版本4.6.2。 默认情况下，使用可执行安装程序的交互安装会检查是否有此版本；如果没有，则会尝试进行安装。 然后，安装程序要求重启计算机。

如果安装这一 Microsoft .NET Framework 更高版本不可行，可以在安装客户端时使用 **DowngradeDotNetRequirement=True** 参数和值，这样就可以在已安装 Microsoft .NET Framework 版本 4.5.1 的情况下忽略这项要求。

例如： `AzInfoProtection_UL.exe DowngradeDotNetRequirement=True`

建议你谨慎使用此参数，并了解当 Azure 信息保护统一标签客户端与此旧版本的 Microsoft .NET Framework 一起使用时，Office 应用程序的报告问题将会挂起。 如果确实遇到了尚未解决的问题，请先升级到建议的版本，然后再尝试其他故障排除解决方案。 

另请注意，如果使用 Windows 更新来保持 Azure 信息保护的统一标签客户端的更新，则必须具有另一个软件部署机制，才能将客户端升级到更高版本。

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>使用 .msi 安装程序安装 Azure 信息保护统一标签客户端

对于中心部署，请使用特定于 Azure 信息保护统一标签客户端的 .msi 安装版本的下列信息。 

如果将 Intune 用于软件部署方法，请将这些说明与[使用 Microsoft Intune 添加应用](/intune/deploy-use/add-apps)一起使用。

1. 从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载 Azure 信息保护统一标签客户端 (AzInfoProtection_UL) 的 .msi 版本。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。

1. 对于运行 .msi 文件的每台计算机，必须确保以下软件依赖项已经就绪。 例如，将这些依赖项与客户端 .msi 版本一起打包，或只部署到满足这些依赖关系的计算机上：
    
    |Office 版本|操作系统|软件|操作|
    |--------------------|--------------|----------------|---------------------|
    |Office 365 1902 或更高版本之外的所有版本|仅限于 Windows 10 版本 1809，操作系统内部版本早于 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|安装|
    |Office 2016|所有支持的版本|64 位：[KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 位：[KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> 版本：1.0|安装|
    |Office 2013|所有支持的版本|64 位：[KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 位：[KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />版本：1.0|安装|
    |Office 2010|所有支持的版本|[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> 版本：2.1|安装|
    |Office 2010|Windows 8.1 和 Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB2843630 或 KB2919355，则进行安装|
    |Office 2010|Windows 8 和 Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|安装|
    
   

1. 对于默认安装，将 .msi 与 /quiet/**** 一起运行，例如，`AzInfoProtection_UL.msi /quiet`。

    可能需要指定其他安装参数。 有关详细信息，请参阅[可执行安装程序说明](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)。

    > [!NOTE]
    > 默认情况下，启用 "**通过将使用情况统计信息发送到 Microsoft 安装" 选项来帮助改进 Azure 信息保护**。 若要禁用此选项，请确保指定**ENABLETELEMETRY = 0**而不是**AllowTelemetry = 0**。
    >

## <a name="next-steps"></a>后续步骤
现在，已安装 Azure 信息保护统一标签客户端，请参阅以下内容，了解支持此客户端所需的其他信息：

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)

