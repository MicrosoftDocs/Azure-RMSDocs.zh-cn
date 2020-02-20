---
title: 类 mip::ProtectionHandler::Observer
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionhandler 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 8f661f3ebf9bc657a4dd6f6356b26cd582d4aa2e
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486811"
---
# <a name="class-mipprotectionhandlerobserver"></a>类 mip::ProtectionHandler::Observer 
接收与 ProtectionHandler 相关的通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess （const std：： shared_ptr\<ProtectionHandler\>& protectionHandler，const std：： shared_ptr\<void\>& 上下文）  |  成功创建 ProtectionHandler 时调用。
public virtual void OnCreateProtectionHandlerFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  当 ProtectionHandler 创建失败时调用。
  
## <a name="members"></a>Members
  
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