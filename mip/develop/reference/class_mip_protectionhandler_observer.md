---
title: 类 ProtectionHandler：：观察程序
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 protectionhandler：： observer 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: bd7a2b24b5eb80b3b17c025c43b0e0b31589a00a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214535"
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