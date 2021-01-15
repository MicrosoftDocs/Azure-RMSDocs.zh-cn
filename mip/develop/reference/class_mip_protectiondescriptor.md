---
title: 类 ProtectionDescriptor
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 protectiondescriptor：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: ad643c235f322a32239d702aa4ecafd3f0e36792
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214688"
---
# <a name="class-protectiondescriptor"></a>类 ProtectionDescriptor 
与某段内容相关的保护说明。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  获取保护类型，无论是否源自保护 SDK 模板。
public std::string GetOwner() const  |  获取保护的所有者。
public std::string GetName() const  |  获取保护名称。
public std::string GetDescription() const  |  获取保护说明。
public std::string GetTemplateId() const  |  获取保护模板 ID（若有）。
public std::string GetLabelId() const  |  获取标签 ID（若有）。
public std：： string GetContentId ( # A1 const  |  获取内容 ID （如果有）。
public std::vector\<UserRights\> GetUserRights() const  |  获取用户到权限映射的集合。
public std::vector\<UserRoles\> GetUserRoles() const  |  获取用户到角色映射的集合。
public bool DoesContentExpire ( # A1 const  |  检查内容是否有过期时间。
public std：： chrono：： time_point \<std::chrono::system_clock\> GetContentValidUntil ( # A1 const  |  获取保护到期时间。
public bool DoesAllowOfflineAccess() const  |  获取保护是否允许脱机访问内容的指示。
public std::string GetReferrer() const  |  获取保护引荐来源网址。
public std：： map \<std::string, std::string\> GetEncryptedAppData ( # A1 const  |  获取已加密的应用特定数据。
public std：： map \<std::string, std::string\> GetSignedAppData ( # A1 const  |  获取已签名的应用特定数据。
public std：： string GetDoubleKeyUrl ( # A1 const  |  获取要用于自定义保护的双键 url。
  
## <a name="members"></a>成员
  
### <a name="getprotectiontype-function"></a>GetProtectionType 函数
获取保护类型，无论是否源自保护 SDK 模板。

  
**返回结果**：保护类型
  
### <a name="getowner-function"></a>GetOwner 函数
获取保护的所有者。

  
**返回结果**：保护的所有者
  
### <a name="getname-function"></a>GetName 函数
获取保护名称。

  
**返回结果**：保护名称
  
### <a name="getdescription-function"></a>GetDescription 函数
获取保护说明。

  
**返回结果**：保护说明
  
### <a name="gettemplateid-function"></a>GetTemplateId 函数
获取保护模板 ID（若有）。

  
**返回**：模板 ID
  
### <a name="getlabelid-function"></a>GetLabelId 函数
获取标签 ID（若有）。

  
**返回**：标签 ID 此属性将仅在 ProtectionDescriptors 中为以前受保护的内容填充。 它是在使用受保护内容时由服务器填充的字段。
  
### <a name="getcontentid-function"></a>GetContentId 函数
获取内容 ID （如果有）。

  
**返回**：内容 ID
  
### <a name="getuserrights-function"></a>GetUserRights 函数
获取用户到权限映射的集合。

  
**返回结果**：用户到权限映射的集合。如果当前用户无权访问此信息（即，如果用户不是所有者并且没有 VIEWRIGHTSDATA 权限），则 UserRights 属性值为空。
  
### <a name="getuserroles-function"></a>GetUserRoles 函数
获取用户到角色映射的集合。

  
**返回结果**：用户到角色映射的集合
  
### <a name="doescontentexpire-function"></a>DoesContentExpire 函数
检查内容是否有过期时间。

  
**返回**：如果内容可以过期，则返回 True; 否则返回 false
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil 函数
获取保护到期时间。

  
**返回结果**：保护到期时间
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess 函数
获取保护是否允许脱机访问内容的指示。

  
**返回结果**：指示保护是否允许脱机访问内容（默认值为 true）
  
### <a name="getreferrer-function"></a>GetReferrer 函数
获取保护引荐来源网址。

  
**返回结果**：保护引荐来源网址。引荐来源是一个 URI，如果用户无法取消对内容的保护，则可以向用户显示该 URI。 它包含有关该用户如何获权访问内容的信息。
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData 函数
获取已加密的应用特定数据。

  
**返回结果**：应用特定数据。ProtectionHandler 可能包含已由保护服务加密的应用特定数据的字典。 此加密数据独立于可通过 ProtectionDescriptor::GetSignedAppData 访问的签名数据
  
### <a name="getsignedappdata-function"></a>GetSignedAppData 函数
获取已签名的应用特定数据。

  
**返回结果**：应用特定数据。ProtectionHandler 可能包含已由保护服务签名的应用特定数据的字典。 此签名数据与可通过 ProtectionDescriptor::GetEncryptedAppData 访问的加密数据无关
  
### <a name="getdoublekeyurl-function"></a>GetDoubleKeyUrl 函数
获取要用于自定义保护的双键 url。

  
**返回**：双键 url 在自定义请求中使用的双键 url，用第二个密钥保护信息