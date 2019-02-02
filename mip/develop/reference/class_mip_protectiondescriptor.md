---
title: 类 mip::ProtectionDescriptor
description: 记录 mip::protectiondescriptor 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: f3bf856982f3e5b4c060a83fe1e822866fb1808b
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651711"
---
# <a name="class-mipprotectiondescriptor"></a>类 mip::ProtectionDescriptor 
与某段内容相关的保护说明。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  获取保护类型，无论是否源自保护 SDK 模板。
public std::string GetOwner() const  |  获取保护的所有者。
public std::string GetName() const  |  获取保护名称。
public std::string GetDescription() const  |  获取保护说明。
public std::string GetTemplateId() const  |  获取保护模板 ID（若有）。
public std::string GetLabelId() const  |  获取标签 ID（若有）。
public std:: vector\<UserRights\> GetUserRights() 常量  |  获取用户到权限映射的集合。
public std:: vector\<UserRoles\> GetUserRoles() 常量  |  获取用户到角色映射的集合。
public bool DoesContentExpire() const  |  检查内容或不具有过期时间。
公共 std::chrono::time_point\<std::chrono::system_clock\> GetContentValidUntil() 常量  |  获取保护到期时间。
public bool DoesAllowOfflineAccess() const  |  获取保护是否允许脱机访问内容的指示。
public std::string GetReferrer() const  |  获取保护引荐来源网址。
public std::map\<std::string, std::string\> GetEncryptedAppData() const  |  获取已加密的应用特定数据。
public std:: map\<std:: string、 std:: string\> GetSignedAppData() 常量  |  获取已签名的应用特定数据。
  
## <a name="members"></a>成員
  
### <a name="getprotectiontype-function"></a>GetProtectionType 函数
获取保护类型，无论是否源自保护 SDK 模板。

  
**返回**:保护类型
  
### <a name="getowner-function"></a>GetOwner 函数
获取保护的所有者。

  
**返回**:保护的所有者
  
### <a name="getname-function"></a>GetName 函数
获取保护名称。

  
**返回**:保护名称
  
### <a name="getdescription-function"></a>GetDescription 函数
获取保护说明。

  
**返回**:保护说明
  
### <a name="gettemplateid-function"></a>GetTemplateId 函数
获取保护模板 ID（若有）。

  
**返回**:模板 ID
  
### <a name="getlabelid-function"></a>GetLabelId 函数
获取标签 ID（若有）。

  
**返回**:[标签](class_mip_label.md)ID 仅 ProtectionDescriptors 将此属性填充为预先存在的受保护的内容。 它是在使用受保护内容时由服务器填充的字段。
  
### <a name="getuserrights-function"></a>GetUserRights 函数
获取用户到权限映射的集合。

  
**返回**:用户到权限映射的集合的值[UserRights](class_mip_userrights.md)属性将为空，如果当前用户不具有访问此信息 （即，如果用户不是所有者，且没有 VIEWRIGHTSDATA 权限）。
  
### <a name="getuserroles-function"></a>GetUserRoles 函数
获取用户到角色映射的集合。

  
**返回**:用户到角色映射的集合
  
### <a name="doescontentexpire-function"></a>DoesContentExpire 函数
检查内容或不具有过期时间。

  
**返回**:如果内容可能会过期，否则返回 false，则返回 true
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil 函数
获取保护到期时间。

  
**返回**:保护过期时间
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess 函数
获取保护是否允许脱机访问内容的指示。

  
**返回**:如果保护是否允许离线访问内容 (默认值 = true)
  
### <a name="getreferrer-function"></a>GetReferrer 函数
获取保护引荐来源网址。

  
**返回**:保护引用网址： 该引用网站是一个 URI，如果它们不能取消保护内容，则可向用户显示。 它包含有关该用户如何获权访问内容的信息。
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData function
获取已加密的应用特定数据。

  
**返回**:应用特定数据： [ProtectionHandler](class_mip_protectionhandler.md)可能持有的加密的保护服务的特定于应用的数据字典。 此加密数据独立于可通过 [ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getappsigneddata-function) 访问的签名数据
  
### <a name="getsignedappdata-function"></a>GetSignedAppData 函数
获取已签名的应用特定数据。

  
**返回**:应用特定数据： [ProtectionHandler](class_mip_protectionhandler.md)可能持有的已签名的保护服务的特定于应用的数据的字典。 此签名数据与可通过 [ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata-function) 访问的加密数据无关