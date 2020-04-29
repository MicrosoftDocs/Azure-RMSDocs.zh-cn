---
title: 类 ProtectionHandler
description: 记录 Microsoft 信息保护（MIP） SDK 的 protectionhandler：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 948db155cbeca6c36c10bac76f26d42952e11e90
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764483"
---
# <a name="class-protectionhandler"></a>类 ProtectionHandler 
管理特定保护配置的保护相关操作。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： shared_ptr\<stream\> CreateProtectedStream （const std：： shared_ptr\<stream\>& backingStream，int64_t contentStartPosition，int64_t contentSize）  |  创建允许加密/解密内容的受保护流。
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  加密缓冲区。
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  解密缓冲区。
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  计算要使用此 ProtectionHandler 加密的内容的大小（以字节为单位）。
public int64_t GetBlockSize()  |  获取此 ProtectionHandler 使用的密码模式的块大小（以字节为单位）。
public std：： vector\<std：： string\> GetRights （） const  |  获取向与此 ProtectionHandler 关联的用户/标识授予的权限。
public bool AccessCheck(const std::string& right) const  |  检查保护处理程序是否向用户授予指定访问权限。
public const std::string GetIssuedTo()  |  获取与保护处理程序关联的用户。
public const std::string GetOwner()  |  获取内容所有者的电子邮件地址。
public bool IsIssuedToOwner()  |  获取当前用户是否为内容所有者的指示。
public std：： shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor （）  |  获取保护详细信息。
public const std::string GetContentId()  |  获取文档/内容的唯一标识符。
public bool DoesUseDeprecatedAlgorithms()  |  获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。
public bool IsAuditedExtractAllowed()  |  获取保护处理程序是否向用户授予“已审核的提取”权限的指示。
public const std：： vector\<Uint8_t\>& GetSerializedPublishingLicense （） const  |  将 ProtectionHandler 序列化为发布许可证 (PL)
public const std：： vector\<Uint8_t\>& GetSerializedPreLicense （PreLicenseFormat 格式） const  |  获取预许可证。
枚举 PreLicenseFormat  |  预许可格式。
  
## <a name="members"></a>成员
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream 函数
创建允许加密/解密内容的受保护流。

参数：  
* **backingStream**：从中执行读/写操作的回溯流 


* **contentStartPosition**：受保护内容在回溯流中的起始位置（以字节为单位） 


* **contentSize**：回溯流中受保护内容的大小（以字节为单位）



  
**返回结果**：受保护流
  
### <a name="encryptbuffer-function"></a>EncryptBuffer 函数
加密缓冲区。

参数：  
* **offsetFromStart**：inputBuffer 与明文内容开头的相对位置 


* **inputBuffer**：将加密的明文内容所在的缓冲区 


* **inputBufferSize**：输入缓冲区大小（以字节为单位） 


* **outputBuffer**：将加密内容复制到的缓冲区 


* **outputBufferSize**：输出缓冲区大小（以字节为单位） 


* **isFinal**：输入缓冲区是否包含最终的明文字节



  
**返回结果**：加密内容的实际大小（以字节为单位）
  
### <a name="decryptbuffer-function"></a>DecryptBuffer 函数
解密缓冲区。

参数：  
* **offsetFromStart**：inputBuffer 与加密内容开头的相对位置 


* **inputBuffer**：将解密的加密内容所在的缓冲区 


* **inputBufferSize**：输入缓冲区大小（以字节为单位） 


* **outputBuffer**：将解密内容复制到的缓冲区 


* **outputBufferSize**：输出缓冲区大小（以字节为单位） 


* **isFinal**：输入缓冲区是否包含最终的加密字节



  
**返回结果**：解密内容的实际大小（以字节为单位）
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength 函数
计算要使用此 ProtectionHandler 加密的内容的大小（以字节为单位）。

参数：  
* **unprotectedLength**：未受保护内容的大小（以字节为单位） 


* **includesFinalBlock**：描述相关的未受保护内容是否包含最终块。 例如，在 CBC4k 加密模式下，非最终受保护块与未受保护块的大小相同，但最终受保护块比未受保护块大。



  
**返回结果**：受保护内容的大小（以字节为单位）
  
### <a name="getblocksize-function"></a>GetBlockSize 函数
获取此 ProtectionHandler 使用的密码模式的块大小（以字节为单位）。

  
**返回结果**：块大小（以字节为单位）
  
### <a name="getrights-function"></a>GetRights 函数
获取向与此 ProtectionHandler 关联的用户/标识授予的权限。

  
**返回结果**：向用户授予的权限
  
### <a name="accesscheck-function"></a>AccessCheck 函数
检查保护处理程序是否向用户授予指定访问权限。

参数：  
* **right**：检查权限



  
**返回结果**：指示保护处理程序是否向用户授予指定访问权限
  
### <a name="getissuedto-function"></a>GetIssuedTo 函数
获取与保护处理程序关联的用户。

  
**返回结果**：与保护处理程序关联的用户
  
### <a name="getowner-function"></a>GetOwner 函数
获取内容所有者的电子邮件地址。

  
**返回结果**：内容所有者的电子邮件地址
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner 函数
获取当前用户是否为内容所有者的指示。

  
**返回结果**：指示当前用户是否为内容所有者
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
获取保护详细信息。

  
**返回结果**：保护详细信息
  
### <a name="getcontentid-function"></a>GetContentId 函数
获取文档/内容的唯一标识符。

  
**返回结果**：唯一内容标识符
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms 函数
获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。

  
**返回结果**：指示保护处理程序是否使用已弃用的加密算法
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed 函数
获取保护处理程序是否向用户授予“已审核的提取”权限的指示。

  
**返回结果**：指示保护处理程序是否向用户授予“已审核的提取”权限
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 函数
将 ProtectionHandler 序列化为发布许可证 (PL)

  
**返回结果**：序列化的发布许可证
  
### <a name="getserializedprelicense-function"></a>GetSerializedPreLicense 函数
获取预许可证。

参数：  
* **格式**：预许可格式



  
**返回**：序列化预许可预许可允许用户立即使用内容而无需进行额外的 HTTP 调用。 必须已使用[ProtectionHandler：:P ublishingsettings：： SetPreLicenseUserEmail](class_mip_protectionhandler_publishingsettings.md)值创建了 ProtectionHandler，否则将返回空矢量。
  
### <a name="prelicenseformat-enum"></a>PreLicenseFormat 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
Xml            | MSIPC 使用的旧版 XML/SOAP 格式
Json            | MIP SDK 和 RMS SDK 使用的 JSON/REST 格式
预许可格式。