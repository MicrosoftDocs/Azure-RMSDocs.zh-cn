---
title: class mip::RemoveContentHeaderAction
description: 记录 mip::removecontentheaderaction 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3cc2fbdcfeae4e168e342a3c7af0edc971039db4
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173382"
---
# <a name="class-mipremovecontentheaderaction"></a>class mip::RemoveContentHeaderAction 
指定从文档中删除内容头的操作类。
  
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