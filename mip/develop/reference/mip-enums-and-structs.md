---
title: 用于引用结构C++和枚举的 MIP SDK
description: MIP C++ SDK 结构和枚举的参考文档。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 6efe7910769dffe809e0661475f9adc8226b37b3
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884917"
---
# <a name="enumerations-and-structures"></a>枚举和结构

## <a name="namespace-mip"></a>命名空间 mip

 成员                        | 说明                                
--------------------------------|---------------------------------------------
枚举 WatermarkLayout       |  水印的布局。
枚举 ContentMarkAlignment       |  内容标记 (内容标头或内容页脚) 的对齐方式。
枚举 AssignmentMethod       |  文档上标签的分配方法。 标签分配是自动完成、标准还是特权操作 (相当于管理员操作)。
枚举 ActionSource       |  定义触发 SetLabel 事件的内容
枚举 DataState       |  定义应用程序所针对的数据的状态。
枚举 ContentFormat       |  内容格式。
枚举 Consent       |  当请求同意连接到服务终结点时用户的响应。
枚举 CacheStorageType       |  缓存的存储类型。
枚举 ErrorType       | _尚无记录。_
枚举 InspectorType       |  与支持的文件类型关联的检查器类型。
枚举 BodyType       |  Body 类型枚举器。
枚举 FlightingFeature       |  按名称定义新功能。
enum HttpRequestType       |  HTTP 请求类型。
枚举 LogLevel       |  跨 MIP SDK 使用的不同日志级别。
枚举 ProtectionHandlerCreationOptions       |  指明其他策略创建行为的位标志。
枚举 ProtectionType       |  描述保护是以模板为依据，还是临时的（自定义）
枚举 ActionType       |  不同操作类型。
枚举 LabelState       | _尚无记录。_
枚举 ActionDataType       | _尚无记录。_
枚举 ConditionDataType       | _尚无记录。_
枚举 ContentMarkPlacement       | _尚无记录。_
枚举 LabelActionDataType       | _尚无记录。_
枚举 ProtectionActionType       | _尚无记录。_
结构 mip:: ApplicationInfo  |  包含应用程序特定信息的结构。
结构 mip:: TelemetryConfiguration  |  自定义遥测设置 (不常用)


## <a name="enumerations-mip"></a>枚举 (mip)

### <a name="watermarklayout-enum"></a>WatermarkLayout 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
横坐标            | 水印布局为水平
条            | 水印布局为对角线

水印的布局。
  
### <a name="contentmarkalignment-enum"></a>ContentMarkAlignment 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
LEFT            | 内容标记靠左对齐
RIGHT            | 内容标记与右侧对齐
中心            | 内容标记居中

内容标记 (内容标头或内容页脚) 的对齐方式。
  
### <a name="assignmentmethod-enum"></a>AssignmentMethod 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
标准            | [标签](class_mip_label.md)分配方法为标准方法
特权            | [标签](class_mip_label.md)分配方法具有特权
自动            | [标签](class_mip_label.md)分配方法为自动

文档上标签的分配方法。 标签分配是自动完成、标准还是特权操作 (相当于管理员操作)。
  
### <a name="actionsource-enum"></a>ActionSource 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
手动            | 用户手动选择
自动            | 按策略条件设置
您            | 策略条件建议后按用户设置标签
DEFAULT 的信任组中的所有虚拟机的复制设置            | 默认情况下在策略中设置

定义触发 SetLabel 事件的内容
  
### <a name="datastate-enum"></a>DataState 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
REST            | 以物理方式存储在数据库/文件/仓库中的非活动数据
动作            | 遍历网络或临时驻留在计算机内存中以供读取或更新的数据
用法            | 在物理上存储在数据库/文件/仓库等中的恒定变化的活动数据

定义应用程序所针对的数据的状态。
  
### <a name="contentformat-enum"></a>ContentFormat 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
DEFAULT 的信任组中的所有虚拟机的复制设置            | 内容格式为标准文件格式
电子邮件            | 内容格式为电子邮件格式

内容格式。
  
### <a name="consent-enum"></a>同意枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
AcceptAlways            | 许可，并记住此决定
接受            | 许可，仅一次
拒绝            | 不许可

当请求同意连接到服务终结点时用户的响应。
  
### <a name="cachestoragetype-enum"></a>CacheStorageType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
InMemory            | 内存存储中
OnDisk            | 磁盘存储上
OnDiskEncrypted            | 使用加密的磁盘存储 (如果平台支持)

