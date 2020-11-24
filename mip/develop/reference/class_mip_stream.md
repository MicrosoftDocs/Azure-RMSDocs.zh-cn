---
title: 类流
description: 记录 stream：：未定义的 Microsoft 信息保护类 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a370d6917306f2865c1d91eb7fa90c2880497a04
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565039"
---
# <a name="class-stream"></a>类流 
一个类，它定义 MIP SDK 和基于流的内容之间的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  从流读取到缓冲区。
public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  从缓冲区写入到流。
public bool Flush()  |  刷新流。
public void Seek(int64_t position)  |  查找流中的特定位置。
public bool CanRead() const  |  检查是否可读取流。
public bool CanWrite() const  |  检查是否可写入流。
public int64_t Position()  |  获取流中的当前位置。
public int64_t Size()  |  获取流中的内容的大小。
public void Size(int64_t value)  |  设置流大小。
  
## <a name="members"></a>成员
  
### <a name="read-function"></a>Read 函数
从流读取到缓冲区。

参数：  
* **buffer**：指向缓冲区的指针 


* **bufferLength**：缓冲区大小。 



  
**返回结果**：读取的字节数。
  
### <a name="write-function"></a>写入函数
从缓冲区写入到流。

参数：  
* **buffer**：指向缓冲区的指针 


* **bufferLength**：缓冲区大小。 



  
**返回结果**：写入的字节数。
  
### <a name="flush-function"></a>Flush 函数
刷新流。

  
**返回结果**：如果成功，则返回 true，否则返回 false。
  
### <a name="seek-function"></a>Seek 函数
查找流中的特定位置。

参数：  
* **位置**：查找流。


  
### <a name="canread-function"></a>CanRead 函数
检查是否可读取流。

  
**返回结果**：如果可读，则返回 true，否则返回 false。
  
### <a name="canwrite-function"></a>CanWrite 函数
检查是否可写入流。

  
**返回结果**：如果可写入，则返回 true，否则返回 false。
  
### <a name="position-function"></a>Position 函数
获取流中的当前位置。

  
**返回结果**：流中的位置。
  
### <a name="size-function"></a>Size 函数
获取流中的内容的大小。

  
**返回结果**：流大小。
  
### <a name="size-function"></a>Size 函数
设置流大小。

参数：  
* **stream**： size。

