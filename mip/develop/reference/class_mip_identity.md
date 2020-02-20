---
title: 类 mip：： Identity
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： identity 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d50092be5277d5e88e6ec408280ca76bbc333a4c
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488018"
---
# <a name="class-mipidentity"></a>类 mip：： Identity 
标识的抽象。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
公共标识（）  |  用户电子邮件地址未知时使用的默认标识构造函数。
公共标识（const 标识 & 其他）  |  标识复制构造函数。
公共显式标识（const std：： string & email）  |  用户电子邮件地址已知时使用的标识构造函数。
公共显式标识（const std：： string & email，const std：： string & name）  |  用户电子邮件地址和用户名已知时使用的标识构造函数。
public const std：： string & GetEmail （） const  |  获取电子邮件。
public const std::string& GetName() const  |  获取用户的友好名称。 用于文本标记。
  
## <a name="members"></a>Members
  
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