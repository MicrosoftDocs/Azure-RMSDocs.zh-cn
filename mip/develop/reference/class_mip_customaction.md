---
title: class mip::CustomAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： customaction 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 450ae0e455f74c6cb9b1f6b0b6d8aded9b30b2bd
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558907"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
CustomAction 是一个通用操作类，它捕获操作的所有子属性作为属性包。 调用方负责理解操作的含义。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  获取操作名称。
public const std：： vector\<std：:p air\<std：： string，std：： string\>\>& GetProperties （） const  |  获取属性键值对列表。
  
## <a name="members"></a>成員
  
### <a name="getname-function"></a>GetName 函数
获取操作名称。

  
返回结果操作名称（如果存在），否则为空字符串。
  
### <a name="getproperties-function"></a>GetProperties 函数
获取属性键值对列表。

  
**返回结果**：键值对列表。