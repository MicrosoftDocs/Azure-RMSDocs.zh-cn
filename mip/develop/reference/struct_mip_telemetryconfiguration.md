---
title: 结构 mip：： TelemetryConfiguration
description: 与 Microsoft 信息保护（MIP） SDK 关联的文档结构。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 4e3e9be086bbcddea5398ccfbe549ffc2ca1aae6
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73567521"
---
# <a name="struct-miptelemetryconfiguration"></a>结构 mip：： TelemetryConfiguration 
自定义遥测设置（不常用）
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string hostNameOverride  |  主机遥测实例名称。 如果未设置，则 MIP 将充当自己的主机。
public std：： string libraryNameOverride  |  备用遥测库（DLL）文件名。
public std：： shared_ptr\<HttpDelegate\> httpDelegateOverride  |  如果已设置，则 HTTP 处理将由此实例管理
public std：： shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  如果已设置，则异步任务处理将由此实例管理，taskDispatcherDelegateOverides 不应共享，因为它们可以持有遥测对象，并阻止其发布，直到 taskDispatcher 释放。
public bool isNetworkDetectionEnabled  |  如果已设置，遥测组件会 ping 后台线程上的网络状态
public bool isLocalCachingEnabled  |  如果设置，遥测组件将使用磁盘上的缓存
public bool isTraceLoggingEnabled  |  如果已设置，遥测组件会将警告/错误日志写入磁盘
public bool isTelemetryOptedOut  |  如果已设置，则仅发送必要的服务数据遥测
public bool isFastShutdownEnabled  |  如果设置此设置，则在关闭时不会上载任何事件，在日志记录后将立即上载审核事件
public std：： map\<std：： string，std：： string\> customSettings  |  自定义遥测设置 >
  
## <a name="members"></a>成員
  
### <a name="hostnameoverride-struct-member"></a>hostNameOverride 结构成员
主机遥测实例名称。 如果未设置，则 MIP 将充当自己的主机。
  
### <a name="librarynameoverride-struct-member"></a>libraryNameOverride 结构成员
备用遥测库（DLL）文件名。
  
### <a name="httpdelegate"></a>HttpDelegate
如果已设置，则 HTTP 处理将由此实例管理
  
### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
如果已设置，则异步任务处理将由此实例管理，taskDispatcherDelegateOverides 不应共享，因为它们可以持有遥测对象，并阻止其发布，直到 taskDispatcher 释放。
  
### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled 结构成员
如果已设置，遥测组件会 ping 后台线程上的网络状态
  
### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled 结构成员
如果设置，遥测组件将使用磁盘上的缓存
  
### <a name="istraceloggingenabled-struct-member"></a>isTraceLoggingEnabled 结构成员
如果已设置，遥测组件会将警告/错误日志写入磁盘
  
### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut 结构成员
如果已设置，则仅发送必要的服务数据遥测
  
### <a name="isfastshutdownenabled-struct-member"></a>isFastShutdownEnabled 结构成员
如果设置此设置，则在关闭时不会上载任何事件，在日志记录后将立即上载审核事件
  
### <a name="customsettings-struct-member"></a>customSettings 结构成员
自定义遥测设置 >