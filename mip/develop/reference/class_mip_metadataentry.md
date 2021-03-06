---
title: 类 MetadataEntry
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 metadataentry：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: dd758d49d0c207fe5e4c5eeb04bb63ba91174fcc
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215181"
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