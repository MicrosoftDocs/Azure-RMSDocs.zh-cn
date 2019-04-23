---
title: class mip::FileEngine
description: 记录 mip::fileengine 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 15ce90a80430f50854580f6c7a2993d92db0a744
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184784"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  返回引擎设置。
public const std:: vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() 常量  |  列出与策略引擎关联的敏感度类型。
public const std::shared_ptr\<Label\> GetDefaultSensitivityLabel() const  |  获取默认敏感度标签。
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  返回敏感度标签列表。
public const std::string& GetMoreInfoUrl() const  |  提供用于查找有关策略/标签详细信息的 URL。
public const std:: string & GetPolicyId() 常量  |  获取策略 id。
public bool IsLabelingRequired() const  |  检查策略是否规定必须标记文档。
公共 std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() 常量  |  获取上次提取策略的时间。
public void CreateFileHandlerAsync (const std:: string & inputFilePath，const std:: string & actualFilePath，bool isAuditDiscoveryEnabled const std::\<filehandler:: Observer\>& fileHandlerObserverconst std:: shared_ptr\<void\>& 上下文、 const std:: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  开始创建给定文件路径的文件处理程序。
public void CreateFileHandlerAsync (const std::\<Stream\>& inputStream，const std:: string & actualFilePath，bool isAuditDiscoveryEnabled const std:: shared_ptr\<filehandler:: Observer\>& fileHandlerObserver，const std:: shared_ptr\<void\>& 上下文、 const std:: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  开始创建给定文件流的文件处理程序。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  将特定于应用程序的事件记录到审核管道。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetCustomSettings() 常量  |  获取自定义设置的列表。
公共 bool HasClassificationRules() 常量  |  获取策略是否自动或建议的规则。
  
## <a name="members"></a>成員
  
### <a name="getsettings-function"></a>GetSettings 函数
返回引擎设置。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 函数
列出与策略引擎关联的敏感度类型。

  
**返回**:敏感度标签列表。 false （LoadSensitivityTypesEnabled 是否为空
  
**另请参阅**:[FileEngine::Settings](class_mip_fileengine_settings.md))。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 函数
获取默认敏感度标签。

  
**返回**:默认敏感度标签，如果存在，nullptr 如果未设置默认标签。
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 函数
返回敏感度标签列表。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 函数
提供用于查找有关策略/标签详细信息的 URL。

  
**返回**:字符串格式中的 url。
  
### <a name="getpolicyid-function"></a>GetPolicyId 函数
获取策略 id。

  
**返回**:一个字符串，表示策略 ID
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 函数
检查策略是否规定必须标记文档。

  
**返回**:如果标记为必需，否则为 false，则为 true。
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 函数
获取上次提取策略的时间。

  
**返回**:上次提取策略的时间
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 函数
开始创建给定文件路径的文件处理程序。

参数：  
* **inputFilePath**:要打开的文件。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 


* **actualFilePath**:实际的 （不是临时的） 文件路径，将用于审核。 


* **isAuditDiscoveryEnabled**： 表示是否已启用审核发现。 


* **fileHandlerObserver**:实现 [FileHandler::Observer](class_mip_filehandler_observer.md) 接口的类。 


* **上下文**:将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 函数
开始创建给定文件流的文件处理程序。

参数：  
* **inputStream**:包含文件数据的流。 


* **actualFilePath**:文件路径。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 此外将使用以标识审核中的文件。 


* **isAuditDiscoveryEnabled**： 表示是否已启用审核发现。 


* **fileHandlerObserver**:实现 [FileHandler::Observer](class_mip_filehandler_observer.md) 接口的类。 


* **上下文**:将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 函数
将特定于应用程序的事件记录到审核管道。

参数：  
* **级别**： 日志级别的说明：信息/错误/警告 


* **eventType**：事件类型的说明 


* **eventData**：与事件关联的数据


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取自定义设置的列表。

  
**返回**:向量的自定义设置
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 函数
获取策略是否自动或建议的规则。

  
**返回**:一个布尔值指示，如果那里任何自动或 recommandation 规则在策略中