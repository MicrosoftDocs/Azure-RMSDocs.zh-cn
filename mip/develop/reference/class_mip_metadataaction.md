---
title: class mip::MetadataAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： metadataaction 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 405bb153527cb3fde346203d3b11c09c97110f12
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558679"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
向内容添加元数据信息的操作。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<std：： string\>& GetMetadataToRemove （） const  |  获取应从内容中删除的元数据名称的列表。
public const std：： vector\<std：:p air\<std：： string，std：： string\>\>& GetMetadataToAdd （） const  |  获取应添加到内容的元数据名称/值对。
  
## <a name="members"></a>成員
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 函数
获取应从内容中删除的元数据名称的列表。

  
**返回结果**：要删除的字符串矢量。 在添加元数据之前应先删除元数据。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 函数
获取应添加到内容的元数据名称/值对。

  
**返回结果**：Const std::vector<std::pair<std::string, std::string>>& 在添加元数据之前应先删除元数据。