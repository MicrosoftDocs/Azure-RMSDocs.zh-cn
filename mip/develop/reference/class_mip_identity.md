---
title: 类 mip：： Identity
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： identity 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 633a0ac8536f7bbd285eee67934f27d65b399bf4
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560162"
---
# <a name="class-mipidentity"></a>类 mip：： Identity 
标识的抽象。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共标识（）  |  用户电子邮件地址未知时使用的默认标识构造函数。
公共标识（const 标识 & 其他）  |  标识复制构造函数。
公共显式标识（const std：： string & email）  |  用户电子邮件地址已知时使用的标识构造函数。
public const std：： string & GetEmail （） const  |  获取电子邮件。
  
## <a name="members"></a>成員
  
### <a name="identity-function"></a>标识函数
用户电子邮件地址未知时使用的默认标识构造函数。
  
### <a name="identity-function"></a>标识函数
标识复制构造函数。

参数：  
* **标识**：用于创建副本。


  
### <a name="identity-function"></a>标识函数
用户电子邮件地址已知时使用的标识构造函数。

参数：  
* **电子邮件**：用户电子邮件地址。


  
### <a name="getemail-function"></a>GetEmail 函数
获取电子邮件。

  
**返回**：电子邮件。