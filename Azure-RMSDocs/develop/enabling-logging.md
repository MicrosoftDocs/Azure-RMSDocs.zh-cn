---
title: "如何&#58;启用错误和性能日志记录 | Azure RMS"
description: "Microsoft Rights Management SDK 4.2 通过单个设备属性管理诊断和性能日志上传。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79e58b8092ea7cb057229d4c464d79f3694296e6
ms.openlocfilehash: 5faea360de8aa9ecb82abf25b5c1392d52d0afad


---

# 如何：启用错误和性能日志记录
Microsoft Rights Management SDK 4.2 通过单个设备属性管理诊断和性能日志上传。

## 概述 ##
通过启用自动诊断和性能日志记录上传到 Microsoft，可以改进你的用户体验并进行故障排除。 为了尊重用户隐私，作为应用开发人员，你在启用自动日志记录之前必须征得用户同意。

你将通过两个属性管理日志记录控件。

-   通过 **IpcCustomerExperienceDataCollectionEnabled** 属性启用日志记录。 跨设备进行重置，该设置具有永久性。
-   使用以下设置通过 **IpcLogLevel** 属性控制日志记录级别。

    * 1 - 详细
    * 2 - 信息性
    * 3 - 警告
    * 4 - 错误
    * 5 - 严重

在下面的每个示例代码片段中，调用应用程序可以设置或查询该属性。

### Android ###
启用自动日志记录

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

获取当前日志记录控制标志设置

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
启用自动日志记录

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

获取当前日志记录控制标志设置

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

设置日志级别控制

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

获取日志级别控制设置

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## Windows ##
启用自动日志记录

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

有关可选设置的详细信息，请参阅 [CustomerExperienceOptions](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions)。

获取当前日志记录控制标志设置

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**请注意** - 上面的 Windows 代码片段使用的是 C++。 对于 C\#，请使用“.” 而不是“::”更新语法。

**Linux / C++** - 此 SDK 中包含一些基本的日志记录，它们没有其他平台的日志记录那样宽泛。 有关详细信息，请参阅[可移植 C++ 的 RMS SDK](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting) 中的“README.md”的**疑难解答**部分。

 

 



<!--HONumber=Jul16_HO3-->


