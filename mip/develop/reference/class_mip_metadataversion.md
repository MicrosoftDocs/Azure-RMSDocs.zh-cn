---
title: 类 MetadataVersion
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 metadataversion：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 05154ec7777fb94478c2065f6e637dea47d58d28
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565087"
---
# <a name="class-metadataversion"></a>类 MetadataVersion 
MetadataVersion 的接口。 MetadataVersion 确定哪些元数据是活动的，以及如何对其进行处理。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public MetadataVersion (uint32_t 版本，MetadataVersionFormat 标志)   |  MetadataVersion 构造函数。
public virtual uint32_t GetValue ( # A1 const  |  获取数值版本。
public virtual bool Enum.hasflag\ (MetadataVersionFormat 标志) const  |  获取是否设置特定标志。
public virtual MetadataVersionFormat GetFlags ( # A1 const  |  获取用于定义给定版本如何处理元数据的标志。
  
## <a name="members"></a>成员
  
### <a name="metadataversion-function"></a>MetadataVersion 函数
MetadataVersion 构造函数。

参数：  
* **版本**：要用于元数据操作的数字版本 


* **flags**：用于指定如何使用版本来计算元数据操作的标志


  
### <a name="getvalue-function"></a>GetValue 函数
获取数值版本。

  
**返回**：数值版本。
  
### <a name="hasflag-function"></a>Enum.hasflag\ 函数
获取是否设置特定标志。

  
**返回**：如果设置了标志，则为 True。
  
### <a name="getflags-function"></a>GetFlags 函数
获取用于定义给定版本如何处理元数据的标志。

  
**返回**：指定如何处理元数据的标志。