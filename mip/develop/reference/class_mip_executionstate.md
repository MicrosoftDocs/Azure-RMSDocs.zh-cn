---
title: 类 mip ExecutionState
description: 类 mip ExecutionState 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 976bca60f3f494a0fbf196e6512b00bdcdd63992
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446305"
---
# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
执行引擎所需的所有状态的接口。
客户端应只调用方法来获取所需的状态。 因此，为了提高效率，客户端可能想要实现该接口，以此动态计算相应的状态而不是提前计算。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  获取应在文档上应用的敏感度标签 ID。
 public ActionSource GetNewLabelActionSource() const  |  获取新标签操作的源。
 public std::string GetContentIdentifier() const  |  获取描述文档的内容标识符。 文件示例：[路径]，电子邮件示例：[主题:发件人]。
 public ContentState GetContentState() const  |  获取应用程序与之交互时内容的状态。
public std::pair<bool, std::string> IsDowngradeJustified() const  |  实现应传递是否提供了降级现有标签的合理理由。
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  获取新标签的分配方法。
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  返回新标签的扩展属性。
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  从内容中获取元数据项。
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor() const  |  获取保护描述符。
 public ContentFormat GetContentFormat() const  |  获取内容格式。
 public ActionType GetSupportedActions() const  |  获取描述所有受支持操作类型的掩码枚举。
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  返回分类结果的映射。
  
## <a name="members"></a>成員
  
### <a name="getnewlabelid"></a>GetNewLabelId
获取应在文档上应用的敏感度标签 ID。

  
**返回结果**：如果存在，则返回要应用于内容的敏感度标签 ID；否则为空以删除标签。
  
### <a name="getnewlabelactionsource"></a>GetNewLabelActionSource
获取新标签操作的源。

  
**返回结果**：操作源。
  
### <a name="getcontentidentifier"></a>GetContentIdentifier
获取描述文档的内容标识符。 文件示例：[路径]，电子邮件示例：[主题:发件人]。

  
**返回结果**：要应用于内容的内容标识符。
审核功能将此值用作内容的用户可读说明
  
### <a name="getcontentstate"></a>GetContentState
获取应用程序与之交互时内容的状态。

  
**返回结果**：内容数据的状态
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
实现应传递是否提供了降级现有标签的合理理由。

  
**返回结果**：如果降级合理并提供了合理理由消息，则返回 true；否则返回 false 
  
另请参阅：[mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
获取新标签的分配方法。

  
**返回结果**：分配方法 STANDARD、PRIVILEGED、AUTO。 
  
另请参阅：mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
返回新标签的扩展属性。

  
**返回结果**：应用于内容的扩展属性。
  
### <a name="getcontentmetadata"></a>GetContentMetadata
从内容中获取元数据项。

  
**返回结果**：应用于内容的元数据。 每个元数据项都是名称和值对。
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
获取保护描述符。

  
**返回结果**：保护描述符
  
### <a name="getcontentformat"></a>GetContentFormat
获取内容格式。

  
**返回结果**：DEFAULT、EMAIL 
  
**另请参阅**：mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
获取描述所有受支持操作类型的掩码枚举。

  
**返回结果**：描述所有受支持操作类型的掩码枚举。
必须支持 ActionType::Justify。 当策略和标签更改需要合理理由时，将始终返回合理理由操作。
  
### <a name="classificationresult"></a>ClassificationResult
返回分类结果的映射。

参数：  
* **classificationId**：分类 ID 的列表。 



  
**返回结果**：分类结果列表。