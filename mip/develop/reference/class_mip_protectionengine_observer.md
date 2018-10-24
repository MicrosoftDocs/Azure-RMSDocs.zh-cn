---
title: 类 mip ProtectionEngine Observer
description: 类 mip ProtectionEngine Observer 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5c5b5e807a80c8db3cbdb69ea5d09da1e79aec6e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446577"
---
# <a name="class-mipprotectionengineobserver"></a>类 mip::ProtectionEngine::Observer 
接收 [ProtectionEngine](class_mip_protectionengine.md) 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  在成功检索模板时调用。
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在检索模板出错时调用。
public virtual void OnGetRightsForLabelIdSuccess(const std::shared_ptr<std::vector<std::string>>& rights, const std::shared_ptr<void>& context)  |  在成功检索到权限时调用。
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在检索用户的标签 ID 权限时调用。
public virtual void OnGetGrantingLabelIdsSuccess(const std::shared_ptr<std::vector<std::string>>& lableIds, const std::shared_ptr<void>& context)  |  在成功检索到标签 ID 时调用。
public virtual void OnGetGrantingLabelIdsFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在检索用户的标签 ID 时调用。
  
## <a name="members"></a>成員
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
在成功检索模板时调用。

参数：  
* **templateIds**：对已检索模板的列表的引用 


* **context**：传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) 或 [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
在检索模板出错时调用。

参数：  
* **error**：检索模板时发生的[错误](class_mip_error.md) 


* **context**：传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) 或 [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongetrightsforlabelidsuccess"></a>OnGetRightsForLabelIdSuccess
在成功检索到权限时调用。

参数：  
* **rights**：对检索到的权限的列表的引用 


* **context**：传递到 [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) 或 [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetrightsforlabelidfailure"></a>OnGetRightsForLabelIdFailure
在检索用户的标签 ID 权限时调用。

参数：  
* **error**：检索权限时发生的[错误](class_mip_error.md) 


* **context**：传递到 [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) 或 [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetgrantinglabelidssuccess"></a>OnGetGrantingLabelIdsSuccess
在成功检索到标签 ID 时调用。

参数：  
* **lableIds**：对检索到的标签 ID 的列表的引用 


* **context**：传递到 [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function 等）传递到 [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) 或 [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)
  
### <a name="ongetgrantinglabelidsfailure"></a>OnGetGrantingLabelIdsFailure
在检索用户的标签 ID 时调用。

参数：  
* **error**：检索标签 ID 时发生的[错误](class_mip_error.md) 


* **context**：传递到 [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync) 的相同上下文


应用程序可以将任何类型的上下文（例如，std::promise、std::function 等）传递到 [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) 或 [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)