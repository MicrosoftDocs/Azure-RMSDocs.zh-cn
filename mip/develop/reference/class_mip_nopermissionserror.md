---
title: 类 mip::NoPermissionsError
description: 记录 mip::nopermissionserror 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4a7b1af035b8a341ef16cabb10c788e5f5bc276c
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258855"
---
# <a name="class-mipnopermissionserror"></a>类 mip::NoPermissionsError 
用户无法访问内容。 例如，无权限、内容已撤销。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  获取联系人时对文档缺少权限。
public std::string GetOwner() const  | _尚无记录。_
public char const* what() const  |  获取错误消息。
public std::\<错误\>const clone （)  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public virtual const std::string& GetErrorName() const  |  获取错误名称。
public virtual const std::string& GetMessage() const  |  获取错误消息。
public virtual void SetMessage(const std::string& msg)  |  设置错误消息。
  
## <a name="members"></a>成員
  
### <a name="getreferrer-function"></a>GetReferrer 函数
获取联系人时对文档缺少权限。

  
**返回**:如果对文档缺少权限联系人。
  
### <a name="getowner-function"></a>GetOwner 函数
_尚无记录。_

  
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

