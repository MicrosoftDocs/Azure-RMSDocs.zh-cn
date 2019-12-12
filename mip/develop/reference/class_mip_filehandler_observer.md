---
title: class mip::FileHandler::Observer
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： filehandler 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d1c1a66ce3821bf3d552ee0daa0648940b645fcb
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560264"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
观察者接口，使客户端能够获取与文件处理程序相关的通知事件。
所有错误都继承自 mip：： Error。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess （const std：： shared_ptr\<FileHandler\>& fileHandler，const std：： shared_ptr\<void\>& 上下文）  |  在成功创建处理程序时调用。
public virtual void OnCreateFileHandlerFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  创建处理程序失败时调用。
public virtual void OnClassifySuccess （const std：： vector\<std：： shared_ptr\<操作\>\>& 操作，const std：： shared_ptr\<void\>& 上下文）  |  分类成功时调用。
public virtual void OnClassifyFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  分类失败时调用。
public virtual void OnGetDecryptedTemporaryFileSuccess （const std：： string & decryptedFilePath，const std：： shared_ptr\<void\>& 上下文）  |  在成功获取已解密的临时文件时调用。
public virtual void OnGetDecryptedTemporaryFileFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在获取解密的临时文件失败时调用。
public virtual void OnGetDecryptedTemporaryStreamSuccess （const std：： shared_ptr\<Stream\>& decryptedStream，const std：： shared_ptr\<void\>& 上下文）  |  在成功获取已解密的临时流时调用。
public virtual void OnGetDecryptedTemporaryStreamFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在获取解密的临时流失败时调用。
public virtual void OnCommitSuccess （已提交 bool，const std：： shared_ptr\<void\>& 上下文）  |  在将更改成功提交至文件时调用。
public virtual void OnCommitFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  在将更改提交至文件失败时调用。
public virtual void OnInspectSuccess （const std：： shared_ptr\<FileInspector\>& fileInspector，const std：： shared_ptr\<void\>& 上下文）  |  检查成功时调用。
public virtual void OnInspectFailure （const std：： exception_ptr & 错误，const std：： shared_ptr\<void\>& 上下文）  |  当检查失败时调用。
  
## <a name="members"></a>成員
  
### <a name="oncreatefilehandlersuccess-function"></a>OnCreateFileHandlerSuccess 函数
在成功创建处理程序时调用。
  
### <a name="oncreatefilehandlerfailure-function"></a>OnCreateFileHandlerFailure 函数
创建处理程序失败时调用。
  
### <a name="onclassifysuccess-function"></a>OnClassifySuccess 函数
分类成功时调用。
  
### <a name="onclassifyfailure-function"></a>OnClassifyFailure 函数
分类失败时调用。
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess 函数
在成功获取已解密的临时文件时调用。
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure 函数
在获取解密的临时文件失败时调用。
  
### <a name="ongetdecryptedtemporarystreamsuccess-function"></a>OnGetDecryptedTemporaryStreamSuccess 函数
在成功获取已解密的临时流时调用。
  
### <a name="ongetdecryptedtemporarystreamfailure-function"></a>OnGetDecryptedTemporaryStreamFailure 函数
在获取解密的临时流失败时调用。
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess 函数
在将更改成功提交至文件时调用。
  
### <a name="oncommitfailure-function"></a>OnCommitFailure 函数
在将更改提交至文件失败时调用。
  
### <a name="oninspectsuccess-function"></a>OnInspectSuccess 函数
检查成功时调用。
  
### <a name="oninspectfailure-function"></a>OnInspectFailure 函数
当检查失败时调用。