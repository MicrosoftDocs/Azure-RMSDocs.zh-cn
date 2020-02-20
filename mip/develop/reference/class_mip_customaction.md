---
title: class mip::CustomAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： customaction 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 9dfbd444684f68b954dd577c9ccdd208f55f9a89
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490189"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
CustomAction 是一个通用操作类，它捕获操作的所有子属性作为属性包。 调用方负责理解操作的含义。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  获取操作名称。
public const std：： vector\<std：:p air\<std：： string，std：： string\>\>& GetProperties （） const  |  获取属性键值对列表。
  
## <a name="members"></a>Members
  
### <a name="getname-function"></a>GetName 函数
获取操作名称。

  
返回结果操作名称（如果存在），否则为空字符串。
  
### <a name="getproperties-function"></a>GetProperties 函数
获取属性键值对列表。

  
**返回结果**：键值对列表。