---
title: 类 mip MetadataAction
description: 类 mip MetadataAction 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 8f7480775a0226c7161c9ad770184e54427a5084
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444613"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
将元数据信息添加到内容的 [Action](class_mip_action.md)。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  获取应从内容中删除的元数据名称的列表。
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  获取应添加到内容的元数据名称/值对。
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
获取应从内容中删除的元数据名称的列表。

  
**返回结果**：要删除的字符串矢量。 在添加元数据之前应先删除元数据。
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
获取应添加到内容的元数据名称/值对。

  
**返回结果**：Const std::vector<std::pair<std::string, std::string>>& 在添加元数据之前应先删除元数据。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。