---
title: 类 mip：： ConsentDelegate
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： consentdelegate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: bbeca67a1ffcd5a7b159883c97a2eb3a08bfb3e2
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490313"
---
# <a name="class-mipconsentdelegate"></a>类 mip：： ConsentDelegate 
执行许可相关操作的委托。
此委托由客户端应用程序实现，以了解应何时向用户显示许可请求通知。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  在 SDK 要求用户许可连接到服务终结点时调用。
  
## <a name="members"></a>Members
  
### <a name="getuserconsent-function"></a>GetUserConsent 函数
在 SDK 要求用户许可连接到服务终结点时调用。

参数：  
* **url**：SDK 要求用户许可的 URL



  
**返回结果**：包含用户决定的许可枚举。
如果 SDK 通过这种方法请求获取用户许可，客户端应用程序应向用户显示 URL。 客户端应用程序应提供一些用于获取用户许可的方法，并返回与用户决定对应的相应许可枚举。