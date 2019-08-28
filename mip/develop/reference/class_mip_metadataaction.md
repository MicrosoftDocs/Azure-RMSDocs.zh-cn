---
title: class mip::MetadataAction
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: metadataaction 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 9175fc9278f012b3f3247cab6a09650c55713ac3
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055912"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
将元数据信息添加到内容的 [Action](class_mip_action.md)。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetMetadataToRemove () const  |  获取应从内容中删除的元数据名称的列表。
public const std:: vector\<std::p air\<std:: string, std:: string\>\>& GetMetadataToAdd () const  |  获取应添加到内容的元数据名称/值对。
  
## <a name="members"></a>成员
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 函数
获取应从内容中删除的元数据名称的列表。

  
**返回**:要移除的字符串的向量。 在添加元数据之前应先删除元数据。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 函数
获取应添加到内容的元数据名称/值对。

  
**返回**:Const std:: vector < std::p air < std:: string, std:: string > > & 删除元数据应在添加元数据之前完成。