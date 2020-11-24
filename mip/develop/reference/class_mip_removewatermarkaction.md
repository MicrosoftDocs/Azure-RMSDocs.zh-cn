---
title: 类 RemoveWatermarkAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 removewatermarkaction：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: eee2617a7f3c1225d789a5d1f6124caa3d3deec0
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565280"
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