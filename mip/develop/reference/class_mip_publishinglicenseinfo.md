---
title: 类 PublishingLicenseInfo
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 publishinglicenseinfo：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: b16c58d7faeea7b91ced99f0a1fc786701ad12a2
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213277"
---
# <a name="class-publishinglicenseinfo"></a>类 PublishingLicenseInfo 
保存用于创建保护处理程序的发布许可证的详细信息。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public PublishingLicenseInfo (const std：： vector \<uint8_t\>& serializedPublishingLicense)   | _尚无记录。_
public PublishingLicenseInfo (const std：： vector \<uint8_t\>& serializedPreLicense，const std：： vector \<uint8_t\>& serializedPublishingLicense)   | _尚无记录。_
public void SetParsedData (const std：： vector \<std::string\>& 域，const std：： string& serverPublicCert，const std：： string& id 为，const std：： string& issuerId)   | _尚无记录。_
public void SetDoubleKeyData (const std：： string& 算法，const std：： map \<std::string, std::string\>& doubleKeyApplicationData)   | _尚无记录。_
public const std：： vector \<uint8_t\>& GetSerializedPublishingLicense ( # A2 const  | _尚无记录。_
public const std：： vector \<uint8_t\>& GetPreLicense ( # A2 const  | _尚无记录。_
public const std：： vector \<std::string\>& GetDomains ( # A2 const  | _尚无记录。_
public const std：： string& GetServerPublicCertificate ( # A2 const  | _尚无记录。_
public const std：： string& GetIssuerId ( # A2 const  | _尚无记录。_
public const std：： string& GetContentId ( # A2 const  | _尚无记录。_
public bool IsLicenseParsed ( # A1 const  | _尚无记录。_
public bool HasPreLicense ( # A1 const  | _尚无记录。_
public bool GetIsDoubleKeyLicense ( # A1 const  | _尚无记录。_
public const std：： string& GetDoubleKeyAlgorithm ( # A2 const  | _尚无记录。_
public const std：： map \<std::string, std::string\>& GetDoubleKeyApplicationData ( # A2 const  | _尚无记录。_
  
## <a name="members"></a>成员
  
### <a name="publishinglicenseinfo-function"></a>PublishingLicenseInfo 函数
_尚无记录。_

  
### <a name="publishinglicenseinfo-function"></a>PublishingLicenseInfo 函数
_尚无记录。_

  
### <a name="setparseddata-function"></a>SetParsedData 函数
_尚无记录。_

  
### <a name="setdoublekeydata-function"></a>SetDoubleKeyData 函数
_尚无记录。_

  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 函数
_尚无记录。_

  
### <a name="getprelicense-function"></a>GetPreLicense 函数
_尚无记录。_

  
### <a name="getdomains-function"></a>GetDomains 函数
_尚无记录。_

  
### <a name="getserverpubliccertificate-function"></a>GetServerPublicCertificate 函数
_尚无记录。_

  
### <a name="getissuerid-function"></a>GetIssuerId 函数
_尚无记录。_

  
### <a name="getcontentid-function"></a>GetContentId 函数
_尚无记录。_

  
### <a name="islicenseparsed-function"></a>IsLicenseParsed 函数
_尚无记录。_

  
### <a name="hasprelicense-function"></a>HasPreLicense 函数
_尚无记录。_

  
### <a name="getisdoublekeylicense-function"></a>GetIsDoubleKeyLicense 函数
_尚无记录。_

  
### <a name="getdoublekeyalgorithm-function"></a>GetDoubleKeyAlgorithm 函数
_尚无记录。_

  
### <a name="getdoublekeyapplicationdata-function"></a>GetDoubleKeyApplicationData 函数
_尚无记录。_
