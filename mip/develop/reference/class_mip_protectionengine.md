---
title: 类 mip ProtectionEngine
description: 类 mip ProtectionEngine 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ddc8cfd58acb2a80d024978084b625f3d3728c87
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446730"
---
# <a name="class-mipprotectionengine"></a>类 mip::ProtectionEngine 
管理与特定标识有关的保护相关操作。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  获取引擎设置。
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  获取用户可用模板的集合。
public std::vector<std::string> GetTemplates(const std::shared_ptr<void>& context)  |  获取用户可用模板的集合。
public void GetRightsForLabelIdAsync(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  获取用户可用于标签 ID 的权限集合。
public std::vector<std::string> GetRightsForLabelId(const std::string& documentId, const std::string& labelId, const std::string& ownerEmail, const std::shared_ptr<void>& context)  |  获取用户可用于 labelId 的权限集合。
public void GetGrantingLabelIdsAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  获取用户可用标签 ID 的集合。
public std::vector<std::string> GetGrantingLabelIds(const std::shared_ptr<void>& context)  |  获取用户可用标签 ID 的集合。
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  创建将权限/角色分配给特定用户的保护处理程序。
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromDescriptor(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  创建将权限/角色分配给特定用户的保护处理程序。
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  根据序列化发布许可证创建保护处理程序。
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicense(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  根据序列化发布许可证创建保护处理程序。
public void CreateProtectionHandlerFromPublishingLicenseContextAsync(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  根据发布许可证上下文创建保护处理程序。
public std::shared_ptr<ProtectionHandler> CreateProtectionHandlerFromPublishingLicenseContext(const PublishingLicenseContext& publishingLicenseContext, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<void>& context)  |  根据发布许可证上下文创建保护处理程序。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取引擎设置。

  
**返回结果**：引擎设置
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
获取用户可用模板的集合。

参数：  
* **observer**：实现 [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 接口的类 


* **context**：将以不透明形式传递回观察程序和可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文


  
### <a name="gettemplates"></a>GetTemplates
获取用户可用模板的集合。

参数：  
* **context**：将以不透明形式传递给可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文



  
**返回结果**：模板 ID 列表
  
### <a name="getrightsforlabelidasync"></a>GetRightsForLabelIdAsync
获取用户可用于标签 ID 的权限集合。

参数：  
* **documentId**：与文档元数据关联的文档 ID 


* **labelId**：与用于创建文档的文档元数据关联的[标签](class_mip_label.md) ID 


* **ownerEmail**：文档的所有者 


* **observer**：实现 [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 接口的类 


* **context**：此相同上下文将转发到 [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) 或 [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)


  
### <a name="getrightsforlabelid"></a>GetRightsForLabelId
获取用户可用于 labelId 的权限集合。

参数：  
* **documentId**：与文档元数据关联的文档 ID 


* **labelId**：与用于创建文档的文档元数据关联的[标签](class_mip_label.md) ID 


* **ownerEmail**：文档的所有者 


* **context**：此相同上下文将转发到可选的 [HttpDelegate](class_mip_httpdelegate.md)



  
**返回结果**：权限列表
  
### <a name="getgrantinglabelidsasync"></a>GetGrantingLabelIdsAsync
获取用户可用标签 ID 的集合。

参数：  
* **observer**：实现 [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 接口的类 


* **context**：此相同上下文将转发到 [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) 或 ProtectionEngine::Observer::OnGrantingLabelIdsFailure


  
### <a name="getgrantinglabelids"></a>GetGrantingLabelIds
获取用户可用标签 ID 的集合。

参数：  
* **context**：此相同上下文将转发到可选的 [HttpDelegate](class_mip_httpdelegate.md)



  
**返回结果**：标签 ID 列表
  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **descriptor**：描述保护配置的 [ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **options**：“创建”选项 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


* **context**：将以不透明形式传递回观察程序和可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文


  
### <a name="protectionhandler"></a>ProtectionHandler
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **descriptor**：描述保护配置的 [ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **options**：“创建”选项 


* **context**：将以不透明形式传递回可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文



  
**返回结果**：[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
根据序列化发布许可证创建保护处理程序。

参数：  
* **serializedPublishingLicense**：序列化的发布许可证 


* **options**：“创建”选项 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


* **context**：将以不透明形式传递回观察程序和可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文


  
### <a name="protectionhandler"></a>ProtectionHandler
根据序列化发布许可证创建保护处理程序。

参数：  
* **serializedPublishingLicense**：序列化的发布许可证 


* **options**：“创建”选项 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


* **context**：将以不透明形式传递回可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文



  
**返回结果**：[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync
根据发布许可证上下文创建保护处理程序。

参数：  
* **publishingLicenseContext**：序列化发布许可证的预处理形式 


* **options**：“创建”选项 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


* **context**：将以不透明形式传递回观察程序和可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文


  
### <a name="protectionhandler"></a>ProtectionHandler
根据发布许可证上下文创建保护处理程序。

参数：  
* **publishingLicenseContext**：序列化发布许可证的预处理形式 


* **options**：“创建”选项 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


* **context**：将以不透明形式传递回可选 [HttpDelegate](class_mip_httpdelegate.md) 的客户端上下文



  
**返回结果**：[ProtectionHandler](class_mip_protectionhandler.md)