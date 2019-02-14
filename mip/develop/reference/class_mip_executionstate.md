---
title: class mip::ExecutionState
description: 记录 mip::executionstate 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 7e036938923a3736dc184046049f30a04f1eb87f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251732"
---
# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
执行引擎所需的所有状态的接口。
客户端应只调用方法来获取所需的状态。 因此，为了提高效率，客户端可能想要实现该接口，以此动态计算相应的状态而不是提前计算。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId() const  |  获取应在文档上应用的敏感度标签 ID。
public ActionSource GetNewLabelActionSource() const  |  获取新标签操作的源。
public std::string GetContentIdentifier() const  |  获取描述文档的内容标识符。 文件的示例: [路径 \ 文件名] 的电子邮件的示例: [发送方使用者:]。
public ContentState GetContentState() const  |  获取应用程序与之交互时内容的状态。
public std::pair\<bool, std::string\> IsDowngradeJustified() const  |  实现应传递是否提供了降级现有标签的合理理由。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  获取新标签的分配方法。
public std:: vector\<std:: pair\<std:: string、 std:: string\> \> GetNewLabelExtendedProperties() 常量  |  返回新标签的扩展属性。
public std:: vector\<std:: pair\<std:: string、 std:: string\> \> GetContentMetadata (const std:: vector\<std:: string\>& 名称、 const std:: vector\<std:: string\>& namePrefixes) 常量  |  从内容中获取元数据项。
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  获取保护描述符。
public ContentFormat GetContentFormat() const  |  获取内容格式。
public ActionType GetSupportedActions() const  |  获取描述所有受支持操作类型的掩码枚举。
public virtual std::map\<std::string, std::shared_ptr\<ClassificationResult\>\> GetClassificationResults(const std::vector\<std::shared_ptr\<ClassificationRequest\>\> &) const  |  返回分类结果的映射。
公共虚拟 std:: map\<std:: string、 std:: string\> GetAuditMetadata() 常量  |  返回应用程序特定审核键-值对的映射。
  
## <a name="members"></a>成員
  
### <a name="getnewlabelid-function"></a>GetNewLabelId 函数
获取应在文档上应用的敏感度标签 ID。

  
**返回**:如果要应用于内容的敏感度标签 ID 存在，否则为空以删除标签。
  
### <a name="getnewlabelactionsource-function"></a>GetNewLabelActionSource function
获取新标签操作的源。

  
**返回**:操作源。
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 函数
获取描述文档的内容标识符。 文件的示例: [路径 \ 文件名] 的电子邮件的示例: [发送方使用者:]。

  
**返回**:要应用于内容的内容标识符。
审核功能将此值用作内容的用户可读说明
  
### <a name="getcontentstate-function"></a>GetContentState 函数
获取应用程序与之交互时内容的状态。

  
**返回**:内容数据的状态
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 函数
实现应传递是否提供了降级现有标签的合理理由。

  
**返回**:如果降级 justifiedalong 理由 messageelse 为 false，则为 true 
  
另请参阅：[mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod 函数
获取新标签的分配方法。

  
**返回**:分配方法 STANDARD、 PRIVILEGED、 AUTO。 
  
**另请参阅**: [mip::AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties 函数
返回新标签的扩展属性。

  
**返回**:扩展的属性应用于内容。
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata function
从内容中获取元数据项。

  
**返回**:应用于内容的元数据。 每个元数据项都是名称和值对。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
获取保护描述符。

  
**返回**:保护描述符
  
### <a name="getcontentformat-function"></a>GetContentFormat 函数
获取内容格式。

  
**返回**:默认情况下，电子邮件 
  
**另请参阅**: [mip::ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 函数
获取描述所有受支持操作类型的掩码枚举。

  
**返回**:描述所有支持的操作类型是掩码的枚举。
必须支持 ActionType::Justify。 当策略和标签更改需要合理理由时，将始终返回合理理由操作。
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **classificationId**：分类 ID 的列表。 



  
**返回**:分类结果的列表。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 函数
返回应用程序特定审核键-值对的映射。

  
**返回**:应用程序特定的审核元数据注册 Key: Value 对发件人的列表：发件人的收件人的电子邮件 Id:表示 LastModifiedBy 一封电子邮件的收件人的 JSON 数组：上次修改内容 LastModifiedDate 的用户的电子邮件 Id:内容的上次修改日期
