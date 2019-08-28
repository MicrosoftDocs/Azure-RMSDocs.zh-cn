---
title: '类 mip:: Identity'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: identity 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 8bb4e30398e6f12214605df6f5ad194334d3eeff
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054772"
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