---
title: 类 MipContext
description: 记录 Microsoft 信息保护（MIP） SDK 的 mipcontext：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: cf191a1e770d13d84603fe593d63dedb98bbb14b
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761464"
---
# <a name="class-mipcontext"></a>类 MipContext 
MipContext 表示在所有配置文件、引擎和处理程序之间共享的状态。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共失效关闭（）  |  终止 MIP。
public bool IsFeatureEnabled （FlightingFeature 功能） const  |  获取是否启用功能。
public const ApplicationInfo& GetApplicationInfo() const  |  获取应用程序说明。
public const std：： string& GetMipPath （） const  |  获取日志、缓存等的文件路径。
public bool IsOfflineOnly （）  |  仅限脱机设置。
public LogLevel GetThresholdLogLevel （） const  |  获取阈值日志级别。
public std：： shared_ptr\<LoggerDelegate\> GetLoggerDelegate （）  |  获取记录器实现。
public LoggerDelegate * GetRawLoggerDelegate （）  |  获取记录器实现。
public const std：： map\<FlightingFeature，Bool\>& GetFlightingFeatures （） const  |  获取试验功能集。
  
## <a name="members"></a>成员
  
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
  
### <a name="getthresholdloglevel-function"></a>GetThresholdLogLevel 函数
获取阈值日志级别。

  
**返回**：阈值日志级别
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 函数
获取记录器实现。

  
返回结果****：记录器
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate 函数
获取记录器实现。

  
返回结果****：记录器
  
### <a name="getflightingfeatures-function"></a>GetFlightingFeatures 函数
获取试验功能集。

  
**返回**：试验功能映射