---
title: '类 mip:: Identity'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: identity 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: d2fefceb87a1bab042fc8b0aeb817421cd9025f1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885558"
---
# <a name="class-mipidentity"></a>类 mip:: Identity 
标识的抽象。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共标识 ()  |  用户电子邮件地址未知时使用的默认[标识](class_mip_identity.md)构造函数。
公共标识 (const 标识 & 其他)  |  [标识](class_mip_identity.md)复制构造函数。
公共显式标识 (const std:: string & email)  |  用户电子邮件地址已知时使用的[标识](class_mip_identity.md)构造函数。
public const std:: string & GetEmail () const  |  获取电子邮件。
  
## <a name="members"></a>成员
  
### <a name="identity-function"></a>标识函数
用户电子邮件地址未知时使用的默认[标识](class_mip_identity.md)构造函数。
  
### <a name="identity-function"></a>标识函数
[标识](class_mip_identity.md)复制构造函数。

参数：  
* **[标识](class_mip_identity.md)** : 用于创建副本。


  
### <a name="identity-function"></a>标识函数
用户电子邮件地址已知时使用的[标识](class_mip_identity.md)构造函数。

参数：  
* **电子邮件**: 用户电子邮件地址。


  
### <a name="getemail-function"></a>GetEmail 函数
获取电子邮件。

  
**返回**:电子邮件。