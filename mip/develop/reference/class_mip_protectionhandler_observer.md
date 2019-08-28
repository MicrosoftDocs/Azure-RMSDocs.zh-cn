---
title: 类 mip::ProtectionHandler::Observer
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionhandler 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a02e84a7be2071340a0ffef6310788823b768de3
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057547"
---
# <a name="class-mipprotectionhandlerobserver"></a>类 mip::ProtectionHandler::Observer 
接收 [ProtectionHandler](class_mip_protectionhandler.md) 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess (const std:: shared_ptr\<ProtectionHandler\>& ProtectionHandler, const std:: shared_ptr\<void\>& context)  |  在成功创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。
public virtual void OnCreateProtectionHandlerFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在无法创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。
  
## <a name="members"></a>成员
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess 函数
在成功创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。

参数：  
* **protectionHandler**:新创建的[ProtectionHandler](class_mip_protectionhandler.md)


* **上下文**:传递给[ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)或[ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)的上下文相同


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure 函数
在无法创建 [ProtectionHandler](class_mip_protectionhandler.md) 时调用。

参数：  
* **错误**:创建过程中出现的故障 


* **上下文**:传递给[ProtectionEngine:: CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function)或[ProtectionEngine:: CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)的上下文相同


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) 或 [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess 或 ProtectionEngine::Observer::OnCreateProtectionHandlerFailure