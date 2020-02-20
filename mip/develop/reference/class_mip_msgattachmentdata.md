---
title: 类 mip：： MsgAttachmentData
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： msgattachmentdata 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f9f47ca1503c912840fe1ed43542b5a4b4f2d0ec
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487661"
---
# <a name="class-mipmsgattachmentdata"></a>类 mip：： MsgAttachmentData 
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<uint8_t\>& GetBytes （）  |  获取作为二进制字节向量的附件。
public std：： shared_ptr\<Stream\> System.resources.resourcemanager.getstream （） const  |  获取作为二进制流的附件。
public const std::string& GetName() const  |  获取字符串形式的附件名称。
public const std：： string & GetLongName （） const  |  以字符串形式获取附件的长名称。
public const std::string& GetPath() const  |  获取字符串形式的附件路径名称。 如果路径不为空，则引用附件。
public const std：： string & GetLongPath （） const  |  获取附件的长路径名称作为字符串。 如果路径不为空，则引用附件。
  
## <a name="members"></a>Members
  
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