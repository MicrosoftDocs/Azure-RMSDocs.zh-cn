---
title: 类 mip::Identity
description: 记录 mip::identity 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b315dd23ee6dddfc20b2c4d9febdbfabd0ecb3b3
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255098"
---
# <a name="class-mipidentity"></a>类 mip::Identity 
标识抽象。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共 Identity()  |  默认值[标识](class_mip_identity.md)不知道用户电子邮件地址时使用的构造函数。
公共显式标识 (const std:: string & 电子邮件)  |  [标识](class_mip_identity.md)知道用户电子邮件地址时使用的构造函数。
public const std:: string & GetEmail() 常量  |  收到电子邮件。
public void SetDelegatedEmail (const std:: string & delegatedEmail)  |  设置委派的电子邮件，委派的电子邮件地址的用户为其执行 opertations 的、 代表。
public const std:: string & GetDelegatedEmail() 常量  |  获取委托的电子邮件，委派的电子邮件地址的用户为其执行 opertations、 代表。
  
## <a name="members"></a>成員
  
### <a name="identity-function"></a>Identity 函数
默认值[标识](class_mip_identity.md)不知道用户电子邮件地址时使用的构造函数。
  
### <a name="identity-function"></a>Identity 函数
[标识](class_mip_identity.md)知道用户电子邮件地址时使用的构造函数。

参数：  
* **电子邮件**： 用户电子邮件地址。


  
### <a name="getemail-function"></a>GetEmail 函数
收到电子邮件。

  
**返回**:电子邮件。
  
### <a name="setdelegatedemail-function"></a>SetDelegatedEmail 函数
设置委派的电子邮件，委派的电子邮件地址的用户为其执行 opertations 的、 代表。

参数：  
* **delegatedEmail**： 委派电子邮件。


  
### <a name="getdelegatedemail-function"></a>GetDelegatedEmail 函数
获取委托的电子邮件，委派的电子邮件地址的用户为其执行 opertations、 代表。

  
**返回**:委派的电子邮件。
