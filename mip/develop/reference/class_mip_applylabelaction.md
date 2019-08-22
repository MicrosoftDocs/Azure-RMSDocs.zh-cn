---
title: class mip::ApplyLabelAction
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: applylabelaction 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 7d2067ad030e909d53602fcdb3eefa9b88af56bf
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884512"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
应用标签操作要求，必须调用应用程序，才能应用特定标签。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<Label\>& GetLabel () const  |  获取所需的标签。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  获取匹配的分类 Id 并导致显示此标签。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
获取所需的标签。

  
**返回**:标签。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 函数
获取匹配的分类 Id 并导致显示此标签。

  
**返回**:Const std:: vector < std:: string > & 导致此标签出现的分类 Id 的列表。