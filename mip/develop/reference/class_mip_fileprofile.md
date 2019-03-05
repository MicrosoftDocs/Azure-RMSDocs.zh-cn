---
title: class mip::FileProfile
description: 记录 mip::fileprofile 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 4bdd96e7f9f414062d969de1ffaf7195ad71d214
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329397"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
典型的应用程序将仅需要一个配置文件。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回配置文件的设置。
public void ListEnginesAsync(const std::shared_ptr\<void\>& context)  |  启动列出引擎操作。
public void UnloadEngineAsync (const std:: string & id，const std::\<void\>& 上下文)  |  开始卸载具有给定 ID 的文件引擎。
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr\<void\>& context)  |  开始向配置文件添加新文件引擎。
public void DeleteEngineAsync (const std:: string & id，const std::\<void\>& 上下文)  |  开始删除具有给定 ID 的文件引擎。 给定配置文件的所有数据都将删除。
  
## <a name="members"></a>成員
  
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
