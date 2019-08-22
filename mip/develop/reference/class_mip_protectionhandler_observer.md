---
title: 类 mip::ProtectionHandler::Observer
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionhandler 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 0e1a1d039928e1244d6c279fe055330eac7f9577
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883399"
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