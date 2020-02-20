---
title: class mip::ExecutionState
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： executionstate& 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e0bf26124a7181dd8e6477a303868b51d6275c6e
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490075"
---
# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
执行引擎所需的所有状态的接口。
客户端应只调用方法来获取所需的状态。 因此，为了提高效率，客户端可能想要实现该接口，以此动态计算相应的状态而不是提前计算。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public std：： shared_ptr\<Label\> GetNewLabel （） const  |  获取应在文档上应用的敏感度标签 ID。
public std::string GetContentIdentifier() const  |  获取描述文档的内容说明。 文件示例： [path\filename] 电子邮件示例： [Subject： Sender]。
public virtual DataState GetDataState （） const  |  获取应用程序与之交互时内容的状态。
公共 std：:p 空中\<bool，std：： string\> IsDowngradeJustified （） const  |  实现应传递是否提供了降级现有标签的合理理由。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  获取新标签的分配方法。
公共虚拟 std：： vector\<std：:p air\<std：： string，std：： string\>\> GetNewLabelExtendedProperties （） const  |  返回新标签的扩展属性。
public std：： vector\<std：:p air\<std：： string，std：： string\>\> GetContentMetadata （const std：： vector\<std：： string\>& 名称，const std：： vector\<std：： string\>& namePrefixes） const  |  从内容中获取元数据项。
public std：： shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor （） const  |  获取保护描述符。
public ContentFormat GetContentFormat() const  |  获取内容格式。
public ActionType GetSupportedActions() const  |  获取描述所有受支持操作类型的掩码枚举。
public virtual std：： shared_ptr\<ClassificationResults\> GetClassificationResults （const std：： vector\<std：： shared_ptr\<ClassificationRequest\>\> &） const  |  返回分类结果的映射。
公共虚拟 std：： map\<std：： string，std：： string\> GetAuditMetadata （） const  |  返回应用程序特定的审核键值对的映射。
  
## <a name="members"></a>Members
  
### <a name="getnewlabel-function"></a>GetNewLabel 函数
获取应在文档上应用的敏感度标签 ID。

  
**返回结果**：如果存在，则返回要应用于内容的敏感度标签 ID；否则为空以删除标签。
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 函数
获取描述文档的内容说明。 文件示例： [path\filename] 电子邮件示例： [Subject： Sender]。

  
**返回**：要应用于内容的内容说明。
审核功能将此值用作内容的用户可读说明
  
### <a name="getdatastate-function"></a>GetDataState 函数
获取应用程序与之交互时内容的状态。

  
**返回结果**：内容数据的状态
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 函数
实现应传递是否提供了降级现有标签的合理理由。

  
**返回结果**：如果降级合理并提供了合理理由消息，则返回 true；否则返回 false 
  
**另请参阅**： mip：： JustifyAction
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod 函数
获取新标签的分配方法。

  
**返回结果**：分配方法 STANDARD、PRIVILEGED、AUTO。 
  
**另请参阅**： [Mip：： AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties 函数
返回新标签的扩展属性。

  
**返回结果**：应用于内容的扩展属性。
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata 函数
从内容中获取元数据项。

  
**返回结果**：应用于内容的元数据。 每个元数据项都是名称和值对。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
获取保护描述符。

  
**返回结果**：保护描述符
  
### <a name="getcontentformat-function"></a>GetContentFormat 函数
获取内容格式。

  
**返回结果**：DEFAULT、EMAIL 
  
**另请参阅**： [Mip：： ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 函数
获取描述所有受支持操作类型的掩码枚举。

  
**返回结果**：描述所有受支持操作类型的掩码枚举。
必须支持 ActionType::Justify。 当策略和标签更改需要合理理由时，将始终返回合理理由操作。
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **classificationIds**：分类 id 列表。 



  
**返回**：分类结果的列表。 如果未执行分类循环，则返回 nullptr。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 函数
返回应用程序特定的审核键值对的映射。

  
**返回**：特定于应用程序的审核元数据注册密钥：值对发送方：发件人接收方的电子邮件 id 的列表：表示电子邮件的 LASTMODIFIEDBY 的 JSON 数组：上次修改内容的用户的电子邮件 id LastModifiedDate：上次修改内容的日期