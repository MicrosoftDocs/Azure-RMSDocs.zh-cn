---
title: class mip::RemoveWatermarkAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： removewatermarkaction 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c2e6eb141d213a9ca19a345a4dac68120200abf8
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489480"
---
# <a name="class-mipremovewatermarkaction"></a>class mip::RemoveWatermarkAction 
指定从文档中删除水印的操作类。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<std：： string\>& GetUIElementNames （）  |  获取应用于查找应删除的 UI 元素的名称列表。
public ActionType GetType() const  |  获取操作的类型。
  
## <a name="members"></a>Members
  
### <a name="getuielementnames-function"></a>GetUIElementNames 函数
获取应用于查找应删除的 UI 元素的名称列表。

  
**返回结果**：UI 元素名称列表。
  
### <a name="gettype-function"></a>GetType 函数
获取操作的类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。