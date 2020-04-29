---
title: 类 ProtectionEngine：：观察程序
description: 记录 Microsoft 信息保护（MIP） SDK 的 protectionengine：：观察者类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: ca1f9c3251df30166b123ae31c8e3c5fceef67fc
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764602"
---
# <a name="class-protectionengineobserver"></a>类 ProtectionEngine：：观察程序 
接收 ProtectionEngine 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess （const std：： vector\<std：： shared_ptr\<TemplateDescriptor\> \>& templateDescriptors，const std：： shared_ptr\<void\>& 上下文）  |  在成功检索模板时调用。
public virtual void OnGetTemplatesFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在检索模板出错时调用。
public virtual void OnGetRightsForLabelIdSuccess （const std：： shared_ptr\<std：： vector\<std：： string\> \>& 权限，const std：： shared_ptr\<void\>& 上下文）  |  在成功检索到权限时调用。
public virtual void OnGetRightsForLabelIdFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  在检索用户的标签 ID 权限时调用。
public virtual void OnLoadUserCertSuccess （const std：： shared_ptr\<void\>& context）  |  成功加载用户证书时进行调用。
public virtual void OnLoadUserCertFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  当用户证书加载失败时调用。
public virtual void OnRegisterContentForTrackingAndRevocationSuccess （const std：： shared_ptr\<void\>& context）  |  当注册要跟踪 & 内容时调用。
public virtual void OnRegisterContentForTrackingAndRevocationFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  当注册内容以进行跟踪 & 吊销失败时调用。
public virtual void OnRevokeContentSuccess （const std：： shared_ptr\<void\>& context）  |  当的吊销成功时调用。
public virtual void OnRevokeContentFailure （const std：： exception_ptr& 错误，const std：： shared_ptr\<void\>& 上下文）  |  当内容撤消失败时调用。
  
## <a name="members"></a>成员
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 函数
在成功检索模板时调用。

参数：  
* **templateDescriptors**：对模板描述符列表的引用 


* **context**：传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md) 的相同上下文


应用程序可将任何类型的上下文（例如，std：:p romise，std：： function）传递给 ProtectionEngine：： GetTemplatesAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnGetTemplatesSuccess 或 ProtectionEngine：： Observer：： OnGetTemplatesFailure。
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 函数
在检索模板出错时调用。

参数：  
* **错误**：检索模板时出现错误 


* **context**：传递到 ProtectionEngine::GetTemplatesAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::GetTemplatesAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnGetTemplatesSuccess 或 ProtectionEngine::Observer::OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 函数
在成功检索到权限时调用。

参数：  
* **rights**：对检索到的权限的列表的引用 


* **上下文**：传递到[ProtectionEngine：： GetRightsForLabelIdAsync](class_mip_protectionengine.md)的上下文相同。


应用程序可将任何类型的上下文（例如，std：:p romise，std：： function）传递给 ProtectionEngine：： GetRightsForLabelIdAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnGetRightsForLabelIdSuccess 或 ProtectionEngine：： Observer：： OnGetRightsForLabelIdFailure。
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 函数
在检索用户的标签 ID 权限时调用。

参数：  
* **错误**：检索权限时发生错误 


* **context**：传递到 ProtectionEngine::GetRightsForLabelIdAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::GetRightsForLabelIdAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess 或 ProtectionEngine::Observer::OnGetRightsForLabelIdFailure
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess 函数
成功加载用户证书时进行调用。

参数：  
* **上下文**：传递到 ProtectionEngine：： LoadUserCert 的上下文相同。


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递到 [ProtectionEngine：： LoadUserCertAsync，同一上下文将按原样转发到[ProtectionEngine：： observer：： OnLoadUserCertSuccess](class_mip_protectionengine_observer.md)或[ProtectionEngine：： Observer：： OnLoadUserCertFailure](class_mip_protectionengine_observer.md)
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure 函数
当用户证书加载失败时调用。

参数：  
* **错误**：检索权限时发生错误 


* **上下文**：传递到 ProtectionEngine：： LoadUserCert 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： LoadUserCertAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnLoadUserCertSuccess 或 ProtectionEngine：： Observer：： OnLoadUserCertFailure
  
### <a name="onregistercontentfortrackingandrevocationsuccess-function"></a>OnRegisterContentForTrackingAndRevocationSuccess 函数
当注册要跟踪 & 内容时调用。

参数：  
* **上下文**：传递到 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync 的上下文相同。


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync，并且同一上下文将按原样转发到[ProtectionEngine：： observer：： OnRegisterContentForTrackingAndRevocationSuccess](class_mip_protectionengine_observer.md)或[ProtectionEngine：： Observer：： OnRegisterContentForTrackingAndRevocationFailure](class_mip_protectionengine_observer.md)
  
### <a name="onregistercontentfortrackingandrevocationfailure-function"></a>OnRegisterContentForTrackingAndRevocationFailure 函数
当注册内容以进行跟踪 & 吊销失败时调用。

参数：  
* **错误**：注册内容时出现的错误 


* **上下文**：传递到 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnRegisterContentForTrackingAndRevocationSuccess 或 ProtectionEngine：： Observer：： OnRegisterContentForTrackingAndRevocationFailure
  
### <a name="onrevokecontentsuccess-function"></a>OnRevokeContentSuccess 函数
当的吊销成功时调用。

参数：  
* **上下文**：传递到 ProtectionEngine：： RevokeContentAsync 的上下文相同。


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： RevokeContentAsync，并且同一上下文将按原样转发到[ProtectionEngine：： observer：： OnRevokeContentSuccess](class_mip_protectionengine_observer.md)或[ProtectionEngine：： Observer：： OnRevokeContentFailure](class_mip_protectionengine_observer.md)
  
### <a name="onrevokecontentfailure-function"></a>OnRevokeContentFailure 函数
当内容撤消失败时调用。

参数：  
* **错误**：在吊销内容时出现的错误 


* **上下文**：传递到 ProtectionEngine：： RevokeContentAsync 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： RevokeContentAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnRevokeContentSuccess 或 ProtectionEngine：： Observer：： OnRevokeContentFailure