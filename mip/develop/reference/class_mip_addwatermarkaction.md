---
title: class mip::AddWatermarkAction
description: 记录 mip::addwatermarkaction 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 8121763106c9f46022264a7eea3bc16e363e523c
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330468"
---
# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
指定添加水印的操作类。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  用于标记水印元素的 API。
public WatermarkLayout GetLayout() const  |  用于获取水印布局的 API。
public const std::string& GetText() const  |  获取应添加到水印的文本。
public const std::string& GetFontName() const  |  获取用于显示水印的字体名称。
public int GetFontSize() const  |  获取用于显示水印的字号。
public const std::string& GetFontColor() const  |  获取用于显示水印的字体颜色。
public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getuielementname-function"></a>GetUIElementName 函数
用于标记水印元素的 API。

  
**返回**:保存水印应使用的用户界面元素的名称。 如果需要删除水印，将在 RemoveWatermarkingAction 中返回相同名称。
  
### <a name="getlayout-function"></a>GetLayout 函数
用于获取水印布局的 API。

  
**返回**:WatermarkLayout：采用枚举水平|对角线形式的水印布局。 、
  
### <a name="gettext-function"></a>GetText 函数
获取应添加到水印的文本。

  
**返回**:内容标头文本。
  
### <a name="getfontname-function"></a>GetFontName 函数
获取用于显示水印的字体名称。

  
**返回**:字体名称。 如果策略未进行任何设置，默认值为 Calibri。
  
### <a name="getfontsize-function"></a>GetFontSize 函数
获取用于显示水印的字号。

  
**返回**:一个整数形式的字体大小。
  
### <a name="getfontcolor-function"></a>GetFontColor 函数
获取用于显示水印的字体颜色。

  
**返回**:字符串 (例如，"#000000") 形式的字体颜色。
  
### <a name="gettype-function"></a>GetType 函数
获取[操作](class_mip_action.md)类型。

  
**返回**:ActionType：此基类可以转换成的派生操作类型。
