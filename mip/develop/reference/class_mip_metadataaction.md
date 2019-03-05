---
title: class mip::MetadataAction
description: 记录 mip::metadataaction 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: c180072eec94b2f71471c10b4344d65321ef49c6
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332406"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
将元数据信息添加到内容的 [Action](class_mip_action.md)。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetMetadataToRemove() 常量  |  获取应从内容中删除的元数据名称的列表。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetMetadataToAdd() 常量  |  获取应添加到内容的元数据名称/值对。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 函数
获取应从内容中删除的元数据名称的列表。

  
**返回**:要删除的字符串矢量。 在添加元数据之前应先删除元数据。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 函数
获取应添加到内容的元数据名称/值对。

  
**返回**:Const std:: vector < std:: pair < std:: string、 std:: string >> 和删除元数据应在添加元数据之前完成。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
