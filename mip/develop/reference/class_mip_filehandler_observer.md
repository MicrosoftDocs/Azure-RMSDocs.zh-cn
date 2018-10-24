---
title: 类 mip FileHandler Observer
description: 类 mip FileHandler Observer 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a587107afc2b8963d64c31ad47af81761bf2b9f8
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446154"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
[Observer](class_mip_filehandler_observer.md) 接口，供客户端获取文件处理程序相关事件的通知。
所有错误都继承自 [mip::Error](class_mip_error.md)。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  在成功创建处理程序时调用。
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  创建处理程序失败时调用。
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  在成功检索到标签时调用。
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  检索标签失败时调用。
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  在成功检索到保护策略时调用。
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  检索保护策略失败时调用。
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  在将更改成功提交至文件时调用。
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  在将更改提交至文件失败时调用。
  
## <a name="members"></a>成員
  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
在成功创建处理程序时调用。
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
创建处理程序失败时调用。
  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
在成功检索到标签时调用。
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
检索标签失败时调用。
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
在成功检索到保护策略时调用。
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
检索保护策略失败时调用。
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
在将更改成功提交至文件时调用。
  
### <a name="oncommitfailure"></a>OnCommitFailure
在将更改提交至文件失败时调用。