---
title: 类 mip：： FileExecutionState
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： fileexecutionstate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a55ad7b5d28a3115ea4f17f36a846011e82d7827
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490041"
---
# <a name="class-mipfileexecutionstate"></a>类 mip：： FileExecutionState 
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState （） const  |  获取应用程序与之交互时内容的状态。
public virtual std：： shared_ptr\<ClassificationResults\> GetClassificationResults （const std：： shared_ptr\<FileHandler\> &，const std：： vector\<std：： shared_ptr\<ClassificationRequest\>\> &） const  |  返回分类结果的映射。
公共虚拟 std：： map\<std：： string，std：： string\> GetAuditMetadata （） const  |  返回应用程序特定的审核键值对的映射。
  
## <a name="members"></a>Members
  
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