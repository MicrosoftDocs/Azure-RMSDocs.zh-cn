---
title: 类 MetadataEntry
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 metadataentry：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 026fecc8da2008a2798ca8bc44951bc97ec5455a
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565093"
---
# <a name="class-metadataentry"></a>类 MetadataEntry 
元数据项的抽象类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public MetadataEntry (const std：： string& key，const std：： string& 值，uint32_t 版本)   |  构造函数 MetadataEntry 抽象。
public MetadataEntry (const std：： string& key，const std：： string& 值，const MetadataVersion& 版本)   |  构造函数 MetadataEntry 抽象。
public MetadataEntry (const std：： string& key，const std：： string& 值)   |  构造函数对于 MetadataEntry 抽象，版本设置为默认值0。
public const std：： string& GetKey ( # A2 const  |  获取元数据输入密钥。
public const std：： string& GetValue ( # A2 const  |  获取元数据输入值。
public MetadataVersion GetVersion ( # A1 const  |  获取元数据条目版本。
  
## <a name="members"></a>成员
  
### <a name="metadataentry-function"></a>MetadataEntry 函数
构造函数 MetadataEntry 抽象。

参数：  
* **key**： metadata 关键字条目。 


* **值**：元数据值输入 


* **版本**：元数据版本值


  
### <a name="metadataentry-function"></a>MetadataEntry 函数
构造函数 MetadataEntry 抽象。

参数：  
* **key**： metadata 关键字条目。 


* **值**：元数据值输入 


* **版本**：元数据版本值


  
### <a name="metadataentry-function"></a>MetadataEntry 函数
构造函数对于 MetadataEntry 抽象，版本设置为默认值0。

参数：  
* **key**： metadata 关键字条目。 


* **值**：元数据值输入


  
### <a name="getkey-function"></a>GetKey 函数
获取元数据输入密钥。

  
**返回**： Metadata 输入密钥。
  
### <a name="getvalue-function"></a>GetValue 函数
获取元数据输入值。

  
**返回**： Metadata 输入值。
  
### <a name="getversion-function"></a>GetVersion 函数
获取元数据条目版本。

  
**返回**：元数据输入版本。