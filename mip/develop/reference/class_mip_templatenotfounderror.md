---
title: 类 TemplateNotFoundError
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 templatenotfounderror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 48182ae5d821aeed65e8c28b086dce0349b9af03
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212852"
---
# <a name="class-templatenotfounderror"></a>类 TemplateNotFoundError 
RMS 服务无法识别模板 ID。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string mMessage  | _尚无记录。_
public std：： map \<std::string, std::string\> mDebugInfo  | _尚无记录。_
public std：： string mName  | _尚无记录。_
公共 ErrorCode GetErrorCode ( # A1 const  |  获取错误输入的错误代码。
public char const* what() const  |  获取错误消息。
public std::shared_ptr\<Error\> Clone() const  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public const std：： string& GetErrorName ( # A2 const  |  获取错误名称。
public const std：： string& GetMessage ( # A2 const  |  获取错误消息。
公共 void SetMessage (const std：： string& msg)   |  设置错误消息。
public void AddDebugInfo (const std：： string& key，const std：： string& 值)   |  添加调试信息项。
public const std：： map \<std::string, std::string\>& GetDebugInfo ( # A2 const  |  获取调试信息。
枚举 ErrorCode  |  错误输入错误的错误代码。
  
## <a name="members"></a>成员
  
### <a name="mmessage"></a>mMessage
_尚无记录。_

  
### <a name="mdebuginfo"></a>mDebugInfo
_尚无记录。_

  
### <a name="mname"></a>mName
_尚无记录。_

  
### <a name="geterrorcode-function"></a>GetErrorCode 函数
获取错误输入的错误代码。

  
**返回**：错误输入错误的 ErrorCode
  
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

  
**返回**：调试信息 (键/值) 
  
### <a name="errorcode-enum"></a>ErrorCode 枚举

错误输入错误的错误代码。

 值                         | 说明                                
--------------------------------|---------------------------------------------
常规            | 常规错误输入错误
FileIsTooLargeForProtection            | 文件太大，无法进行保护
