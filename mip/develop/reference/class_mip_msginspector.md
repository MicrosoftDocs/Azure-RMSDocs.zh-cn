---
title: 类 mip：： MsgInspector
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： msginspector 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d1234168e4ce3996077b705e904f5765b761ec4c
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558614"
---
# <a name="class-mipmsginspector"></a>类 mip：： MsgInspector 
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector\<uint8_t\>& GetBody （）  |  获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。
public BodyType GetBodyType （） const  |  获取正文类型。
public const std：： vector\<std：： unique_ptr\<MsgAttachmentData\>\>& GetAttachments （） const  |  获取附件列表作为消息附件数据对象。
  
## <a name="members"></a>成員
  
### <a name="getbody-function"></a>GetBody 函数
获取消息的正文。如果将 TXT/HTML 格式设置为 utf8，则为。

  
**返回**：字节向量。
  
### <a name="getbodytype-function"></a>GetBodyType 函数
获取正文类型。

  
**返回**：消息的正文类型。
  
### <a name="getattachments-function"></a>GetAttachments 函数
获取附件列表作为消息附件数据对象。

  
**返回**： std：： unique_ptr 的矢量<MsgAttachmentData>