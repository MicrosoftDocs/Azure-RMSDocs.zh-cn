---
title: 类 mip::P rotectionHandler::P ublishingSettings
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionhandler 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 83489b41811cdaaf46b7336b21eeccb8289eb9f1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893117"
---
# <a name="class-mipprotectionhandlerpublishingsettings"></a>类 mip::P rotectionHandler::P ublishingSettings 
用于创建[ProtectionHandler](class_mip_protectionhandler.md)以保护新内容的设置。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public PublishingSettings (const std:: shared_ptr\<ProtectionDescriptor\>& ProtectionDescriptor)  |  用于创建新引擎的 ProtectionHandler:: Settings 构造函数。
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  | _尚无记录。_
public bool GetIsAuditedExtractionAllowed () const  |  获取是否允许非 MIP 感知应用程序打开受保护的内容。
public void SetIsAuditedExtractionAllowed (bool isAuditedExtractionAllowed)  |  设置是否允许非 MIP 感知应用程序打开受保护的内容。
public bool GetIsDeprecatedAlgorithmPreferred () const  |  获取是否首选不推荐使用的加密算法 (ECB) 来实现向后兼容性。
public void SetIsDeprecatedAlgorithmPreferred (bool isDeprecatedAlgorithmPreferred)  |  设置是否首选不推荐使用的加密算法 (ECB) 来实现向后兼容性。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  设置委派的用户。
public const std:: string & GetDelegatedUserEmail () const  |  获取委托的用户。
  
## <a name="members"></a>成员
  
### <a name="publishingsettings-function"></a>PublishingSettings 函数
用于创建新引擎的 ProtectionHandler:: Settings 构造函数。

参数：  
* **protectionDescriptor**:保护详细信息


  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
_尚无记录。_

  
### <a name="getisauditedextractionallowed-function"></a>GetIsAuditedExtractionAllowed 函数
获取是否允许非 MIP 感知应用程序打开受保护的内容。

  
**返回**:如果允许非 MIP 感知应用程序打开受保护的内容
  
### <a name="setisauditedextractionallowed-function"></a>SetIsAuditedExtractionAllowed 函数
设置是否允许非 MIP 感知应用程序打开受保护的内容。

参数：  
* **isAuditedExtractionAllowed**:如果允许非 MIP 感知应用程序打开受保护的内容


  
### <a name="getisdeprecatedalgorithmpreferred-function"></a>GetIsDeprecatedAlgorithmPreferred 函数
获取是否首选不推荐使用的加密算法 (ECB) 来实现向后兼容性。

  
**返回**:如果首选 deprectated 加密算法
  
### <a name="setisdeprecatedalgorithmpreferred-function"></a>SetIsDeprecatedAlgorithmPreferred 函数
设置是否首选不推荐使用的加密算法 (ECB) 来实现向后兼容性。

参数：  
* **If**: deprectated 加密算法是首选的


  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 函数
设置委派的用户。

参数：  
* **delegatedUserEmail**: 委派电子邮件。


当正在进行身份验证的用户/应用程序代表其他用户时, 将指定委派的用户
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 函数
获取委托的用户。

  
**返回**:委派的用户当身份验证用户/应用程序代表其他用户操作时, 指定了委派的用户