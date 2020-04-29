---
title: 类 ProtectionEngine
description: 记录 Microsoft 信息保护（MIP） SDK 的 protectionengine：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 61311ec2ac7c622099e9e7f56f22191e0287278c
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763920"
---
# <a name="class-protectionengine"></a>类 ProtectionEngine 
管理与特定标识有关的保护相关操作。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取引擎设置。
public std：： shared_ptr\<AsyncControl\> GetTemplatesAsync （const std：： Shared_ptr\<ProtectionEngine：： observer\>& 观察程序，const std：：\<shared_ptr\> void& 上下文）  |  获取用户可用模板的集合。
public std：： vector\<std：： shared_ptr\<TemplateDescriptor\> \> templatedescriptor.gettemplates （const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用模板的集合。
public bool IsFeatureSupported （FeatureId featureId）  |  勾选功能是否受支持。
public std：： shared_ptr\<AsyncControl\> GetRightsForLabelIdAsync （const std：： string& documentId，const std：： string，const std：： string& 面部，const std：： string& ownerEmail，const std：：&\<delegatedUserEmail：： Observer\> shared_ptr 观察程序，const std：：\<&\> void shared_ptr 的上下文）  |  获取用户可用于标签 ID 的权限集合。
public std：： vector\<std：： string\> GetRightsForLabelId （const std：： string& documentId，const std：： string& 面部，const std：： string& ownerEmail，const std：： string& delegatedUserEmail，const std：： shared_ptr\<void\>& 上下文）  |  获取用户可用于 labelId 的权限集合。
public std：： shared_ptr\<AsyncControl\> CreateProtectionHandlerForPublishingAsync （Const ProtectionHandler：:P ublishingsettings& settings，const std：： Shared_ptr\<ProtectionHandler：： observer\>& 观察程序，const std：：\<shared_ptr\> void& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForPublishing （Const ProtectionHandler：:P ublishingsettings& settings，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<AsyncControl\> CreateProtectionHandlerForConsumptionAsync （Const ProtectionHandler：： ConsumptionSettings& settings，const std：： Shared_ptr\<ProtectionHandler：： observer\>& 观察程序，const std：：\<shared_ptr\> void& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public std：： shared_ptr\<ProtectionHandler\> CreateProtectionHandlerForConsumption （Const ProtectionHandler：： ConsumptionSettings& settings，const std：： shared_ptr\<void\>& 上下文）  |  创建将权限/角色分配给特定用户的保护处理程序。
public bool LoadUserCert （const std：： shared_ptr\<void\>& context）  |  预先加载用户许可方证书，在使用 prelicense 的后台加载其他情况下非常有用。
public std：： shared_ptr\<AsyncControl\> LoadUserCertAsync （const std：： Shared_ptr\<ProtectionEngine：： observer\>& 观察程序，const std：：\<shared_ptr\> void& 上下文）  |  预先加载用户许可方证书，在使用 prelicense 的后台加载其他情况下非常有用。
public void RegisterContentForTrackingAndRevocation （const std：： vector\<Uint8_t\>& serializedPublishingLicense，const std：： string& contentName，bool isOwnerNotificationEnabled，const std：： shared_ptr\<void\>& 上下文）  |  为文档跟踪注册发布许可证（PL） & 吊销。
public std：： shared_ptr\<AsyncControl\> RegisterContentForTrackingAndRevocationAsync （const std：： vector\<uint8_t\>& SerializedPublishingLicense，const std：： string& contentName，Bool std：：，bool\<IsOwnerNotificationEnabled，const std\> ：： shared_ptr ProtectionEngine：： Observer&\<观察\>程序，const std：： shared_ptr void& 上下文）  |  为文档跟踪注册发布许可证（PL） & 吊销。
public void RevokeContent （const std：： vector\<Uint8_t\>& serializedPublishingLicense，const std：： shared_ptr\<void\>& 上下文）  |  对内容执行撤消。
public std：： shared_ptr\<AsyncControl\> RevokeContentAsync （const std：： vector\<uint8_t\>& serializedPublishingLicense，Const std：： shared_ptr\<ProtectionEngine：： observer\>& 观察程序，const std：：\<shared_ptr\> void& 上下文）  |  对内容执行撤消。
  
