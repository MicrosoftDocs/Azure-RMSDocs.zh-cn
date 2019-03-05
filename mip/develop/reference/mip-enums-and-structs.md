---
title: MIP SDK for c + + 参考结构和枚举
description: MIP c + + SDK 的结构和枚举的参考文档。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2c0c600cc6a77b656d5e5dd1e86401fb4a9a66e4
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333188"
---
# <a name="summary"></a>总结

 成員                        | 说明                                
--------------------------------|---------------------------------------------
**Namespace `mip` :** |
枚举 ActionSource       |  定义触发 SetLabel 事件的原因
枚举 ActionType       |  不同操作类型。
枚举 AssignmentMethod       |  在文档上标签的分配方法。 是否在标签的分配自动执行操作，标准或作为一项特权操作 （相当于管理员操作）。
枚举 Consent       |  当请求同意连接到服务终结点时用户的响应。
枚举 ContentFormat       |  内容格式。
enum ContentMarkAlignment       |  内容的对齐方式将标记 （内容标头或内容脚注）。
枚举 ContentState       |  定义的状态数据的应用程序起作用时。
枚举 ErrorType       | _尚无记录。_
enum HttpRequestType       |  HTTP 请求类型。
枚举 LogLevel       |  跨 MIP SDK 使用的不同日志级别。
枚举 ProtectionHandlerCreationOptions       |  指明其他策略创建行为的位标志。
枚举 ProtectionType       |  描述保护是以模板为依据，还是临时的（自定义）
枚举 watermarklayout:       |  水印布局。
结构 ApplicationInfo  |  包含应用程序特定信息的结构。
结构 PublishingLicenseContext | 保存用于创建保护处理程序的发布许可证的详细信息。
  
## <a name="enumerations-mip"></a>枚举 (`mip`)

### <a name="actionsource-enum"></a>ActionSource 枚举

定义触发 SetLabel 事件的原因

 值                         | 说明                                
--------------------------------|---------------------------------------------
手动            | 由用户手动选择
自动            | 由策略条件设置
建议            | 标签建议的策略条件后，由用户设置
默认值            | 默认情况下，在策略中设置
必需            | 策略强制设置标签后由用户设置


### <a name="actiontype-enum"></a>ActionType 枚举

不同操作类型。 CUSTOM 是通用操作类型。 其他各个操作类型是有特定意义的具体操作。

 值                         | 说明                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | 向文档操作类型添加内容页脚。
ADD_CONTENT_HEADER            | 向文档操作类型添加内容页眉。
ADD_WATERMARK            | 向整个文档操作类型添加水印。
自定义            | 自定义的操作类型。
JUSTIFY            | 两端对齐操作类型。
元数据            | 元数据更改操作类型。
PROTECT_ADHOC            | 临时策略保护操作类型。
PROTECT_BY_TEMPLATE            | 模板保护操作类型。
PROTECT_DO_NOT_FORWARD            | “不转发”保护操作类型。
REMOVE_CONTENT_FOOTER            | 删除内容页脚操作类型。
REMOVE_CONTENT_HEADER            | 删除内容页眉操作类型。
REMOVE_PROTECTION            | 删除保护操作类型。
REMOVE_WATERMARK            | 删除水印操作类型。
APPLY_LABEL            | 应用标签操作类型。
RECOMMEND_LABEL            | 建议标签操作类型。

### <a name="assignmentmethod-enum"></a>AssignmentMethod 枚举

在文档上标签的分配方法。 是否在标签的分配自动执行操作，标准或作为一项特权操作 （相当于管理员操作）。

 值                         | 说明                                
--------------------------------|---------------------------------------------
标准            | [标签](class_mip_label.md)分配方法为标准
特权            | [标签](class_mip_label.md)一项特权分配方法
自动            | [标签](class_mip_label.md)分配方法为自动


### <a name="consent-enum"></a>同意的情况下枚举

当请求同意连接到服务终结点时用户的响应。

 值                         | 说明                                
--------------------------------|---------------------------------------------
AcceptAlways            | 许可，并记住此决定
接受            | 许可，仅一次
拒绝            | 不许可


### <a name="contentformat-enum"></a>ContentFormat 枚举

内容格式。

 值                         | 说明                                
--------------------------------|---------------------------------------------
默认值            | 内容格式是标准文件格式
电子邮件            | 内容格式是电子邮件格式

### <a name="contentmarkalignment-enum"></a>ContentMarkAlignment enum

内容的对齐方式将标记 （内容标头或内容脚注）。

 值                         | 说明                                
