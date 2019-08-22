---
title: '类 mip::P rotectionHandler:: ConsumptionSettings'
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionhandler 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 259c29cb0da2635bc1aa8973b5e975e526fb81b3
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893134"
---
# <a name="class-mipprotectionhandlerconsumptionsettings"></a>类 mip::P rotectionHandler:: ConsumptionSettings 
用于创建[ProtectionHandler](class_mip_protectionhandler.md)以使用现有内容的设置。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std:: vector\<uint8_t\>& serializedPublishingLicense)  | 用于创建新处理程序的 ProtectionHandler:: ConsumptionSettings 构造函数。
public ConsumptionSettings (const std:: shared_ptr\<PublishingLicenseInfo\>& licenseInfo)  |  用于创建新处理程序的 ProtectionHandler:: ConsumptionSettings 构造函数。
public std:: shared_ptr\<PublishingLicenseInfo\> GetPublishingLicenseInfo () const  |  获取与受保护内容相关联的发布许可证。
public bool GetIsOfflineOnly () const  |  获取[ProtectionHandler](class_mip_protectionhandler.md)创建是否允许联机 HTTP 操作。
public void SetIsOfflineOnly (bool isOfflineOnly)  |  设置[ProtectionHandler](class_mip_protectionhandler.md)创建是否允许联机 HTTP 操作。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  设置委派的用户。
public const std:: string & GetDelegatedUserEmail () const  |  获取委托的用户。
  
## <a name="members"></a>成员
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 函数
用于创建新处理程序的 ProtectionHandler:: ConsumptionSettings 构造函数。

参数：  
* **serializedPublishingLicense**:受保护内容的序列化发布许可证


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 函数
用于创建新处理程序的 ProtectionHandler:: ConsumptionSettings 构造函数。

参数：  
* **licenseInfo**:发布受保护内容的许可证信息


提供 PublishingLicenseInfo (而不只是原始序列化发布许可证) 将不再需要 MIP SDK 来解析发布许可证。
  
### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo 函数
获取与受保护内容相关联的发布许可证。

  
**返回**:发布许可证信息
  
### <a name="getisofflineonly-function"></a>GetIsOfflineOnly 函数
获取[ProtectionHandler](class_mip_protectionhandler.md)创建是否允许联机 HTTP 操作。

  
**返回**:如果不允许 HTTP 操作, 则为 True; 否则, 如果此设置为 true, 则仅当已对内容进行了解密并缓存了未过期的许可证时, [ProtectionHandler](class_mip_protectionhandler.md)创建才会成功。 如果找不到缓存的内容, 将引发 mip:: NetworkError =。
  
### <a name="setisofflineonly-function"></a>SetIsOfflineOnly 函数
设置[ProtectionHandler](class_mip_protectionhandler.md)创建是否允许联机 HTTP 操作。

参数：  
* **isOfflineOnly**:如果不允许 HTTP 操作, 则为 True, 否则为 false


如果此值设置为 true, 则仅当以前已解密内容并缓存其未过期许可证时, [ProtectionHandler](class_mip_protectionhandler.md)创建才会成功。 如果找不到缓存的内容, 将引发 mip:: NetworkError。
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 函数
设置委派的用户。

参数：  
* **delegatedUserEmail**: 委派电子邮件。


当正在进行身份验证的用户/应用程序代表其他用户时, 将指定委派的用户
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 函数
获取委托的用户。

  
**返回**:委派的用户当身份验证用户/应用程序代表其他用户操作时, 指定了委派的用户