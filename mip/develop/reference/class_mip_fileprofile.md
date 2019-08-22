---
title: class mip::FileProfile
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: fileprofile 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 00b56c5b45c8c05bf50229c3b462611ce48945c4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884277"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
典型的应用程序将仅需要一个配置文件。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回配置文件的设置。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& 上下文)  |  启动列出引擎操作。
public void UnloadEngineAsync (const std:: string & id, const std:: shared_ptr\<void\>& 上下文)  |  开始卸载具有给定 ID 的文件引擎。
public void AddEngineAsync (const FileEngine:: settings & settings, const std:: shared_ptr\<void\>& context)  |  开始向配置文件添加新文件引擎。
public void DeleteEngineAsync (const std:: string & id, const std:: shared_ptr\<void\>& 上下文)  |  开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
  
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