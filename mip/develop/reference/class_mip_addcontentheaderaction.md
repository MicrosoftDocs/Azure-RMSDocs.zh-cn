---
title: class mip AddContentHeaderAction
description: class mip AddContentHeaderAction 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: bc60fe32005a0c6bc8088ab7687a3f711ae7a99a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445642"
---
# <a name="class-mipaddcontentheaderaction"></a>class mip::AddContentHeaderAction 
指定添加内容头的操作类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
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
  
### <a name="getuielementname"></a>GetUIElementName
用来标记内容头元素的 API。

  
**返回结果**：应用于保存内容头的 UI 元素的名称。 如果需要删除内容头，将在 [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) 中返回相同名称。
  
### <a name="gettext"></a>GetText
获取应添加到内容页眉的文本。

  
**返回结果**：内容头文本。
  
### <a name="getfontname"></a>GetFontName
获取用于显示内容页眉的字体名称。

  
**返回结果**：字体名称。 如果策略未进行任何设置，默认值为 Calibri。
  
### <a name="getfontsize"></a>GetFontSize
获取用于显示内容页眉的字号。

  
**返回结果**：整数形式的字体大小。
  
### <a name="getfontcolor"></a>GetFontColor
获取用于显示内容页眉的字体颜色。

  
返回结果：字符串形式的字体颜色（例如“#000000”）。
  
### <a name="getalignment"></a>GetAlignment
获取内容页眉的对齐方式。

  
**返回结果**：ContentMarkAlignment 枚举器：LEFT|RIGHT|CENTER。 
  
另请参阅：ContentMarkAlignment
  
### <a name="getmargin"></a>GetMargin
从底部获取标头的边距。

  
返回结果：文档底部的边距（例如 10 毫米）。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。