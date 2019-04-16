---
title: 类 mip::ProtectionHandler
description: 记录 mip::protectionhandler 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 20ac5207e744224d9d8eaef72607708721c55172
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573885"
---
# <a name="class-mipprotectionhandler"></a>类 mip::ProtectionHandler 
管理特定保护配置的保护相关操作。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::\<Stream\> CreateProtectedStream (const std:: shared_ptr\<Stream\>& backingStream，int64_t contentStartPosition int64_t contentSize)  |  创建允许加密/解密内容的受保护流。
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  加密缓冲区。
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  解密缓冲区。
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  计算要使用此 [ProtectionHandler](class_mip_protectionhandler.md) 加密的内容的大小（以字节为单位）。
public int64_t GetBlockSize()  |  获取此 [ProtectionHandler](class_mip_protectionhandler.md) 使用的密码模式的块大小（以字节为单位）。
public std:: vector\<std:: string\> GetRights() 常量  |  获取向与此 [ProtectionHandler](class_mip_protectionhandler.md) 关联的用户/标识授予的权限。
public bool AccessCheck(const std::string& right) const  |  检查保护处理程序是否向用户授予指定访问权限。
public const std::string GetIssuedTo()  |  获取与保护处理程序关联的用户。
public const std::string GetOwner()  |  获取内容所有者的电子邮件地址。
public bool IsIssuedToOwner()  |  获取当前用户是否为内容所有者的指示。
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor()  |  获取保护详细信息。
public const std::string GetContentId()  |  获取文档/内容的唯一标识符。
public bool DoesUseDeprecatedAlgorithms()  |  获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。
public bool IsAuditedExtractAllowed()  |  获取保护处理程序是否向用户授予“已审核的提取”权限的指示。
public const std::vector\<uint8_t\> GetSerializedPublishingLicense()  |  将 [ProtectionHandler](class_mip_protectionhandler.md) 序列化为发布许可证 (PL)
public const std::vector\<uint8_t\> GetSerializedProtectionInfo()  |  获取保护信息。
  
## <a name="members"></a>成員
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream 函数
创建允许加密/解密内容的受保护流。

参数：  
* **backingStream**:从其读取/写入备份流 


* **contentStartPosition**:在受保护的内容的开始处的后备流内的起始位置 （以字节为单位） 


* **contentSize**:中支持流的受保护内容的大小 （以字节为单位）



  
**返回**:受保护的流
  
### <a name="encryptbuffer-function"></a>EncryptBuffer 函数
加密缓冲区。

参数：  
* **offsetFromStart**:从一开始的明文内容的 inputBuffer 的相对位置 


* **inputBuffer**:将加密的明文内容的缓冲区 


* **inputBufferSize**:输入缓冲区的大小 （以字节为单位） 


* **outputBuffer**:加密的内容将复制到其中的缓冲区 


* **outputBufferSize**:输出缓冲区的大小 （以字节为单位） 


* **是最终版本**:如果输入的缓冲区或不包含最终明文字节



  
**返回**:加密的内容的实际大小 （以字节为单位）
  
### <a name="decryptbuffer-function"></a>DecryptBuffer 函数
解密缓冲区。

参数：  
* **offsetFromStart**:从加密的内容的最开始的 inputBuffer 的相对位置 


* **inputBuffer**:将解密的加密内容的缓冲区 


* **inputBufferSize**:输入缓冲区的大小 （以字节为单位） 


* **outputBuffer**:已解密的内容将复制到其中的缓冲区 


* **outputBufferSize**:输出缓冲区的大小 （以字节为单位） 


* **是最终版本**:如果输入的缓冲区或不包含最终加密的字节



  
**返回**:已解密内容的实际大小 （以字节为单位）
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength 函数
计算要使用此 [ProtectionHandler](class_mip_protectionhandler.md) 加密的内容的大小（以字节为单位）。

参数：  
* **unprotectedLength**:未受保护内容的大小 （以字节为单位） 


* **includesFinalBlock**:描述如果问题未受保护的内容或不包括最后一个块。 例如，在 CBC4k 加密模式下，非最终受保护块与未受保护块的大小相同，但最终受保护块比未受保护块大。



  
**返回**:受保护的内容的大小 （以字节为单位）
  
### <a name="getblocksize-function"></a>GetBlockSize 函数
获取此 [ProtectionHandler](class_mip_protectionhandler.md) 使用的密码模式的块大小（以字节为单位）。

  
**返回**:块大小 （以字节为单位）
  
### <a name="getrights-function"></a>GetRights 函数
获取向与此 [ProtectionHandler](class_mip_protectionhandler.md) 关联的用户/标识授予的权限。

  
**返回**:向用户授予的权限
  
### <a name="accesscheck-function"></a>访问权限检查函数
检查保护处理程序是否向用户授予指定访问权限。

参数：  
* **右**:若要检查的权限



  
**返回**:如果保护处理程序权限或不授予用户对指定的访问
  
### <a name="getissuedto-function"></a>GetIssuedTo 函数
获取与保护处理程序关联的用户。

  
**返回**:与保护处理程序关联的用户
  
### <a name="getowner-function"></a>GetOwner 函数
获取内容所有者的电子邮件地址。

  
**返回**:内容所有者的电子邮件地址
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner 函数
获取当前用户是否为内容所有者的指示。

  
**返回**:如果当前用户是否是内容所有者
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
获取保护详细信息。

  
**返回**:保护详细信息
  
### <a name="getcontentid-function"></a>GetContentId 函数
获取文档/内容的唯一标识符。

  
**返回**:唯一内容标识符
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms 函数
获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。

  
**返回**:如果保护处理程序使用的是弃用的加密算法或不
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed 函数
获取保护处理程序是否向用户授予“已审核的提取”权限的指示。

  
**返回**:如果保护处理程序授予用户审核提取权限或不
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 函数
将 [ProtectionHandler](class_mip_protectionhandler.md) 序列化为发布许可证 (PL)

  
**返回**:序列化的发布许可证
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
获取保护信息。

  
**返回**:序列化的保护信息