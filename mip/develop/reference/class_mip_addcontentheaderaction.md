---
title: 类 AddContentHeaderAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 addcontentheaderaction：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 090bf4e1ad70238d6023a914fba4786a97a25a0d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565245"
---
# <a name="class-addcontentheaderaction"></a>类 AddContentHeaderAction 
指定添加内容头的操作类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  用来标记内容头元素的 API。
public const std::string& GetText() const  |  获取应添加到内容页眉的文本。
public const std::string& GetFontName() const  |  获取用于显示内容页眉的字体名称。
public int GetFontSize() const  |  获取用于显示内容页眉的字号。
public const std::string& GetFontColor() const  |  获取用于显示内容页眉的字体颜色。
public ContentMarkAlignment GetAlignment() const  |  获取内容页眉的对齐方式。
public int GetMargin() const  |  从底部获取标头的边距。
  
## <a name="members"></a>成员
  
### <a name="getuielementname-function"></a>GetUIElementName 函数
用来标记内容头元素的 API。

  
**返回结果**：应用于保存内容头的 UI 元素的名称。 如果需要删除内容头，将在 RemoveContentHeaderAction 中返回相同名称。
  
### <a name="gettext-function"></a>GetText 函数
获取应添加到内容页眉的文本。

  
**返回结果**：内容头文本。
  
### <a name="getfontname-function"></a>GetFontName 函数
获取用于显示内容页眉的字体名称。

  
**返回结果**：字体名称。 如果策略未进行任何设置，默认值为 Calibri。
  
### <a name="getfontsize-function"></a>GetFontSize 函数
获取用于显示内容页眉的字号。

  
**返回结果**：整数形式的字体大小。
  
### <a name="getfontcolor-function"></a>GetFontColor 函数
获取用于显示内容页眉的字体颜色。

  
**返回**：字体颜色作为字符串 (例如，#000000 ") 。
  
### <a name="getalignment-function"></a>GetAlignment 函数
获取内容页眉的对齐方式。

  
**返回**： ContentMarkAlignment 枚举器： LEFT |RIGHT |CENTER. 
  
另请参阅：ContentMarkAlignment
  
### <a name="getmargin-function"></a>GetMargin 函数
从底部获取标头的边距。

  
返回结果：文档底部的边距（例如 10 毫米）。