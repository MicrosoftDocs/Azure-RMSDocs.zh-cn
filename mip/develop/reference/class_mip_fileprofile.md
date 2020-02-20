---
title: class mip::FileProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： fileprofile 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 44d6024473555c0745ff3156ff5cd004f83b6f6b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488137"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
FileProfile 类是用于使用 Microsoft 信息保护操作的根类。
典型的应用程序将仅需要一个配置文件。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回配置文件的设置。
public std：： shared_ptr\<AsyncControl\> ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public std：： shared_ptr\<AsyncControl\> UnloadEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的文件引擎。
public std：： shared_ptr\<AsyncControl\> AddEngineAsync （const FileEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新文件引擎。
public std：： shared_ptr\<AsyncControl\> DeleteEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings 函数
返回配置文件的设置。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。

  
**返回**： Async control 对象。
FileProfile：：在成功或失败时将调用观察程序。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 函数
开始卸载具有给定 ID 的文件引擎。

  
**返回**： Async control 对象。
FileProfile：：在成功或失败时将调用观察程序。
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新文件引擎。

  
**返回**： Async control 对象。
FileProfile：：在成功或失败时将调用观察程序。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。

  
**返回**： Async control 对象。
FileProfile：：在成功或失败时将调用观察程序。