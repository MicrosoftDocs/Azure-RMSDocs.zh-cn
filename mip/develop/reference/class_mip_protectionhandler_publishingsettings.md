---
title: 类 mip：:P rotectionHandler：:P ublishingSettings
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionhandler 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 358c96b15b4e9eeb10a42937602487ec4d59b050
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560743"
---
# <a name="class-mipprotectionhandlerpublishingsettings"></a>类 mip：:P rotectionHandler：:P ublishingSettings 
用于创建 ProtectionHandler 以保护新内容的设置。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public PublishingSettings （const std：： shared_ptr\<ProtectionDescriptor\>& protectionDescriptor）  |  用于创建新引擎的 ProtectionHandler：： Settings 构造函数。
public std：： shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor （） const  | 尚未记录。
public bool GetIsAuditedExtractionAllowed （） const  |  获取是否允许非 MIP 感知应用程序打开受保护的内容。
public void SetIsAuditedExtractionAllowed （bool isAuditedExtractionAllowed）  |  设置是否允许非 MIP 感知应用程序打开受保护的内容。
public bool GetIsDeprecatedAlgorithmPreferred （） const  |  获取是否首选不推荐使用的加密算法（ECB）来实现向后兼容性。
public void SetIsDeprecatedAlgorithmPreferred （bool isDeprecatedAlgorithmPreferred）  |  设置是否首选不推荐使用的加密算法（ECB）来实现向后兼容性。
public void SetDelegatedUserEmail （const std：： string & delegatedUserEmail）  |  设置委派的用户。
public const std：： string & GetDelegatedUserEmail （） const  |  获取委托的用户。
public bool IsPublishingFormatJson （） const  |  获取返回的 pl 是否为 json 格式（xml 格式是否被广泛接受并且为默认值）。
public void SetPublishingFormatJson （bool isPublishingFormatJson）  |  返回的 pl 是否为 json 格式（xml 格式更广泛地接受并且是默认值）。
  
## <a name="members"></a>成員
  
### <a name="publishingsettings-function"></a>PublishingSettings 函数
用于创建新引擎的 ProtectionHandler：： Settings 构造函数。

参数：  
* **protectionDescriptor**：保护详细信息


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
_尚无记录。_

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed 函数
获取是否允许非 MIP 感知应用程序打开受保护的内容。

  
**返回**：如果允许非 MIP 感知的应用程序打开受保护的内容
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed 函数
设置是否允许非 MIP 感知应用程序打开受保护的内容。

参数：  
* **isAuditedExtractionAllowed**：如果允许非 MIP 感知的应用程序打开受保护的内容


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred 函数
获取是否首选不推荐使用的加密算法（ECB）来实现向后兼容性。

  
**返回**：如果首选 deprectated 加密算法
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred 函数
设置是否首选不推荐使用的加密算法（ECB）来实现向后兼容性。

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
获取返回的 pl 是否为 json 格式（xml 格式是否被广泛接受并且为默认值）。

  
如果设置为 json 格式输出，则**返回**： True。
  
### <a name="setpublishingformatjson-function"></a>SetPublishingFormatJson 函数
返回的 pl 是否为 json 格式（xml 格式更广泛地接受并且是默认值）。

参数：  
* **isPublishingFormatJson**：如果启用 json 格式，则为。

