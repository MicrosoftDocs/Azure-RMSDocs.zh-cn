---
title: class mip::ProtectByTemplateAction
description: 记录 mip::protectbytemplateaction 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 9c7114bcceceef537675ca04499cdb1710456b82
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252361"
---
# <a name="class-mipprotectbytemplateaction"></a>class mip::ProtectByTemplateAction 
指定向文档添加模板保护的操作类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetTemplateId() const  |  获取与操作关联的保护模板 ID。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="gettemplateid-function"></a>GetTemplateId 函数
获取与操作关联的保护模板 ID。

  
**返回**:保护模板 id。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
