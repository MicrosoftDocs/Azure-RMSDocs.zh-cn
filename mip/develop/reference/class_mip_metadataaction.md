---
title: 类 MetadataAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 metadataaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d36a97130fd8a04f8053b6c272cea9af050cb89c
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761616"
---
# <a name="class-metadataaction"></a>类 MetadataAction 
将元数据信息添加到内容的 Action。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<std：： String\>& GetMetadataToRemove （） const  |  获取应从内容中删除的元数据名称的列表。
public const std：： vector\<MetadataEntry\>& GetMetadataToAdd （） const  |  获取应添加到内容的元数据名称/值对。
  
## <a name="members"></a>成员
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 函数
获取应从内容中删除的元数据名称的列表。

  
**返回结果**：要删除的字符串矢量。 在添加元数据之前应先删除元数据。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 函数
获取应添加到内容的元数据名称/值对。

  
**返回**： Const std：： vector<MetadataEntry>& 在添加元数据之前应完成删除元数据。