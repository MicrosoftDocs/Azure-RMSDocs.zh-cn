---
title: class mip PolicyEngine
description: class mip PolicyEngine 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 57dd325e9c00a3cb2a4056f7ef0b522efef5d0c4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446033"
---
# <a name="class-mippolicyengine"></a>class mip::PolicyEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  获取策略引擎[设置](class_mip_policyengine_settings.md)。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  列出与策略引擎关联的敏感度标签。
 public const std::string& GetMoreInfoUrl() const  |  提供用于查找有关策略/标签详细信息的 URL。
 public bool IsLabelingRequired() const  |  检查策略是否规定必须标记文档。
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  获取默认敏感度标签。
public std::shared_ptr<PolicyHandler> CreatePolicyHandler(const std::string& contentIdentifier)  |  创建策略处理程序以在文件的执行状态下执行与策略相关的功能。
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  将特定于应用程序的事件记录到审核管道。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取策略引擎[设置](class_mip_policyengine_settings.md)。

  
**返回结果**：策略引擎设置。 
  
另请参阅：[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Label
列出与策略引擎关联的敏感度标签。

  
**返回结果**：敏感度标签列表。
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
提供用于查找有关策略/标签详细信息的 URL。

  
**返回结果**：字符串格式的 URL。
  
### <a name="islabelingrequired"></a>IsLabelingRequired
检查策略是否规定必须标记文档。

  
**返回结果**：如果标记是必需的，则返回 True，否则返回 False。
  
### <a name="label"></a>Label
获取默认敏感度标签。

  
**返回结果**：如果存在，则返回默认敏感度标签，如果未设置默认标签，则返回 nullptr。
  
### <a name="policyhandler"></a>PolicyHandler
创建策略处理程序以在文件的执行状态下执行与策略相关的功能。

参数：  
* **contentIdentifier**：内容的可读标识符。 文件示例："C:\mip-sdk-for-cpp\files\audit.docx" [路径] 电子邮件示例："RE: Audit design:user1@contoso.com" [主题：发件人]



  
**返回结果**：策略处理程序。
  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
将特定于应用程序的事件记录到审核管道。

参数：  
* **description**：日志级别：信息/错误/警告 


* **eventType**：事件类型的说明 


* **eventData**：与事件关联的数据