缓存的存储类型。
  
### <a name="errortype-enum"></a>ErrorType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 调用方传递了的输入不正确。
FILE_IO_ERROR            | 通用文件 IO 错误。
NETWORK_ERROR            | 一般网络问题;例如, 无法访问服务。
TRANSIENT_NETWORK_ERROR            | 暂时性的网络问题;例如, 网关错误。
INTERNAL_ERROR            | 内部意外错误。
JUSTIFICATION_REQUIRED            | 应提供对齐方式，才能完成对文件执行的操作。
NOT_SUPPORTED_OPERATION            | 尚不支持请求的操作。
PRIVILEGED_REQUIRED            | 当新标签方法为标准时，无法替代特权标签。
ACCESS_DENIED            | 用户无法访问服务。
CONSENT_DENIED            | 需要用户同意的操作未获得同意。
POLICY_SYNC_ERROR            | 同步策略数据尝试失败。
NO_PERMISSIONS            | 用户无法访问内容。 例如, 没有权限, 吊销内容
NO_AUTH_TOKEN            | 由于身份验证令牌为空, 用户无法访问内容。
DISABLED_SERVICE            | 由于服务被禁用, 用户无法访问内容
PROXY_AUTH_ERROR            | 代理身份验证失败。
NO_POLICY            | 未为用户/租户配置策略
OPERATION_CANCELLED            | 操作已取消
ADHOC_PROTECTION_REQUIRED            | 应设置即席保护来完成对文件的操作
DEPRECATED_API            | 调用方调用了已弃用的 API
TEMPLATE_NOT_FOUND            | 无法识别模板 ID
LABEL_NOT_FOUND            | [标签](class_mip_label.md)ID 无法识别
LABEL_DISABLED            | [标签](class_mip_label.md)已禁用或处于非活动状态
  
### <a name="inspectortype-enum"></a>InspectorType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
Unknown            | 未知文件检查器。
缺少            | 消息样式文件检查器, 基于 .rpmsg/消息。

与支持的文件类型关联的检查器类型。
  
### <a name="bodytype-enum"></a>BodyType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
未知            | 未知正文类型
TXT            | 文本样式正文类型, 编码以 utf8 形式返回
HTML            | HTML 样式正文类型, 编码以 utf8 格式返回
RTF            | RTF 样式正文类型, 二进制格式

Body 类型枚举器。
  
### <a name="flightingfeature-enum"></a>FlightingFeature 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | 依靠单独的 HTTP 调用来确定 RMS 服务终结点
AuthInfoCache            | 缓存每个域/租户的 OAuth2 难题, 减少不必要的401响应。 针对管理自己的 HTTP 身份验证 (如 SPO) 的应用/服务禁用
LinuxEncryptedCache            | 为 Linux 平台启用加密缓存 (请阅读此功能的先决条件)

按名称定义新功能。
  
### <a name="httprequesttype-enum"></a>HttpRequestType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
Get            | GET
Post            | 发布

HTTP 请求类型。
  
### <a name="loglevel-enum"></a>LogLevel 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
跟踪            | 
T:System.Diagnostics.Switch            | 
警告            | 
Error            | 

跨 MIP SDK 使用的不同日志级别。
  
### <a name="protectionhandlercreationoptions-enum"></a>ProtectionHandlerCreationOptions 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
无            | 无
OfflineOnly            | 不允许 UI 和网络操作
AllowAuditedExtraction            | 可以在不受保护且能感知 SDK 的应用中打开内容
PreferDeprecatedAlgorithms            | 使用已弃用的加密算法 (ECB) 实现后向兼容性

指明其他策略创建行为的位标志。

> 弃用删除 CreateProtectionHandlerFromDescriptor 和 CreateProtectionHandlerFromPublishingLicense 时, 此枚举即将弃用
  
### <a name="protectiontype-enum"></a>ProtectionType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
TemplateBased            | 图柄是通过模板创建
自定义            | 图柄是临时创建

描述保护是以模板为依据，还是临时的（自定义）
  
