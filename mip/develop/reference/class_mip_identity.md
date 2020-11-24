---
title: 类标识
description: 记录 (MIP) SDK 的标识：：未定义的 Microsoft 信息保护类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: ae89ed32a48deae7132bc65adabf86f7fb63ffe1
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565115"
---
# <a name="class-identity"></a>类标识 
标识的抽象。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共标识 ( # A1  |  用户电子邮件地址未知时使用的默认标识构造函数。
公共标识 (const 标识& 其他)   |  标识复制构造函数。
公共显式标识 (const std：： string& email)   |  用户电子邮件地址已知时使用的标识构造函数。
公共显式标识 (const std：： string& email，const std：： string& 名称)   |  用户电子邮件地址和用户名已知时使用的标识构造函数。
public const std：： string& GetEmail ( # A2 const  |  获取电子邮件。
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