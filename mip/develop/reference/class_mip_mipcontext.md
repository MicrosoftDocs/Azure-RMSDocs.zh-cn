---
title: 类 mip：： MipContext
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： mipcontext 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 9efbe9330014458a26f62e4dfac9ea24ad5d4475
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73561035"
---
# <a name="class-mipmipcontext"></a>类 mip：： MipContext 
MipContext 表示在所有配置文件、引擎和处理程序之间共享的状态。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共失效关闭（）  |  终止 MIP。
public bool IsFeatureEnabled （FlightingFeature 功能） const  |  获取是否启用功能。
public const ApplicationInfo& GetApplicationInfo() const  |  获取应用程序说明。
public const std：： string & GetMipPath （） const  |  获取日志、缓存等的文件路径。
public bool IsOfflineOnly （）  |  仅限脱机设置。
public std：： shared_ptr\<LoggerDelegate\> GetLoggerDelegate （）  |  获取记录器实现。
public LoggerDelegate * GetRawLoggerDelegate （）  |  获取记录器实现。
public static MIP_API std：： shared_ptr&lt;MipContext&gt; __CDECL MIP：： MipContext：： Create | 创建要在初始化配置文件时使用的新的 MipContext 实例。
public static MIP_API std：： shared_ptr&lt;MipContext&gt; __CDECL MIP：： MipContext：： CreateWithCustomFeatureSettings | 使用自定义功能设置创建新的 MipContext 实例。

## <a name="members"></a>成員
  
### <a name="shutdown-function"></a>ShutDown 函数
终止 MIP。
必须先调用此方法，然后才能关闭进程/DLL
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled 函数
获取是否启用功能。

参数：  
* **功能**：启用/禁用功能



  
**返回**：如果应用程序未提供 FeatureFlightingDelegate，是否启用功能，这将始终返回 true
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 函数
获取应用程序说明。

  
**返回**：应用程序说明
  
### <a name="getmippath-function"></a>GetMipPath 函数
获取日志、缓存等的文件路径。

  
**返回**：文件路径（带有 "mip" 叶目录）
  
### <a name="isofflineonly-function"></a>IsOfflineOnly 函数
仅限脱机设置。

  
**返回**：应用程序是否在仅脱机模式下运行
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 函数
获取记录器实现。

  
返回结果：记录器
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate 函数
获取记录器实现。

  
返回结果：记录器

### <a name="create-function"></a>Create 函数
创建要在初始化配置文件时使用的新的 MipContext 实例。

**返回**： MipContext 实例。

### <a name="createwithcustomfeaturesettings-function"></a>CreateWithCustomFeatureSettings 函数
使用自定义功能设置创建新的 MipContext 实例。

**返回**： MipContext 实例。