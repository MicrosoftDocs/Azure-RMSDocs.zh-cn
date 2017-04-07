---
title: "刷新 Azure RMS 模板 - AIP"
description: "使用 Azure Rights Management 服务时，模板会自动下载到客户端计算机，因而用户能够从他们的应用程序选择这些模板。 但是，如果对模板进行了更改，可能还需要执行附加步骤。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 77bd9e7bedf4a319f8f911782c995066a26a7055
ms.sourcegitcommit: 8ae83a9fc03bf2ee39ea758835ef52156f19784d
translationtype: HT
---
# <a name="refreshing-templates-for-users"></a>为用户刷新模板

>*适用于：Azure 信息保护、Office 365*

使用 Azure 信息保护的 Azure Rights Management 服务时，模板会自动下载到客户端计算机，因而用户能够从他们的应用程序选择这些模板。 但是，如果你对模板进行了更改，可能还需要执行附加步骤：

|应用程序或服务|如何在更改后刷新模板|
|--------------------------|---------------------------------------------|
|Exchange Online|需要手动配置来刷新模板。<br /><br />有关配置步骤，请参阅以下部分：[仅适用于 Exchange Online：如何将 Exchange 配置为下载已更改的自定义模板](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates)。|
|Azure 信息保护客户端|每当在客户端上的 Azure 信息保护策略刷新时，都会自动刷新：<br /><br /> - 打开支持 Azure 信息保护栏的 Office 应用程序时。 <br /><br /> - 右键单击以分类和保护文件或文件夹时。 <br /><br /> - 运行 PowerShell cmdlet 以实现标记和保护（Get-AIPFileStatus 和 Set-AIPFileLabel）。<br /><br /> - 每 24 小时一次。<br /><br /> 此外，由于 Azure 信息保护客户端与 Office 紧密集成，因此任何适用于 Office 2016 或 Office 2013 的刷新后模板也会针对 Azure 信息保护客户端进行刷新。|
|Office 2016 和 Office 2013<br /><br />适用于 Windows 的 RMS 共享应用程序|自动刷新 – 按计划刷新：<br /><br />- 对于更高版本的 Office：默认刷新时间间隔为 7 天。<br /><br />- 对于 Windows RMS 共享应用程序：对于版本 1.0.1784.0 及更高版本，默认刷新时间间隔为 1 天。 以前版本的默认刷新间隔为 7 天。<br /><br />若要强制早于计划执行刷新，请参阅以下部分 [Office 2016、Office 2013 和 Windows RMS 共享应用程序：如何强制刷新更改的自定义模板](#office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template)。|
|Office 2010|当用户注销 Windows 后重新登录并等待长达 1 小时时自动刷新。|
|Office 2016 for Mac|自动刷新 – 无需额外的步骤。|
|适用于移动设备的 RMS 共享应用程序|自动刷新 – 无需额外的步骤。|


## <a name="exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates"></a>仅适用于 Exchange Online：如何将 Exchange 配置为下载已更改的自定义模板
如果你已经为 Exchange Online 配置了信息权限管理 (IRM)，则不会为用户下载自定义模板，除非你使用 Windows PowerShell 在 Exchange Online 中进行了下列更改：

> [!NOTE]
> 有关如何在 Exchange Online 中使用 Windows PowerShell 的详细信息，请参阅[在 Exchange Online 中使用 PowerShell](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx)。

每次更改模板时，你必须执行此过程。

### <a name="to-update-templates-for-exchange-online"></a>为 Exchange Online 更新模板

1.  在 Exchange Online 中使用 Windows PowerShell 连接到服务：

    1.  提供你的 Office 365 用户名和密码：

        ```
        $UserCredential = Get-Credential
        ```

    2.  通过运行以下两个命令连接到 Exchange Online 服务：

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  使用 [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) cmdlet，从 Azure RMS 重新导入你的受信任发布域 (TPD)：

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    例如，如果 TPD 名为 **RMS Online - 1**（很多组织的典型名称），则输入：**Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > 若要验证你的 TPD 名称，可以使用 [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) cmdlet。

3.  若要确认模板已经成功导入，请等候几分钟，然后运行 [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) cmdlet 并将 Type 设为 All。 例如：

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > 保留输出的副本很有用，这样，如果你以后将模板存档，可以轻松地复制模板名称或 GUID。

4.  对于需要在 Outlook Web App 中使用的每个已导入的模板，你必须使用 [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet 并将 Type 设置为 Distributed：

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    由于 Outlook Web Access 缓存 UI 24 小时，用户可能最长在一天之内都看不到新模板。

此外，如果你存档一个模板（自定义或默认），并将 Exchange Online 和 Office 365 配合使用，则如果用户使用 Outlook Web App 或运行 Exchange ActiveSync 协议的移动设备，他们仍然可以看到存档的模板。

因此用户再也看不到这些模板，这种情况下，请使用 Exchange Online 中的 Windows PowerShell 连接到服务，然后通过运行以下命令来使用 [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) cmdlet：

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

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

    > 1.  对 Azure RMS 运行 [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet。 如果你尚未安装适用于 Azure RMS 的 Windows PowerShell 模块，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。
    > 2.  在输出中找到 **LicensingIntranetDistributionPointUrl** 值。
    > 
    >     示例：**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  在该值中，将 **https://** 和 **/_wmcs/licensing** 从该字符串中删除。 剩下的值就是 Microsoft RMS 服务 FQDN。 在我们的示例中，Microsoft RMS 服务 FQDN 会是以下值：
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  删除以下文件夹及其包含的所有文件：**%localappdata%\Microsoft\MSIPC\Templates**

3.  请重启 Office 应用程序和文件资源管理器实例。


## <a name="see-also"></a>另请参阅
[为 Azure Rights Management 配置自定义模板](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]