---
title: 类 ProtectionHandler：： ConsumptionSettings
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 protectionhandler：： consumptionsettings 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8ac0e4d3067528d6e860244abca2d70f0cf6a530
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214586"
---
# <a name="class-protectionhandlerconsumptionsettings"></a>类 ProtectionHandler：： ConsumptionSettings 
用于创建 ProtectionHandler 以使用现有内容的设置。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std：： vector \<uint8_t\>& serializedPublishingLicense)   |  用于创建新处理程序的 ProtectionHandler：： ConsumptionSettings 构造函数。
public ConsumptionSettings (const std：： vector \<uint8_t\>& serializedPreLicense，const std：： vector \<uint8_t\>& serializedPublishingLicense)   |  用于创建新处理程序的 ProtectionHandler：： ConsumptionSettings 构造函数。
public ConsumptionSettings (const std：： shared_ptr \<PublishingLicenseInfo\>& licenseInfo)   |  用于创建新处理程序的 ProtectionHandler：： ConsumptionSettings 构造函数。
public std：： shared_ptr \<PublishingLicenseInfo\> GetPublishingLicenseInfo ( # A1 const  |  获取与受保护内容相关联的发布许可证。
public bool GetIsOfflineOnly ( # A1 const  |  获取 ProtectionHandler 创建是否允许联机 HTTP 操作。
public void SetIsOfflineOnly (bool isOfflineOnly)   |  设置 ProtectionHandler 创建是否允许联机 HTTP 操作。
public void SetDelegatedUserEmail (const std：： string& delegatedUserEmail)   |  设置委派的用户。
public void SetContentName (const std：： string& contentName)   | _尚无记录。_
public const std：： string& GetDelegatedUserEmail ( # A2 const  |  获取委托的用户。
public const std：： string& GetContentName ( # A2 const  | _尚无记录。_
  
## <a name="members"></a>成员
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 函数
用于创建新处理程序的 ProtectionHandler：： ConsumptionSettings 构造函数。

参数：  
* **serializedPublishingLicense**：从受保护内容序列化发布许可证


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 函数
用于创建新处理程序的 ProtectionHandler：： ConsumptionSettings 构造函数。

参数：  
* **serializedPreLicense**：从附加到内容的序列化前许可证。 


* **serializedPublishingLicense**：从受保护内容序列化发布许可证


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 函数
用于创建新处理程序的 ProtectionHandler：： ConsumptionSettings 构造函数。

参数：  
* **licenseInfo**：发布受保护内容的许可证信息


仅提供 PublishingLicenseInfo (而不是原始序列化发布许可证) 将不再需要 MIP SDK 分析发布许可证。
  
### <a name="getpublishinglicenseinfo-function"></a>GetPublishingLicenseInfo 函数
获取与受保护内容相关联的发布许可证。

  
**返回**：发布许可证信息
  
### <a name="getisofflineonly-function"></a>GetIsOfflineOnly 函数
获取 ProtectionHandler 创建是否允许联机 HTTP 操作。

  
**返回**：如果不允许 HTTP 操作，则为 true; 否则，如果此设置为 true，则仅当已对内容进行了解密并缓存了未过期的许可证时，ProtectionHandler 创建才会成功。 如果找不到缓存的内容，将引发 mip：： NetworkError。
  
### <a name="setisofflineonly-function"></a>SetIsOfflineOnly 函数
设置 ProtectionHandler 创建是否允许联机 HTTP 操作。

参数：  
* **isOfflineOnly**：如果不允许 HTTP 操作，则为 True，否则为 false


如果此值设置为 true，则仅当以前已解密内容并缓存其未过期许可证时，ProtectionHandler 创建才会成功。 如果找不到缓存的内容，将引发 mip：： NetworkError。
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 函数
设置委派的用户。

参数：  
* **delegatedUserEmail**：委派电子邮件。


当正在进行身份验证的用户/应用程序代表其他用户时，将指定委派的用户
  
### <a name="setcontentname-function"></a>SetContentName 函数
_尚无记录。_

  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 函数
获取委托的用户。

  
**返回**：已委派的用户在进行身份验证的用户/应用程序代表其他用户时指定了委派的用户
  
### <a name="getcontentname-function"></a>GetContentName 函数
_尚无记录。_
