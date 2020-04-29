---
title: 类 TemplateNotFoundError
description: 记录 Microsoft 信息保护（MIP） SDK 的 templatenotfounderror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 9c8a1f1d89c581950bc1760a7bcb339e10114c2a
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764238"
---
# <a name="class-templatenotfounderror"></a>类 TemplateNotFoundError 
RMS 服务无法识别模板 ID。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string mMessage  | _尚无记录。_
public std：： map\<std：： string，std：： string\> mDebugInfo  | _尚无记录。_
public char const* what() const  |  获取错误消息。
public std：： shared_ptr\<错误\> Clone （） const  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public const std：： string& GetErrorName （） const  |  获取错误名称。
public const std：： string& GetMessage （） const  |  获取错误消息。
public void SetMessage （const std：： string& msg）  |  设置错误消息。
public void AddDebugInfo （const std：： string& key，const std：： string& 值）  |  添加调试信息项。
public const std：： map\<std：： string，std：： String\>& GetDebugInfo （） const  |  获取调试信息。
  
## <a name="members"></a>成员
  
### <a name="mmessage"></a>mMessage
_尚无记录。_

  
### <a name="mdebuginfo"></a>mDebugInfo
_尚无记录。_

  
### <a name="what-function"></a>什么函数
获取错误消息。

  
**返回**：错误消息
  
### <a name="clone-function"></a>Clone 函数
克隆错误。

  
**返回结果**：错误副本。
  
### <a name="geterrortype-function"></a>GetErrorType 函数
获取错误类型。

  
**返回结果**：错误类型。
  
### <a name="geterrorname-function"></a>GetErrorName 函数
获取错误名称。

  
**返回结果**：错误名称。
  
### <a name="getmessage-function"></a>GetMessage 函数
获取错误消息。

  
**返回**：错误消息。
  
### <a name="setmessage-function"></a>SetMessage 函数
设置错误消息。

参数：  
* **msg**：错误消息。


  
### <a name="adddebuginfo-function"></a>AddDebugInfo 函数
添加调试信息项。

参数：  
* **密钥**：调试信息密钥 


* **值**：调试信息值


  
### <a name="getdebuginfo-function"></a>GetDebugInfo 函数
获取调试信息。

  
**返回**：调试信息（键/值）