---
title: "刷新 Azure RMS 模板 - AIP"
description: "使用 Azure Rights Management 服务时，模板会自动下载到客户端计算机，因而用户能够从他们的应用程序选择这些模板。 但是，如果对模板进行了更改，可能还需要执行附加步骤。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/22/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 73ba65e3c453b1e06e02925a0b3ecc09a0bca1f0
ms.sourcegitcommit: 240378d216e386ad760460c50b7a664099c669e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="refreshing-templates-for-users-and-services"></a>为用户和服务刷新模板

>*适用于：Azure 信息保护、Office 365*

使用 Azure 信息保护的 Azure Rights Management 服务时，模板会自动下载到客户端计算机，因而用户能够从他们的应用程序选择这些模板。 但是，如果你对模板进行了更改，可能还需要执行附加步骤：

|应用程序或服务|如何在更改后刷新模板|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />适用于传输规则和 Outlook Web App |1 小时内自动刷新 – 无需额外的步骤。<br /><br />如果使用[具有新功能的 Office 365 邮件加密](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)，则会出现这种情况。 如果之前已通过导入受信任的发布域 (TPD) 将 Exchange Online 配置为使用 Azure Rights Management 服务，请使用同一系列的说明在 Exchange Online 中启用这些新功能。|
|Azure 信息保护客户端|每当在客户端上的 Azure 信息保护策略刷新时，都会自动刷新：<br /><br /> - 打开支持 Azure 信息保护栏的 Office 应用程序时。 <br /><br /> - 右键单击以分类和保护文件或文件夹时。 <br /><br /> - 运行 PowerShell cmdlet 以实现标记和保护（Get-AIPFileStatus 和 Set-AIPFileLabel）。<br /><br /> - 启动 Azure 信息保护扫描程序服务时，以及本地策略已执行超过一小时时。 此外，扫描程序服务每小时检查一次更改，并将在下一个扫描周期中使用这些更改。<br /><br /> - 每 24 小时一次。<br /><br /> 此外，由于 Azure 信息保护客户端与 Office 紧密集成，因此任何适用于 Office 2016 或 Office 2013 的刷新后模板也会针对 Azure 信息保护客户端进行刷新。|
|Office 2016 和 Office 2013<br /><br />适用于 Windows 的 RMS 共享应用程序|自动刷新 – 按计划刷新：<br /><br />- 对于更高版本的 Office：默认刷新时间间隔为 7 天。<br /><br />- 对于 Windows RMS 共享应用程序：对于版本 1.0.1784.0 及更高版本，默认刷新时间间隔为 1 天。 以前版本的默认刷新间隔为 7 天。<br /><br />若要强制早于计划执行刷新，请参阅以下部分 [Office 2016、Office 2013 和 Windows RMS 共享应用程序：如何强制刷新更改的自定义模板](#office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template)。|
|Office 2010|当用户注销 Windows 后重新登录并等待长达 1 小时时自动刷新。|
|Exchange 內部部署与权限管理连接器<br /><br />适用于传输规则和 Outlook Web App|自动刷新 – 无需额外的步骤。 但是，Outlook Web App 可将该 UI 缓存一天。|
|Office 2016 for Mac|自动刷新 – 无需额外的步骤。|
|适用于 Mac 计算机的 RMS 共享应用|自动刷新 – 无需额外的步骤。|

当客户端应用程序需要下载模板（初始下载或刷新用于更改）时，请准备在下载完成并且新的或更新的模板完全可操作之前等待 15 分钟。 实际时间会因多种因素而异，例如模板配置的大小和复杂性以及网络连接。 

## <a name="office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template"></a>适用于 Windows 的 Office 2016、Office 2013 和 RMS 共享应用程序：如何强制执行针对已更改自定义模板的刷新
通过编辑运行 Office 2016、Office 2013 或适用于 Windows 的 Rights Management (RMS) 共享应用程序的计算机上的注册表，你可以更改自动计划，以便更改的模板在计算机上的刷新频率比其默认值更频繁。 你还可以通过删除注册表值中的现有数据，强制执行即时刷新。

> [!WARNING]
> 如果你没有正确使用注册表编辑器，则可能导致严重问题，需要你重新安装操作系统。 Microsoft 不保证能够解决因注册表编辑器使用不当而导致的问题。 你自行承担使用注册表编辑器的风险。

### <a name="to-change-the-automatic-schedule"></a>更改自动计划

1.  使用注册表编辑器，创建并设置以下注册表值中的某一个：

    - 设置以天为单位的更新频率（最少为 1 天）：创建名为“TemplateUpdateFrequency”  的新注册表值，并为该数据定义整数值，该值将指定向已下载模板下载任何更改的频率（以天为单位）。 使用以下信息查找创建此新注册表值的注册表路径。

        **注册表路径：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **类型：**REG_DWORD

        **值：**TemplateUpdateFrequency

    - 设置以秒为单位的更新频率（最少为 1 秒）：创建名为“TemplateUpdateFrequencyInSeconds”  的新注册表值，并为该数据定义整数值，该值将指定向已下载模板下载任何更改的频率（以秒为单位）。 使用以下信息查找创建此新注册表值的注册表路径。

        **注册表路径：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **类型：**REG_DWORD

        **值：**TemplateUpdateFrequencyInSeconds

    请确保你创建并设置这两个注册表值中的其中一个，而不是对这两个注册表值都执行此操作。 如果两者均存在，将忽略 **TemplateUpdateFrequency** 。

2.  如果你想要强制即时刷新模板，请转到下一个过程。 否则，请立即重启 Office 应用程序和文件资源管理器实例。

### <a name="to-force-an-immediate-refresh"></a>强制执行即时刷新

1.  使用注册表编辑器，删除“LastUpdatedTime”  值的数据。 例如，数据可能显示 **2015-04-20T15:52**；删除 2015-04-20T15:52 后，不会显示任何数据。 使用以下信息查找删除此注册表值数据的注册表路径。

    **注册表路径：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<*MicrosoftRMS_FQDN*>\Template

    **类型：** REG_SZ

    **值：**LastUpdatedTime

    > [!TIP]
        > 在注册表路径中，<*MicrosoftRMS_FQDN*> 是指你的 Microsoft RMS 服务 FQDN。 如果你想要验证此值：

    > 1.  对 Azure RMS 运行 [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet。 如果尚未安装适用于 Azure RMS 的 Windows PowerShell 模块，请参阅[安装 AADRM PowerShell 模块](install-powershell.md)。
    > 2.  在输出中找到 **LicensingIntranetDistributionPointUrl** 值。
    >
    >     示例：**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  在该值中，将 **https://** 和 **/_wmcs/licensing** 从该字符串中删除。 剩下的值就是 Microsoft RMS 服务 FQDN。 在我们的示例中，Microsoft RMS 服务 FQDN 会是以下值：
    >
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  删除以下文件夹及其包含的所有文件：**%localappdata%\Microsoft\MSIPC\Templates**

3.  请重启 Office 应用程序和文件资源管理器实例。


## <a name="see-also"></a>另请参阅
[在 Azure 信息保护策略中配置和管理模板](../deploy-use/configure-policy-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
