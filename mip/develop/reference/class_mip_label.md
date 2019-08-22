---
title: class mip::Label
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: label 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 3d746c1f271d75c160ca721ebe6f0fef0f15bd5e
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884038"
---
# <a name="class-miplabel"></a>class mip::Label 
单个 Microsoft 信息保护标签的抽象。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取标签 ID。
public const std::string& GetName() const  |  获取标签名称。
public const std::string& GetDescription() const  |  获取标签说明。
public const std::string& GetColor() const  |  获取应显示的标签颜色。
public int GetSensitivity() const  |  获取标签的敏感度。
public const std::string& GetTooltip() const  |  获取标签的工具提示说明。
public bool IsActive() const  |  获取一个布尔值，指示标签是否处于活动状态。
public std:: weak_ptr\<Label\> GetParent () const  |  获取父标签。
public const std:: vector\<std:: shared_ptr\<Label\>\>& GetChildren () const  |  获取当前标签的子标签。
public const std:: vector\<std::p air\<std:: string, std:: string\>\>& GetCustomSettings () const  |  获取标签的自定义设置。
public ActionSource GetActionSource() const  |  获取标签的操作源。
  
## <a name="members"></a>成员
  
### <a name="getid-function"></a>GetId 函数
获取标签 ID。

  
**返回**:标签 ID。
  
### <a name="getname-function"></a>GetName 函数
获取标签名称。

  
**返回**:标签名称。
  
### <a name="getdescription-function"></a>GetDescription 函数
获取标签说明。

  
**返回**:标签说明。
  
### <a name="getcolor-function"></a>GetColor 函数
获取应显示的标签颜色。

  
**返回**:字符串格式的颜色值。 “#RRGGBB”，其中每个 RR、GG、BB 都是十六进制 0-f。
  
### <a name="getsensitivity-function"></a>GetSensitivity 函数
获取标签的敏感度。

  
**返回**:一个数值。 值越大表示敏感度越高。
  
### <a name="gettooltip-function"></a>GetTooltip 函数
获取标签的工具提示说明。

  
**返回**:工具提示字符串。
  
### <a name="isactive-function"></a>IsActive 函数
获取一个布尔值，指示标签是否处于活动状态。
仅活动标签才能应用。 不能应用处于非活动状态的标签，并且仅用于显示目的。 

  
**返回**:如果标签处于活动状态, 则为 True; 否则为 false。
  
### <a name="getparent-function"></a>GetParent 函数
获取父标签。

  
**返回**:指向父标签的弱指针 (如果存在), 否则为空指针。
  
### <a name="getchildren-function"></a>GetChildren 函数
获取当前标签的子标签。

  
**返回**:指向标签的共享指针的矢量。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取标签的自定义设置。

  
**返回**:表示自定义设置的键值对的向量。
  
### <a name="getactionsource-function"></a>GetActionSource 函数
获取标签的操作源。

  
**返回**:[操作](class_mip_action.md)源