### <a name="actiontype-enum"></a>ActionType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
ADD_CONTENT_FOOTER            | 向文档操作类型添加内容页脚。
ADD_CONTENT_HEADER            | 向文档操作类型添加内容页眉。
ADD_WATERMARK            | 向整个文档操作类型添加水印。
自定义            | 自定义的操作类型。
JUSTIFY            | 两端对齐操作类型。
新元            | 元数据更改操作类型。
PROTECT_ADHOC            | 临时策略保护操作类型。
PROTECT_BY_TEMPLATE            | 模板保护操作类型。
PROTECT_DO_NOT_FORWARD            | “不转发”保护操作类型。
REMOVE_CONTENT_FOOTER            | 删除内容页脚操作类型。
REMOVE_CONTENT_HEADER            | 删除内容页眉操作类型。
REMOVE_PROTECTION            | 删除保护操作类型。
REMOVE_WATERMARK            | 删除水印操作类型。
APPLY_LABEL            | 应用标签操作类型。
RECOMMEND_LABEL            | 建议标签操作类型。

不同操作类型。 CUSTOM 是通用操作类型。 其他各个操作类型是有特定意义的具体操作。
  
### <a name="labelstate-enum"></a>LabelState 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
NoChange            | 
删除            | 
Update            | 
  
### <a name="actiondatatype-enum"></a>ActionDataType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
自定义            | 
保护            | 
ContentMarking            | 
AddWatermark            | 
Label            | 
  
### <a name="conditiondatatype-enum"></a>ConditionDataType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
默认            | 
敏感度            | 
  
### <a name="contentmarkplacement-enum"></a>ContentMarkPlacement 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
Header            | 
尾行            | 
  
### <a name="labelactiondatatype-enum"></a>LabelActionDataType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
推荐            | 
应用            | 
  
### <a name="protectionactiontype-enum"></a>ProtectionActionType 枚举

值                         | 说明                                
--------------------------------|---------------------------------------------
自定义            | 
模板            | 
DoNotForward            | 
特别            | 
DoNotForwardWithPrompt            | 
Hyok            | 
PredefinedTemplate            | 
RemoveProtection            | 
  


## <a name="structures"></a>結構 

### <a name="mipapplicationinfo"></a>mip::ApplicationInfo 
包含应用程序特定信息的结构。
  
#### <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  AAD 门户中设置的应用程序标识符 (应为不带方括号的 GUID)。
public std::string applicationName  |  应用程序名称 (应仅 containValid ASCII 字符, 不包括 ";")
public std::string applicationVersion  |  使用的应用程序版本 (应仅 containValid ASCII 字符, 不包括 ";")
  
#### <a name="members"></a>成员
  
##### <a name="applicationid-struct-member"></a>applicationId struct 成员
AAD 门户中设置的应用程序标识符 (应为不带方括号的 GUID)。
  
##### <a name="applicationname-struct-member"></a>applicationName 结构成员
应用程序名称 (应仅 containValid ASCII 字符, 不包括 ";")
  
##### <a name="applicationversion-struct-member"></a>applicationVersion 结构成员
使用的应用程序版本 (应仅 containValid ASCII 字符, 不包括 ";")

### <a name="miptelemetryconfiguration"></a>mip:: TelemetryConfiguration 
自定义遥测设置 (不常用)
  
#### <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std:: string hostNameOverride  |  主机遥测实例名称。 如果未设置, 则 MIP 将充当自己的主机。
public std:: string libraryNameOverride  |  备用遥测库 (DLL) 文件名。
public std:: shared_ptr\<HttpDelegate\> httpDelegateOverride  |  如果已设置, 则 HTTP 处理将由此实例管理
public std:: shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  如果已设置, 则异步任务处理将由此实例管理
public bool isNetworkDetectionEnabled  |  如果已设置, 遥测组件会 ping 后台线程上的网络状态
public bool isLocalCachingEnabled  |  如果设置, 遥测组件将使用磁盘上的缓存
public bool isTelemetryOptedOut  |  如果已设置, 则仅发送必要的服务数据遥测
  
#### <a name="members"></a>成员
  
##### <a name="hostnameoverride-struct-member"></a>hostNameOverride 结构成员
主机遥测实例名称。 如果未设置, 则 MIP 将充当自己的主机。
  
##### <a name="librarynameoverride-struct-member"></a>libraryNameOverride 结构成员
备用遥测库 (DLL) 文件名。
  
##### <a name="httpdelegate"></a>HttpDelegate
如果已设置, 则 HTTP 处理将由此实例管理
  
##### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
如果已设置, 则异步任务处理将由此实例管理
  
##### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled 结构成员
如果已设置, 遥测组件会 ping 后台线程上的网络状态
  
##### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled 结构成员
如果设置, 遥测组件将使用磁盘上的缓存
  
##### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut 结构成员
如果已设置, 则仅发送必要的服务数据遥测