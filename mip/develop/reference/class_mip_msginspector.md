---
title: 类 MsgInspector
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 msginspector：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: aaf9cc6803e0111cd37960f356d8a6bb19fd60a5
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215164"
---
# <a name="class-msginspector"></a>类 MsgInspector 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector \<uint8_t\>& GetBody ( # A2 const  |  获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。
公共无符号 int GetCodePage ( # A1 const  |  获取正文编码代码页，与 txt、html 正文格式相关。
public BodyType GetBodyType ( # A1 const  |  获取正文类型。
public const std：： vector \<std::shared_ptr\<MsgAttachmentData\> \>& GetAttachments ( # A2 const  |  获取附件列表作为消息附件数据对象。
public InspectorType GetInspectorType ( # A1 const  |  获取文件类型，。
public std：： shared_ptr \<Stream\> GetFileStream ( # A1 const  |  获取文件流。
  
## <a name="members"></a>成员
  
### <a name="getbody-function"></a>GetBody 函数
获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。

  
**返回**：字节向量。
  
### <a name="getcodepage-function"></a>GetCodePage 函数
获取正文编码代码页，与 txt、html 正文格式相关。

  
**返回**：未签名的代码页。 
  
**另请参阅**： [https://docs.microsoft.com/en-us/windows/win32/intl/code-page-identifiers](https://docs.microsoft.com/windows/win32/intl/code-page-identifiers)
  
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