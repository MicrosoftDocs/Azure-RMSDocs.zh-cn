---
title: 类 DelegationLicenseSettings
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 delegationlicensesettings：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 947accd8104f8eda9f7b7320a1fbdb956810f34d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224875"
---
# <a name="class-delegationlicensesettings"></a>类 DelegationLicenseSettings 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： shared_ptr \<const PublishingLicenseInfo\> GetLicenseInfo ( # A1 const  |  获取 PublishingLicenseInfo，发布许可证。
public const std：： vector \<std::string\>& GetUsers ( # A2 const  |  获取请求的用户列表。
public bool GetAquireEndUserLicenses ( # A1 const  |  获取一个布尔值，该值指示除了获取委托许可证以外，是否还获取最终用户许可证。
  
## <a name="members"></a>成员
  
### <a name="getlicenseinfo-function"></a>GetLicenseInfo 函数
获取 PublishingLicenseInfo，发布许可证。

  
**返回**： PublishingLicenseInfo
  
### <a name="getusers-function"></a>GetUsers 函数
获取请求的用户列表。

  
**返回**：用户
  
### <a name="getaquireenduserlicenses-function"></a>GetAquireEndUserLicenses 函数
获取一个布尔值，该值指示除了获取委托许可证以外，是否还获取最终用户许可证。

  
**返回**：是否获取最终用户许可证