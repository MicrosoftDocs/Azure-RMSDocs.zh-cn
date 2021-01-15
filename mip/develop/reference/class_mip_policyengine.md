---
title: 类 PolicyEngine
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 policyengine：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 10f913029af2be9f0430c55b8296269eb04beb7b
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213430"
---
# <a name="class-policyengine"></a>类 PolicyEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取策略引擎设置。
public const std：： vector \<std::shared_ptr\<Label\> \> ListSensitivityLabels (const std：： Vector \<std::string\>& contentFormats)   |  根据提供的 contentFormats 列出与策略引擎关联的敏感度标签。
public const std：： vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& ListSensitivityTypes ( # A2 const  |  列出与策略引擎关联的敏感度类型。
public const std::string& GetMoreInfoUrl() const  |  提供用于查找有关策略/标签详细信息的 URL。
public bool IsLabelingRequired (const std：： string& contentFormat) const  |  检查策略是否规定必须根据提供的 contentFormat 对内容进行标记。
public const std：： shared_ptr \<Label\> GetDefaultSensitivityLabel (const std：： string& contentFormat) const  |  根据所提供的 contentFormat 获取默认的敏感度标签。
public std：： shared_ptr \<Label\> GetLabelById (const std：： string& id) const  |  根据提供的 id 获取标签。
public std：： shared_ptr \<PolicyHandler\> CreatePolicyHandler (Bool isAuditDiscoveryEnabled，Bool isGetSensitivityLabelAuditDiscoveryEnabled)   |  创建策略处理程序以在文件的执行状态下执行与策略相关的功能。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  将特定于应用程序的事件记录到审核管道。
public const std：： string& GetTenantId ( # A2 const  |  获取与引擎关联的租户 ID。
public const std：： string& GetPolicyDataXml ( # A2 const  |  获取策略数据 XML，该 XML 描述与此策略关联的设置、标签和规则。
public const std：： string& GetSensitivityTypesDataXml ( # A2 const  |  获取描述与此策略关联的敏感度类型的敏感类型数据 XML。
public const std：： vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings ( # A2 const  |  获取自定义设置的列表。
public const std：： string& GetPolicyFileId ( # A2 const  |  获取策略文件 ID。
public const std：： string& GetSensitivityFileId ( # A2 const  |  获取敏感度文件 ID。
public bool HasClassificationRules (const std：： vector \<std::string\>& contentFormats) const  |  根据提供的 contentFormats，获取策略是否具有自动或建议规则。
public std：： chrono：： time_point \<std::chrono::system_clock\> GetLastPolicyFetchTime ( # A1 const  |  获取上次提取策略的时间。
public uint32_t GetWxpMetadataVersion ( # A1 const  |  获取建议的 WXP (Word、Excel、Powerpoint) 元数据版本，当前为0（对于共同创作启用版本，则为旧版本1）。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取策略引擎设置。

  
**返回结果**：策略引擎设置。 
  
**另请参阅**： mip：:P olicyengine：： Settings
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 函数
根据提供的 contentFormats 列出与策略引擎关联的敏感度标签。

参数：  
* **contentFormats**： contentFormats 用于筛选敏感度标签的格式矢量，如 "文件"、"电子邮件" 等。将 contentFormats 设置为空矢量，以按默认格式筛选敏感度标签。



  
**返回结果**：敏感度标签列表。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 函数
列出与策略引擎关联的敏感度类型。

  
**返回结果**：敏感度标签列表。 如果 LoadSensitivityTypesEnabled 为 false，则为空 (
  
**另请参阅**： PolicyEngine：： Settings) 。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 函数
提供用于查找有关策略/标签详细信息的 URL。

  
**返回结果**：字符串格式的 URL。
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 函数
检查策略是否规定必须根据提供的 contentFormat 对内容进行标记。

参数：  
* **contentFormat**：确定是否需要标签时进行筛选的格式-例如： "file"、"email" 等。将 contentFormat 设置为空字符串，以确定默认格式是否需要标签。



  
**返回结果**：如果标记是必需的，则返回 True，否则返回 False。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 函数
根据所提供的 contentFormat 获取默认的敏感度标签。

参数：  
* **contentFormat**：检索默认敏感度标签时要按其进行筛选的格式-例如 "文件"、"电子邮件" 等。将 contentFormat 设置为空字符串，以检索默认格式的默认敏感度标签。



  
**返回结果**：如果存在，则返回默认敏感度标签，如果未设置默认标签，则返回 nullptr。
  
### <a name="getlabelbyid-function"></a>GetLabelById 函数
根据提供的 id 获取标签。

参数：  
* **id**：标签的标识符。



  
**返回**：标签
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler 函数
创建策略处理程序以在文件的执行状态下执行与策略相关的功能。

参数：  
* **isAuditDiscoveryEnabled**：描述是否启用了审核发现。



  
**返回结果**：策略处理程序。
应用程序需要在文档的生存期内保留策略处理程序对象。
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 函数
将特定于应用程序的事件记录到审核管道。

参数：  
* **level**：% Level： Info/Error/Warning。 


* **事件类型：事件** 类型的说明。 


* **eventData**：与事件关联的数据。


  
### <a name="gettenantid-function"></a>GetTenantId 函数
获取与引擎关联的租户 ID。

  
**返回**：租户 ID
  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml 函数
获取策略数据 XML，该 XML 描述与此策略关联的设置、标签和规则。

  
**返回**：策略数据 XML。
  
### <a name="getsensitivitytypesdataxml-function"></a>GetSensitivityTypesDataXml 函数
获取描述与此策略关联的敏感度类型的敏感类型数据 XML。

  
**返回**：敏感类型数据 XML。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
获取自定义设置的列表。

  
**返回**：自定义设置的向量。
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId 函数
获取策略文件 ID。

  
**返回**：表示策略文件 ID 的字符串
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId 函数
获取敏感度文件 ID。

  
**返回**：表示策略文件 ID 的字符串
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 函数
根据提供的 contentFormats，获取策略是否具有自动或建议规则。

参数：  
* **contentFormat**：确定是否为所提供的任何格式定义规则时要考虑的格式矢量。 将 contentFormats 设置为空矢量指示提供的 contentFormats 为默认格式。



  
**返回**：一个布尔值，将指示策略中是否存在任何自动或建议规则
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 函数
获取上次提取策略的时间。

  
**返回**：上次提取策略的时间
  
### <a name="getwxpmetadataversion-function"></a>GetWxpMetadataVersion 函数
获取建议的 WXP (Word、Excel、Powerpoint) 元数据版本，当前为0（对于共同创作启用版本，则为旧版本1）。

  
**返回**： Uint32_t int indecating 租户支持 WXP 文件的元数据版本。