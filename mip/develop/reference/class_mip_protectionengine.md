---
title: 类 mip::ProtectionEngine
description: 记录 mip::protectionengine 类的 Microsoft 信息保护 (MIP) SDK。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d12fbe050ba86dbcef58dada971134c96dc637d1
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252905"
---
# <a name="class-mipprotectionengine"></a>类 mip::ProtectionEngine 
管理与特定标识有关的保护相关操作。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取引擎设置。
public void GetTemplatesAsync (const std::\<ProtectionEngine::Observer\>& observer，const std:: shared_ptr\<void\>& 上下文)  |  获取用户可用模板的集合。
public std::vector\<std::string\> GetTemplates(const std::shared_ptr\<void\>& context)  |  获取用户可用模板的集合。
public void GetRightsForLabelIdAsync (const std:: string & documentId，const std:: string & labelId，const std:: string & ownerEmail，const std::\<ProtectionEngine::Observer\>& observer，const std:: shared_ptr\<void\>& 上下文)  |  获取用户可用于标签 ID 的权限集合。
public std:: vector\<std:: string\> GetRightsForLabelId (const std:: string & documentId，const std:: string & labelId，const std:: string & ownerEmail，const std:: shared_ptr\<void\>& 上下文)  |  获取用户可用于 labelId 的权限集合。
public void CreateProtectionHandlerFromDescriptorAsync (const std::\<ProtectionDescriptor\>& 描述符，const ProtectionHandlerCreationOptions 和选项、 const std:: shared_ptr\<ProtectionHandler::Observer\>& observer，const std:: shared_ptr\<void\>& 上下文)  |  创建将权限/角色分配给特定用户的保护处理程序。
public std::\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std:: shared_ptr\<ProtectionDescriptor\>& 描述符，const ProtectionHandlerCreationOptions& 选项、 const std:: shared_ptr\<void\>& 上下文)  |  创建将权限/角色分配给特定用户的保护处理程序。
public void CreateProtectionHandlerFromPublishingLicenseAsync (const std:: vector\<uint8_t\>& serializedPublishingLicense，const ProtectionHandlerCreationOptions 和选项，const std:: shared_ptr\<ProtectionHandler::Observer\>& observer，const std:: shared_ptr\<void\>& 上下文)  |  根据序列化发布许可证创建保护处理程序。
public std::\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std:: vector\<uint8_t\>& serializedPublishingLicense，constProtectionHandlerCreationOptions 和选项、 const std:: shared_ptr\<void\>& 上下文)  |  根据序列化发布许可证创建保护处理程序。
public void CreateProtectionHandlerFromProtectionInfoAsync (const std:: vector\<uint8_t\>& serializedPublishingLicense，const std:: vector\<uint8_t\>& serializedProtectionInfo，const std:: shared_ptr\<ProtectionHandler::Observer\>& observer，const std:: shared_ptr\<void\>& 上下文)  |  从序列化的发布许可证和序列化的保护信息创建一个保护处理程序。
public std::\<ProtectionHandler\> CreateProtectionHandlerFromProtectionInfo (const std:: vector\<uint8_t\>& serializedPublishingLicense，const std:: vector\<uint8_t\>& serializedProtectionInfo，const std:: shared_ptr\<void\>& 上下文)  |  从序列化的发布许可证和序列化的保护信息创建一个保护处理程序。
public void CreateProtectionHandlerFromPublishingLicenseContextAsync (const PublishingLicenseContext & publishingLicenseContext，const ProtectionHandlerCreationOptions 和选项，const std::\<ProtectionHandler::Observer\>& observer，const std:: shared_ptr\<void\>& 上下文)  |  根据发布许可证上下文创建保护处理程序。
public std::\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicenseContext (const PublishingLicenseContext & publishingLicenseContext，const ProtectionHandlerCreationOptions （& a)选项、 const std:: shared_ptr\<void\>& 上下文)  |  根据发布许可证上下文创建保护处理程序。
  
## <a name="members"></a>成員
  
### <a name="getsettings-function"></a>GetSettings 函数
获取引擎设置。

  
**返回**:引擎设置
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync 函数
获取用户可用模板的集合。

参数：  
* **observer**:类实现[ProtectionEngine::Observer](class_mip_protectionengine_observer.md)接口 


