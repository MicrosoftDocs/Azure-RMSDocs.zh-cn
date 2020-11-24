---
title: 类 MetadataAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 metadataaction：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 082a4332482bce35a436b70d4fa86ee7320d6f52
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565091"
---
# <a name="class-metadataaction"></a>类 MetadataAction 
将元数据信息添加到内容的 Action。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector \<std::string\>& GetMetadataToRemove ( # A2 const  |  获取应从内容中删除的元数据名称的列表。
public const std：： vector \<MetadataEntry\>& GetMetadataToAdd ( # A2 const  |  获取应添加到内容的元数据名称/值对。
  
## <a name="members"></a>成员
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 函数
获取应从内容中删除的元数据名称的列表。

  
**返回结果**：要删除的字符串矢量。 在添加元数据之前应先删除元数据。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 函数
获取应添加到内容的元数据名称/值对。

  
**返回**： Const std：： vector <MetadataEntry>& 在添加元数据之前应完成删除元数据。