---
title: class mip::AddWatermarkAction
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： addwatermarkaction 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 80ae66e54fe00ad96652b3568d49e256211dffc4
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490704"
---
# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
指定添加水印的操作类。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  用于标记水印元素的 API。
public WatermarkLayout GetLayout() const  |  用于获取水印布局的 API。
public const std::string& GetText() const  |  获取应添加到水印的文本。
public const std::string& GetFontName() const  |  获取用于显示水印的字体名称。
public int GetFontSize() const  |  获取用于显示水印的字号。
public const std::string& GetFontColor() const  |  获取用于显示水印的字体颜色。
  
## <a name="members"></a>Members
  
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