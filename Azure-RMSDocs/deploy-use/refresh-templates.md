---
# required metadata

title: 刷新模板 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# 为用户刷新模板
当你使用 Azure RMS 时，模板会自动下载到客户端计算机，因而用户能够从他们的应用程序选择这些模板。 但是，如果你对模板进行了更改，可能还需要执行附加步骤：

|应用程序或服务|如何在更改后刷新模板|
|--------------------------|---------------------------------------------|
|Exchange Online|需要手动配置来刷新模板。<br /><br />有关配置步骤，请参阅以下部分：[仅适用于 Exchange Online：如何将 Exchange 配置为下载已更改的自定义模板](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates)。|
|Office 365|自动刷新 – 无需额外的步骤。|
|Office 2016 和 Office 2013<br /><br />适用于 Windows 的 RMS 共享应用程序|自动刷新 – 按计划刷新：<br /><br />对于这些更高版本的 Office：默认刷新间隔是 7 天。<br /><br />对于适用于 Windows 的 RMS 共享应用程序：从版本 1.0.1784.0 开始，默认刷新间隔是 1 天。 以前版本的默认刷新间隔为 7 天。<br /><br />若要强制执行比此计划更快的刷新，请参阅以下部分：[适用于 Windows 的 Office 2016、Office 2013 和 RMS 共享应用程序：如何强制执行针对已更改自定义模板的刷新](#office-2016-office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template)。|
|Office 2010|当用户登录时刷新。<br /><br />若要强制执行刷新，应要求或强制用户注销和重新登录。 或者，请参阅以下部分：[仅适用于 Office 2010：如何强制执行针对已更改自定义模板的刷新](#office-2010-only-how-to-force-a-refresh-for-a-changed-custom-template)。|
对于使用 RMS 共享应用程序的移动设备，模板会自动下载（必要时还会刷新），而无需其他配置。

## 仅适用于 Exchange Online：如何将 Exchange 配置为下载已更改的自定义模板
如果你已经为 Exchange Online 配置了信息权限管理 (IRM)，则不会为用户下载自定义模板，除非你使用 Windows PowerShell 在 Exchange Online 中进行了下列更改：

> [!NOTE]
> 有关如何在 Exchange Online 中使用 Windows PowerShell 的详细信息，请参阅[在 Exchange Online 中使用 PowerShell](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx)。

每次更改模板时，你必须执行此过程。

### 为 Exchange Online 更新模板

1.  在 Exchange Online 中使用 Windows PowerShell 连接到服务：

    1.  提供你的 Office 365 用户名和密码：

        ```
        $Cred = Get-Credential
        ```

    2.  通过运行以下两个命令连接到 Exchange Online 服务：

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
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

## 适用于 Windows 的 Office 2016、Office 2013 和 RMS 共享应用程序：如何强制执行针对已更改自定义模板的刷新
通过编辑运行 Office 2016、Office 2013 或适用于 Windows 的 Rights Management (RMS) 共享应用程序的计算机上的注册表，你可以更改自动计划，以便更改的模板在计算机上的刷新频率比其默认值更频繁。 你还可以通过删除注册表值中的现有数据，强制执行即时刷新。

> [!WARNING]
> 如果你没有正确使用注册表编辑器，则可能导致严重问题，需要你重新安装操作系统。 Microsoft 无法保证你能够解决由于错误使用注册表编辑器而导致的问题。 你自行承担使用注册表编辑器的风险。

### 更改自动计划

1.  使用注册表编辑器，创建并设置以下注册表值中的某一个：

    - 设置以天为单位的更新频率（最少为 1 天）：创建名为“TemplateUpdateFrequency” **** 的新注册表值，并为该数据定义整数值，该值将指定向已下载模板下载任何更改的频率（以天为单位）。 使用下表查找创建此新注册表值的注册表路径。

        **注册表路径：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **类型：**REG_DWORD

        **值：**TemplateUpdateFrequency


    - To set an update frequency in seconds (minimum of 1 second):  Create a new registry value named **TemplateUpdateFrequencyInSeconds** and define an integer value for the data, which specifies the frequency in seconds to download any changes to a downloaded template. Use the following table to locate the registry path to create this new registry value.

        **Registry path:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Type:** REG_DWORD

        **Value:** TemplateUpdateFrequencyInSeconds

    Make sure that you create and set one of these registry values, not both. If both are present, **TemplateUpdateFrequency** is ignored.

2.  如果你想要强制即时刷新模板，请转到下一个过程。 否则，请立即重启 Office 应用程序和文件资源管理器实例。

### 强制执行即时刷新

1.  使用注册表编辑器，删除“LastUpdatedTime” **** 值的数据。 例如，数据可能显示 **2015-04-20T15:52**；删除 2015-04-20T15:52 后，不会显示任何数据。 使用以下信息查找删除此注册表值数据的注册表路径。

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

## 仅适用于 Office 2010：如何强制执行针对已更改自定义模板的刷新
通过编辑运行 Office 2010 的计算机上的注册表，你可以设置值，使得更改的模板在计算机上无需等待用户注销后又重新打开即可刷新。 你还可以通过删除注册表值中的现有数据，强制执行即时刷新。

> [!WARNING]
> 如果你没有正确使用注册表编辑器，则可能导致严重问题，需要你重新安装操作系统。 Microsoft 无法保证你能够解决由于错误使用注册表编辑器而导致的问题。 你自行承担使用注册表编辑器的风险。

### 更改更新频率

1.  使用注册表编辑器，创建名为“UpdateFrequency” **** 的新注册表值，并为该数据定义整数值，该值将指定向已下载模板下载任何更改的频率（以天为单位）。 使用下表查找创建此新注册表值的注册表路径。

    **注册表路径：**HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **类型：**REG_DWORD

    **值：**UpdateFrequency

2.  如果你想要强制即时刷新模板，请转到下一个过程。 否则，请立即重新启动 Office 应用程序。

### 强制执行即时刷新

1.  使用注册表编辑器，删除“LastUpdatedTime” **** 值的数据。 例如，数据可能显示 **2015-04-20T15:52**；删除 2015-04-20T15:52 后，不会显示任何数据。 使用下表查找删除此注册表值数据的注册表路径。

    **注册表路径：**HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **类型：** REG_SZ

    **值：**lastUpdatedTime


2.  删除以下文件夹及其包含的所有文件：**%localappdata%\Microsoft\MSIPC\Templates**

3.  重新启动 Office 应用程序。

## 另请参阅
[为 Azure Rights Management 配置自定义模板](configure-custom-templates.md)

<!--HONumber=Apr16_HO3-->

