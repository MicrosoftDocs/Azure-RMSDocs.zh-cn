---
title: 类 mip::ServiceDisabledError
description: 记录 mip::servicedisablederror 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: adcdb252fc6988f7047c2d940ddaa19fe8381405
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256441"
---
# <a name="class-mipservicedisablederror"></a>类 mip::ServiceDisabledError 
用户无法获取访问内容，因为服务被禁用。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共扩展盘区 GetExtent() 常量  |  获取为其禁用该服务的范围。
public char const* what() const  |  获取错误消息。
public std::\<错误\>const clone （)  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public virtual const std::string& GetErrorName() const  |  获取错误名称。
public virtual const std::string& GetMessage() const  |  获取错误消息。
public virtual void SetMessage(const std::string& msg)  |  设置错误消息。
枚举范围  |  介绍了为其禁用该服务的范围。
  
## <a name="members"></a>成員
  
### <a name="getextent-function"></a>GetExtent 函数
获取为其禁用该服务的范围。

  
**返回**:为其禁用该服务的范围
  
### <a name="what-function"></a>哪项功能
获取错误消息。

  
**返回**:错误消息
  
### <a name="clone-function"></a>Clone 函数
克隆错误。

  
**返回**:错误的副本。
  
### <a name="geterrortype-function"></a>GetErrorType 函数
获取错误类型。

  
**返回**:错误类型。
  
### <a name="geterrorname-function"></a>GetErrorName 函数
获取错误名称。

  
**返回**:错误名称。
  
### <a name="getmessage-function"></a>GetMessage 函数
获取错误消息。

  
**返回**:错误消息中。
  
### <a name="setmessage-function"></a>SetMessage 函数
设置错误消息。

参数：  
* **msg**：错误消息。


  
### <a name="extent-enum"></a>程度枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
“用户”            | 服务已禁用的用户。
设备            | 服务已禁用的设备。
平台            | 服务已禁用的平台。
租户            | 服务已禁用的租户。
介绍了为其禁用该服务的范围。
