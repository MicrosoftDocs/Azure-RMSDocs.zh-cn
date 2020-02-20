---
title: class mip::MetadataAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： metadataaction 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 85d2742d5602dc2e36d9370a33fd04050fbeee9d
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487712"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
向内容添加元数据信息的操作。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<std：： string\>& GetMetadataToRemove （） const  |  获取应从内容中删除的元数据名称的列表。
public const std：： vector\<std：:p air\<std：： string，std：： string\>\>& GetMetadataToAdd （） const  |  获取应添加到内容的元数据名称/值对。
  
## <a name="members"></a>Members
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 函数
获取应从内容中删除的元数据名称的列表。

  
**返回结果**：要删除的字符串矢量。 在添加元数据之前应先删除元数据。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 函数
获取应添加到内容的元数据名称/值对。

  
**返回结果**：Const std::vector<std::pair<std::string, std::string>>& 在添加元数据之前应先删除元数据。