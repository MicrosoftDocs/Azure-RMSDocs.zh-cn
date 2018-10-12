---
title: class mip LabelingOptions
description: class mip LabelingOptions 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 1f3bdb5084dfa0d9121d1b1f7987161ba6d6ae6f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445676"
---
# <a name="class-miplabelingoptions"></a>class mip::LabelingOptions 
用于为 SetLabel/DeleteLabel 方法配置标记选项的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public LabelingOptions(AssignmentMethod method, ActionSource actionSource)  | _尚无记录。_
 public AssignmentMethod GetAssignmentMethod() const  | _尚无记录。_
 public ActionSource GetActionSource() const  | _尚无记录。_
 public bool IsDowngradeJustified() const  | _尚无记录。_
 public const std::string& GetJustificationMessage() const  | _尚无记录。_
public const std::vector<std::pair<std::string, std::string>>& GetExtendedProperties() const  | _尚无记录。_
 public void SetDowngradeJustification(bool isDowngradeJustified, const std::string& justificationMessage)  | _尚无记录。_
public void SetExtendedProperties(const std::vector<std::pair<std::string, std::string>>& extendedProperties)  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="labelingoptions"></a>LabelingOptions
_尚无记录。_

  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
_尚无记录。_

  
### <a name="getactionsource"></a>GetActionSource
_尚无记录。_

  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
_尚无记录。_

  
### <a name="getjustificationmessage"></a>GetJustificationMessage
_尚无记录。_

  
### <a name="getextendedproperties"></a>GetExtendedProperties
_尚无记录。_

  
### <a name="setdowngradejustification"></a>SetDowngradeJustification
_尚无记录。_

  
### <a name="setextendedproperties"></a>SetExtendedProperties
_尚无记录。_
