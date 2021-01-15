---
title: 类 DocumentState
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 documentstate：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 1d584ba1f0c66c51646b6fe6fc4dd4fa9a6ccf0d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215470"
---
# <a name="class-documentstate"></a>类 DocumentState 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  获取描述文档的内容说明。 文件示例： [path\filename] 电子邮件示例： [Subject： Sender]。
public virtual DataState GetDataState ( # A1 const  |  获取应用程序与之交互时内容的状态。
public std：： vector \<MetadataEntry\> GetContentMetadata (const std：： vector \<std::string\>& 名称，const std：： Vector \<std::string\>& namePrefixes) const  |  从内容中获取元数据项。
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  获取保护描述符。
public std：： string GetContentFormat ( # A1 const  |  获取内容格式。
public virtual MetadataVersion GetContentMetadataVersion ( # A1 const  |  获取租户的应用程序支持的最高元数据版本。
公共虚拟 std：： shared_ptr \<ClassificationResults\> GetClassificationResults (const std：： vector \<std::shared_ptr\<ClassificationRequest\> \> &) 常量  |  返回分类结果的映射。
public virtual std：： map \<std::string, std::string\> GetAuditMetadata ( # A1 const  |  返回应用程序特定的审核键值对的映射。
public virtual std：： chrono：： time_point \<std::chrono::system_clock\> GetLastModifiedTime ( # A1 const  |  返回上次修改文档的时间点。
  
## <a name="members"></a>成员
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 函数
获取描述文档的内容说明。 文件示例： [path\filename] 电子邮件示例： [Subject： Sender]。

  
**返回**：要应用于内容的内容说明。
审核功能将此值用作内容的用户可读说明
  
### <a name="getdatastate-function"></a>GetDataState 函数
获取应用程序与之交互时内容的状态。

  
**返回结果**：内容数据的状态
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata 函数
从内容中获取元数据项。

  
**返回结果**：应用于内容的元数据。 
  
**另请参阅**： mip：： MetadataEntry。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
获取保护描述符。

  
**返回结果**：保护描述符
  
### <a name="getcontentformat-function"></a>GetContentFormat 函数
获取内容格式。

  
**返回**：内容格式
  
### <a name="getcontentmetadataversion-function"></a>GetContentMetadataVersion 函数
获取租户的应用程序支持的最高元数据版本。

  
**返回**：内容元数据版本。 如果为0，则不对元数据进行版本控制。 如果文件格式支持多个版本的元数据，则可以使用 MIP 来理解所有元数据，并根据每个版本来报告精细的元数据更改。
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **classificationIds**：分类 id 列表。 



  
**返回**：分类结果的列表。 如果未执行分类循环，则返回 nullptr。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 函数
返回应用程序特定的审核键值对的映射。

  
**返回**：特定于应用程序的审核元数据注册密钥：值对发送方：发件人接收方的电子邮件 id 的列表：表示电子邮件的 LASTMODIFIEDBY 的 JSON 数组：上次修改内容的用户的电子邮件 id LastModifiedDate：上次修改内容的日期
  
### <a name="getlastmodifiedtime-function"></a>GetLastModifiedTime 函数
返回上次修改文档的时间点。

  
**返回**：文档时间点的上次修改时间。