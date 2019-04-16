---
title: class mip::RemoveContentFooterAction
description: 记录 mip::removecontentfooteraction 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 14afd4688c13f419ab3019e9c268ba7d355121c8
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574255"
---
# <a name="class-mipremovecontentfooteraction"></a>class mip::RemoveContentFooterAction 
指定从文档中删除内容脚注的操作类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetUIElementNames()  |  获取应用于查找应删除的 UI 元素的名称列表。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。

## <a name="members"></a>成員
  
### <a name="getuielementnames-function"></a>GetUIElementNames 函数
获取应用于查找应删除的 UI 元素的名称列表。

  
**返回**:Ui 元素名称的列表。

### <a name="gettype-function"></a>GetType 函数    
获取[操作](class_mip_action.md)类型。  

**返回**:ActionType：此基类可以转换成的派生操作类型。