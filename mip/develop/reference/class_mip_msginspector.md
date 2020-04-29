---
title: 类 MsgInspector
description: 记录 Microsoft 信息保护（MIP） SDK 的 msginspector：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 79a044099c09d799d77f4af11eb0b80ecc21d6d6
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761478"
---
# <a name="class-msginspector"></a>类 MsgInspector 
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<Uint8_t\>& GetBody （）  |  获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。
public BodyType GetBodyType （） const  |  获取正文类型。
public const std：： vector\<std：： shared_ptr\<MsgAttachmentData\> \>& GetAttachments （） const  |  获取附件列表作为消息附件数据对象。
public InspectorType GetInspectorType （） const  |  获取文件类型，。
public std：： shared_ptr\<Stream\> GetFileStream （） const  |  获取文件流。
  
## <a name="members"></a>成员
  
### <a name="getbody-function"></a>GetBody 函数
获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。

  
**返回**：字节向量。
  
### <a name="getbodytype-function"></a>GetBodyType 函数
获取正文类型。

  
**返回**：消息的正文类型。
  
### <a name="getattachments-function"></a>GetAttachments 函数
获取附件列表作为消息附件数据对象。

  
**返回**： std：： unique_ptr 的向量<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType 函数
获取文件类型，。

  
**返回**： InspectorType。
  
### <a name="getfilestream-function"></a>GetFileStream 函数
获取文件流。

  
**返回**：文件流的共享指针。