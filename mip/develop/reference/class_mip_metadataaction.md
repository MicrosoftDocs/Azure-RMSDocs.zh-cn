---
title: class mip::MetadataAction
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: metadataaction 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 26a189d714001f4145ce328c163a052313923136
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885423"
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