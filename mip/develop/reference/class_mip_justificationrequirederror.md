---
title: class mip JustificationRequiredError
description: class mip JustificationRequiredError 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 059d139fc5222fd5f1865c66834519347e23a5a9
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445982"
---
# <a name="class-mipjustificationrequirederror"></a>class mip::JustificationRequiredError 
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual std::shared_ptr<Error> Clone() const  |  克隆错误。
 public char const* what() const  |  获取错误消息。
 public virtual ErrorType GetErrorType() const  |  获取错误类型。
 public virtual const std::string& GetErrorName() const  |  获取错误名称。
 public virtual const std::string& GetMessage() const  |  获取错误消息。
 public virtual void SetMessage(const std::string& msg)  |  设置错误消息。
  
## <a name="members"></a>成員
  
### <a name="error"></a>错误
克隆错误。

  
**返回结果**：错误副本。
  
### <a name="what"></a>what
获取错误消息。

  
返回结果：错误消息
  
### <a name="errortype"></a>ErrorType
获取错误类型。

  
**返回结果**：错误类型。
  
### <a name="geterrorname"></a>GetErrorName
获取错误名称。

  
**返回结果**：错误名称。
  
### <a name="getmessage"></a>GetMessage
获取错误消息。

  
**返回结果**：错误消息。
  
### <a name="setmessage"></a>SetMessage
设置错误消息。

参数：  
* **msg**：错误消息。

