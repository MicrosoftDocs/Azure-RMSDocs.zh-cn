---
title: class mip RemoveWatermarkAction
description: class mip RemoveWatermarkAction 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 8f0b0a06088ed8a48e358c4ff9f005abf50db38f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445319"
---
# <a name="class-mipremovewatermarkaction"></a>class mip::RemoveWatermarkAction 
指定从文档中删除水印的操作类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetUIElementNames()  |  获取应用于查找应删除的 UI 元素的名称列表。
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getuielementnames"></a>GetUIElementNames
获取应用于查找应删除的 UI 元素的名称列表。

  
**返回结果**：UI 元素名称列表。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。