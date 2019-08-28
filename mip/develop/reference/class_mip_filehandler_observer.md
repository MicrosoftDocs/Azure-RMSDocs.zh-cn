---
title: class mip::FileHandler::Observer
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: filehandler 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: bcaf01e24ed01819e973576a70258e00e900ad28
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054980"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
[Observer](class_mip_filehandler_observer.md) 接口，供客户端获取文件处理程序相关事件的通知。
所有错误都继承自 [mip::Error](class_mip_error.md)。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess (const std:: shared_ptr\<FileHandler\>& FileHandler, const std:: shared_ptr\<void\>& context)  |  在成功创建处理程序时调用。
public virtual void OnCreateFileHandlerFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  创建处理程序失败时调用。
public virtual void OnClassifySuccess (const std:: vector\<std:: shared_ptr\<Action\>\>& 操作, const std:: shared_ptr\<void\>& context)  |  分类成功时调用。
public virtual void OnClassifyFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  分类失败时调用。
public virtual void OnGetDecryptedTemporaryFileSuccess (const std:: string & decryptedFilePath, const std:: shared_ptr\<void\>& context)  |  在成功获取已解密的临时文件时调用。
public virtual void OnGetDecryptedTemporaryFileFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在获取解密的临时文件失败时调用。
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std:: shared_ptr\<Stream\>& decryptedStream, const std:: shared_ptr\<void\>& context)  |  在成功获取已解密的临时流时调用。
public virtual void OnGetDecryptedTemporaryStreamFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在获取解密的临时流失败时调用。
public virtual void OnCommitSuccess (已提交 bool, const std::\<shared_ptr\>void & 上下文)  |  在将更改成功提交至文件时调用。
public virtual void OnCommitFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  在将更改提交至文件失败时调用。
public virtual void OnInspectSuccess (const std:: shared_ptr\<FileInspector\>& FileInspector, const std:: shared_ptr\<void\>& context)  |  检查成功时调用。
public virtual void OnInspectFailure (const std:: exception_ptr & 错误, const std:: shared_ptr\<void\>& context)  |  当检查失败时调用。
  
## <a name="members"></a>成员
  
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