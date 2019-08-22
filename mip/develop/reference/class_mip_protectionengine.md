---
title: 类 mip::ProtectionEngine
description: 记录 Microsoft 信息保护 (MIP) SDK 的 mip::p rotectionengine 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 88cb6565e8e392a83d01ded79186cf7dbb6fb43c
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883502"
---
# <a name="class-mipprotectionengine"></a>类 mip::ProtectionEngine 
管理与特定标识有关的保护相关操作。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取引擎设置。
public void GetTemplatesAsync (const std:: shared_ptr\<ProtectionEngine:: observer\>& 观察程序, const std::\<shared_ptr\>void & context)  |  获取用户可用模板的集合。
public std:: vector\<std:: string\> templatedescriptor.gettemplates (const std:: shared_ptr\<void\>& 上下文)  |  获取用户可用模板的集合。
public void GetRightsForLabelIdAsync (const std:: string & documentId, const std:: string & 面部, const std:: string & ownerEmail, const std:: string & delegatedUserEmail, const std:: shared_ptr\<ProtectionEngine:: Observer\>& 观察程序, const std::\<shared_ptr\>void & context)  |  获取用户可用于标签 ID 的权限集合。
public std:: vector\<std:: string\> GetRightsForLabelId (const std:: string & documentId, const std:: string & 面部, const std:: string & ownerEmail, const std:: string & delegatedUserEmail, const std:: shared_ptr\<void\>& 上下文)  |  获取用户可用于 labelId 的权限集合。
public void CreateProtectionHandlerFromDescriptorAsync (const std:: shared_ptr\<ProtectionDescriptor\>& 说明符, const ProtectionHandlerCreationOptions & options, const std:: shared_ptr\<ProtectionHandler:: observer\>& 观察程序, const std::\<shared_ptr\>void & 上下文)  |  创建将权限/角色分配给特定用户的保护处理程序。
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromDescriptor (const std:: shared_ptr\<ProtectionDescriptor\>& 说明符, const ProtectionHandlerCreationOptions& 选项, const std:: shared_ptr\<void\>& context)  |  创建将权限/角色分配给特定用户的保护处理程序。
public void CreateProtectionHandlerFromPublishingLicenseAsync (const std:: vector\<uint8_t\>& serializedPublishingLicense, const ProtectionHandlerCreationOptions & options, const std:: shared_ptr\<ProtectionHandler:: observer\>& 观察程序, const std::\<shared_ptr\>void & 上下文)  |  根据序列化发布许可证创建保护处理程序。
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerFromPublishingLicense (const std:: vector\<uint8_t\>& serializedPublishingLicense, constProtectionHandlerCreationOptions & 选项, const std:: shared_ptr\<void\>& 上下文)  |  根据序列化发布许可证创建保护处理程序。
public void CreateProtectionHandlerForPublishingAsync (const ProtectionHandler::P ublishingsettings & settings, const std:: shared_ptr\<ProtectionHandler:: observer\>& 观察程序, const std:: shared_ptr\<void\>& 上下文)  |  创建将权限/角色分配给特定用户的保护处理程序。
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing (const ProtectionHandler::P ublishingsettings & settings, const std:: shared_ptr\<void\>& 上下文)  |  创建将权限/角色分配给特定用户的保护处理程序。
public void CreateProtectionHandlerForConsumptionAsync (const ProtectionHandler:: ConsumptionSettings & settings, const std:: shared_ptr\<ProtectionHandler:: observer\>& 观察程序, const std:: shared_ptr\<void\>& 上下文)  |  创建将权限/角色分配给特定用户的保护处理程序。
public std:: shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption (const ProtectionHandler:: ConsumptionSettings & settings, const std:: shared_ptr\<void\>& context)  |  创建将权限/角色分配给特定用户的保护处理程序。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取引擎设置。

  
**返回**:引擎设置
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync 函数
获取用户可用模板的集合。

参数：  
* **观察**程序:实现[ProtectionEngine:: Observer](class_mip_protectionengine_observer.md)接口的类 


