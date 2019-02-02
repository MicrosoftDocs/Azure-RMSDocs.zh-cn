---
title: class mip::FileHandler::Observer
description: 记录 mip::filehandler 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 33f8a9c0d90d7f64295d469004c36a4c4cc80338
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650623"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
[Observer](class_mip_filehandler_observer.md) 接口，供客户端获取文件处理程序相关事件的通知。
所有错误都继承自 [mip::Error](class_mip_error.md)。 客户端不应在调用观察程序的线程上调用回引擎。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr\<FileHandler\>& fileHandler, const std::shared_ptr\<void\>& context)  |  在成功创建处理程序时调用。
公共虚拟 void OnCreateFileHandlerFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  创建处理程序失败时调用。
public virtual void OnClassifySuccess(const std::vector\<std::shared_ptr\<Action\>\>& actions, const std::shared_ptr\<void\>& context)  |  调用时对成功进行分类。
公共虚拟 void OnClassifyFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  时调用分类失败。
public virtual void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr\<void\>& context)  |  获取已解密的临时文件成功时调用。
public virtual void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  获取已解密的临时文件失败时调用。
公共虚拟 void OnCommitSuccess (bool 提交，const std::\<void\>& 上下文)  |  在将更改成功提交至文件时调用。
公共虚拟 void OnCommitFailure (const std::exception_ptr 和错误、 const std::\<void\>& 上下文)  |  在将更改提交至文件失败时调用。
  
## <a name="members"></a>成員
  
### <a name="oncreatefilehandlersuccess-function"></a>OnCreateFileHandlerSuccess 函数
在成功创建处理程序时调用。
  
### <a name="oncreatefilehandlerfailure-function"></a>OnCreateFileHandlerFailure 函数
创建处理程序失败时调用。
  
### <a name="onclassifysuccess-function"></a>OnClassifySuccess 函数
调用时对成功进行分类。
  
### <a name="onclassifyfailure-function"></a>OnClassifyFailure 函数
时调用分类失败。
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess 函数
获取已解密的临时文件成功时调用。
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure function
获取已解密的临时文件失败时调用。
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess 函数
在将更改成功提交至文件时调用。
  
### <a name="oncommitfailure-function"></a>OnCommitFailure 函数
在将更改提交至文件失败时调用。