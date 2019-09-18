---
title: class mip::FileProfile
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： fileprofile 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 9971ae734b17186bd9ba942ca7dc991ab3e4ef15
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070594"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
典型的应用程序将仅需要一个配置文件。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回配置文件的设置。
public void ListEnginesAsync （const std：： shared_ptr\<void\>& 上下文）  |  启动列出引擎操作。
public void UnloadEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始卸载具有给定 ID 的文件引擎。
public void AddEngineAsync （const FileEngine：： settings & settings，const std：： shared_ptr\<void\>& context）  |  开始向配置文件添加新文件引擎。
public void DeleteEngineAsync （const std：： string & id，const std：： shared_ptr\<void\>& 上下文）  |  开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
public static FILE_API void __CDECL mip：： FileProfile：： LoadAsync | 开始基于提供的设置加载配置文件
public static const FILE_API char * __CDECL mip：： FileProfile：： GetVersion | 获取库版本。


## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
返回配置文件的设置。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 函数
启动列出引擎操作。
[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 函数
开始卸载具有给定 ID 的文件引擎。
[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。
  
### <a name="addengineasync-function"></a>AddEngineAsync 函数
开始向配置文件添加新文件引擎。
[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 函数
开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。

### <a name="loadasync-function"></a>LoadAsync 函数
基于提供的设置开始加载配置文件。

[FileProfile::Observer](class_mip_fileprofile_observer.md) 将在成功或失败时调用。

### <a name="getversion-function"></a>GetVersion 函数
获取库版本。
