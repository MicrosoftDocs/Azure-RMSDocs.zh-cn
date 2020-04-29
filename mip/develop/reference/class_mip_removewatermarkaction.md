---
title: 类 RemoveWatermarkAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 removewatermarkaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 93c99a0bd66df636de618629ff25d7f37d0cddd8
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760508"
---
# <a name="class-removewatermarkaction"></a>类 RemoveWatermarkAction 
指定从文档中删除水印的操作类。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<std：： String\>& GetUIElementNames （）  |  获取应用于查找应删除的 UI 元素的名称列表。
public ActionType GetType() const  |  获取操作类型。
  
## <a name="members"></a>成员
  
### <a name="getuielementnames-function"></a>GetUIElementNames 函数
获取应用于查找应删除的 UI 元素的名称列表。

  
**返回结果**：UI 元素名称列表。
  
### <a name="gettype-function"></a>GetType 函数
获取操作类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。