--------------------------------|---------------------------------------------
左侧            | 内容标记为左对齐
右侧            | 内容标记为右对齐
中心            | 居中内容标记

### <a name="contentstate-enum"></a>ContentState 枚举

定义的状态数据的应用程序起作用时。

 值                         | 说明                                
--------------------------------|---------------------------------------------
REST            | 以物理方式存储在数据库/文件/仓库中的非活动数据
运动            | 遍历网络或暂时驻留在要读取或更新的计算机内存中的数据
使用            | 在以物理方式存储在数据库/文件/仓库等的不断变化的活动数据

### <a name="errortype-enum"></a>错误类型枚举

 值                         | 说明                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 调用方传递了的输入不正确。
FILE_IO_ERROR            | 通用文件 IO 错误。
NETWORK_ERROR            | 常规网络问题;例如，无法访问服务。
TRANSIENT_NETWORK_ERROR            | 暂时性网络问题;例如，错误的网关。
INTERNAL_ERROR            | 内部意外错误。
JUSTIFICATION_REQUIRED            | 应提供对齐方式，才能完成对文件执行的操作。
NOT_SUPPORTED_OPERATION            | 尚不支持请求的操作。
PRIVILEGED_REQUIRED            | 当新标签方法为标准时，无法替代特权标签。
ACCESS_DENIED            | 用户无法获取对服务的访问。
CONSENT_DENIED            | 需要用户同意的操作未获得同意。
POLICY_SYNC_ERROR            | 同步策略数据尝试失败。
NO_PERMISSIONS            | 用户无法访问内容。 例如，内容没有权限被吊销
NO_AUTH_TOKEN            | 用户无法获取由于空身份验证令牌内容的访问权限。
DISABLED_SERVICE            | 用户无法获取访问内容，因为服务被禁用
PROXY_AUTH_ERROR            | 代理身份验证失败。
NO_POLICY_ERROR            | 为用户/租户不配置任何策略
  
### <a name="httprequesttype-enum"></a>HttpRequestType enum

HTTP 请求类型。

 值                         | 说明                                
--------------------------------|---------------------------------------------
Get            | GET
Post            | 发布

  
### <a name="loglevel-enum"></a>LogLevel 枚举

跨 MIP SDK 使用的不同日志级别。

 值                         | 说明                                
--------------------------------|---------------------------------------------
跟踪            | 
T:System.Diagnostics.Switch            | 
警告            | 
错误            | 

  
### <a name="protectionhandlercreationoptions-enum"></a>ProtectionHandlerCreationOptions 枚举

指明其他策略创建行为的位标志。

 值                         | 说明                                
--------------------------------|---------------------------------------------
无            | 无
OfflineOnly            | 不允许执行 UI 和网络操作。
AllowAuditedExtraction            | 可以在不受保护且能感知 SDK 的应用中打开内容
PreferDeprecatedAlgorithms            | 使用已弃用的加密算法 (ECB) 实现后向兼容性
  
### <a name="protectiontype-enum"></a>ProtectionType 枚举

介绍保护基于模板或临时 （自定义）。

 值                         | 说明                                
--------------------------------|---------------------------------------------
TemplateBased            | 图柄是通过模板创建
自定义            | 图柄是临时创建
  
### <a name="watermarklayout-enum"></a>Watermarklayout： 枚举

水印布局。

 值                         | 说明                                
--------------------------------|---------------------------------------------
水平            | 水印布局为水平
对角线            | 水印布局是沿对角方向


## <a name="structures"></a>结构 

### `mip::ApplicationInfo` 

包含应用程序特定信息的结构。
  
 成員                        | 说明                                
--------------------------------|---------------------------------------------
 public std::string applicationId  |  作为应用程序标识符的 AAD 门户中设置，（应为不带方括号的 GUID）。
 public std::string applicationName  |  应用程序名称 (只应包含有效 ASCII 字符不包括;)
 public std::string applicationVersion  |  正在使用的应用程序的版本 (只应包含有效 ASCII 字符不包括;)
  
### `mip::PublishingLicenseContext` 

保存用于创建保护处理程序的发布许可证的详细信息。
  
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\> licenseInfo  | _尚无记录。_
public const std:: vector\<uint8_t\> serializedPublishingLicense  | _尚无记录。_
公共 PublishingLicenseContext (const std:: vector\<uint8_t\>& licenseInfo，const std:: vector\<uint8_t\>& serializedPublishingLicense)  | _尚无记录。_
  
