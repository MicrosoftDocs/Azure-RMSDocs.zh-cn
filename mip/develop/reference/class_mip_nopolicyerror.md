---
title: 类 mip::NoPolicyError
description: 记录 mip::nopolicyerror 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 107aab66dc62592bda5b6833911a446e0013db41
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573507"
---
# <a name="class-mipnopolicyerror"></a>类 mip::NoPolicyError 
租户策略未配置的分类/标签。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public char const* what() const  |  获取错误消息。
public std::\<错误\>const clone （)  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public virtual const std::string& GetErrorName() const  |  获取错误名称。
public virtual const std::string& GetMessage() const  |  获取错误消息。
public virtual void SetMessage(const std::string& msg)  |  设置错误消息。
  
## <a name="members"></a>成員
  
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
