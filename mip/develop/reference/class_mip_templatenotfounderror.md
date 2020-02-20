---
title: 类 mip：： TemplateNotFoundError
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： templatenotfounderror 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: babcf77de224a75b2beec7e0b15c867698b49c15
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489310"
---
# <a name="class-miptemplatenotfounderror"></a>类 mip：： TemplateNotFoundError 
RMS 服务无法识别模板 ID。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string mMessage  | _尚无记录。_
public std：： map\<std：： string，std：： string\> mDebugInfo  | _尚无记录。_
public char const* what() const  |  获取错误消息。
公共 std：： shared_ptr\<错误\> Clone （） const  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public const std：： string & GetErrorName （） const  |  获取错误名称。
public const std：： string & GetMessage （） const  |  获取错误消息。
public void SetMessage （const std：： string & msg）  |  设置错误消息。
public void AddDebugInfo （const std：： string & key，const std：： string & 值）  |  添加调试信息项。
public const std：： map\<std：： string，std：： string\>& GetDebugInfo （） const  |  获取调试信息。
  
## <a name="members"></a>Members
  
### <a name="mmessage"></a>mMessage
_尚无记录。_

  
### <a name="mdebuginfo"></a>mDebugInfo
_尚无记录。_

  
### <a name="what-function"></a>什么函数
获取错误消息。

  
**返回结果**：错误消息
  
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

  
**返回结果**：错误消息。
  
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