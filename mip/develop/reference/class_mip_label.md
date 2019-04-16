---
title: class mip::Label
description: '记录 mip:: label 类的 Microsoft 信息保护 (MIP) SDK。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: e4f8246cbc0f6f1f897de4710e155e0099b71244
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574102"
---
# <a name="class-miplabel"></a>class mip::Label 
单个 Microsoft 信息保护标签的抽象。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  获取标签 ID。
public const std::string& GetName() const  |  获取标签名称。
public const std::string& GetDescription() const  |  获取标签说明。
public const std::string& GetColor() const  |  获取应显示的标签颜色。
public int GetSensitivity() const  |  获取标签的敏感度。
public const std::string& GetTooltip() const  |  获取标签的工具提示说明。
public bool IsActive() const  |  获取一个布尔值，指示标签是否处于活动状态。
公共 std::weak_ptr\<标签\>GetParent() 常量  |  获取父标签。
public const std:: vector\<std:: shared_ptr\<标签\>\>& GetChildren() 常量  |  获取当前标签的子标签。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetCustomSettings() 常量  |  获取标签的自定义设置。
  
## <a name="members"></a>成員
  
### <a name="getid-function"></a>GetId 函数
获取标签 ID。

  
**返回**:标签 id。
  
### <a name="getname-function"></a>GetName 函数
获取标签名称。

  
**返回**:标签名称。
  
### <a name="getdescription-function"></a>GetDescription 函数
获取标签说明。

  
**返回**:标签说明。
  
### <a name="getcolor-function"></a>GetColor 函数
获取应显示的标签颜色。

  
**返回**:颜色值的字符串格式。 “#RRGGBB”，其中每个 RR、GG、BB 都是十六进制 0-f。
  
### <a name="getsensitivity-function"></a>GetSensitivity 函数
获取标签的敏感度。

  
**返回**:一个数值。 值越大表示敏感度越高。
  
### <a name="gettooltip-function"></a>GetTooltip 函数
获取标签的工具提示说明。

  
**返回**:一个工具提示的字符串。
  
### <a name="isactive-function"></a>IsActive 函数
获取一个布尔值，指示标签是否处于活动状态。
仅活动标签才能应用。 不能应用处于非活动状态的标签，并且仅用于显示目的。 

  
**返回**:如果标签处于活动状态，否则为 false，则为 true。
  
### <a name="getparent-function"></a>GetParent 函数
获取父标签。

  
**返回**:指向父级的弱指针标签如果存在，否则返回空指针。
  
### <a name="getchildren-function"></a>GetChildren 函数
获取当前标签的子标签。

  
**返回**:为标签的共享指针的向量。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取标签的自定义设置。

  
**返回**:表示自定义设置的键/值对的向量。