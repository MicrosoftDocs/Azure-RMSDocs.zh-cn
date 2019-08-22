---
title: 类 mip::D ocumentState
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::d ocumentstate 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 44fc6faf6b92e9f31dad96185e18b50be3a97e32
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69892896"
---
# <a name="class-mipdocumentstate"></a>类 mip::D ocumentState 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  获取描述文档的内容说明。 文件示例: [path\filename] 电子邮件示例: [Subject: Sender]。
public virtual DataState GetDataState () const  |  获取应用程序与之交互时内容的状态。
public std:: vector\<std::p 风\<std:: string、std:: string\> \> GetContentMetadata (const std:: vector\<std:: string\>& 名称、const std:: vector\<std:: string\>& namePrefixes) const  |  从内容中获取元数据项。
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  获取保护描述符。
public ContentFormat GetContentFormat() const  |  获取内容格式。
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: vector\<std:: shared_ptr\<ClassificationRequest\> \> &) const  |  返回分类结果的映射。
public virtual std:: map\<std:: string, std:: string\> GetAuditMetadata () const  |  返回应用程序特定的审核键值对的映射。
  
## <a name="members"></a>成员
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 函数
获取描述文档的内容说明。 文件示例: [path\filename] 电子邮件示例: [Subject: Sender]。

  
**返回**:要应用于内容的内容说明。
审核功能将此值用作内容的用户可读说明
  
### <a name="getdatastate-function"></a>GetDataState 函数
获取应用程序与之交互时内容的状态。

  
**返回**:内容数据的状态
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata 函数
从内容中获取元数据项。

  
**返回**:应用于内容的元数据。 每个元数据项都是名称和值对。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 函数
获取保护描述符。

  
**返回**:保护描述符
  
### <a name="getcontentformat-function"></a>GetContentFormat 函数
获取内容格式。

  
**返回**:默认、电子邮件 
  
**另请参阅**: [Mip:: ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 函数
返回分类结果的映射。

参数：  
* **classificationIds**: 分类 id 列表。 



  
**返回**:分类结果的列表。 如果未执行分类循环, 则返回 nullptr。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 函数
返回应用程序特定的审核键值对的映射。

  
**返回**:特定于应用程序的审核元数据注册密钥: 值对发送程序的列表:发件人收件人的电子邮件 Id:表示电子邮件 LastModifiedBy 的收件人的 JSON 数组:上次修改内容 LastModifiedDate 的用户的电子邮件 Id:上次修改内容的日期