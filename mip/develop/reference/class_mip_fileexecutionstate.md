---
title: 类 FileExecutionState
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 fileexecutionstate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 991daab4e2b0d72a747f747dabd5860373fabfc1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215300"
---
# <a name="class-fileexecutionstate"></a>类 FileExecutionState 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState ( # A1 const  |  获取应用程序与之交互时内容的状态。
公共虚拟 std：： shared_ptr \<ClassificationResults\> GetClassificationResults (const std：： shared_ptr \<FileHandler\> &，const std：： vector \<std::shared_ptr\<ClassificationRequest\> \> &) const  |  返回分类结果的映射。
public virtual std：： map \<std::string, std::string\> GetAuditMetadata ( # A1 const  |  返回应用程序特定的审核键值对的映射。
  
## <a name="members"></a>成员
  
### <a name="getdatastate-function"></a>GetDataState 函数
获取应用程序与之交互时内容的状态。

  
**返回结果**：内容数据的状态
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **fileHandler**：-所用文件的文件处理程序 


* **classificationIds**：分类 id 列表。 



  
**返回**：分类结果的列表。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 函数
返回应用程序特定的审核键值对的映射。

  
**返回**：特定于应用程序的审核元数据注册密钥：值对发送方：发件人接收方的电子邮件 id 的列表：表示电子邮件的 LASTMODIFIEDBY 的 JSON 数组：上次修改内容的用户的电子邮件 id LastModifiedDate：上次修改内容的日期