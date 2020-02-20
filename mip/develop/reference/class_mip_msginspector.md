---
title: 类 mip：： MsgInspector
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： msginspector 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d2c4f85989e5d9d77ebb540b0b4adfd64b8334c1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489888"
---
# <a name="class-mipmsginspector"></a>类 mip：： MsgInspector 
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<uint8_t\>& GetBody （）  |  获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。
public BodyType GetBodyType （） const  |  获取正文类型。
public const std：： vector\<std：： unique_ptr\<MsgAttachmentData\>\>& GetAttachments （） const  |  获取附件列表作为消息附件数据对象。
public InspectorType GetInspectorType （） const  |  获取文件类型，。
public std：： shared_ptr\<Stream\> GetFileStream （） const  |  获取文件流。
  
## <a name="members"></a>Members
  
### <a name="getbody-function"></a>GetBody 函数
获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。

  
**返回**：字节向量。
  
### <a name="getbodytype-function"></a>GetBodyType 函数
获取正文类型。

  
**返回**：消息的正文类型。
  
### <a name="getattachments-function"></a>GetAttachments 函数
获取附件列表作为消息附件数据对象。

  
**返回**： std：： unique_ptr 的矢量<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType 函数
获取文件类型，。

  
**返回**： InspectorType。
  
### <a name="getfilestream-function"></a>GetFileStream 函数
获取文件流。

  
**返回**：文件流的共享指针。