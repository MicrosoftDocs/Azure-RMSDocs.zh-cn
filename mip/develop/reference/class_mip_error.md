---
title: class mip::Error
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： error 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f59a2b394cbf0bfa5deb555e2c4cdd8c427ed7ea
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560297"
---
# <a name="class-miperror"></a>class mip::Error 
将从 MIP SDK 报告（引发或返回）的所有错误的基类。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public char const* what() const  |  获取错误消息。
public std：： shared_ptr\<错误\> Clone （） const  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public virtual const std::string& GetErrorName() const  |  获取错误名称。
public virtual const std::string& GetMessage() const  |  获取错误消息。
public virtual void SetMessage(const std::string& msg)  |  设置错误消息。
  
## <a name="members"></a>成員
  
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

