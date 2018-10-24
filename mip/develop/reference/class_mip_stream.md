---
title: class mip Stream
description: class mip Stream 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e6296c5e15590741e008979dcf12373ff5fcdf00
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445217"
---
# <a name="class-mipstream"></a>class mip::Stream 
一个类，它定义 MIP SDK 和基于流的内容之间的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
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
  
## <a name="members"></a>成員
  
### <a name="read"></a>读取
从流读取到缓冲区。

参数：  
* **buffer**：指向缓冲区的区指针 


* **bufferLength**：缓冲区大小。 



  
**返回结果**：读取的字节数。
  
### <a name="write"></a>写入
从缓冲区写入到流。

参数：  
* **buffer**：指向缓冲区的区指针 


* **bufferLength**：缓冲区大小。 



  
**返回结果**：写入的字节数。
  
### <a name="flush"></a>刷新
刷新流。

  
**返回结果**：如果成功，则返回 true，否则返回 false。
  
### <a name="seek"></a>Seek
查找流中的特定位置。

参数：  
* **position**：在流中要查找的位置。


  
### <a name="canread"></a>CanRead
检查是否可读取流。

  
**返回结果**：如果可读，则返回 true，否则返回 false。
  
### <a name="canwrite"></a>CanWrite
检查是否可写入流。

  
**返回结果**：如果可写入，则返回 true，否则返回 false。
  
### <a name="position"></a>位置
获取流中的当前位置。

  
**返回结果**：流中的位置。
  
### <a name="size"></a>大小
获取流中的内容的大小。

  
**返回结果**：流大小。
  
### <a name="size"></a>大小
设置流大小。

参数：  
* **stream**：流大小。

