---
title: class mip::PolicyEngine
description: 记录 mip::policyengine 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ce8ef7df12cdc9823a62234b5dadaaacdb7fed37
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573779"
---
# <a name="class-mippolicyengine"></a>class mip::PolicyEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取策略引擎[设置](class_mip_policyengine_settings.md)。
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  列出与策略引擎关联的敏感度标签。
public const std:: vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() 常量  |  列出与策略引擎关联的敏感度类型。
public const std::string& GetMoreInfoUrl() const  |  提供用于查找有关策略/标签详细信息的 URL。
public bool IsLabelingRequired() const  |  检查策略是否规定必须标记文档。
public std::shared_ptr\<Label\> GetDefaultSensitivityLabel()  |  获取默认敏感度标签。
public std::\<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  创建策略处理程序以在文件的执行状态下执行与策略相关的功能。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  将特定于应用程序的事件记录到审核管道。
public const std:: string & GetPolicyDataXml() 常量  |  获取策略数据描述设置、 标签和规则与此策略相关联的 XML。
public const std:: vector\<std:: pair\<std:: string、 std:: string\>\>& GetCustomSettings() 常量  |  获取自定义设置的列表。
public const std:: string & GetPolicyId() 常量  |  获取策略 id。
公共 bool HasClassificationRules() 常量  |  获取策略是否自动或建议的规则。
公共 std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() 常量  |  获取上次提取策略的时间。
  
## <a name="members"></a>成員
  
### <a name="getsettings-function"></a>GetSettings 函数
获取策略引擎[设置](class_mip_policyengine_settings.md)。

  
**返回**:策略引擎设置。 
  
另请参阅：[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 函数
列出与策略引擎关联的敏感度标签。

  
**返回**:敏感度标签列表。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 函数
列出与策略引擎关联的敏感度类型。

  
**返回**:敏感度标签列表。 false （LoadSensitivityTypesEnabled 是否为空
  
**另请参阅**:[PolicyEngine::Settings](class_mip_policyengine_settings.md))。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 函数
提供用于查找有关策略/标签详细信息的 URL。

  
**返回**:字符串格式中的 url。
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 函数
检查策略是否规定必须标记文档。

  
**返回**:如果标记为必需，否则为 false，则为 true。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 函数
获取默认敏感度标签。

  
**返回**:默认敏感度标签，如果存在，nullptr 如果未设置默认标签。
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler 函数
创建策略处理程序以在文件的执行状态下执行与策略相关的功能。

参数：  
* **一个**: bool，表示是否已启用审核发现。



  
**返回**:策略处理程序。
应用程序必须文档的生存期内保留策略处理程序对象。
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 函数
将特定于应用程序的事件记录到审核管道。

参数：  
* **级别**： 的日志级别：信息/错误/警告。 


* **eventType**： 事件的类型的说明。 


* **eventData**： 与事件相关联的数据。


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml 函数
获取策略数据描述设置、 标签和规则与此策略相关联的 XML。

  
**返回**:策略数据的 XML。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取自定义设置的列表。

  
**返回**:自定义设置的向量。
  
### <a name="getpolicyid-function"></a>GetPolicyId 函数
获取策略 id。

  
**返回**:一个字符串，表示策略 ID
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 函数
获取策略是否自动或建议的规则。

  
**返回**:一个布尔值指示，如果那里任何自动或 recommandation 规则在策略中
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 函数
获取上次提取策略的时间。

  
**返回**:上次提取策略的时间