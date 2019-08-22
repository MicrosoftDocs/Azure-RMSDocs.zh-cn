---
title: 类 mip::ProtectionHandler
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionhandler 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 306748121e34122a5623aea3e1d7ff4ba7f14787
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883411"
---
# <a name="class-mipprotectionhandler"></a>类 mip::ProtectionHandler 
管理特定保护配置的保护相关操作。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<stream\> CreateProtectedStream (const std:: shared_ptr\<stream\>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  创建允许加密/解密内容的受保护流。
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  加密缓冲区。
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  解密缓冲区。
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  计算要使用此 [ProtectionHandler](class_mip_protectionhandler.md) 加密的内容的大小（以字节为单位）。
public int64_t GetBlockSize()  |  获取此 [ProtectionHandler](class_mip_protectionhandler.md) 使用的密码模式的块大小（以字节为单位）。
public std:: vector\<std:: string\> GetRights () const  |  获取向与此 [ProtectionHandler](class_mip_protectionhandler.md) 关联的用户/标识授予的权限。
public bool AccessCheck(const std::string& right) const  |  检查保护处理程序是否向用户授予指定访问权限。
public const std::string GetIssuedTo()  |  获取与保护处理程序关联的用户。
public const std::string GetOwner()  |  获取内容所有者的电子邮件地址。
public bool IsIssuedToOwner()  |  获取当前用户是否为内容所有者的指示。
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor ()  |  获取保护详细信息。
public const std::string GetContentId()  |  获取文档/内容的唯一标识符。
public bool DoesUseDeprecatedAlgorithms()  |  获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。
public bool IsAuditedExtractAllowed()  |  获取保护处理程序是否向用户授予“已审核的提取”权限的指示。
public const std:: vector\<uint8_t\> GetSerializedPublishingLicense ()  |  将 [ProtectionHandler](class_mip_protectionhandler.md) 序列化为发布许可证 (PL)
  
## <a name="members"></a>成员
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream 函数
创建允许加密/解密内容的受保护流。

参数：  
* **backingStream**:要从其读取/写入的支持流 


* **contentStartPosition**:受保护内容开始的后备流中的开始位置 (以字节为单位) 


* **contentSize**:受保护内容在支持流中的大小 (以字节为单位)



  
**返回**:受保护的流
  
### <a name="encryptbuffer-function"></a>EncryptBuffer 函数
加密缓冲区。

参数：  
* **offsetFromStart**:从明文内容的开头开始 inputBuffer 的相对位置 


* **inputBuffer**:要加密的明文内容的缓冲区 


* **inputBufferSize**:输入缓冲区的大小 (以字节为单位) 


* **outputBuffer**:要将加密内容复制到其中的缓冲区 


* **outputBufferSize**:输出缓冲区的大小 (以字节为单位) 


* **isFinal**:如果输入缓冲区包含最终明文字节



  
**返回**:加密内容的实际大小 (以字节为单位)
  
### <a name="decryptbuffer-function"></a>DecryptBuffer 函数
解密缓冲区。

参数：  
* **offsetFromStart**:从加密内容的最开始位置 inputBuffer 的相对位置 


* **inputBuffer**:要解密的加密内容的缓冲区 


* **inputBufferSize**:输入缓冲区的大小 (以字节为单位) 


* **outputBuffer**:解密内容将复制到的缓冲区 


* **outputBufferSize**:输出缓冲区的大小 (以字节为单位) 


* **isFinal**:如果输入缓冲区包含最终加密字节



  
**返回**:解密内容的实际大小 (以字节为单位)
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength 函数
计算要使用此 [ProtectionHandler](class_mip_protectionhandler.md) 加密的内容的大小（以字节为单位）。

参数：  
* **unprotectedLength**:未保护内容的大小 (以字节为单位) 


* **includesFinalBlock**:介绍相关的未受保护内容是否包括最终块。 例如，在 CBC4k 加密模式下，非最终受保护块与未受保护块的大小相同，但最终受保护块比未受保护块大。



  
**返回**:受保护内容的大小 (以字节为单位)
  
### <a name="getblocksize-function"></a>GetBlockSize 函数
获取此 [ProtectionHandler](class_mip_protectionhandler.md) 使用的密码模式的块大小（以字节为单位）。

  
**返回**:块大小 (以字节为单位)
  
### <a name="getrights-function"></a>GetRights 函数
获取向与此 [ProtectionHandler](class_mip_protectionhandler.md) 关联的用户/标识授予的权限。

  
**返回**:向用户授予的权限
  
### <a name="accesscheck-function"></a>AccessCheck 函数
检查保护处理程序是否向用户授予指定访问权限。

参数：  
* **right**:检查权限



  
**返回**:如果保护处理程序向用户授予对指定权限的访问权限
  
### <a name="getissuedto-function"></a>GetIssuedTo 函数
获取与保护处理程序关联的用户。

  
**返回**:与保护处理程序关联的用户
  
### <a name="getowner-function"></a>GetOwner 函数
获取内容所有者的电子邮件地址。

  
**返回**:内容所有者的电子邮件地址
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner 函数
获取当前用户是否为内容所有者的指示。

  
**返回**:当前用户是否为内容所有者
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
获取保护详细信息。

  
**返回**:保护详细信息
  
### <a name="getcontentid-function"></a>GetContentId 函数
获取文档/内容的唯一标识符。

  
**返回**:唯一内容标识符
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms 函数
获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。

  
**返回**:如果保护处理程序使用不推荐使用的加密算法
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed 函数
获取保护处理程序是否向用户授予“已审核的提取”权限的指示。

  
**返回**:如果保护处理程序向用户授予 "审核提取" 权限
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 函数
将 [ProtectionHandler](class_mip_protectionhandler.md) 序列化为发布许可证 (PL)

  
**返回**:序列化发布许可证