---
title: class mip::Stream
description: 记录 mip::stream 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1987aea2e90a3ded3a55f509e3d49a689d361c62
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60185107"
---
# <a name="class-mipstream"></a>class mip::Stream 
一个类，它定义 MIP SDK 和基于流的内容之间的接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
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
  
### <a name="read-function"></a>Read 函数
从流读取到缓冲区。

参数：  
* **buffer**：指向缓冲区的区指针 


* **bufferLength**：缓冲区大小。 



  
**返回**:读取的字节数。
  
### <a name="write-function"></a>编写函数
从缓冲区写入到流。

参数：  
* **buffer**：指向缓冲区的区指针 


* **bufferLength**：缓冲区大小。 



  
**返回**:写入的字节数。
  
### <a name="flush-function"></a>Flush 函数
刷新流。

  
**返回**:如果成功则为 true，否则返回 false。
  
### <a name="seek-function"></a>Seek 函数
查找流中的特定位置。

参数：  
* **position**：在流中要查找的位置。


  
### <a name="canread-function"></a>CanRead 函数
检查是否可读取流。

  
**返回**:如果可读，则返回 true，否则返回 false。
  
### <a name="canwrite-function"></a>CanWrite 函数
检查是否可写入流。

  
**返回**:如果可写则为 true，否则返回 false。
  
### <a name="position-function"></a>Position 函数
获取流中的当前位置。

  
**返回**:流中的位置。
  
### <a name="size-function"></a>大小函数
获取流中的内容的大小。

  
**返回**:流大小。
  
### <a name="size-function"></a>大小函数
设置流大小。

参数：  
* **stream**：流大小。

