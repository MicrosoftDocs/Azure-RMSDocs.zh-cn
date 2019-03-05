---
title: 类 mip::ProtectionHandler::Observer
description: 记录 mip::protectionhandler 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 00d74069374850a562547cd161ad4c5f15927b0a
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333715"
---
# <a name="class-mipprotectionhandlerobserver"></a>类 mip::ProtectionHandler::Observer 
接收 [ProtectionHandler](class_mip_protectionhandler.md) 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 void OnCreateProtectionHandlerSuccess (const std::\<ProtectionHandler\>& protectionHandler，const std:: shared_ptr\<void\>& 上下文)  |  在成功创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。
公共虚拟 void OnCreateProtectionHandlerFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在无法创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。
  
## <a name="members"></a>成員
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess 函数
在成功创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。

参数：  
* **protectionHandler**:新创建[ProtectionHandler](class_mip_protectionhandler.md)


* **上下文**:传递给同一上下文[ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)或[ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure 函数
在无法创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。

参数：  
* **错误**:在创建期间发生的故障 


* **上下文**:传递给同一上下文[ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)或[ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
