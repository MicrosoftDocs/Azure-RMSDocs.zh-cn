---
title: class mip::PolicyEngine
description: 记录 mip::policyengine 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 87eff7d2ca82a59f7a4c521d6803acc5208101d6
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259059"
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
* **一个**: bool，表示是否已启用审核发现



  
**返回**:策略处理程序。
应用程序需要的文档生存期内保留策略处理程序对象
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 函数
将特定于应用程序的事件记录到审核管道。

参数：  
* **级别**： 的日志级别：信息/错误/警告 


* **eventType**：事件类型的说明 


* **eventData**：与事件关联的数据


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml 函数
获取策略数据描述设置、 标签和规则与此策略相关联的 XML。

  
**返回**:策略数据的 XML
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取自定义设置的列表。

  
**返回**:向量的自定义设置
