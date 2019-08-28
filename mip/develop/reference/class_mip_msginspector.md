---
title: '类 mip:: MsgInspector'
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: msginspector 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 274ada562bae46add2429a2f87442bb77528ea05
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054273"
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