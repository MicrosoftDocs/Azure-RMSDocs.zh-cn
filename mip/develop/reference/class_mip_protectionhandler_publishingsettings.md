---
title: 类 ProtectionHandler：:P ublishingSettings
description: 记录 Microsoft 信息保护 (MIP) SDK 的 protectionhandler：:p ublishingsettings 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c5edcb9eca5e14d0f0f611f32e2f91d9ed2fcb25
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565176"
---
# <a name="class-protectionhandlerpublishingsettings"></a>类 ProtectionHandler：:P ublishingSettings 
用于创建 ProtectionHandler 以保护新内容的设置。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public PublishingSettings (const std：： shared_ptr \<ProtectionDescriptor\>& protectionDescriptor)   |  用于创建新引擎的 ProtectionHandler：： Settings 构造函数。
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  | _尚无记录。_
public bool GetIsAuditedExtractionAllowed ( # A1 const  |  获取是否允许非 MIP 感知应用程序打开受保护的内容。
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)   |  设置是否允许非 MIP 感知应用程序打开受保护的内容。
public bool GetIsDeprecatedAlgorithmPreferred ( # A1 const  |  获取是否推荐使用不推荐使用的加密算法 (ECB) 是否为向后兼容性。
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)   |  设置是否推荐使用不推荐使用的加密算法 (ECB) 是否为向后兼容性。
public void SetDelegatedUserEmail (const std：： string& delegatedUserEmail)   |  设置委派的用户。
public const std：： string& GetDelegatedUserEmail ( # A2 const  |  获取委托的用户。
public bool IsPublishingFormatJson ( # A1 const  |  获取返回的 pl 是否为 json 格式 (xml 格式是否被广泛接受并且是默认的) 。
public void SetPublishingFormatJson (bool isPublishingFormatJson)   |  无论返回的 pl 是否为 json 格式 (xml 格式是否被广泛接受并且是默认) 。
public void SetPreLicenseUserEmail (const std：： string& preLicenseUserEmail)   |  设置许可用户。
public const std：： string& GetPreLicenseUserEmail ( # A2 const  |  获取预许可用户。
  
## <a name="members"></a>成员
  
### <a name="publishingsettings-function"></a>PublishingSettings 函数
用于创建新引擎的 ProtectionHandler：： Settings 构造函数。

参数：  
* **protectionDescriptor**：保护详细信息


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
尚无记录。

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed 函数
获取是否允许非 MIP 感知应用程序打开受保护的内容。

  
**返回**：如果允许非 MIP 感知的应用程序打开受保护的内容
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed 函数
设置是否允许非 MIP 感知应用程序打开受保护的内容。

参数：  
* **isAuditedExtractionAllowed**：如果允许非 MIP 感知的应用程序打开受保护的内容


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred 函数
获取是否推荐使用不推荐使用的加密算法 (ECB) 是否为向后兼容性。

  
**返回**：如果首选 deprectated 加密算法
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred 函数
设置是否推荐使用不推荐使用的加密算法 (ECB) 是否为向后兼容性。

参数：  
* **If**： deprectated 加密算法是首选的


  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 函数
设置委派的用户。

参数：  
* **delegatedUserEmail**：委派电子邮件。


当正在进行身份验证的用户/应用程序代表其他用户时，将指定委派的用户
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 函数
获取委托的用户。

  
**返回**：已委派的用户在进行身份验证的用户/应用程序代表其他用户时指定了委派的用户
  
### <a name="ispublishingformatjson-function"></a>IsPublishingFormatJson 函数
获取返回的 pl 是否为 json 格式 (xml 格式是否被广泛接受并且是默认的) 。

  
如果设置为 json 格式输出，则 **返回**： True。
  
### <a name="setpublishingformatjson-function"></a>SetPublishingFormatJson 函数
无论返回的 pl 是否为 json 格式 (xml 格式是否被广泛接受并且是默认) 。

参数：  
* **isPublishingFormatJson**：如果启用 json 格式，则为。


  
### <a name="setprelicenseuseremail-function"></a>SetPreLicenseUserEmail 函数
设置许可用户。

参数：  
* **preLicenseUserEmail**：许可前用户


如果未指定预许可用户，则将不会获得预许可证
  
### <a name="getprelicenseuseremail-function"></a>GetPreLicenseUserEmail 函数
获取预许可用户。

  
**返回**：预许可用户