* **上下文**:将以不透明形式传递回观察程序和可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="gettemplates-function"></a>GetTemplates 函数
获取用户可用模板的集合。

参数：  
* **上下文**:将以不透明形式传递到可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)



  
**返回**:模板 Id 的列表
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync function
获取用户可用于标签 ID 的权限集合。

参数：  
* **documentId**:文档元数据与关联的文档 ID 


* **labelId**:[标签](class_mip_label.md)创建文档的文档元数据与关联 ID 


* **ownerEmail**：文档的所有者 


* **observer**:类实现[ProtectionEngine::Observer](class_mip_protectionengine_observer.md)接口 


* **上下文**:此上下文将转发到[ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)或[ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 函数
获取用户可用于 labelId 的权限集合。

参数：  
* **documentId**:文档元数据与关联的文档 ID 


* **labelId**:[标签](class_mip_label.md)创建文档的文档元数据与关联 ID 


* **ownerEmail**:文档的所有者 


* **上下文**:此上下文将转发到可选[HttpDelegate](class_mip_httpdelegate.md)



  
**返回**:权限的列表
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>CreateProtectionHandlerFromDescriptorAsync 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **描述符**:一个[ProtectionDescriptor](class_mip_protectiondescriptor.md)描述的保护配置 


* **选项**:创建选项 


* **observer**:类实现[ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)接口 


* **上下文**:将以不透明形式传递回观察程序和可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfromdescriptor-function"></a>CreateProtectionHandlerFromDescriptor 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **描述符**:一个[ProtectionDescriptor](class_mip_protectiondescriptor.md)描述的保护配置 


* **选项**:创建选项 


* **上下文**:将以不透明形式传递回可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>CreateProtectionHandlerFromPublishingLicenseAsync 函数
根据序列化发布许可证创建保护处理程序。

参数：  
* **serializedPublishingLicense**:序列化的发布许可证 


* **选项**:创建选项 


* **observer**:类实现[ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)接口 


* **上下文**:将以不透明形式传递回观察程序和可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>CreateProtectionHandlerFromPublishingLicense 函数
根据序列化发布许可证创建保护处理程序。

参数：  
* **serializedPublishingLicense**:序列化的发布许可证 


* **选项**:创建选项 


* **observer**:类实现[ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)接口 


* **上下文**:将以不透明形式传递回可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfromprotectioninfoasync-function"></a>CreateProtectionHandlerFromProtectionInfoAsync 函数
从序列化的发布许可证和序列化的保护信息创建一个保护处理程序。

参数：  
* **serializedPublishingLicense**:序列化的发布许可证 


* **serializedProtectionInfo**:序列化的保护信息 


* **observer**:类实现[ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)接口 


* **上下文**:将以不透明形式传递回观察程序的客户端上下文


  
### <a name="createprotectionhandlerfromprotectioninfo-function"></a>CreateProtectionHandlerFromProtectionInfo 函数
从序列化的发布许可证和序列化的保护信息创建一个保护处理程序。

参数：  
* **serializedPublishingLicense**:序列化的发布许可证 


* **serializedProtectionInfo**:序列化的保护信息 


* **上下文**:将以不透明形式传递回观察程序的客户端上下文



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerfrompublishinglicensecontextasync-function"></a>CreateProtectionHandlerFromPublishingLicenseContextAsync 函数
根据发布许可证上下文创建保护处理程序。

参数：  
* **publishingLicenseContext**:序列化的发布许可证预先处理窗体 


* **选项**:创建选项 


* **observer**:类实现[ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)接口 


* **上下文**:将以不透明形式传递回观察程序和可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)


  
### <a name="createprotectionhandlerfrompublishinglicensecontext-function"></a>CreateProtectionHandlerFromPublishingLicenseContext 函数
根据发布许可证上下文创建保护处理程序。

参数：  
* **publishingLicenseContext**:序列化的发布许可证预先处理窗体 


* **选项**:创建选项 


* **observer**:类实现[ProtectionHandler::Observer](class_mip_protectionhandler_observer.md)接口 


* **上下文**:将以不透明形式传递回可选的客户端上下文[HttpDelegate](class_mip_httpdelegate.md)



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)
