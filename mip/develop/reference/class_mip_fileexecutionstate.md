---
title: 类 mip::FileExecutionState
description: 记录 mip::fileexecutionstate 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 08a9064645f0ffb3ffbaa72f00db26c5b29d3643
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652330"
---
# <a name="class-mipfileexecutionstate"></a>类 mip::FileExecutionState 
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
公共虚拟 std:: map\<std:: string、 std:: shared_ptr\<ClassificationResult\> \> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &、 const std:: vector\<std:: shared_ptr\<ClassificationRequest\> \> &) 常量  |  返回分类结果的映射。
公共虚拟 std:: vector\<uint8_t\> GetSerializedProtectionInfo() 常量  |  返回具有序列化计的缓冲区
  
## <a name="members"></a>成員
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **fileHandler**:-使用的文件的文件处理程序 


* **classificationIds**： 分类 Id 的列表。 



  
**返回**:分类结果的列表。
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
返回具有序列化计的缓冲区

  
**返回**:具有序列化计的缓冲区