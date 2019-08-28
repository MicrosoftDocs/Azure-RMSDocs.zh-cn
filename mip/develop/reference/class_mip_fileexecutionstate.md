---
title: '类 mip:: FileExecutionState'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: fileexecutionstate 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d6159bf22bf1c887ed74232472163f74440c2051
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056047"
---
# <a name="class-mipfileexecutionstate"></a>类 mip:: FileExecutionState 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState () const  |  获取应用程序与之交互时内容的状态。
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &, const std:: vector\<std:: shared_ptr\<ClassificationRequest\> &)\> const  |  返回分类结果的映射。
public virtual std:: map\<std:: string, std:: string\> GetAuditMetadata () const  |  返回应用程序特定的审核键值对的映射。
  
## <a name="members"></a>成员
  
### <a name="getdatastate-function"></a>GetDataState 函数
获取应用程序与之交互时内容的状态。

  
**返回**:内容数据的状态
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **fileHandler**:-所用文件的文件处理程序 


* **classificationIds**: 分类 id 列表。 



  
**返回**:分类结果的列表。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 函数
返回应用程序特定的审核键值对的映射。

  
**返回**:特定于应用程序的审核元数据注册密钥: 值对发送程序的列表:发件人收件人的电子邮件 Id:表示电子邮件 LastModifiedBy 的收件人的 JSON 数组:上次修改内容 LastModifiedDate 的用户的电子邮件 Id:上次修改内容的日期