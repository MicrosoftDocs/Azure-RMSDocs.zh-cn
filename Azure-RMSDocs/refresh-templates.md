---
title: 刷新 Azure RMS 模板 - AIP
description: 使用 Azure Rights Management 服务时，模板会自动下载到客户端计算机，因而用户能够从他们的应用程序选择这些模板。 但是，如果对模板进行了更改，可能还需要执行附加步骤。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6f095c7cfd7a41663da3fd4f19d47012fa2604b5
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566244"
---
# <a name="refreshing-templates-for-users-and-services"></a>为用户和服务刷新模板

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

使用 Azure 信息保护中的 Azure Rights Management 服务时，会自动将保护模板下载到客户端计算机，以便用户可以从应用程序中选择它们。 但是，如果你对模板进行了更改，可能还需要执行附加步骤：

|应用程序或服务|如何在更改后刷新模板|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />适用于传输规则和 Outlook Web App |1 小时内自动刷新 – 无需额外的步骤。|
|Azure 信息保护客户端|每当在客户端上的 Azure 信息保护策略刷新时，都会自动刷新：<br /><br /> - 打开支持 Azure 信息保护栏的 Office 应用程序时。 <br /><br /> - 右键单击以分类和保护文件或文件夹时。 <br /><br /> - 运行 PowerShell cmdlet 以实现标记和保护（Get-AIPFileStatus 和 Set-AIPFileLabel）。<br /><br /> - 启动 Azure 信息保护扫描程序服务时，以及本地策略已执行超过一小时时。 此外，扫描程序服务每小时检查一次更改，并将在下一个扫描周期中使用这些更改。<br /><br /> - 每 24 小时一次。<br /><br /> 此外，由于此客户端与 Office 紧密集成，因此对于 Azure 信息保护客户端，还会刷新适用于 Microsoft 365 应用、Office 2019、Office 2016 或 Office 2013 的任何刷新模板。|
|Azure 信息保护统一标识客户端|对于 Office 应用程序，每次打开应用程序时，模板都会自动刷新。<br /><br /> 此外，由于此客户端与 Office 紧密集成，因此对于 Azure 信息保护统一标签客户端，还会刷新适用于 Microsoft 365 应用、Office 2019、Office 2016 或 Office 2013 的任何刷新模板。<br /><br /> 对于文件资源管理器、PowerShell 和扫描程序，客户端不会下载模板，只需将其联机访问，无需执行其他步骤。|
|Microsoft 365 应用、Office 2019、Office 2016 和 Office 2013|自动刷新 – 按计划刷新：<br /><br />- 对于更高版本的 Office：默认刷新时间间隔为 7 天。<br /><br />若要强制执行比计划更快的刷新，请参阅以下部分 [： Microsoft 365 应用、office 2019、office 2016 和 office 2013：如何强制刷新模板](#microsoft-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-templates)。|
|Office 2010|当用户注销 Windows 后重新登录并等待长达 1 小时时自动刷新。|
|Exchange 內部部署与权限管理连接器<br /><br />适用于传输规则和 Outlook Web App|自动刷新 – 无需额外的步骤。 但是，Outlook Web App 可将该 UI 缓存一天。|
|Office 2019 for Mac 和 Office 2016 for Mac|当你打开受保护的内容时自动刷新。 若要强制执行刷新，请参阅以下部分 [：适用于 mac 的 office 2019 和适用于 mac 的 office 2016：如何强制刷新模板](#office-2019-for-mac-and-office-2016-for-mac-how-to-force-a-refresh-for-templates)。|
|适用于 Mac 计算机的 RMS 共享应用|自动刷新 – 无需额外的步骤。|
|带有[内置标记](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)的 Office 365 ProPlus|此内置标签客户端不会下载模板，而是联机访问模板-无需执行其他步骤。|
| | |

如果客户端应用程序需要下载模板 (初始或刷新) ，请在下载完成前等待30分钟，新的或更新的模板完全可操作。 实际时间会因多种因素而异，例如模板配置的大小和复杂性以及网络连接。 

## <a name="microsoft-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-templates"></a>Microsoft 365 应用、Office 2019、Office 2016 和 Office 2013：如何强制执行模板刷新
通过在运行 Microsoft 365 应用、Office 2019、Office 2016 或 Office 2013 的计算机上编辑注册表，你可以更改自动计划，使更改的模板在计算机上的刷新频率比其默认值更频繁。 你还可以通过删除注册表值中的现有数据，强制执行即时刷新。

> [!WARNING]
> 如果不正确地使用注册表编辑器，可能会导致也许需要你重新安装操作系统的严重问题。 Microsoft 不保证能够解决因注册表编辑器使用不当而导致的问题。 你自行承担使用注册表编辑器的风险。

### <a name="to-change-the-automatic-schedule"></a>更改自动计划

1.  使用注册表编辑器，创建并设置以下注册表值中的某一个：
    
    - 设置以天为单位的更新频率（最少为 1 天）：创建名为“TemplateUpdateFrequency”  的新注册表值，并为该数据定义整数值，该值将指定向已下载模板下载任何更改的频率（以天为单位）。 使用以下信息查找创建此新注册表值的注册表路径。

        **注册表路径：** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **类型:** REG_DWORD

        **值：** TemplateUpdateFrequency

    - 设置以秒为单位的更新频率（最少为 1 秒）：创建名为“TemplateUpdateFrequencyInSeconds”  的新注册表值，并为该数据定义整数值，该值将指定向已下载模板下载任何更改的频率（以秒为单位）。 使用以下信息查找创建此新注册表值的注册表路径。

        **注册表路径：** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **类型:** REG_DWORD

        **值：** TemplateUpdateFrequencyInSeconds

    请确保你创建并设置这两个注册表值中的其中一个，而不是对这两个注册表值都执行此操作。 如果两者均存在，将忽略 **TemplateUpdateFrequency** 。

2.  如果你想要强制即时刷新模板，请转到下一个过程。 否则，请立即重启 Office 应用程序和文件资源管理器实例。

### <a name="to-force-an-immediate-refresh"></a>强制执行即时刷新

1. 使用注册表编辑器，删除“LastUpdatedTime”值的数据。 例如，数据可能显示“2015-04-20T15:52”；删除 2015-04-20T15:52，使得数据不会显示。 使用以下信息查找删除此注册表值数据的注册表路径。

   **注册表路径：** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\ < *MicrosoftRMS_FQDN*> \template \\ < *user_alias*>

   **类型:** REG_SZ

   **值：** LastUpdatedTime

   > [!TIP]
   > 在注册表路径中，<*MicrosoftRMS_FQDN*> 是指你的 Microsoft RMS 服务 FQDN。 如果你想要验证此值：
   > 
   > 运行 Azure 信息保护的 [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) cmdlet。 如果尚未安装 AIPService PowerShell 模块，请参阅 [安装 AIPService powershell 模块](install-powershell.md)。
   > 
   > 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。
   > 
   > 例如：LicensingIntranetDistributionPointUrl：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
   > 
   > 在该值中，将“https://”和“/_wmcs/licensing”从字符串中删除。 剩下的值就是 Microsoft RMS 服务 FQDN。 在我们的示例中，Microsoft RMS 服务 FQDN 会是以下值：
   > 
   > **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2. 删除以下文件夹及其包含的所有文件：**%localappdata%\Microsoft\MSIPC\Templates**

3. 请重启 Office 应用程序和文件资源管理器实例。

## <a name="office-2019-for-mac-and-office-2016-for-mac-how-to-force-a-refresh-for-templates"></a>适用于 mac 的 office 2019 和适用于 Mac 的 Office 2016：如何强制刷新模板

在这些版本的 Office for Mac 中，模板会在你打开受保护的内容时刷新，或使用新配置为应用加密的灵敏度标签来保护内容。 如果需要强制刷新模板，可以使用以下说明。 但是，指令中的命令将删除模板、密钥链中的 RMS 令牌缓存，并为以前打开的所有受保护内容使用本地许可证。 因此，你将需要重新进行身份验证，并且必须具有 internet 连接才能打开以前打开的受保护内容。

1. 打开终端并输入以下命令：
    
    ```sh
    defaults write ~/Library/Containers/com.microsoft.Outlook/Data/Library/Preferences/com.microsoft.Outlook ResetRMSCache 1
    ```

2. 重新启动 Outlook for Mac。

3. 创建新电子邮件并选择 " **加密**"，然后 **验证凭据**。


## <a name="see-also"></a>另请参阅
[在 Azure 信息保护策略中配置和管理模板](configure-policy-templates.md)