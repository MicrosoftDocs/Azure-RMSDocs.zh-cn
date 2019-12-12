---
title: 类 mip::ProtectionEngine::Observer
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionengine 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e5196535dc474d2649c084b55c55a80c3af349b9
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560761"
---
# <a name="class-mipprotectionengineobserver"></a>类 mip::ProtectionEngine::Observer 
接收与 ProtectionEngine 相关的通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess （const std：： shared_ptr\<std：： vector\<std：： string\>\>& templateIds，const std：： shared_ptr\<void\>& 上下文）  |  在成功检索模板时调用。
public virtual void OnGetTemplatesFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在检索模板出错时调用。
public virtual void OnGetRightsForLabelIdSuccess （const std：： shared_ptr\<std：： vector\<std：： string\>\>& 权限，const std：： shared_ptr\<void\>& 上下文）  |  在成功检索到权限时调用。
public virtual void OnGetRightsForLabelIdFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在检索用户的标签 ID 权限时调用。
  
## <a name="members"></a>成員
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 函数
在成功检索模板时调用。

参数：  
* **templateIds**：对已检索模板的列表的引用 


* **上下文**：传递到 ProtectionEngine：： GetTemplatesAsync 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： GetTemplatesAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnGetTemplatesSuccess 或 ProtectionEngine：： Observer::OnGetTemplatesFailure
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure 函数
在检索模板出错时调用。

参数：  
* **错误**：检索模板时出现错误 


* **上下文**：传递到 ProtectionEngine：： GetTemplatesAsync 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： GetTemplatesAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnGetTemplatesSuccess 或 ProtectionEngine：： Observer::OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess 函数
在成功检索到权限时调用。

参数：  
* **rights**：对检索到的权限的列表的引用 


* **上下文**：传递到 ProtectionEngine：： GetRightsForLabelIdAsync 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： GetRightsForLabelIdAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnGetRightsForLabelIdSuccess 或ProtectionEngine：： Observer：： OnGetRightsForLabelIdFailure
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure 函数
在检索用户的标签 ID 权限时调用。

参数：  
* **错误**：检索权限时发生错误 


* **上下文**：传递到 ProtectionEngine：： GetRightsForLabelIdAsync 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： GetRightsForLabelIdAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnGetRightsForLabelIdSuccess 或ProtectionEngine：： Observer：： OnGetRightsForLabelIdFailure