* **上下文**:将以不透明的形式传递回观察者和可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文


  
### <a name="gettemplates-function"></a>Templatedescriptor.gettemplates 函数
获取用户可用模板的集合。

参数：  
* **上下文**:将以不透明形式传递到可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文



  
**返回**:模板 Id 列表
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 函数
获取用户可用于标签 ID 的权限集合。

参数：  
* **documentId**:与文档元数据关联的文档 ID 


* **面部**:[标签](class_mip_label.md)与文档所创建的文档元数据关联的 ID 


* **ownerEmail**：文档的所有者 


* **答**: 当身份验证用户/应用程序代表另一个用户时指定了委派的用户, 如果没有, 则为空 


* **观察**程序:实现[ProtectionEngine:: Observer](class_mip_protectionengine_observer.md)接口的类 


* **上下文**:此相同的上下文将转发到[ProtectionEngine:: observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function)或[ProtectionEngine:: Observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 函数
获取用户可用于 labelId 的权限集合。

参数：  
* **documentId**:与文档元数据关联的文档 ID 


* **面部**:[标签](class_mip_label.md)与文档所创建的文档元数据关联的 ID 


* **ownerEmail**:文档的所有者 


* **答**: 当身份验证用户/应用程序代表另一个用户时指定了委派的用户, 如果没有, 则为空 


* **上下文**:此相同的上下文将转发到可选[HttpDelegate](class_mip_httpdelegate.md)



  
**返回**:权限列表
  
### <a name="createprotectionhandlerfromdescriptorasync-function"></a>CreateProtectionHandlerFromDescriptorAsync 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **描述符**:描述保护配置的[ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **选项**:创建选项 


* **观察**程序:实现[ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md)接口的类 


* **上下文**:将以不透明的形式传递回观察者和可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文


> 弃用此方法将很快弃用, 以支持 CreateProtectionHandlerForPublishingAsync
  
### <a name="createprotectionhandlerfromdescriptor-function"></a>CreateProtectionHandlerFromDescriptor 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **描述符**:描述保护配置的[ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **选项**:创建选项 


* **上下文**:将以不透明形式传递回可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)
> 弃用此方法将很快弃用, 以支持 CreateProtectionHandlerForPublishingAsync
  
### <a name="createprotectionhandlerfrompublishinglicenseasync-function"></a>CreateProtectionHandlerFromPublishingLicenseAsync 函数
根据序列化发布许可证创建保护处理程序。

参数：  
* **serializedPublishingLicense**:序列化发布许可证 


* **选项**:创建选项 


* **观察**程序:实现[ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md)接口的类 


* **上下文**:将以不透明的形式传递回观察者和可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文


> 弃用此方法将很快弃用, 以支持 CreateProtectionHandlerForConsumptionAsync
  
### <a name="createprotectionhandlerfrompublishinglicense-function"></a>CreateProtectionHandlerFromPublishingLicense 函数
根据序列化发布许可证创建保护处理程序。

参数：  
* **serializedPublishingLicense**:序列化发布许可证 


* **选项**:创建选项 


* **观察**程序:实现[ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md)接口的类 


* **上下文**:将以不透明形式传递回可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)
> 弃用此方法将很快弃用, 以支持 CreateProtectionHandlerForConsumption
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**:保护设置 


* **观察**程序:实现[ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md)接口的类 


* **上下文**:将以不透明转发到观察者和可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文


  
### <a name="createprotectionhandlerforpublishing-function"></a>CreateProtectionHandlerForPublishing 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**:保护设置 


* **上下文**:将以不透明转发到可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**:保护设置 


* **观察**程序:实现[ProtectionHandler:: Observer](class_mip_protectionhandler_observer.md)接口的类 


* **上下文**:将以不透明转发到观察者和可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文


  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**:保护设置 


* **上下文**:将以不透明转发到可选[HttpDelegate](class_mip_httpdelegate.md)的客户端上下文



  
**返回**:[ProtectionHandler](class_mip_protectionhandler.md)