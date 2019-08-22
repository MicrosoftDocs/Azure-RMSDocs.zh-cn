---
title: '类 mip:: MsgInspector'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: msginspector 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: cb0b85b0de42eae46d6cd7c9c6d6e18680b2e545
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69892743"
---
# <a name="class-mipmsginspector"></a>类 mip:: MsgInspector 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\>& GetBody ()  |  获取消息的正文。如果将 TXT/HTML 格式设置为 utf8, 则为。
public BodyType GetBodyType () const  |  获取正文类型。
public const std:: vector\<std:: unique_ptr\<MsgAttachmentData\>\>& GetAttachments () const  |  获取附件列表作为消息附件数据对象。
public InspectorType GetInspectorType () const  |  获取文件类型,。
public std:: shared_ptr\<Stream\> GetFileStream () const  |  获取文件流。
  
## <a name="members"></a>成员
  
### <a name="getbody-function"></a>GetBody 函数
获取消息的正文。如果将 TXT/HTML 格式设置为 utf8, 则为。

  
**返回**:字节向量。
  
### <a name="getbodytype-function"></a>GetBodyType 函数
获取正文类型。

  
**返回**:消息的正文类型。
  
### <a name="getattachments-function"></a>GetAttachments 函数
获取附件列表作为消息附件数据对象。

  
**返回**:Std:: unique_ptr 的矢量<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType 函数
获取文件类型,。

  
**返回**:InspectorType.
  
### <a name="getfilestream-function"></a>GetFileStream 函数
获取文件流。

  
**返回**:文件流的共享指针。