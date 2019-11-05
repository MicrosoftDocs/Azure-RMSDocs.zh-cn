---
title: 类 mip::ProtectionHandler::Observer
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionhandler 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8b48d6e5aacacb6f678fc7d5aea2aee531da88fa
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560084"
---
# <a name="class-mipprotectionhandlerobserver"></a>类 mip::ProtectionHandler::Observer 
接收与 ProtectionHandler 相关的通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess （const std：： shared_ptr\<ProtectionHandler\>& protectionHandler，const std：： shared_ptr\<void\>& 上下文）  |  成功创建 ProtectionHandler 时调用。
public virtual void OnCreateProtectionHandlerFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  当 ProtectionHandler 创建失败时调用。
  
## <a name="members"></a>成員
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess 函数
成功创建 ProtectionHandler 时调用。

参数：  
* **protectionHandler**：新创建的 protectionHandler


* **上下文**：传递到 ProtectionEngine：： CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine：： CreateProtectionHandlerFromPublishingLicenseAsync 的上下文相同


应用程序可将任何类型的上下文（例如，std：:p romise，std：： function）传递给 ProtectionEngine：： CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine：： CreateProtectionHandlerFromPublishingLicenseAsync，并将该上下文传递给同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnCreateProtectionHandlerSuccess 或 ProtectionEngine：： Observer：： OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure 函数
当 ProtectionHandler 创建失败时调用。

参数：  
* 错误：创建过程中发生的故障 


* **上下文**：传递到 ProtectionEngine：： CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine：： CreateProtectionHandlerFromPublishingLicenseAsync 的上下文相同


应用程序可将任何类型的上下文（例如，std：:p romise，std：： function）传递给 ProtectionEngine：： CreateProtectionHandlerFromDescriptorAsync 或 ProtectionEngine：： CreateProtectionHandlerFromPublishingLicenseAsync，并将该上下文传递给同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnCreateProtectionHandlerSuccess 或 ProtectionEngine：： Observer：： OnCreateProtectionHandlerFailure