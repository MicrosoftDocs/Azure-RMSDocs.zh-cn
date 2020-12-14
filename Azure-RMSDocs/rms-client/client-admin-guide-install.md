---
title: 为用户安装 Azure 信息保护经典客户端
description: 适用于管理员的说明和信息，用于在企业网络上部署适用于 Windows 的 Azure 信息保护经典客户端。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 64735f0a4e9343ced3839f9dcdd9f56985c0b2fa
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386043"
---
# <a name="admin-guide-install-the-azure-information-protection-classic-client-for-users"></a>管理员指南：为用户安装 Azure 信息保护经典客户端

>***适用于**： Active Directory Rights Management Services， [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，Windows 8，Windows Server 2019，Windows Server 2016，windows Server 2012 R2，windows server 2012 *
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>
> **若要部署 AIP 经典客户端**，请打开支持票证以获取下载访问权限。

在企业网络中安装 Azure 信息保护客户端之前，请检查计算机是否具有 Azure 信息保护所需的操作系统版本和应用程序：[Azure 信息保护要求](../requirements.md)。

然后检查 Azure 信息保护客户端可能需要的其他先决条件（如下一部分所述）。 安装程序不会检查所有先决条件。

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的其他先决条件

- Microsoft .NET Framework 4.6.2

    默认情况下，完整安装的 Azure 信息保护客户端要求至少有 Microsoft .NET Framework 4.6.2；如果没有，那么可执行安装程序的安装向导会尝试下载并安装此系统必备。 在客户端安装过程中安装此必备项后，将重启计算机。 可以使用[自定义安装参数](#more-information-about-the-downgradedotnetrequirement-installation-parameter)在使用安装向导时忽略此系统必备，尽管不建议这样做。

    当你使用可执行安装程序、Windows 更新或 Windows 安装程序无提示安装客户端时，不会自动安装此系统必备。 对于这些情况，如果需要，你必须单独安装此系统必备，否则安装将失败。 你可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53344)下载 Microsoft .NET Framework 4.6.2（脱机安装程序）。

- Microsoft .NET Framework 4.5.2

    如果单独安装 Azure 信息保护查看器，则要求的最低版本为 Microsoft .NET Framework 4.5.2，如果缺少此版本，可执行安装程序不会下载并安装它。

- Windows PowerShell 最低版本4。0

    客户端的 PowerShell 模块需要 Windows PowerShell 的最低版本4.0，可能需要将其安装在较早的操作系统上。 有关详细信息，请参阅[如何：安装 Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)。 安装程序不会为你检查或安装此必备项。 若要确认正在运行的 Windows PowerShell 的版本，请在 PowerShell 会话中键入 `$PSVersionTable`。

- 屏幕分辨率大于 800 x 600

    当右键单击文件资源管理器中的文件或文件夹时，分辨率 800x600 及以下无法完全显示“分类和保护 - Azure信息保护”对话框。

- Microsoft Online Services 登录助手 7.250.4303.0

    运行 Office 2010 的计算机需要安装 Microsoft Online Services 登录助手版本 7.250.4303.0。 此版本包含在客户端安装中。 如果已安装登录助手的更高版本，请先将其卸载，然后再安装 Azure 信息保护客户端。 例如，通过使用 **"控制面板" "**  >  **程序和功能**"  >  **卸载或更改程序** 来检查版本并卸载登录助手。

- KB 4482887

    仅适用于 Windows 10 版本 1809，操作系统内部版本早于 17763.348，安装 [2019 年 3 月 1 日—KB4482887 (OS 内部版本 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) 以确保信息保护栏在 Office 应用程序中正确显示。 如果已有 Office 365 1902 或更高版本，则不需要此更新。

- 配置组策略，以免 Azure 信息保护加载项被禁用

    对于 Office 2013 及更高版本，配置组策略以确保始终为 Office 应用程序启用 Microsoft Azure 信息保护加载项。 如果没有此配置，则可能禁用 Microsoft Azure 信息保护加载项，并且用户无法在其 Office 应用程序中标记其文档和电子邮件。

    - 对于 Outlook：使用 Office 文档的[系统管理员对加载项的控制](/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins)中记录的组策略设置。

    - 对于 Word、Excel 和 PowerPoint：使用支持文章[由于 Office 2013 和 Office 2016 项目的组策略设置，没有加载加载项](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)中记录的组策略设置托管加载项列表。

        为 Azure 信息保护指定以下编程标识符 (ProgID)，并将该选项设置为 1：始终启用外接程序。

        对于 Word：`MSIP.WordAddin`

        对于 Excel：`MSIP.ExcelAddin`

        对于 PowerPoint：`MSIP.PowerPointAddin`

- 使用启用了 [Exploit protection](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) 的 .net 版本2或3的计算机不支持 AIP 客户端。 如果你的计算机除了上面列出的 .NET 4.x 版本之外，还具有 .NET 版本2或3，请确保在安装 AIP 客户端之前 [禁用 Exploit protection](../known-issues.md#known-issues-for-aip-and-exploit-protection) 。  

> [!IMPORTANT]
> 安装 Azure 信息保护客户端需要本地管理权限。

## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>为用户安装 Azure 信息保护客户端的选项

使用下列选项之一来为用户安装客户端：

|安装选项  |说明  |
|---------|---------|
|**运行客户端可执行文件 ( .exe)**  <br><br> [说明](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)      | 建议运行的客户端版本的客户端以交互方式或无提示方式运行安装。<br><br> 运行 .exe 文件具有最大的灵活性，但建议使用它，因为它还会检查许多先决条件，还可以安装任何缺少的必备组件。 |
|**将客户端的 Windows installer 部署 ( .msi)** <br><br> [说明](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)    | Azure 信息保护客户端 Windows installer 仅支持使用集中部署机制的无提示安装。<br><br> 例如，在使用组策略进行部署、Configuration Manager 和 Microsoft Intune 时，请使用 .msi 文件。<br><br> 必须将 tis 方法用于由 Intune 管理的 Windows 10 电脑和移动设备管理 (MDM) ，因为这些计算机不支持 .exe 文件。<br><br>**注意**：使用 .Msi 安装时，必须手动检查先决条件，并安装或卸载所需的任何依赖软件。 |

安装客户端后，请重复相同的安装方法以执行更新，或使用 Windows 更新来保持客户端的自动更新。 在安装新版本之前，无需卸载旧版本的客户端。

有关详细信息，请参阅[升级和维护 Azure 信息保护客户端](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)。

> [!NOTE]
> 若要卸载客户端，请使用 Windows 的 " **添加或删除程序** " 选项，如 [windows "控制面板](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs)"。

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>使用可执行安装程序安装 Azure 信息保护客户端

如果在使用 Microsoft Update 目录，或使用 Intune 之类的集中部署方法部署 .msi，请使用以下说明安装客户端。

1. 对于默认安装，只需运行可执行文件，例如 **AzInfoProtection.exe**。 

    若要查看其他安装选项，请先通过 **/help** 运行可执行文件： `AzInfoProtection.exe /help`

    有关无提示安装客户端的示例：`AzInfoProtection.exe /quiet`

    有关无提示仅安装 PowerShell cmdlet 的示例：`AzInfoProtection.exe  PowerShellOnly=true /quiet`

    帮助屏幕中未列出的其他参数：

    - **ServiceLocation**：如果要在运行 Office 2010 的计算机上安装客户端，且你的用户不是其计算机上的本地管理员，或者你不希望系统会向他们发出提示，请使用此参数。 [详细信息](#more-information-about-the-servicelocation-installation-parameter)

    - **DowngradeDotNetRequirement**：使用此参数可以不遵守一定要有 Microsoft Framework .NET 版本 4.6.2 的要求。 [详细信息](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

    - **AllowTelemetry=0**：使用此参数来禁用安装选项“通过向 Microsoft 发送使用情况统计信息来帮助改进 Azure 信息保护”。

1. 如果要以交互方式安装，请选择安装 **演示策略** 的选项（如果无法连接到 Microsoft 365 或 Azure Active Directory），但想要通过使用本地策略查看和体验 Azure 信息保护的客户端，以便进行演示。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。

1. 若要完成安装：

    - 如果计算机运行的是 Office 2010，请重新启动计算机。

        如果未使用 ServiceLocation 参数安装客户端，首次打开一个使用 Azure 信息保护栏的 Office 应用程序（如 Word）时，必须确认是否有任何要求首次使用时更新注册表的提示。 利用[服务发现](client-deployment-notes.md#rms-service-discovery)功能填充注册表项。

    - 对于其他版本的 Office，请重启任一 Office 应用程序和文件管理器的所有实例。

1. 可以查看默认在 %temp% 文件夹中创建的安装日志文件来确认安装是否成功。 可以使用 **/log** 安装参数更改此位置。

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

1. 在 PowerShell 会话中，首先运行 [AipService](/powershell/module/aipservice/connect-aipservice) 并指定管理员凭据以连接到 Azure Rights Management 服务。 然后运行 [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)。

    如果尚未安装 Azure Rights Management 服务的 PowerShell 模块，请参阅 [安装 AIPService PowerShell 模块](../install-powershell.md)。

2. 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

    例如：LicensingIntranetDistributionPointUrl：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. 该值中，将 **/_wmcs/licensing** 从此字符串删除。 例如：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    Remainin' 字符串是要为 ServiceLocation 参数指定的值。

有关为 Office 2010 和 Azure RMS 无提示安装客户端的示例：`AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`

#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>详细了解 DowngradeDotNetRequirement 安装参数

为了使用 Windows 更新支持自动更新，并与 Office 应用程序可靠集成，Azure 信息保护客户端使用 Microsoft .NET Framework 版本 4.6.2。 默认情况下，使用可执行安装程序的交互安装会检查是否有此版本；如果没有，则会尝试进行安装。 然后，安装程序要求重启计算机。

如果安装这一 Microsoft .NET Framework 更高版本不可行，可以在安装客户端时使用 **DowngradeDotNetRequirement=True** 参数和值，这样就可以在已安装 Microsoft .NET Framework 版本 4.5.1 的情况下忽略这项要求。

例如： `AzInfoProtection.exe DowngradeDotNetRequirement=True`

建议谨慎使用此参数。还请注意，将 Azure 信息保护客户端与旧版 Microsoft .NET Framework 结合使用时，Office 应用程序存在报告的尚未解决的问题。 如果确实遇到了尚未解决的问题，请先升级到建议的版本，然后再尝试其他故障排除解决方案。 

此外，还请注意，如果使用 Windows 更新来不断更新 Azure 信息保护客户端，还需要使用另一软件部署机制，才能将客户端升级到更高版本。

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>使用 .msi 安装程序安装 Azure 信息保护客户端

对于集中部署，请使用以下特定于 Azure信息保护客户端 .msi 安装版本的信息。 

如果将 Intune 用于软件部署方法，请将这些说明与[使用 Microsoft Intune 添加应用](/intune/apps/apps-add)一起使用。

1. 对于运行 .msi 文件的每台计算机，必须确保以下软件依赖项已经就绪。 例如，将这些依赖项与客户端 .msi 版本一起打包，或只部署到满足这些依赖关系的计算机上：
    
    |Office 版本|操作系统|软件|操作|
    |--------------------|--------------|----------------|---------------------|
    |Office 365 1902 或更高版本之外的所有版本|仅限于 Windows 10 版本 1809，操作系统内部版本早于 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|安装|
    |Office 2013|所有支持的版本|64 位：[KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 位：[KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />版本：1.0|安装|
    |Office 2010|所有支持的版本|[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> 版本：2.1|安装|
    |Office 2016|所有支持的版本|64 位：[KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 位：[KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> 版本：1.0|安装|
    |Office 2010|所有支持的版本|[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> 版本：2.1|安装|
    |Office 2010|Windows 8.1 和 Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB2843630 或 KB2919355，则进行安装|
    |Office 2010|Windows 8 和 Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|安装|

1. 对于默认安装，将 .msi 与 /quiet/ 一起运行，例如，`AzInfoProtection.msi /quiet`。 但是，你可能需要指定[可执行安装程序说明](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)中记录的其他安装参数。

    > [!NOTE]
    > 默认情况下，启用 " **通过将使用情况统计信息发送到 Microsoft 安装" 选项来帮助改进 Azure 信息保护** 。 若要禁用此选项，请确保执行下列操作之一：
    >
    >- 在安装过程中，指定 **AllowTelemetry = 0**
    >- 安装后，按如下所示更新注册表项： **EnableTelemetry = 0**。
    >

## <a name="how-to-install-the-azure-information-protection-scanner"></a>如何安装 Azure 信息保护扫描程序

Azure 信息保护客户端包括的 PowerShell 模块具有用于安装和配置扫描程序的 cmdlet。 但是，要使用扫描程序，必须安装完整版本的客户端，而不能仅安装 PowerShell 模块。

要安装客户端以获取扫描程序，请按照前面部分中的相同说明进行操作。 然后，你就可以配置并安装扫描程序了。 有关详细信息，请参阅 [什么是 Azure 信息保护经典扫描器？](../deploy-aip-scanner-classic.md)。

## <a name="next-steps"></a>后续步骤

现在你已安装 Azure 信息保护客户端，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)