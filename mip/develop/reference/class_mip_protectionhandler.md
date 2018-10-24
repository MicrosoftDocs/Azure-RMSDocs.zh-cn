---
title: 类 mip ProtectionHandler
description: 类 mip ProtectionHandler 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6fbae05030f56d3c9e680e6de9c8177a11b2f1e2
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446747"
---
# <a name="class-mipprotectionhandler"></a>类 mip::ProtectionHandler 
管理特定保护配置的保护相关操作。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, int64_t contentStartPosition, int64_t contentSize)  |  创建允许加密/解密内容的受保护流。
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  加密缓冲区。
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  解密缓冲区。
 public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  计算要使用此 [ProtectionHandler](class_mip_protectionhandler.md) 加密的内容的大小（以字节为单位）。
 public int64_t GetBlockSize()  |  获取此 [ProtectionHandler](class_mip_protectionhandler.md) 使用的密码模式的块大小（以字节为单位）。
public std::vector<std::string> GetRights() const  |  获取向与此 [ProtectionHandler](class_mip_protectionhandler.md) 关联的用户/标识授予的权限。
 public bool AccessCheck(const std::string& right) const  |  检查保护处理程序是否向用户授予指定访问权限。
 public const std::string GetIssuedTo()  |  获取与保护处理程序关联的用户。
 public const std::string GetOwner()  |  获取内容所有者的电子邮件地址。
 public bool IsIssuedToOwner()  |  获取当前用户是否为内容所有者的指示。
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  获取保护详细信息。
 public const std::string GetContentId()  |  获取文档/内容的唯一标识符。
 public bool DoesUseDeprecatedAlgorithms()  |  获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。
 public bool IsAuditedExtractAllowed()  |  获取保护处理程序是否向用户授予“已审核的提取”权限的指示。
public const std::vector<uint8_t> GetSerializedPublishingLicense()  |  将 [ProtectionHandler](class_mip_protectionhandler.md) 序列化为发布许可证 (PL)
  
## <a name="members"></a>成員
  
### <a name="stream"></a>流
创建允许加密/解密内容的受保护流。

参数：  
* **backingStream**：从中执行读/写操作的回溯流 


* **contentStartPosition**：受保护内容在回溯流中的起始位置（以字节为单位） 


* **contentSize**：回溯流中受保护内容的大小（以字节为单位）



  
**返回结果**：受保护流
  
### <a name="encryptbuffer"></a>EncryptBuffer
加密缓冲区。

参数：  
* **offsetFromStart**：inputBuffer 与明文内容开头的相对位置 


* **inputBuffer**：将加密的明文内容所在的缓冲区 


* **inputBufferSize**：输入缓冲区大小（以字节为单位） 


* **outputBuffer**：将加密内容复制到的缓冲区 


* **outputBufferSize**：输出缓冲区大小（以字节为单位） 


* **isFinal**：输入缓冲区是否包含最终的明文字节



  
**返回结果**：加密内容的实际大小（以字节为单位）
  
### <a name="decryptbuffer"></a>DecryptBuffer
解密缓冲区。

参数：  
* **offsetFromStart**：inputBuffer 与加密内容开头的相对位置 


* **inputBuffer**：将解密的加密内容所在的缓冲区 


* **inputBufferSize**：输入缓冲区大小（以字节为单位） 


* **outputBuffer**：将解密内容复制到的缓冲区 


* **outputBufferSize**：输出缓冲区大小（以字节为单位） 


* **isFinal**：输入缓冲区是否包含最终的加密字节



  
**返回结果**：解密内容的实际大小（以字节为单位）
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
计算要使用此 [ProtectionHandler](class_mip_protectionhandler.md) 加密的内容的大小（以字节为单位）。

参数：  
* **unprotectedLength**：未受保护内容的大小（以字节为单位） 


* **includesFinalBlock**：描述相关的未受保护内容是否包含最终块。 例如，在 CBC4k 加密模式下，非最终受保护块与未受保护块的大小相同，但最终受保护块比未受保护块大。



  
**返回结果**：受保护内容的大小（以字节为单位）
  
### <a name="getblocksize"></a>GetBlockSize
获取此 [ProtectionHandler](class_mip_protectionhandler.md) 使用的密码模式的块大小（以字节为单位）。

  
**返回结果**：块大小（以字节为单位）
  
### <a name="getrights"></a>GetRights
获取向与此 [ProtectionHandler](class_mip_protectionhandler.md) 关联的用户/标识授予的权限。

  
**返回结果**：向用户授予的权限
  
### <a name="accesscheck"></a>AccessCheck
检查保护处理程序是否向用户授予指定访问权限。

参数：  
* **right**：检查权限



  
**返回结果**：指示保护处理程序是否向用户授予指定访问权限
  
### <a name="getissuedto"></a>GetIssuedTo
获取与保护处理程序关联的用户。

  
**返回结果**：与保护处理程序关联的用户
  
### <a name="getowner"></a>GetOwner
获取内容所有者的电子邮件地址。

  
**返回结果**：内容所有者的电子邮件地址
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
获取当前用户是否为内容所有者的指示。

  
**返回结果**：指示当前用户是否为内容所有者
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
获取保护详细信息。

  
**返回结果**：保护详细信息
  
### <a name="getcontentid"></a>GetContentId
获取文档/内容的唯一标识符。

  
**返回结果**：唯一内容标识符
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
获取保护处理程序是否使用已弃用的加密算法 (ECB) 来实现后向兼容性的指示。

  
**返回结果**：指示保护处理程序是否使用已弃用的加密算法
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
获取保护处理程序是否向用户授予“已审核的提取”权限的指示。

  
**返回结果**：指示保护处理程序是否向用户授予“已审核的提取”权限
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
将 [ProtectionHandler](class_mip_protectionhandler.md) 序列化为发布许可证 (PL)

  
**返回结果**：序列化的发布许可证