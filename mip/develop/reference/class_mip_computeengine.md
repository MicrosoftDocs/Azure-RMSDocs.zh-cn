---
title: 类 ComputeEngine
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 computeengine：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 7371c72cb10e1f08fcacaf286597f9534737996d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565212"
---
# <a name="class-computeengine"></a>类 ComputeEngine 
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const std：： vector \<std::shared_ptr\<Label\> \>& ListSensitivityLabels ( # A2  | _尚无记录。_
public std：： shared_ptr \<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& context，Const DocumentState& 状态)   | _尚无记录。_
public std：： vector \<std::shared_ptr\<Action\> \> ComputeActions (ComputeEngineContext& context，const documentState& DocumentState，const ApplicationActionState& actionState)   | _尚无记录。_
公共 std：:p 气流 \<std::vector\<std::shared_ptr\<Action\> \> 、bool \> ComputeActionsWithRemoteState (ComputeEngineContext& 上下文、Const DocumentState& LocalDocumentState、Const DocumentState& RemoteDocumentState、Const ApplicationActionState& actionState)   |  在远程状态和本地状态之间进行选择时计算操作。
public void NotifyCommittedActions (ComputeEngineContext& context，const DocumentState& documentState，const ApplicationActionState& actionState)   | _尚无记录。_
public const std：： shared_ptr \<Label\>& GetDefaultLabel ( # A2 const  | _尚无记录。_
public const std::string& GetMoreInfoUrl() const  | _尚无记录。_
public const std：： string& GetUpn ( # A2 const  | _尚无记录。_
public bool IsLabelingRequired() const  | _尚无记录。_
public const std：： string& GetFileId ( # A2 const  | _尚无记录。_
public bool HasClassificationRules ( # A1 const  | _尚无记录。_
public bool IsEnhancedClassificationEnabled ( # A1 const  | _尚无记录。_
public std：： shared_ptr \<Label\> GetLabelById (const std：： string& id) const  | _尚无记录。_
public const std：： string& GetTenantId ( # A2 const  | _尚无记录。_
public void SetSensitivityTypesRulePackages (std：： vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \> && 自定义)   | _尚无记录。_
public const std：： vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& GetSensitivityTypesRulePackages ( # A2 const  | _尚无记录。_
public const std：： vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings ( # A2 const  | _尚无记录。_
public uint32_t GetOpcMetadataVersion ( # A1 const  | _尚无记录。_
public const std：： string& GetUserObjectId ( # A2 const  | _尚无记录。_
public virtual ~ ComputeEngine ( # A1  | _尚无记录。_
  
## <a name="members"></a>成员
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 函数
尚无记录。

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 函数
尚无记录。

  
### <a name="computeactions-function"></a>ComputeActions 函数
尚无记录。

  
### <a name="computeactionswithremotestate-function"></a>ComputeActionsWithRemoteState 函数
在远程状态和本地状态之间进行选择时计算操作。
使用此优先级选择状态。 未知的保护类型、 (模板或临时的) 不在策略中。 保护状态始终优于 "未保护" 状态。 带有标签的文档状态在没有的情况下优先。 推荐的标签顺序越高。 标签时间戳，喜欢最新的标记文档。 DocumentState LastModifiedTime （可选），首选新修改的文件。

参数：  
* **上下文**：计算机引擎上下文。 


* **localDocumentState**：本地文档状态。 


* **remoteDocumentState**：远程文档状态。 


* **actionState**：应用程序的操作状态。



  
**返回**：方法返回成对。 首先包含操作的列表，第二个操作是应在本地应用的操作，如果应在远程文档上应用错误操作并且应使用文档状态，则为。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 函数
尚无记录。

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel 函数
尚无记录。

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 函数
尚无记录。

  
### <a name="getupn-function"></a>GetUpn 函数
尚无记录。

  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 函数
尚无记录。

  
### <a name="getfileid-function"></a>GetFileId 函数
尚无记录。

  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 函数
尚无记录。

  
### <a name="isenhancedclassificationenabled-function"></a>IsEnhancedClassificationEnabled 函数
尚无记录。

  
### <a name="getlabelbyid-function"></a>GetLabelById 函数
尚无记录。

  
### <a name="gettenantid-function"></a>GetTenantId 函数
尚无记录。

  
### <a name="setsensitivitytypesrulepackages-function"></a>SetSensitivityTypesRulePackages 函数
尚无记录。

  
### <a name="getsensitivitytypesrulepackages-function"></a>GetSensitivityTypesRulePackages 函数
尚无记录。

  
### <a name="getcustomsettings-function"></a>GetCustomSettings 函数
尚无记录。

  
### <a name="getopcmetadataversion-function"></a>GetOpcMetadataVersion 函数
尚无记录。

  
### <a name="getuserobjectid-function"></a>GetUserObjectId 函数
尚无记录。

  
### <a name="computeengine-function"></a>~ ComputeEngine 函数
尚无记录。
