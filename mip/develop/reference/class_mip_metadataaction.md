---
title: 类 MetadataAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 metadataaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 873901994f452f8a1b521653e9fc078ce1933883
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213668"
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