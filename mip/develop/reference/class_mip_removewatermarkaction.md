---
title: 类 RemoveWatermarkAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 removewatermarkaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 2c140461d0cf8b01b25893900191563b1fe3c8b0
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213158"
---
# <a name="class-removewatermarkaction"></a>类 RemoveWatermarkAction 
指定从文档中删除水印的操作类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector \<std::string\>& GetUIElementNames ( # A2  |  获取应用于查找应删除的 UI 元素的名称列表。
public ActionType GetType() const  |  获取操作类型。
  
## <a name="members"></a>成员
  
### <a name="getuielementnames-function"></a>GetUIElementNames 函数
获取应用于查找应删除的 UI 元素的名称列表。

  
**返回结果**：UI 元素名称列表。
  
### <a name="gettype-function"></a>GetType 函数
获取操作类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。