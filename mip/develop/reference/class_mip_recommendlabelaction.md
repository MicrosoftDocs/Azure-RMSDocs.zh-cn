---
title: 类 mip::RecommendLabelAction
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: recommendlabelaction 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: dd3d2d0ecf7b549105e1a6373a998e77d4e77de8
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883214"
---
# <a name="class-miprecommendlabelaction"></a>类 mip::RecommendLabelAction 
建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<Label\>& GetLabel () const  |  获取建议的标签。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
获取建议的标签。

  
**返回**:标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**:Const std:: vector < std:: string > & 导致此标签出现的分类 Id 的列表。