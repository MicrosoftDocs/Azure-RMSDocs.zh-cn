---
title: class mip::RemoveWatermarkAction
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: removewatermarkaction 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 9d67dc7839183e148cb2792482e1fc186858ce7e
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883137"
---
# <a name="class-mipremovewatermarkaction"></a>class mip::RemoveWatermarkAction 
指定从文档中删除水印的操作类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetUIElementNames ()  |  获取应用于查找应删除的 UI 元素的名称列表。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成员
  
### <a name="getuielementnames-function"></a>GetUIElementNames 函数
获取应用于查找应删除的 UI 元素的名称列表。

  
**返回**:Ui 元素名称的列表。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。