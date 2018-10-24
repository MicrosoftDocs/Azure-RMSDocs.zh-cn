---
title: 类 mip ProtectionDescriptor
description: 类 mip ProtectionDescriptor 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e723041af1eec7be7a839bf36f6d3db67b32447f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446543"
---
# <a name="class-mipprotectiondescriptor"></a>类 mip::ProtectionDescriptor 
与某段内容相关的保护说明。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  获取保护类型，无论是否源自保护 SDK 模板。
 public std::string GetOwner() const  |  获取保护的所有者。
 public std::string GetName() const  |  获取保护名称。
 public std::string GetDescription() const  |  获取保护说明。
 public std::string GetTemplateId() const  |  获取保护模板 ID（若有）。
 public std::string GetLabelId() const  |  获取标签 ID（若有）。
public std::vector<UserRights> GetUserRights() const  |  获取用户到权限映射的集合。
public std::vector<UserRoles> GetUserRoles() const  |  获取用户到角色映射的集合。
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil() const  |  获取保护到期时间。
 public bool DoesAllowOfflineAccess() const  |  获取保护是否允许脱机访问内容的指示。
 public std::string GetReferrer() const  |  获取保护引荐来源网址。
public std::map<std::string, std::string> GetEncryptedAppData() const  |  获取已加密的应用特定数据。
public std::map<std::string, std::string> GetSignedAppData() const  |  获取已签名的应用特定数据。
  
## <a name="members"></a>成員
  
### <a name="protectiontype"></a>ProtectionType
获取保护类型，无论是否源自保护 SDK 模板。

  
**返回结果**：保护类型
  
### <a name="getowner"></a>GetOwner
获取保护的所有者。

  
**返回结果**：保护的所有者
  
### <a name="getname"></a>GetName
获取保护名称。

  
**返回结果**：保护名称
  
### <a name="getdescription"></a>GetDescription
获取保护说明。

  
**返回结果**：保护说明
  
### <a name="gettemplateid"></a>GetTemplateId
获取保护模板 ID（若有）。

  
**返回结果**：模板 ID
  
### <a name="getlabelid"></a>GetLabelId
获取标签 ID（若有）。

  
**返回结果**：[标签](class_mip_label.md) ID。仅在 ProtectionDescriptors 中针对预先存在的受保护内容填充此属性。 它是在使用受保护内容时由服务器填充的字段。
  
### <a name="userrights"></a>UserRights
获取用户到权限映射的集合。

  
**返回结果**：用户到权限映射的集合。如果当前用户无权访问此信息（即，如果用户不是所有者并且没有 VIEWRIGHTSDATA 权限），则 [UserRights](class_mip_userrights.md) 属性值为空。
  
### <a name="userroles"></a>UserRoles
获取用户到角色映射的集合。

  
**返回结果**：用户到角色映射的集合
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
获取保护到期时间。

  
**返回结果**：保护到期时间
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
获取保护是否允许脱机访问内容的指示。

  
**返回结果**：指示保护是否允许脱机访问内容（默认值为 true）
  
### <a name="getreferrer"></a>GetReferrer
获取保护引荐来源网址。

  
**返回结果**：保护引荐来源网址。引荐来源是一个 URI，如果用户无法取消对内容的保护，则可以向用户显示该 URI。 它包含有关该用户如何获权访问内容的信息。
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
获取已加密的应用特定数据。

  
**返回结果**：应用特定数据。[ProtectionHandler](class_mip_protectionhandler.md) 可能包含已由保护服务加密的应用特定数据的字典。 此加密数据独立于可通过 [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata) 访问的签名数据
  
### <a name="getsignedappdata"></a>GetSignedAppData
获取已签名的应用特定数据。

  
**返回结果**：应用特定数据。[ProtectionHandler](class_mip_protectionhandler.md) 可能包含已由保护服务签名的应用特定数据的字典。 此签名数据与可通过 [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata) 访问的加密数据无关