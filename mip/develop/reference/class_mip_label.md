---
title: class mip Label
description: class mip Label 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 2a80748430df83a16a4d5ee716344d17ce7deee4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446271"
---
# <a name="class-miplabel"></a>class mip::Label 
单个 Microsoft 信息保护标签的抽象。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const std::string& GetId() const  |  获取标签 ID。
 public const std::string& GetName() const  |  获取标签名称。
 public const std::string& GetDescription() const  |  获取标签说明。
 public const std::string& GetColor() const  |  获取应显示的标签颜色。
 public int GetSensitivity() const  |  获取标签的敏感度。
 public const std::string& GetTooltip() const  |  获取标签的工具提示说明。
 public bool IsActive() const  |  获取一个布尔值，指示标签是否处于活动状态。
public std::weak_ptr<Label> GetParent() const  |  获取父标签。
public const std::vector<std::shared_ptr<Label>>& GetChildren() const  |  获取当前标签的子标签。
  
## <a name="members"></a>成員
  
### <a name="getid"></a>GetId
获取标签 ID。

  
返回结果：标签 ID。
  
### <a name="getname"></a>GetName
获取标签名称。

  
**返回结果**：标签名称。
  
### <a name="getdescription"></a>GetDescription
获取标签说明。

  
**返回结果**：标签说明。
  
### <a name="getcolor"></a>GetColor
获取应显示的标签颜色。

  
**返回结果**：字符串格式的颜色值。 “#RRGGBB”，其中每个 RR、GG、BB 都是十六进制 0-f。
  
### <a name="getsensitivity"></a>GetSensitivity
获取标签的敏感度。

  
**返回结果**：数字值。 值越大表示敏感度越高。
  
### <a name="gettooltip"></a>GetTooltip
获取标签的工具提示说明。

  
**返回结果**：一个工具提示字符串。
  
### <a name="isactive"></a>IsActive
获取一个布尔值，指示标签是否处于活动状态。
仅活动标签才能应用。 不能应用处于非活动状态的标签，并且仅用于显示目的。 

  
**返回结果**：如果标签处于活动状态，则为 true，否则为 false。
  
### <a name="label"></a>Label
获取父标签。

  
**返回结果**：如果存在，则返回指向父标签的弱指针，否则返回空指针。
  
### <a name="label"></a>Label
获取当前标签的子标签。

  
**返回结果**：一个指向标签的共享指针的矢量。