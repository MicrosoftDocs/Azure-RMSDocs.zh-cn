---
title: 类 mip::ProtectionEngine::Observer
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionengine 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 688bc59b992e885b2b9724111c19f69f860badd9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489667"
---
# <a name="class-mipprotectionengineobserver"></a>类 mip::ProtectionEngine::Observer 
接收与 ProtectionEngine 相关的通知的接口。
此接口必须通过应用程序使用保护 SDK 来实现
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess （const std：： vector\<std：： shared_ptr\<TemplateDescriptor\>\>& templateDescriptors，const std：： shared_ptr\<void\>& 上下文）  |  在成功检索模板时调用。
public virtual void OnGetTemplatesFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在检索模板出错时调用。
public virtual void OnGetRightsForLabelIdSuccess （const std：： shared_ptr\<std：： vector\<std：： string\>\>& 权限，const std：： shared_ptr\<void\>& 上下文）  |  在成功检索到权限时调用。
public virtual void OnGetRightsForLabelIdFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在检索用户的标签 ID 权限时调用。
public virtual void OnLoadUserCertSuccess （const std：： shared_ptr\<void\>& 上下文）  |  成功加载用户证书时进行调用。
public virtual void OnLoadUserCertFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  当用户证书加载失败时调用。
  
## <a name="members"></a>Members
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess 函数
在成功检索模板时调用。

参数：  
* **templateDescriptors**：对模板描述符列表的引用 


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
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess 函数
成功加载用户证书时进行调用。

参数：  
* **上下文**：传递到 ProtectionEngine：： LoadUserCert 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： LoadUserCertAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnLoadUserCertSuccess 或 ProtectionEngine：： Observer::OnLoadUserCertFailure
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure 函数
当用户证书加载失败时调用。

参数：  
* **错误**：检索权限时发生错误 


* **上下文**：传递到 ProtectionEngine：： LoadUserCert 的上下文相同


应用程序可将任何类型的上下文（例如 std：:p romise，std：： function）传递给 ProtectionEngine：： LoadUserCertAsync，并且同一上下文将按原样转发到 ProtectionEngine：： Observer：： OnLoadUserCertSuccess 或 ProtectionEngine：： Observer::OnLoadUserCertFailure