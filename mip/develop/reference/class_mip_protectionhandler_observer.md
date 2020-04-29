---
title: 类 ProtectionHandler：：观察程序
description: 记录 Microsoft 信息保护（MIP） SDK 的 protectionhandler：：观察者类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 66453d343505cc57427e177eac258b83a2663eb0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764436"
---
# <a name="class-protectionhandlerobserver"></a>类 ProtectionHandler：：观察程序 
接收 ProtectionHandler 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess （const std：： shared_ptr\<protectionHandler\>& ProtectionHandler，const std：： shared_ptr\<void\>& 上下文）  |  在成功创建 ProtectionHandler 时调用。
public virtual void OnCreateProtectionHandlerFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在无法创建 ProtectionHandler 时调用。
  
## <a name="members"></a>成员
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess 函数
在成功创建 ProtectionHandler 时调用。

参数：  
* protectionHandler****：新建的 ProtectionHandler


* **context**：传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure 函数
在无法创建 ProtectionHandler 时调用。

参数：  
* 错误****：创建过程中发生的故障 


* **context**：传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure