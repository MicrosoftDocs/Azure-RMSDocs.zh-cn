---
title: 类 mip::RecommendLabelAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： recommendlabelaction 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 2038c8eb1a6baa52dc696be998853ca6774edccf
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489531"
---
# <a name="class-miprecommendlabelaction"></a>类 mip::RecommendLabelAction 
建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： shared_ptr\<Label\>& GetLabel （） const  |  获取建议的标签。
public const std：： vector\<std：： string\>& GetClassificationIds （） const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>GetLabel 函数
获取建议的标签。

  
**返回**：标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**： Const std：： vector < std：： string > & 导致此标签出现的分类 id 的列表。