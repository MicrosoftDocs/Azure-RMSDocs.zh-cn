---
title: 类 mip::ProtectionEngine
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionengine 类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 9eb44a39f32c2997729e6d77ddace96c580328cd
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73557746"
---
# <a name="class-mipprotectionengine"></a>类 mip::ProtectionEngine 
管理与特定标识有关的保护相关操作。
  
## <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取引擎设置。
public void GetTemplatesAsync （const std：： shared_ptr\<ProtectionEngine：： Observer\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用模板的集合。
public std：： vector\<std：： string\> Templatedescriptor.gettemplates （const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用模板的集合。
public void GetRightsForLabelIdAsync （const std：： string & documentId，const std：： string & 面部，const std：： string & ownerEmail，const std：： string & delegatedUserEmail，const std：： shared_ptr\<ProtectionEngine：： Observer\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用于标签 ID 的权限集合。
public std：： vector\<std：： string\> GetRightsForLabelId （const std：： string & documentId，const std：： string & 面部，const std：： string & delegatedUserEmail，const std：： & shared_ptr void\<\>上下文）  |  获取用户可用于 labelId 的权限集合。
public void CreateProtectionHandlerForPublishingAsync （const ProtectionHandler：:P ublishingSettings & settings，const std：： shared_ptr\<ProtectionHandler：： Observer\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing （const ProtectionHandler：:P ublishingSettings & settings，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public void CreateProtectionHandlerForConsumptionAsync （const ProtectionHandler：： ConsumptionSettings & settings，const std：： shared_ptr\<ProtectionHandler：：观察器\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption （const ProtectionHandler：： ConsumptionSettings & settings，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
  
## <a name="members"></a>成員
  
### <a name="getsettings-function"></a>GetSettings 函数
获取引擎设置。

  
**返回结果**：引擎设置
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync 函数
获取用户可用模板的集合。

参数：  
* **观察**程序：一个实现 ProtectionEngine：： observer 接口的类 


* **上下文**：将以不透明的形式传递回观察者和可选 HttpDelegate 的客户端上下文


  
### <a name="gettemplates-function"></a>Templatedescriptor.gettemplates 函数
获取用户可用模板的集合。

参数：  
* **上下文**：将以不透明的形式传递到可选 HttpDelegate 的客户端上下文



  
**返回结果**：模板 ID 列表
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 函数
获取用户可用于标签 ID 的权限集合。

参数：  
* **documentId**：与文档元数据关联的文档 ID 


* **面部**：与文档所创建的文档元数据关联的标签 ID 


* **ownerEmail**：文档的所有者 


* **答**：当身份验证用户/应用程序代表另一个用户时指定了委派的用户，如果没有，则为空 


* **观察**程序：一个实现 ProtectionEngine：： observer 接口的类 


* **上下文**：此相同的上下文将转发到 ProtectionEngine：： observer：： OnGetRightsForLabelIdSuccess 或 ProtectionEngine：： observer：： OnGetRightsForLabelIdFailure


  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 函数
获取用户可用于 labelId 的权限集合。

参数：  
* **documentId**：与文档元数据关联的文档 ID 


* **面部**：与文档所创建的文档元数据关联的标签 ID 


* **ownerEmail**：文档的所有者 


* **答**：当身份验证用户/应用程序代表另一个用户时指定了委派的用户，如果没有，则为空 


* **上下文**：此相同的上下文将转发到可选 HttpDelegate



  
**返回结果**：权限列表
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**：保护设置 


* **观察**程序：一个实现 ProtectionHandler：： observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文


  
### <a name="createprotectionhandlerforpublishing-function"></a>CreateProtectionHandlerForPublishing 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**：保护设置 


* **上下文**：将以不透明转发到可选 HttpDelegate 的客户端上下文



  
**返回**： ProtectionHandler
  
### <a name="createprotectionhandlerforconsumptionasync-function"></a>CreateProtectionHandlerForConsumptionAsync 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**：保护设置 


* **观察**程序：一个实现 ProtectionHandler：： observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文


  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**：保护设置 


* **上下文**：将以不透明转发到可选 HttpDelegate 的客户端上下文



  
**返回**： ProtectionHandler