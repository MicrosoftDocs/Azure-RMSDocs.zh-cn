---
title: class mip::TransientNetworkError
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: transientnetworkerror 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 5787c5742edc2daefee00a3c5a9b2bf826b81529
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882906"
---
# <a name="class-miptransientnetworkerror"></a>class mip::TransientNetworkError 
暂时性网络错误。 对服务终结点执行网络调用时，由于意外行为所致。 此错误是暂时性错误，因此可重试该操作。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public char const* what() const  |  获取错误消息。
public std:: shared_ptr\<错误\> Clone () const  |  克隆错误。
public virtual ErrorType GetErrorType() const  |  获取错误类型。
public virtual const std::string& GetErrorName() const  |  获取错误名称。
public virtual const std::string& GetMessage() const  |  获取错误消息。
public virtual void SetMessage(const std::string& msg)  |  设置错误消息。
  
## <a name="members"></a>成员
  
### <a name="what-function"></a>什么函数
获取错误消息。

  
**返回**:错误消息
  
### <a name="clone-function"></a>Clone 函数
克隆错误。

  
**返回**:错误的克隆。
  
### <a name="geterrortype-function"></a>GetErrorType 函数
获取错误类型。

  
**返回**:错误类型。
  
### <a name="geterrorname-function"></a>GetErrorName 函数
获取错误名称。

  
**返回**:错误名称。
  
### <a name="getmessage-function"></a>GetMessage 函数
获取错误消息。

  
**返回**:错误消息。
  
### <a name="setmessage-function"></a>SetMessage 函数
设置错误消息。

参数：  
* **msg**：错误消息。

