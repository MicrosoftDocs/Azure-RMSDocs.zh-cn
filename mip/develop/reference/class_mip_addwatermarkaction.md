---
title: 类 AddWatermarkAction
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 addwatermarkaction：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8b5767999b666e6cd8a2b9f42d9d86e690000681
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212359"
---
# <a name="class-addwatermarkaction"></a>类 AddWatermarkAction 
指定添加水印的操作类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  用于标记水印元素的 API。
public WatermarkLayout GetLayout() const  |  用于获取水印布局的 API。
public const std::string& GetText() const  |  获取应添加到水印的文本。
public const std::string& GetFontName() const  |  获取用于显示水印的字体名称。
public int GetFontSize() const  |  获取用于显示水印的字号。
public const std::string& GetFontColor() const  |  获取用于显示水印的字体颜色。
  
## <a name="members"></a>成员
  
### <a name="getuielementname-function"></a>GetUIElementName 函数
用于标记水印元素的 API。

  
**返回结果**：应用于保存水印的 UI 元素的名称。 如果需要删除水印，将在 RemoveWatermarkingAction 中返回相同名称。
  
### <a name="getlayout-function"></a>GetLayout 函数
用于获取水印布局的 API。

  
**返回结果**：WatermarkLayout：采用枚举水平|对角线形式的水印布局。 ,
  
### <a name="gettext-function"></a>GetText 函数
获取应添加到水印的文本。

  
**返回结果**：内容头文本。
  
### <a name="getfontname-function"></a>GetFontName 函数
获取用于显示水印的字体名称。

  
**返回结果**：字体名称。 如果策略未进行任何设置，默认值为 Calibri。
  
### <a name="getfontsize-function"></a>GetFontSize 函数
获取用于显示水印的字号。

  
**返回结果**：整数形式的字体大小。
  
### <a name="getfontcolor-function"></a>GetFontColor 函数
获取用于显示水印的字体颜色。

  
返回结果：字符串形式的字体颜色（例如“#000000”）。