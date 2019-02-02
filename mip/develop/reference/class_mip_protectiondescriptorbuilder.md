---
title: 类 mip::ProtectionDescriptorBuilder
description: 记录 mip::protectiondescriptorbuilder 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b6ac49c7cb4d6f7592abac041365191d90951b7a
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651279"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>类 mip::ProtectionDescriptorBuilder 
构造 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，用于描述与一段内容相关的保护。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr\<ProtectionDescriptor\> Build()  |  创建 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，它的访问权限由此 [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) 实例定义。
public void SetName(const std::string& value)  |  设置保护策略名称。
public void SetDescription(const std::string& value)  |  设置保护策略说明。
public void SetContentValidUntil (const std::chrono::time_point\<std::chrono::system_clock\>& 值)  |  设置保护策略到期时间。
public void SetAllowOfflineAccess(bool value)  |  设置保护策略是否允许脱机访问内容。
public void SetReferrer(const std::string& uri)  |  设置保护策略引荐来源网址。
public void SetEncryptedAppData (const std:: map\<std:: string、 std:: string\>& 值)  |  设置应加密的应用特定数据。
public void SetSignedAppData (const std:: map\<std:: string、 std:: string\>& 值)  |  设置应签名的应用特定数据。
public virtual ~ProtectionDescriptorBuilder()  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="build-function"></a>生成函数
创建 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，它的访问权限由此 [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) 实例定义。

  
**返回**:新[ProtectionDescriptor](class_mip_protectiondescriptor.md)实例
  
### <a name="setname-function"></a>SetName 函数
设置保护策略名称。

参数：  
* **值**:保护策略名称


  
### <a name="setdescription-function"></a>SetDescription 函数
设置保护策略说明。

参数：  
* **值**:策略说明


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil 函数
设置保护策略到期时间。

参数：  
* **值**:策略过期时间


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess 函数
设置保护策略是否允许脱机访问内容。

参数：  
* **值**:如果策略是否允许离线访问内容


  
### <a name="setreferrer-function"></a>SetReferrer 函数
设置保护策略引荐来源网址。

参数：  
* **uri**:策略引用网址


引荐来源网址是向无法获取保护策略的用户显示的 URI，其中介绍了用户如何才能获取内容访问权限。
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData function
设置应加密的应用特定数据。

参数：  
* **值**:特定于应用的数据


应用程序可以指定保护服务加密的应用专用数据的字典。 此加密数据与 SetSignedAppData 设置的签名数据无关。
  
### <a name="setsignedappdata-function"></a>SetSignedAppData function
设置应签名的应用特定数据。

参数：  
* **值**:特定于应用的数据


应用程序可以指定保护服务签名的应用专用数据的字典。 此签名数据与 SetEncryptedAppData 设置的加密数据无关。
  
### <a name="protectiondescriptorbuilder-function"></a>~ProtectionDescriptorBuilder function
_尚无记录。_
