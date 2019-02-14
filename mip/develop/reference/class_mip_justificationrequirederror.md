---
title: class mip::JustificationRequiredError
description: 记录 mip::justificationrequirederror 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 5c69aa3e8086fc19bc56cff4cf29347d7962a47d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259563"
---
# <a name="class-mipjustificationrequirederror"></a>class mip::JustificationRequiredError 
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 std:: shared_ptr\<错误\>const clone （)  |  克隆错误。
public char const* what() const  |  获取错误消息。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public virtual const std::string& GetErrorName() const  |  获取错误名称。
public virtual const std::string& GetMessage() const  |  获取错误消息。
public virtual void SetMessage(const std::string& msg)  |  设置错误消息。
  
## <a name="members"></a>成員
  
### <a name="clone-function"></a>Clone 函数
克隆错误。

  
**返回**:错误的副本。
  
### <a name="what-function"></a>哪项功能
获取错误消息。

  
**返回**:错误消息
  
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

