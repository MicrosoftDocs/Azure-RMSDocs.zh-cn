---
title: 类标识
description: 记录 Microsoft 信息保护（MIP） SDK 的标识：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 1b1dbbe146832773613124917c1ea6d43f5cf13a
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762364"
---
# <a name="class-identity"></a>类标识 
标识的抽象。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共标识（）  |  用户电子邮件地址未知时使用的默认标识构造函数。
公共标识（const 标识& 其他）  |  标识复制构造函数。
公共显式标识（const std：： string& email）  |  用户电子邮件地址已知时使用的标识构造函数。
公共显式标识（const std：： string& email，const std：： string& name）  |  用户电子邮件地址和用户名已知时使用的标识构造函数。
public const std：： string& GetEmail （） const  |  获取电子邮件。
public const std::string& GetName() const  |  获取用户的友好名称。 用于文本标记。
  
## <a name="members"></a>成员
  
### <a name="identity-function"></a>标识函数
用户电子邮件地址未知时使用的默认标识构造函数。
  
### <a name="identity-function"></a>标识函数
标识复制构造函数。

参数：  
* **标识**：用于创建副本。


  
### <a name="identity-function"></a>标识函数
用户电子邮件地址已知时使用的标识构造函数。

参数：  
* **电子邮件**：必须是有效的电子邮件地址。


  
### <a name="identity-function"></a>标识函数
用户电子邮件地址和用户名已知时使用的标识构造函数。

参数：  
* **电子邮件**：必须是有效的电子邮件地址。 


* **名称**：用户名。


  
### <a name="getemail-function"></a>GetEmail 函数
获取电子邮件。

  
**返回**：电子邮件。
  
### <a name="getname-function"></a>GetName 函数
获取用户的友好名称。 用于文本标记。

  
**返回**：友好名称。