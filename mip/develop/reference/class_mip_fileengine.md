---
title: 类 FileEngine
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 fileengine：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 5b9c3d33fe538810975d4f156aef36280fdd4bda
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215317"
---
# <a name="class-fileengine"></a>类 FileEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回引擎设置。
public const std：： vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& ListSensitivityTypes ( # A2 const  |  列出与策略引擎关联的敏感度类型。
public const std：： shared_ptr \<Label\> GetDefaultSensitivityLabel ( # A1 const  |  获取默认敏感度标签。
public std：： shared_ptr \<Label\> GetLabelById (const std：： string& id) const  |  根据提供的 id 获取标签。
public const std：： vector \<std::shared_ptr\<Label\> \> ListSensitivityLabels ( # A1  |  返回敏感度标签列表。
public const std::string& GetMoreInfoUrl() const  |  提供用于查找有关策略/标签详细信息的 URL。
public const std：： string& GetPolicyFileId ( # A2 const  |  获取策略文件 ID。
public const std：： string& GetSensitivityFileId ( # A2 const  |  获取敏感度文件 ID。
public bool IsLabelingRequired() const  |  检查策略是否规定必须标记文档。
public std：： chrono：： time_point \<std::chrono::system_clock\> GetLastPolicyFetchTime ( # A1 const  |  获取上次提取策略的时间。
public const std：： string& GetPolicyDataXml ( # A2 const  |  获取策略数据 XML，该 XML 描述与此策略关联的设置、标签和规则。
public std：： shared_ptr \<AsyncControl\> CreateFileHandlerAsync (const std：： string& inputFilePath，const std：： string& actualFilePath，Bool isAuditDiscoveryEnabled，const std：： shared_ptr \<FileHandler::Observer\>& fileHandlerObserver，const std：： shared_ptr \<void\>& context，const std：： shared_ptr \<FileExecutionState\>& fileExecutionState，bool isGetSensitivityLabelAuditDiscoveryEnabled)   |  开始创建给定文件路径的文件处理程序。
public std：： shared_ptr \<AsyncControl\> CreateFileHandlerAsync (const std：： shared_ptr \<Stream\>& inputStream，const std：： String& actualFilePath，bool isAuditDiscoveryEnabled，const std：： shared_ptr \<FileHandler::Observer\>& fileHandlerObserver，const std：： shared_ptr \<void\>& context，const std：： shared_ptr \<FileExecutionState\>& fileExecutionState，bool isGetSensitivityLabelAuditDiscoveryEnabled)   |  开始创建给定文件流的文件处理程序。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  将特定于应用程序的事件记录到审核管道。
public const std：： vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings ( # A2 const  |  获取自定义设置的列表。
public bool HasClassificationRules ( # A1 const  |  获取策略是否具有自动或建议规则。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
返回引擎设置。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 函数
列出与策略引擎关联的敏感度类型。

  
**返回结果**：敏感度标签列表。 如果 LoadSensitivityTypesEnabled 为 false，则为空 (
  
**另请参阅**： FileEngine：： Settings) 。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 函数
获取默认敏感度标签。

  
**返回结果**：如果存在，则返回默认敏感度标签，如果未设置默认标签，则返回 nullptr。
  
### <a name="getlabelbyid-function"></a>GetLabelById 函数
根据提供的 id 获取标签。
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 函数
返回敏感度标签列表。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 函数
提供用于查找有关策略/标签详细信息的 URL。

  
**返回结果**：字符串格式的 URL。
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId 函数
获取策略文件 ID。

  
**返回**：表示策略文件 ID 的字符串
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId 函数
获取敏感度文件 ID。

  
**返回**：表示策略文件 ID 的字符串
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 函数
检查策略是否规定必须标记文档。

  
**返回结果**：如果标记是必需的，则返回 True，否则返回 False。
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 函数
获取上次提取策略的时间。

  
**返回**：上次提取策略的时间
  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml 函数
获取策略数据 XML，该 XML 描述与此策略关联的设置、标签和规则。

  
**返回**：策略数据 XML。
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 函数
开始创建给定文件路径的文件处理程序。

参数：  
* **inputFilePath**：要打开的文件。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 


* **actualFilePath**：实际 (不是临时) 文件路径，将用于审核。 


* **isAuditDiscoveryEnabled**：表示是否启用了审核发现。 


* **fileHandlerObserver**：实现 FileHandler::Observer 接口的类。 


* **context**：将以不透明形式传递回观察程序的客户端上下文。 


* **isGetSensitivityLabelAuditDiscoveryEnabled**：表示是否对 getSensitivityLabel 触发审核发现。 



  
**返回**： Async control 对象。
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 函数
开始创建给定文件流的文件处理程序。

参数：  
* **inputStream**：包含文件数据的流。 


* **actualFilePath**：文件的路径。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 还将使用来标识审核中的文件。 


* **isAuditDiscoveryEnabled**：表示是否启用了审核发现。 


* **fileHandlerObserver**：实现 FileHandler::Observer 接口的类。 


* **context**：将以不透明形式传递回观察程序的客户端上下文。 


* **isGetSensitivityLabelAuditDiscoveryEnabled**：表示是否对 getSensitivityLabel 触发审核发现。 



  
**返回**： Async control 对象。
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 函数
将特定于应用程序的事件记录到审核管道。

参数：  
* **level**：日志级别说明：信息/错误/警告 


* **eventType**：事件类型的说明 


* **eventData**：与事件关联的数据


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取自定义设置的列表。

  
**返回**：自定义设置的向量
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 函数
获取策略是否具有自动或建议规则。

  
**返回**：一个布尔值，将指示策略中是否存在任何自动或建议规则