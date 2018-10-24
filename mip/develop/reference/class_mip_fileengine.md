---
title: class mip FileEngine
description: class mip FileEngine 的引用
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7342edf27b19f43881b2e8d378fa243d26f7056
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446067"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  返回引擎设置。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  返回敏感度标签列表。
 public const std::string& GetMoreInfoUrl() const  |  提供用于查找有关策略/标签详细信息的 URL。
 public bool IsLabelingRequired() const  |  检查策略是否规定必须标记文档。
public void CreateFileHandlerAsync(const std::string& inputFilePath, const ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  开始创建给定文件路径的文件处理程序。
public void CreateFileHandlerAsync(const std::shared_ptr<Stream>& inputStream, const std::string& inputFilePath, const mip::ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  开始创建给定文件流的文件处理程序。
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  将特定于应用程序的事件记录到审核管道。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
返回引擎设置。
  
### <a name="label"></a>Label
返回敏感度标签列表。
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
提供用于查找有关策略/标签详细信息的 URL。

  
**返回结果**：字符串格式的 URL。
  
### <a name="islabelingrequired"></a>IsLabelingRequired
检查策略是否规定必须标记文档。

  
**返回结果**：如果标记是必需的，则返回 True，否则返回 False。
  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
开始创建给定文件路径的文件处理程序。

参数：  
* 要打开的文件。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 


* **contentState**：应用程序与之交互时的内容状态。 


* 实现 [FileHandler::Observer](class_mip_filehandler_observer.md) 接口的类。 


* **context**：将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
开始创建给定文件流的文件处理程序。

参数：  
* **inputStream**：包含文件数据的流。 


* **inputFilePath**：文件路径。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 


* **contentState**：应用程序与之交互时的内容状态。 


* **fileHandlerObserver**：实现 [FileHandler::Observer](class_mip_filehandler_observer.md) 接口的类。 


* **context**：将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
将特定于应用程序的事件记录到审核管道。

参数：  
* **level**：日志级别说明：信息/错误/警告 


* **eventType**：事件类型的说明 


* **eventData**：与事件关联的数据

