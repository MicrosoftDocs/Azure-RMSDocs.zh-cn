---
title: class mip::JustificationRequiredError
description: 记录 mip::justificationrequirederror 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: f24b380b892739faec0602f3dd6b60467e4f4993
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60174130"
---
# <a name="class-mipjustificationrequirederror"></a>class mip::JustificationRequiredError 
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 std:: shared_ptr\<错误\>const clone （)  |  克隆错误。
public char const* what() const  |  获取错误消息。
public std::\<错误\>const clone （)  |  克隆错误。
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