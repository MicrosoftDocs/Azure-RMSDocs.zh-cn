---
title: 类 mip::ProtectionEngine
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p rotectionengine 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 23f9f54a3f9701d0c9321b7ba643ed7dd3f47be1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486828"
---
# <a name="class-mipprotectionengine"></a>类 mip::ProtectionEngine 
管理与特定标识有关的保护相关操作。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取引擎设置。
public std：： shared_ptr\<AsyncControl\> GetTemplatesAsync （const std：： shared_ptr\<ProtectionEngine：： Observer\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用模板的集合。
公共 std：： vector\<std：： shared_ptr\<TemplateDescriptor\>\> Templatedescriptor.gettemplates （const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用模板的集合。
public bool IsFeatureSupported （FeatureId featureId）  |  勾选功能是否受支持。
public std：： shared_ptr\<AsyncControl\> GetRightsForLabelIdAsync （const std：： string & documentId，const std：： string & 面部，const std：： string & ownerEmail，const std：： & delegatedUserEmail，const std：： shared_ptr\<ProtectionEngine：：\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用于标签 ID 的权限集合。
public std：： vector\<std：： string\> GetRightsForLabelId （const std：： string & documentId，const std：： string & 面部，const std：： string & delegatedUserEmail，const std：： & shared_ptr void\<\>上下文）  |  获取用户可用于 labelId 的权限集合。
public std：： shared_ptr\<AsyncControl\> CreateProtectionHandlerForPublishingAsync （const ProtectionHandler：:P ublishingSettings & 设置，const std：： shared_ptr\<ProtectionHandler：： Observer\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing （const ProtectionHandler：:P ublishingSettings & settings，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<AsyncControl\> CreateProtectionHandlerForConsumptionAsync （const ProtectionHandler：： ConsumptionSettings & settings，const std：： shared_ptr\<ProtectionHandler：： Observer\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption （const ProtectionHandler：： ConsumptionSettings & settings，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public bool LoadUserCert （const std：： shared_ptr\<void\>& 上下文）  |  预先加载用户许可方证书，在使用 prelicense 的后台加载其他情况下非常有用。
public std：： shared_ptr\<AsyncControl\> LoadUserCertAsync （const std：： shared_ptr\<ProtectionEngine：： Observer\>& 观察程序，const std：： shared_ptr\<void\>& 上下文）  |  预先加载用户许可方证书，在使用 prelicense 的后台加载其他情况下非常有用。
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings 函数
获取引擎设置。

  
**返回结果**：引擎设置
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync 函数
获取用户可用模板的集合。

参数：  
* **观察**程序：一个实现 ProtectionEngine：： observer 接口的类 


* **上下文**：将以不透明的形式传递回观察者和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。
  
### <a name="gettemplates-function"></a>Templatedescriptor.gettemplates 函数
获取用户可用模板的集合。

参数：  
* **上下文**：将以不透明的形式传递到可选 HttpDelegate 的客户端上下文



  
**返回结果**：模板 ID 列表
  
### <a name="isfeaturesupported-function"></a>IsFeatureSupported 函数
勾选功能是否受支持。

参数：  
* **featureId**：要检查的功能的 id



  
**返回**：布尔值结果
  
### <a name="getrightsforlabelidasync-function"></a>GetRightsForLabelIdAsync 函数
获取用户可用于标签 ID 的权限集合。

参数：  
* **documentId**：与文档元数据关联的文档 ID 


* **面部**：与文档所创建的文档元数据关联的标签 ID 


* **ownerEmail**：文档的所有者 


* **答**：当身份验证用户/应用程序代表另一个用户时指定了委派的用户，如果没有，则为空 


* **观察**程序：一个实现 ProtectionEngine：： observer 接口的类 


* **上下文**：此相同的上下文将转发到 ProtectionEngine：： observer：： OnGetRightsForLabelIdSuccess 或 ProtectionEngine：： observer：： OnGetRightsForLabelIdFailure



  
**返回**： Async control 对象。
  
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



  
**返回**： Async control 对象。
  
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



  
**返回**： Async control 对象。
  
### <a name="createprotectionhandlerforconsumption-function"></a>CreateProtectionHandlerForConsumption 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**：保护设置 


* **上下文**：将以不透明转发到可选 HttpDelegate 的客户端上下文



  
**返回**： ProtectionHandler
  
### <a name="loadusercert-function"></a>LoadUserCert 函数
预先加载用户许可方证书，在使用 prelicense 的后台加载其他情况下非常有用。

参数：  
* **上下文**：将以不透明转发到可选 HttpDelegate 的客户端上下文



  
**返回**：如果成功加载，则为 True; 否则为 false。
  
### <a name="loadusercertasync-function"></a>LoadUserCertAsync 函数
预先加载用户许可方证书，在使用 prelicense 的后台加载其他情况下非常有用。

参数：  
* **观察**程序：一个实现 ProtectionHandler：： observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。