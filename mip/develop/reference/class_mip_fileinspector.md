---
title: 类 mip：： FileInspector
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： fileinspector 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8ae396cc529cbeb17afa8ad0c4617e4bfcfbed3a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558822"
---
# <a name="class-mipfileinspector"></a>类 mip：： FileInspector 
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public InspectorType GetInspectorType （） const  |  获取文件类型，。
public std：： shared_ptr\<Stream\> GetFileStream （） const  |  获取文件流。
  
## <a name="members"></a>成員
  
### <a name="getinspectortype-function"></a>GetInspectorType 函数
获取文件类型，。

  
**返回**： InspectorType。
  
### <a name="getfilestream-function"></a>GetFileStream 函数
获取文件流。

  
**返回**：文件流的共享指针。