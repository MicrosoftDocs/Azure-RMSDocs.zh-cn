---
title: 类 mip::ConsentDelegate
description: 记录 mip::consentdelegate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 69ffbe72ac9d8241115fecd5bbae28052fb93e33
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333222"
---
# <a name="class-mipconsentdelegate"></a>类 mip::ConsentDelegate 
执行许可相关操作的委托。
此委托由客户端应用程序实现，以了解应何时向用户显示许可请求通知。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  在 SDK 要求用户许可连接到服务终结点时调用。
  
## <a name="members"></a>成員
  
### <a name="getuserconsent-function"></a>GetUserConsent 函数
在 SDK 要求用户许可连接到服务终结点时调用。

参数：  
* **url**:为其 SDK 需要用户同意 URL



  
**返回**:与用户的决定是同意的情况下枚举。
如果 SDK 通过这种方法请求获取用户许可，客户端应用程序应向用户显示 URL。 客户端应用程序应提供一些用于获取用户许可的方法，并返回与用户决定对应的相应许可枚举。
