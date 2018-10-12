---
title: class mip ProtectByTemplateAction
description: class mip ProtectByTemplateAction 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: cb5f42b25e6f499bc09f3f460ec4a253627b45a5
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445455"
---
# <a name="class-mipprotectbytemplateaction"></a>class mip::ProtectByTemplateAction 
指定向文档添加模板保护的操作类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const std::string& GetTemplateId() const  |  获取与操作关联的保护模板 ID。
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="gettemplateid"></a>GetTemplateId
获取与操作关联的保护模板 ID。

  
返回结果：保护模板 ID。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。