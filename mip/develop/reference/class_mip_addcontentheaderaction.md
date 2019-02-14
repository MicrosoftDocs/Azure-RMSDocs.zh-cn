---
title: class mip::AddContentHeaderAction
description: 记录 mip::addcontentheaderaction 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ab4ce12c9a11c0e2319bcf2b337b6a6f0f7f9f0e
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256764"
---
# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
指定添加内容头的操作类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  用来标记内容头元素的 API。
public const std::string& GetText() const  |  获取应添加到内容页眉的文本。
public const std::string& GetFontName() const  |  获取用于显示内容页眉的字体名称。
public int GetFontSize() const  |  获取用于显示内容页眉的字号。
public const std::string& GetFontColor() const  |  获取用于显示内容页眉的字体颜色。
public ContentMarkAlignment GetAlignment() const  |  获取内容页眉的对齐方式。
public int GetMargin() const  |  从底部获取标头的边距。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getuielementname-function"></a>GetUIElementName 函数
用来标记内容头元素的 API。

  
**返回**:保存内容标头应使用的用户界面元素的名称。 如果需要删除内容头，将在 [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) 中返回相同名称。
  
### <a name="gettext-function"></a>GetText 函数
获取应添加到内容页眉的文本。

  
**返回**:内容标头文本。
  
### <a name="getfontname-function"></a>GetFontName 函数
获取用于显示内容页眉的字体名称。

  
**返回**:字体名称。 如果策略未进行任何设置，默认值为 Calibri。
  
### <a name="getfontsize-function"></a>GetFontSize 函数
获取用于显示内容页眉的字号。

  
**返回**:一个整数形式的字体大小。
  
### <a name="getfontcolor-function"></a>GetFontColor 函数
获取用于显示内容页眉的字体颜色。

  
**返回**:以字符串形式的字体颜色 (例如，#000000")。
  
### <a name="getalignment-function"></a>GetAlignment 函数
获取内容页眉的对齐方式。

  
**返回**:ContentMarkAlignment 枚举器：左侧 |右 |中心。 
  
**另请参阅**:[ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin 函数
从底部获取标头的边距。

  
**返回**:从文档 （例如，10 毫米） 的下边距。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
