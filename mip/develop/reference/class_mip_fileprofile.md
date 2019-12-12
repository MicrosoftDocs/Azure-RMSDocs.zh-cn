---
title: class mip::FileProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： fileprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a436024aefe58a73ea03747fce5c5f2f4b4fc4b1
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558806"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
FileProfile 类是用于使用 Microsoft 信息保护操作的根类。
典型的应用程序将仅需要一个配置文件。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回配置文件的设置。
public void ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public void UnloadEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的文件引擎。
public void AddEngineAsync （const FileEngine：： Settings & settings，const std：： shared_ptr\<void\>& 上下文）  |  开始向配置文件添加新文件引擎。
public void DeleteEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
public static FILE_API void __CDECL mip：： FileProfile：： LoadAsync | 开始基于提供的设置加载配置文件
public static const FILE_API char * __CDECL mip：： FileProfile：： GetVersion | 获取库版本。

## <a name="members"></a>成員
  
### <a name="getsettings-function"></a>GetSettings 函数
返回配置文件的设置。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。
FileProfile：：在成功或失败时将调用观察程序。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 函数
开始卸载具有给定 ID 的文件引擎。
FileProfile：：在成功或失败时将调用观察程序。
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新文件引擎。
FileProfile：：在成功或失败时将调用观察程序。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
FileProfile：：在成功或失败时将调用观察程序。

### <a name="loadasync-function"></a>LoadAsync 函数
基于提供的设置开始加载配置文件。

[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。

### <a name="getversion-function"></a>GetVersion 函数
获取库版本。