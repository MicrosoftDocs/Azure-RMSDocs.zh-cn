---
title: class mip::AddContentHeaderAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： addcontentheaderaction 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f58fe47de4ee1f79f64415013fc1949ef53b2adf
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490721"
---
# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
指定添加内容头的操作类。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  用来标记内容头元素的 API。
public const std::string& GetText() const  |  获取应添加到内容页眉的文本。
public const std::string& GetFontName() const  |  获取用于显示内容页眉的字体名称。
public int GetFontSize() const  |  获取用于显示内容页眉的字号。
public const std::string& GetFontColor() const  |  获取用于显示内容页眉的字体颜色。
public ContentMarkAlignment GetAlignment() const  |  获取内容页眉的对齐方式。
public int GetMargin() const  |  从底部获取标头的边距。
  
## <a name="members"></a>Members
  
### <a name="getuielementname-function"></a>GetUIElementName 函数
用来标记内容头元素的 API。

  
**返回结果**：应用于保存内容头的 UI 元素的名称。 如果需要删除内容标头，则将在 RemoveContentHeaderAction 中返回相同的名称。
  
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

  
返回结果：字符串形式的字体颜色（例如“#000000”）。
  
### <a name="getalignment-function"></a>GetAlignment 函数
获取内容页眉的对齐方式。

  
**返回结果**：ContentMarkAlignment 枚举器：LEFT|RIGHT|CENTER。 
  
**另请参阅**： [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin 函数
从底部获取标头的边距。

  
返回结果：文档底部的边距（例如 10 毫米）。