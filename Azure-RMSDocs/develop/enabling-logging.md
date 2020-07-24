---
title: 如何&#58;启用错误和性能日志记录 | Azure RMS
description: Microsoft Rights Management SDK 4.2 通过单个设备属性管理诊断和性能日志上传。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 4a9f0b375f9e152d44f4d5b5251a9259456db53c
ms.sourcegitcommit: 84b45c949d85a7291c088a050d2a66d356fc9af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2020
ms.locfileid: "87135702"
---
# <a name="how-to-enable-error-and-performance-logging"></a>如何：启用错误和性能日志记录
Microsoft Rights Management SDK 4.2 通过单个设备属性管理诊断和性能日志上传。

## <a name="overview"></a>概述 ##
通过启用将自动诊断、性能和遥测日志记录数据上传到 Microsoft 的功能，可以改进用户的体验并进行故障排除。 

> [!IMPORTANT] 
> 为了尊重用户隐私，作为应用开发人员，你在启用自动日志记录之前必须征得用户同意。

> [!NOTE]
> 例如，下面是 Microsoft 用于日志记录通知的标准消息： 
>
> *通过启用错误和性能日志记录，你同意将错误和性能数据发送给 Microsoft。 Microsoft 将通过 internet 收集错误和性能数据（"数据"）。 Microsoft 使用此数据提供并改进 Microsoft 产品和服务的质量、安全性和完整性。 例如，我们会分析性能和可靠性，如您使用哪些功能、功能响应的速度、设备性能、用户界面交互以及您对产品所遇到的任何问题。 数据还将包含有关软件配置的信息（如当前正在运行的软件）以及 IP 地址。*  

你将通过两个属性管理日志记录控件。

-   通过 **IpcCustomerExperienceDataCollectionEnabled** 属性启用日志记录。 跨设备进行重置，该设置具有永久性。
-   使用以下设置通过 **IpcLogLevel** 属性控制日志记录级别。

    * 1 - 详细
    * 2 - 信息性
    * 3 - 警告
    * 4 - 错误
    * 5 - 严重

在下面的每个示例代码片段中，调用应用程序可以设置或查询该属性。

### <a name="android"></a>Android ###
启用自动日志记录

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
SharedPreferences.Editor editor = preferences.edit();
editor.putBoolean("IpcCustomerExperienceDataCollectionEnabled", true);
editor.commit();
```

获取当前日志记录控制标志设置

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);
```

## <a name="ios"></a>iOS ##
启用自动日志记录

```objectivec
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setBool:FALSE forKey:@"IpcCustomerExperienceDataCollectionEnabled"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

获取当前日志记录控制标志设置

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcCustomerExperienceDataCollectionEnabled"];
```

设置日志级别控制

```java
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setInteger:1 forKey:@"IpcLogLevel"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

获取日志级别控制设置

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcLogLevel"];
```

## <a name="windows"></a>Windows ##
启用自动日志记录

```cpp
CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;
```

有关可选设置的详细信息，请参阅 [CustomerExperienceOptions](https://msdn.microsoft.com/library/microsoft.rightsmanagement.customerexperienceoptions.aspx)。

获取当前日志记录控制标志设置

```cpp
CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;
```

**请注意** - 上面的 Windows 代码片段使用的是 C++。 对于 C\#，请使用“.” 而不是“::”更新语法。

**Linux / C++** - 此 SDK 中包含一些基本的日志记录，它们没有其他平台的日志记录那样宽泛。 有关详细信息，请参阅[可移植 C++ 的 RMS SDK](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting) 中的“README.md”的**疑难解答**部分。
