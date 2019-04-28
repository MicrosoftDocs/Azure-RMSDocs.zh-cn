---
title: 类 mip::FileExecutionState
description: 记录 mip::fileexecutionstate 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bdf0814e56d64bd16918a6f4d269a057620f92f5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184665"
---
# <a name="class-mipfileexecutionstate"></a>类 mip::FileExecutionState 
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 DataState GetDataState() 常量  |  获取应用程序与之交互时内容的状态。
public virtual std::shared_ptr\<ClassificationResults\> GetClassificationResults(const std::shared_ptr\<FileHandler\> &, const std::vector\<std::shared_ptr\<ClassificationRequest\>\> &) const  |  返回分类结果的映射。
公共虚拟 std:: vector\<uint8_t\> GetSerializedProtectionInfo() 常量  |  返回具有序列化计的缓冲区
公共虚拟 std:: map\<std:: string、 std:: string\> GetAuditMetadata() 常量  |  返回应用程序特定审核键-值对的映射。
  
## <a name="members"></a>成員
  
### <a name="getdatastate-function"></a>GetDataState 函数
获取应用程序与之交互时内容的状态。

  
**返回**:内容数据的状态
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **fileHandler**:-使用的文件的文件处理程序 


* **classificationIds**： 分类 Id 的列表。 



  
**返回**:分类结果的列表。
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
返回具有序列化计的缓冲区

  
**返回**:具有序列化计的缓冲区
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 函数
返回应用程序特定审核键-值对的映射。

  
**返回**:应用程序特定的审核元数据注册 Key: Value 对发件人的列表：发件人的收件人的电子邮件 Id:表示 LastModifiedBy 一封电子邮件的收件人的 JSON 数组：上次修改内容 LastModifiedDate 的用户的电子邮件 Id:内容的上次修改日期