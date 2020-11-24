---
title: 类 MsgAttachmentData
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 msgattachmentdata：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c729b2907878aa383b058689c55072e53541a595
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565082"
---
# <a name="class-msgattachmentdata"></a>类 MsgAttachmentData 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector \<uint8_t\>& GetBytes ( # A2  |  获取作为二进制字节向量的附件。
public std：： shared_ptr \<Stream\> system.resources.resourcemanager.getstream ( # A1 const  |  获取作为二进制流的附件。
public const std::string& GetName() const  |  获取字符串形式的附件名称。
public const std：： string& GetLongName ( # A2 const  |  以字符串形式获取附件的长名称。
public const std::string& GetPath() const  |  获取字符串形式的附件路径名称。 如果路径不为空，则引用附件。
public const std：： string& GetLongPath ( # A2 const  |  获取附件的长路径名称作为字符串。 如果路径不为空，则引用附件。
  
## <a name="members"></a>成员
  
### <a name="getbytes-function"></a>GetBytes 函数
获取作为二进制字节向量的附件。
  
### <a name="getstream-function"></a>System.resources.resourcemanager.getstream 函数
获取作为二进制流的附件。
  
### <a name="getname-function"></a>GetName 函数
获取字符串形式的附件名称。
  
### <a name="getlongname-function"></a>GetLongName 函数
以字符串形式获取附件的长名称。
  
### <a name="getpath-function"></a>GetPath 函数
获取字符串形式的附件路径名称。 如果路径不为空，则引用附件。
  
### <a name="getlongpath-function"></a>GetLongPath 函数
获取附件的长路径名称作为字符串。 如果路径不为空，则引用附件。