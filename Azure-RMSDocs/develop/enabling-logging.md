---
title: 如何&#58;启用错误和性能日志记录 | Azure RMS
description: Microsoft Rights Management SDK 4.2 通过单个设备属性管理诊断和性能日志上传。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 906746990fd08a749d2879fbc04b054e49e65f01
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
ms.locfileid: "27764448"
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
> *启用错误和性能日志记录即表示同意向 Microsoft 发送错误和性能数据。Microsoft 会通过 Internet 收集错误和性能数据（统称“数据”）。Microsoft 利用此数据来保证并改进 Microsoft 产品和服务的质量、安全性和完整性。例如，会分析性能和可靠性（如使用哪些功能、功能的响应速度、设备性能、用户界面交互和遇到的任何产品问题）。数据还包括当前运行的软件以及 IP 地址的配置信息。*  

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

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

获取当前日志记录控制标志设置

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## <a name="ios"></a>iOS ##
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
 

## <a name="windows"></a>Windows ##
启用自动日志记录

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

有关可选设置的详细信息，请参阅 [CustomerExperienceOptions](https://msdn.microsoft.com/library/microsoft.rightsmanagement.customerexperienceoptions.aspx)。

获取当前日志记录控制标志设置

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**请注意** - 上面的 Windows 代码片段使用的是 C++。 对于 C\#，请使用“.” 而不是“::”更新语法。

**Linux / C++** - 此 SDK 中包含一些基本的日志记录，它们没有其他平台的日志记录那样宽泛。 有关详细信息，请参阅[可移植 C++ 的 RMS SDK](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting) 中的“README.md”的**疑难解答**部分。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]