---
title: 类 ProtectionHandler：：观察程序
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 protectionhandler：： observer 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 092448f4af5c27625b8a19f7cfea039e9bcd8071
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565183"
---
# <a name="class-protectionhandlerobserver"></a>类 ProtectionHandler：：观察程序 
接收 ProtectionHandler 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr\<ProtectionHandler\>& protectionHandler, const std::shared_ptr\<void\>& context)  |  在成功创建 ProtectionHandler 时调用。
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  在无法创建 ProtectionHandler 时调用。
  
## <a name="members"></a>成员
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess 函数
在成功创建 ProtectionHandler 时调用。

参数：  
* protectionHandler：新建的 ProtectionHandler


* **context**：传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure 函数
在无法创建 ProtectionHandler 时调用。

参数：  
* 错误：创建过程中发生的故障 


* **context**：传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure