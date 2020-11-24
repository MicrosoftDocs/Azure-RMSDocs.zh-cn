---
title: 类 ProtectionEngine：：观察程序
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 protectionengine：： observer 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 7a576882376caa8cc5f9c5c1b3d3036ee7e57b21
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565186"
---
# <a name="class-protectionengineobserver"></a>类 ProtectionEngine：：观察程序 
接收 ProtectionEngine 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std：： vector \<std::shared_ptr\<TemplateDescriptor\> \>& templateDescriptors，const std：： shared_ptr \<void\>& 上下文)   |  在成功检索模板时调用。
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  在检索模板出错时调用。
public virtual void OnGetRightsForLabelIdSuccess (const std：： shared_ptr \<std::vector\<std::string\> \>& 权限，const std：： shared_ptr \<void\>& 上下文)   |  在成功检索到权限时调用。
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  在检索用户的标签 ID 权限时调用。
public virtual void OnLoadUserCertSuccess (const std：： shared_ptr \<void\>& 上下文)   |  成功加载用户证书时进行调用。
public virtual void OnLoadUserCertFailure (const std：： exception_ptr& 错误，const std：： shared_ptr \<void\>& 上下文)   |  当用户证书加载失败时调用。
public virtual void OnRegisterContentForTrackingAndRevocationSuccess (const std：： shared_ptr \<void\>& 上下文)   |  当注册要跟踪 & 内容时调用。
public virtual void OnRegisterContentForTrackingAndRevocationFailure (const std：： exception_ptr& 错误，const std：： shared_ptr \<void\>& 上下文)   |  当注册内容以进行跟踪 & 吊销失败时调用。
public virtual void OnRevokeContentSuccess (const std：： shared_ptr \<void\>& 上下文)   |  当的吊销成功时调用。
public virtual void OnRevokeContentFailure (const std：： exception_ptr& 错误，const std：： shared_ptr \<void\>& 上下文)   |  当内容撤消失败时调用。
  
## <a name="members"></a>成员
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 函数
在成功检索模板时调用。

参数：  
* **templateDescriptors**：对模板描述符列表的引用 


* **context**：传递到 ProtectionEngine::GetTemplatesAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::GetTemplatesAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnGetTemplatesSuccess 或 ProtectionEngine::Observer::OnGetTemplatesFailure
  
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


* **context**：传递到 ProtectionEngine::GetRightsForLabelIdAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::GetRightsForLabelIdAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess 或 ProtectionEngine::Observer::OnGetRightsForLabelIdFailure
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 函数
在检索用户的标签 ID 权限时调用。

参数：  
* **错误**：检索权限时发生错误 


* **context**：传递到 ProtectionEngine::GetRightsForLabelIdAsync 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 ProtectionEngine::GetRightsForLabelIdAsync，而此相同上下文将按原样转发给 ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess 或 ProtectionEngine::Observer::OnGetRightsForLabelIdFailure
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess 函数
成功加载用户证书时进行调用。

参数：  
* **上下文**：传递到 ProtectionEngine：： LoadUserCert 的上下文相同


应用程序可将任何类型的上下文 (例如，std：:p romise，std：： function) 到 ProtectionEngine：： LoadUserCertAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnLoadUserCertSuccess 或 ProtectionEngine：： Observer：： OnLoadUserCertFailure
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure 函数
当用户证书加载失败时调用。

参数：  
* **错误**：检索权限时发生错误 


* **上下文**：传递到 ProtectionEngine：： LoadUserCert 的上下文相同


应用程序可将任何类型的上下文 (例如，std：:p romise，std：： function) 到 ProtectionEngine：： LoadUserCertAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnLoadUserCertSuccess 或 ProtectionEngine：： Observer：： OnLoadUserCertFailure
  
### <a name="onregistercontentfortrackingandrevocationsuccess-function"></a>OnRegisterContentForTrackingAndRevocationSuccess 函数
当注册要跟踪 & 内容时调用。

参数：  
* **上下文**：传递到 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync 的上下文相同


应用程序可将任何类型的上下文 (例如，std：:p romise，std：： function) 到 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnRegisterContentForTrackingAndRevocationSuccess 或 ProtectionEngine：： Observer：： OnRegisterContentForTrackingAndRevocationFailure
  
### <a name="onregistercontentfortrackingandrevocationfailure-function"></a>OnRegisterContentForTrackingAndRevocationFailure 函数
当注册内容以进行跟踪 & 吊销失败时调用。

参数：  
* **错误**：注册内容时出现的错误 


* **上下文**：传递到 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync 的上下文相同


应用程序可将任何类型的上下文 (例如，std：:p romise，std：： function) 到 ProtectionEngine：： RegisterContentForTrackingAndRevocationAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnRegisterContentForTrackingAndRevocationSuccess 或 ProtectionEngine：： Observer：： OnRegisterContentForTrackingAndRevocationFailure
  
### <a name="onrevokecontentsuccess-function"></a>OnRevokeContentSuccess 函数
当的吊销成功时调用。

参数：  
* **上下文**：传递到 ProtectionEngine：： RevokeContentAsync 的上下文相同


应用程序可将任何类型的上下文 (例如，std：:p romise，std：： function) 到 ProtectionEngine：： RevokeContentAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnRevokeContentSuccess 或 ProtectionEngine：： Observer：： OnRevokeContentFailure
  
### <a name="onrevokecontentfailure-function"></a>OnRevokeContentFailure 函数
当内容撤消失败时调用。

参数：  
* **错误**：在吊销内容时出现的错误 


* **上下文**：传递到 ProtectionEngine：： RevokeContentAsync 的上下文相同


应用程序可将任何类型的上下文 (例如，std：:p romise，std：： function) 到 ProtectionEngine：： RevokeContentAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnRevokeContentSuccess 或 ProtectionEngine：： Observer：： OnRevokeContentFailure