## <a name="members"></a>成员
  
### <a name="getsettings-function"></a>GetSettings 函数
获取引擎设置。

  
**返回结果**：引擎设置
  
### <a name="gettemplatesasync-function"></a>GetTemplatesAsync 函数
获取用户可用模板的集合。

参数：  
* **observer**：实现 [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) 接口的类 


* **context**：将以不透明形式传递回观察程序和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。
  
### <a name="gettemplates-function"></a>Templatedescriptor.gettemplates 函数
获取用户可用模板的集合。

参数：  
* **context**：将以不透明形式传递给可选 HttpDelegate 的客户端上下文



  
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


* **observer**：实现 ProtectionEngine::Observer 接口的类 


* **context**：此相同上下文将转发到 ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess 或 ProtectionEngine::Observer::OnGetRightsForLabelIdFailure



  
**返回**： Async control 对象。
  
### <a name="getrightsforlabelid-function"></a>GetRightsForLabelId 函数
获取用户可用于 labelId 的权限集合。

参数：  
* **documentId**：与文档元数据关联的文档 ID 


* **面部**：与文档所创建的文档元数据关联的标签 ID 


* **ownerEmail**：文档的所有者 


* **答**：当身份验证用户/应用程序代表另一个用户时指定了委派的用户，如果没有，则为空 


* **context**：此相同上下文将转发到可选的 HttpDelegate



  
**返回结果**：权限列表
  
### <a name="createprotectionhandlerforpublishingasync-function"></a>CreateProtectionHandlerForPublishingAsync 函数
创建将权限/角色分配给特定用户的保护处理程序。

参数：  
* **设置**：保护设置 


* **observer**：实现 [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) 接口的类 


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


* **observer**：实现 ProtectionHandler::Observer 接口的类 


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
* **observer**：实现 ProtectionHandler::Observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。
  
### <a name="registercontentfortrackingandrevocation-function"></a>RegisterContentForTrackingAndRevocation 函数
为文档跟踪注册发布许可证（PL） & 吊销。

参数：  
* **contentName**：与 serializedPublishingLicense 指定的内容关联的名称。 如果 serializedPublishingLicense 指定内容名称，则该值将优先。 


* **isOwnerNotificationEnabled**：设置为 true 可在文档解密时通过电子邮件通知所有者，或设置为 false 将不发送通知。 


* **上下文**：将以不透明转发到可选 HttpDelegate 的客户端上下文


  
### <a name="registercontentfortrackingandrevocationasync-function"></a>RegisterContentForTrackingAndRevocationAsync 函数
为文档跟踪注册发布许可证（PL） & 吊销。

参数：  
* **serializedPublishingLicense**：从受保护内容序列化发布许可证 


* **contentName**：与 serializedPublishingLicense 指定的内容关联的名称。 如果 serializedPublishingLicense 指定内容名称，则该值优先 


* **isOwnerNotificationEnabled**：设置为 true 可在文档解密时通过电子邮件通知所有者，或设置为 false 将不发送通知。 


* **observer**：实现 ProtectionHandler::Observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。
  
### <a name="revokecontent-function"></a>RevokeContent 函数
对内容执行撤消。

参数：  
* **serializedPublishingLicense**：从受保护内容序列化发布许可证 


* **上下文**：将以不透明转发到可选 HttpDelegate 的客户端上下文


  
### <a name="revokecontentasync-function"></a>RevokeContentAsync 函数
对内容执行撤消。

参数：  
* **serializedPublishingLicense**：从受保护内容序列化发布许可证 


* **observer**：实现 ProtectionHandler::Observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。