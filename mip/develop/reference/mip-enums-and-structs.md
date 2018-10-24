---
title: “摘要”
description: “摘要”
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 5af209d5a627263399c8c60f474495dcadab24a0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446492"
---
# <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
**common** |
枚举 Consent       |  当请求同意连接到服务终结点时用户的响应。
结构 ApplicationInfo  |  包含应用程序特定信息的结构。
**mip** |
枚举 ErrorType       | _尚无记录。_
enum HttpRequestType       |  HTTP 请求类型。
枚举 LogLevel       |  跨 MIP SDK 使用的不同日志级别。
枚举 ProtectionHandlerCreationOptions       |  指明其他策略创建行为的位标志。
枚举 ProtectionType       |  描述保护是以模板为依据，还是临时的（自定义）
枚举 ActionType       |  不同操作类型。
结构 mip::PublishingLicenseContext | 保存用于创建保护处理程序的发布许可证的详细信息。

  
## <a name="enumerations-common"></a>枚举（通用）
  
### <a name="consent"></a>Consent
表示用户许可连接到服务终结点的决定。

 值                         | 描述                                
--------------------------------|---------------------------------------------
AcceptAlways            | 许可，并记住此决定
接受            | 许可，仅一次
拒绝            | 不许可
  
## <a name="enumerations-mip"></a>枚举 (mip)

### <a name="actiontype"></a>ActionType

不同操作类型。

 值                         | 描述                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | 向文档操作类型添加内容页脚。
ADD_CONTENT_HEADER            | 向文档操作类型添加内容页眉。
ADD_WATERMARK            | 向整个文档操作类型添加水印。
自定义            | 自定义的操作类型。
JUSTIFY            | 两端对齐操作类型。
METADATA            | 元数据更改操作类型。
PROTECT_ADHOC            | 临时策略保护操作类型。
PROTECT_BY_TEMPLATE            | 模板保护操作类型。
PROTECT_DO_NOT_FORWARD            | “不转发”保护操作类型。
REMOVE_CONTENT_FOOTER            | 删除内容页脚操作类型。
REMOVE_CONTENT_HEADER            | 删除内容页眉操作类型。
REMOVE_PROTECTION            | 删除保护操作类型。
REMOVE_WATERMARK            | 删除水印操作类型。
APPLY_LABEL            | 应用标签操作类型。
RECOMMEND_LABEL            | 建议标签操作类型。

CUSTOM 是通用操作类型。 其他各个操作类型是有特定意义的具体操作。

可以使用以下运算符组合 ActionType 值：

- And (&) 运算符，适用于 [Action](class_mip_action.md) (`operator &(ActionType a, ActionType b)`)
- 逻辑 OR (Xor) (^) 运算符，适用于 [Action](class_mip_action.md)。 (`operator ^(ActionType a, ActionType b)`)


### <a name="errortype"></a>ErrorType
 值                         | 描述                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 调用方传递了的输入不正确。
FILE_IO_ERROR            | 通用文件 IO 错误。
NETWORK_ERROR            | 一般网络问题（例如，服务不可供访问）。
TRANSIENT_NETWORK_ERROR            | 暂时性网络问题；例如，网关错误。
INTERNAL_ERROR            | 内部意外错误。 例如，客户端服务器协议出错（收到了意外响应）。
JUSTIFICATION_REQUIRED            | 应提供对齐方式，才能完成对文件执行的操作。
NOT_SUPPORTED_OPERATION            | 尚不支持请求的操作。
PRIVILEGED_REQUIRED            | 当新标签方法为标准时，无法替代特权标签。
ACCESS_DENIED            | 用户无法访问内容。 例如，无权限、内容已撤销等。
CONSENT_DENIED            | 需要用户同意的操作未获得同意。
  
### <a name="httprequesttype"></a>HttpRequestType
HTTP 请求类型。

 值                         | 描述                                
--------------------------------|---------------------------------------------
Get            | GET
Post            | POST
  
### <a name="loglevel"></a>日志级别

跨 MIP SDK 使用的不同日志级别。

 值                         | 描述                                
--------------------------------|---------------------------------------------
Trace            | 
信息            | 
警告            | 
错误            | 
跨 mip SDK 使用的不同日志级别。
  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions

指明其他策略创建行为的位标志。

 值                         | 描述                                
--------------------------------|---------------------------------------------
无            | 无
OfflineOnly            | 不允许执行 UI 和网络操作。
AllowAuditedExtraction            | 可以在不受保护且能感知 SDK 的应用中打开内容
PreferDeprecatedAlgorithms            | 使用已弃用的加密算法 (ECB) 实现后向兼容性


### <a name="protectiontype"></a>ProtectionType
描述保护是以模板为依据，还是临时的（自定义）

 值                         | 描述                                
--------------------------------|---------------------------------------------
TemplateBased            | 图柄是通过模板创建
自定义            | 图柄是临时创建

  
### <a name="protectionhandlercreationoptions"></a>ProtectionHandlerCreationOptions
ProtectionHandlerCreationOptions 位 OR 运算符。

参数：  
* **a**：左值 

* **b**：右值

### <a name="releaseallresources"></a>ReleaseAllResources
在关闭之前释放所有资源（线程等）。
如果应用程序延迟加载 MIP 动态库，则必须在应用程序显式卸载这些 MIP 库之前调用此函数，以避免死锁。 例如，在 win32 上，必须在用于通过 FreeLibrary 或 \__FUnloadDelayLoadedDLL2 显式卸载 MIP DLL 的任何调用之前调用此函数。 在调用此函数之前，应用程序必须释放对所有 MIP 对象（例如，配置文件、引擎、处理程序）的引用。
  
**返回结果**：参数的位 OR 运算符
  
## <a name="structures"></a>结构

### <a name="applicationinfo"></a>ApplicationInfo 
包含应用程序特定信息的结构。

 字段                        | 描述                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  Azure AD 门户中设置的应用程序标识符。
 public std::string applicationName  |  应用程序名称
 public std::string applicationVersion  |  正在使用的应用程序的版本
  
### <a name="mippublishinglicensecontext"></a>mip::PublishingLicenseContext 
保存用于创建保护处理程序的发布许可证的详细信息。
  
 字段                        | 描述                                
--------------------------------|---------------------------------------------
public const std::vector<uint8_t> licenseInfo  | _尚无记录。_
public const std::vector<uint8_t> serializedPublishingLicense  | _尚无记录。_
public PublishingLicenseContext(const std::vector<uint8_t>& licenseInfo, const std::vector<uint8_t>& serializedPublishingLicense)  | _尚无记录。_
  
