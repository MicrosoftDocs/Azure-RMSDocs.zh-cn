---
title: 类 mip::ProtectionEngine::Observer
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionengine 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 8985b5646849338213855017da042538a27c935b
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057632"
---
# <a name="class-mipprotectionengineobserver"></a>类 mip::ProtectionEngine::Observer 
接收 [ProtectionEngine](class_mip_protectionengine.md) 相关通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: shared_ptr\<std:: vector\<std:: string\>\>& templateIds, const std:: shared_ptr\<void\>& context)  |  在成功检索模板时调用。
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在检索模板出错时调用。
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr\<std:: vector\<std:: string\>\>& 权限, const std:: shared_ptr\<void\>& context)  |  在成功检索到权限时调用。
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在检索用户的标签 ID 权限时调用。
  
## <a name="members"></a>成员
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 函数
在成功检索模板时调用。

参数：  
* **templateIds**:对检索到的模板列表的引用 


* **上下文**:传递给[ProtectionEngine:: GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)的上下文相同


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) 或 [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 函数
在检索模板出错时调用。

参数：  
* **错误**:检索模板时出现的[错误](class_mip_error.md) 


* **上下文**:传递给[ProtectionEngine:: GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)的上下文相同


应用程序可以将任何类型的上下文（例如，std::promise、std::function）传递到 [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)，而此相同上下文将按原样转发给 [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) 或 [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 函数
在成功检索到权限时调用。

参数：  
* **权限**:对检索到的权限列表的引用 


* **上下文**:传递给 ProtectionEngine:: GetRightsForLabelIdAsync 的上下文相同。


应用程序可将任何类型的上下文 (例如, std::p romise, std:: function) 传递给 ProtectionEngine:: GetRightsForLabelIdAsync。 同一上下文将按原样转发到[ProtectionEngine:: observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)或[ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 函数
在检索用户的标签 ID 权限时调用。

参数：  
* **错误**:检索权限时发生的[错误](class_mip_error.md) 


* **上下文**:传递给 ProtectionEngine:: GetRightsForLabelIdAsync 的上下文相同。


应用程序可将任何类型的上下文 (例如, std::p romise, std:: function) 传递给 ProtectionEngine:: GetRightsForLabelIdAsync, 同一上下文将按原样转发到[ProtectionEngine:: Observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)或[ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)