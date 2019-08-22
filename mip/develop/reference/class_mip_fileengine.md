---
title: class mip::FileEngine
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: fileengine 类。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 86437533b2451b613231d668857b1402fc9f4272
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885809"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回引擎设置。
public const std:: vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  列出与策略引擎关联的敏感度类型。
public const std:: shared_ptr\<Label\> GetDefaultSensitivityLabel () const  |  获取默认敏感度标签。
public std:: shared_ptr\<标签\> GetLabelById (const std:: string & id) const  |  根据提供的 id 获取标签。
public const std:: vector\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels ()  |  返回敏感度标签列表。
public const std::string& GetMoreInfoUrl() const  |  提供用于查找有关策略/标签详细信息的 URL。
public const std:: string & GetPolicyFileId () const  |  获取策略文件 ID。
public bool IsLabelingRequired() const  |  检查策略是否规定必须标记文档。
public std:: chrono:: time_point\<std:: chrono:: system_clock\> GetLastPolicyFetchTime () const  |  获取上次提取策略的时间。
public void CreateFileHandlerAsync (const std:: string & inputFilePath, const std:: string & actualFilePath, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<FileHandler:: Observer\>& fileHandlerObserver, const std:: shared_ptr\<void\>& context, const std:: shared_ptr\<FileExecutionState\>& FileExecutionState)  |  开始创建给定文件路径的文件处理程序。
public void CreateFileHandlerAsync (const std:: shared_ptr\<Stream\>& inputStream, const std:: string & actualFilePath, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<FileHandler:: 观察程序\>\<\>\<& fileHandlerObserver, const std:: shared_ptr void & context, const std:: shared_ptr FileExecutionState & FileExecutionState) \>  |  开始创建给定文件流的文件处理程序。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  将特定于应用程序的事件记录到审核管道。
public const std:: vector\<std::p air\<std:: string, std:: string\>\>& GetCustomSettings () const  |  获取自定义设置的列表。
public bool HasClassificationRules () const  |  获取策略是否具有自动或建议规则。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
返回引擎设置。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 函数
列出与策略引擎关联的敏感度类型。

  
**返回**:敏感度标签的列表。 如果 LoadSensitivityTypesEnabled 为 false, 则为空 (
  
**另请参阅**:[FileEngine:: Settings](class_mip_fileengine_settings.md))。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 函数
获取默认敏感度标签。

  
**返回**:如果存在默认的敏感度标签, 则为, 如果没有设置默认标签, 则为 nullptr。
  
### <a name="getlabelbyid-function"></a>GetLabelById 函数
根据提供的 id 获取标签。
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 函数
返回敏感度标签列表。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 函数
提供用于查找有关策略/标签详细信息的 URL。

  
**返回**:字符串格式的 url。
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId 函数
获取策略文件 ID。

  
**返回**:表示策略文件 ID 的字符串
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 函数
检查策略是否规定必须标记文档。

  
**返回**:如果标签是必需的, 则为 True; 否则为 false。
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 函数
获取上次提取策略的时间。

  
**返回**:上次提取策略的时间
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 函数
开始创建给定文件路径的文件处理程序。

参数：  
* **inputFilePath**:要打开的文件。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 


* **actualFilePath**:实际 (而非临时) 文件路径将用于审核。 


* **isAuditDiscoveryEnabled**: 表示是否启用了审核发现。 


* **fileHandlerObserver**:实现 [FileHandler::Observer](class_mip_filehandler_observer.md) 接口的类。 


* **上下文**:将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 函数
开始创建给定文件流的文件处理程序。

参数：  
* **inputStream**:包含文件数据的流。 


* **actualFilePath**:文件路径。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 还将使用来标识审核中的文件。 


* **isAuditDiscoveryEnabled**: 表示是否启用了审核发现。 


* **fileHandlerObserver**:实现 [FileHandler::Observer](class_mip_filehandler_observer.md) 接口的类。 


* **上下文**:将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 函数
将特定于应用程序的事件记录到审核管道。

参数：  
* **level**: 日志级别的说明:信息/错误/警告 


* **eventType**：事件类型的说明 


* **eventData**：与事件关联的数据


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取自定义设置的列表。

  
**返回**:自定义设置的向量
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 函数
获取策略是否具有自动或建议规则。

  
**返回**:一个布尔值, 将指示策略中是否存在任何自动或建议规则