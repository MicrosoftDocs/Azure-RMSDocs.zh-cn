---
title: 类 mip::ProtectionDescriptorBuilder
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectiondescriptorbuilder 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: ed9d7085f7406e5c921843d32069f2f6af9f5807
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489684"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>类 mip::ProtectionDescriptorBuilder 
构造描述与一段内容相关联的保护的 ProtectionDescriptor。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public MIP_API std：： shared_ptr\<ProtectionDescriptor\> Build （）  |  创建一个 ProtectionDescriptor，其访问权限由此 ProtectionDescriptorBuilder 实例定义。
public void SetName(const std::string& value)  |  设置保护策略名称。
public void SetDescription(const std::string& value)  |  设置保护策略说明。
public void SetContentValidUntil （const std：： chrono：： time_point\<std：： chrono：： system_clock\>& 值）  |  设置保护策略到期时间。
public void SetAllowOfflineAccess(bool value)  |  设置保护策略是否允许脱机访问内容。
public void SetReferrer(const std::string& uri)  |  设置保护策略引荐来源网址。
public void SetEncryptedAppData （const std：： map\<std：： string，std：： string\>& 值）  |  设置应加密的应用特定数据。
public void SetSignedAppData （const std：： map\<std：： string，std：： string\>& 值）  |  设置应签名的应用特定数据。
public virtual ~ProtectionDescriptorBuilder()  | _尚无记录。_
  
## <a name="members"></a>Members
  
### <a name="build-function"></a>生成函数
创建一个 ProtectionDescriptor，其访问权限由此 ProtectionDescriptorBuilder 实例定义。

  
**返回**： New ProtectionDescriptor 实例
  
### <a name="setname-function"></a>SetName 函数
设置保护策略名称。

参数：  
* **value**：保护策略名称


  
### <a name="setdescription-function"></a>SetDescription 函数
设置保护策略说明。

参数：  
* **value**：策略说明


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil 函数
设置保护策略到期时间。

参数：  
* **value**：策略过期时间


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess 函数
设置保护策略是否允许脱机访问内容。

参数：  
* value：策略是否允许脱机访问内容


  
### <a name="setreferrer-function"></a>SetReferrer 函数
设置保护策略引荐来源网址。

参数：  
* **uri**：策略引用网址


引荐来源网址是向无法获取保护策略的用户显示的 URI，其中介绍了用户如何才能获取内容访问权限。
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData 函数
设置应加密的应用特定数据。

参数：  
* **value**：应用特定数据


应用程序可以指定保护服务加密的应用专用数据的字典。 此加密数据与 SetSignedAppData 设置的签名数据无关。
  
### <a name="setsignedappdata-function"></a>SetSignedAppData 函数
设置应签名的应用特定数据。

参数：  
* **value**：应用特定数据


应用程序可以指定保护服务签名的应用专用数据的字典。 此签名数据与 SetEncryptedAppData 设置的加密数据无关。
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder 函数
_尚无记录。_
