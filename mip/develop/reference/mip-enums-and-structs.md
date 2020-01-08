---
title: 用于引用结构C++和枚举的 MIP SDK
description: MIP C++ SDK 结构和枚举的参考文档。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2a641ace68d6999e3d452fa7f5c014ec1215556a
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556004"
---
# <a name="enumerations-and-structures"></a>枚举和结构

## <a name="namespace-mip"></a>命名空间 mip

成員                        | 说明                                
--------------------------------|---------------------------------------------
枚举 WatermarkLayout       |  水印的布局。
枚举 ContentMarkAlignment       |  内容标记（内容标头或内容页脚）的对齐方式。
枚举 AssignmentMethod       |  文档上标签的分配方法。 标签分配是自动完成、标准还是特权操作（相当于管理员操作）。
枚举 ActionSource       |  定义触发 SetLabel 事件的内容
枚举 DataState       |  定义应用程序所针对的数据的状态。
枚举 ContentFormat       |  内容格式。
枚举 LabelFilterType       |  标签筛选器类型，可选的属性集，可用于在调用列表敏感度标签时筛选标签。
枚举 Consent       |  当请求同意连接到服务终结点时用户的响应。
枚举 CacheStorageType       |  缓存的存储类型。
枚举 PFileExtensionBehavior       |  介绍 .Pfile 扩展行为。
枚举 ErrorType       | 尚未记录。
枚举 InspectorType       |  与支持的文件类型关联的检查器类型。
枚举 BodyType       |  Body 类型枚举器。
枚举 FlightingFeature       |  按名称定义新功能。
enum HttpRequestType       |  HTTP 请求类型。
枚举 LogLevel       |  跨 MIP SDK 使用的不同日志级别。
枚举 ProtectionType       |  描述保护是以模板为依据，还是临时的（自定义）
枚举 ActionType       |  不同操作类型。
枚举 LabelState       | 尚未记录。
枚举 ActionDataType       | 尚未记录。
枚举 ConditionDataType       | 尚未记录。
枚举 ContentMarkPlacement       | 尚未记录。
枚举 LabelActionDataType       | 尚未记录。
枚举 ProtectionActionType       | 尚未记录。
结构 mip：： ApplicationInfo  |  包含应用程序特定信息的结构。
结构 mip：： TelemetryConfiguration  |  自定义遥测设置（不常用）

### <a name="enumerations"></a>枚举

#### <a name="watermarklayout-enum"></a>WatermarkLayout 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
横坐标            | 水印布局为水平
条            | 水印布局为对角线
水印的布局。
  
#### <a name="contentmarkalignment-enum"></a>ContentMarkAlignment 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
LEFT            | 内容标记靠左对齐
RIGHT            | 内容标记与右侧对齐
中心            | 内容标记居中
内容标记（内容标头或内容页脚）的对齐方式。
  
#### <a name="assignmentmethod-enum"></a>AssignmentMethod 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
标准            | 标签分配方法为标准方法
特权            | 标签分配方法具有特权
AUTO            | 标签分配方法为自动
文档上标签的分配方法。 标签分配是自动完成、标准还是特权操作（相当于管理员操作）。
  
#### <a name="actionsource-enum"></a>ActionSource 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
MANUAL            | 用户手动选择
AUTOMATIC            | 按策略条件设置
RECOMMENDED            | 策略条件建议后按用户设置标签
DEFAULT 的信任组中的所有虚拟机的复制设置            | 默认情况下在策略中设置
定义触发 SetLabel 事件的内容
  
#### <a name="datastate-enum"></a>DataState 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
REST            | 以物理方式存储在数据库/文件/仓库中的非活动数据
动作            | 遍历网络或临时驻留在计算机内存中以供读取或更新的数据
USE            | 在物理上存储在数据库/文件/仓库等中的恒定变化的活动数据
定义应用程序所针对的数据的状态。
  
#### <a name="contentformat-enum"></a>ContentFormat 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
DEFAULT 的信任组中的所有虚拟机的复制设置            | 内容格式为标准文件格式
电子邮件            | 内容格式为电子邮件格式
内容格式。
  
#### <a name="labelfiltertype-enum"></a>LabelFilterType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
无            | 禁用默认标记筛选
自定义            | 筛选可能导致自定义保护的标签
TemplateProtection            | 可能导致不转发的筛选标签
DoNotForwardProtection            | 筛选可能导致模板保护的标签
AdhocProtection            | 可能导致即席保护的筛选标签
HyokProtection            | 筛选可能会导致 hyok 保护的标签
PredefinedTemplate            | 可能导致预定义模板保护的筛选标签
标签筛选器类型，可选的属性集，可用于在调用列表敏感度标签时筛选标签。
  
#### <a name="consent-enum"></a>同意枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
AcceptAlways            | 许可，并记住此决定
接受            | 许可，仅一次
拒绝            | 不许可
当请求同意连接到服务终结点时用户的响应。
  
#### <a name="cachestoragetype-enum"></a>CacheStorageType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
InMemory            | 内存存储中
OnDisk            | 磁盘存储上
OnDiskEncrypted            | 使用加密的磁盘存储（如果平台支持）
缓存的存储类型。
  
#### <a name="pfileextensionbehavior-enum"></a>PFileExtensionBehavior 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
默认值            | 扩展将变为 SDK 默认行为
PFileSuffix            | 扩展将变为 <EXT>.PFILE
PPrefix            | 扩展将变为 P<EXT>
介绍 .Pfile 扩展行为。
  
#### <a name="errortype-enum"></a>ErrorType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
BAD_INPUT_ERROR            | 调用方传递了的输入不正确。
FILE_IO_ERROR            | 通用文件 IO 错误。
NETWORK_ERROR            | 一般网络问题;例如，无法访问服务。
TRANSIENT_NETWORK_ERROR            | 暂时性的网络问题;例如，网关错误。
INTERNAL_ERROR            | 内部意外错误。
JUSTIFICATION_REQUIRED            | 应提供对齐方式，才能完成对文件执行的操作。
NOT_SUPPORTED_OPERATION            | 尚不支持请求的操作。
PRIVILEGED_REQUIRED            | 当新标签方法为标准时，无法替代特权标签。
ACCESS_DENIED            | 用户无法访问服务。
CONSENT_DENIED            | 需要用户同意的操作未获得同意。
POLICY_SYNC_ERROR            | 同步策略数据尝试失败。
NO_PERMISSIONS            | 用户无法访问内容。 例如，没有权限，吊销内容
NO_AUTH_TOKEN            | 由于身份验证令牌为空，用户无法访问内容。
DISABLED_SERVICE            | 由于服务被禁用，用户无法访问内容
PROXY_AUTH_ERROR            | 代理身份验证失败。
NO_POLICY            | 未为用户/租户配置策略
OPERATION_CANCELLED            | 操作已取消
ADHOC_PROTECTION_REQUIRED            | 应设置即席保护来完成对文件的操作
DEPRECATED_API            | 调用方调用了已弃用的 API
TEMPLATE_NOT_FOUND            | 无法识别模板 ID
LABEL_NOT_FOUND            | 无法识别标签 ID
LABEL_DISABLED            | 标签已禁用或处于非活动状态
  
#### <a name="inspectortype-enum"></a>InspectorType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
Unknown            | 未知文件检查器。
Msg            | 消息样式文件检查器，基于 .rpmsg/消息。
与支持的文件类型关联的检查器类型。
  
#### <a name="bodytype-enum"></a>BodyType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
未知            | 未知正文类型
TXT            | 文本样式正文类型，编码以 utf8 形式返回
HTML            | HTML 样式正文类型，编码以 utf8 格式返回
RTF            | RTF 样式正文类型，二进制格式
Body 类型枚举器。
  
#### <a name="flightingfeature-enum"></a>FlightingFeature 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
ServiceDiscovery            | 依靠单独的 HTTP 调用来确定 RMS 服务终结点
AuthInfoCache            | 缓存每个域/租户的 OAuth2 难题，减少不必要的401响应。 针对管理自己的 HTTP 身份验证的应用/服务（如 SPO、Edge）禁用
LinuxEncryptedCache            | 为 Linux 平台启用加密缓存（请阅读此功能的先决条件）
SingleDomainName            | 启用单一公司名称进行 dns 查找。 例如[https://corprights](https://corprights)
PolicyAuth            | 为发送到策略服务的请求启用自动 HTTP 身份验证。 针对管理自己的 HTTP 身份验证的应用/服务（如 SPO、Edge）禁用
按名称定义新功能。
  
#### <a name="httprequesttype-enum"></a>HttpRequestType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
Get            | GET
Post            | POST
HTTP 请求类型。
  
#### <a name="loglevel-enum"></a>LogLevel 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
Trace            | 
信息            | 
警告            | 
错误            | 
跨 MIP SDK 使用的不同日志级别。
  
#### <a name="protectiontype-enum"></a>ProtectionType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
TemplateBased            | 图柄是通过模板创建
自定义            | 图柄是临时创建
描述保护是以模板为依据，还是临时的（自定义）
  
#### <a name="actiontype-enum"></a>ActionType 枚举
 值                         | 说明                                
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
不同操作类型。
CUSTOM 是通用操作类型。 其他各个操作类型是有特定意义的具体操作。
  
#### <a name="labelstate-enum"></a>LabelState 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
NoChange            | 
移除            | 
更新            | 
  
#### <a name="actiondatatype-enum"></a>ActionDataType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
自定义            | 
Protection            | 
ContentMarking            | 
AddWatermark            | 
标签            | 
  
#### <a name="conditiondatatype-enum"></a>ConditionDataType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
默认值            | 
敏感度            | 
  
#### <a name="contentmarkplacement-enum"></a>ContentMarkPlacement 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
Header            | 
页脚            | 
  
#### <a name="labelactiondatatype-enum"></a>LabelActionDataType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
推荐            | 
应用            | 
  
#### <a name="protectionactiontype-enum"></a>ProtectionActionType 枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
自定义            | 
模板            | 
DoNotForward            | 
Adhoc            | 
DoNotForwardWithPrompt            | 
Hyok            | 
PredefinedTemplate            | 
RemoveProtection            | 

### <a name="structures"></a>結構

#### <a name="struct-mipapplicationinfo"></a>结构 mip：： ApplicationInfo 
包含应用程序特定信息的结构。
  
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  AAD 门户中设置的应用程序标识符（应为不带方括号的 GUID）。
public std::string applicationName  |  应用程序名称（应仅包含有效 ASCII 字符，不包括 ";"）
public std::string applicationVersion  |  所使用的应用程序的版本（应只包含有效的 ASCII 字符，不包括 ";"）
  

##### <a name="applicationid-struct-member"></a>applicationId struct 成员
AAD 门户中设置的应用程序标识符（应为不带方括号的 GUID）。
  
##### <a name="applicationname-struct-member"></a>applicationName 结构成员
应用程序名称（应仅包含有效 ASCII 字符，不包括 ";"）
  
##### <a name="applicationversion-struct-member"></a>applicationVersion 结构成员
所使用的应用程序的版本（应只包含有效的 ASCII 字符，不包括 ";"）

#### <a name="struct-miptelemetryconfiguration"></a>结构 mip：： TelemetryConfiguration 
自定义遥测设置（不常用）
  
成員                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string hostNameOverride  |  主机遥测实例名称。 如果未设置，则 MIP 将充当自己的主机。
public std：： string libraryNameOverride  |  备用遥测库（DLL）文件名。
public std：： shared_ptr\<HttpDelegate\> httpDelegateOverride  |  如果已设置，则 HTTP 处理将由此实例管理
public std：： shared_ptr\<TaskDispatcherDelegate\> taskDispatcherDelegateOverride  |  如果已设置，则异步任务处理将由此实例管理，taskDispatcherDelegateOverides 不应共享，因为它们可以持有遥测对象，并阻止其发布，直到 taskDispatcher 释放。
public bool isNetworkDetectionEnabled  |  如果已设置，遥测组件会 ping 后台线程上的网络状态
public bool isLocalCachingEnabled  |  如果设置，遥测组件将使用磁盘上的缓存
public bool isTraceLoggingEnabled  |  如果已设置，遥测组件会将警告/错误日志写入磁盘
public bool isTelemetryOptedOut  |  如果已设置，则仅发送必要的服务数据遥测
public bool isFastShutdownEnabled  |  如果设置此设置，则在关闭时不会上载任何事件，在日志记录后将立即上载审核事件
public std：： map\<std：： string，std：： string\> customSettings  |  自定义遥测设置 >
    
##### <a name="hostnameoverride-struct-member"></a>hostNameOverride 结构成员
主机遥测实例名称。 如果未设置，则 MIP 将充当自己的主机。
  
##### <a name="librarynameoverride-struct-member"></a>libraryNameOverride 结构成员
备用遥测库（DLL）文件名。
  
##### <a name="httpdelegate"></a>HttpDelegate
如果已设置，则 HTTP 处理将由此实例管理
  
##### <a name="taskdispatcherdelegate"></a>TaskDispatcherDelegate
如果已设置，则异步任务处理将由此实例管理，taskDispatcherDelegateOverides 不应共享，因为它们可以持有遥测对象，并阻止其发布，直到 taskDispatcher 释放。
  
##### <a name="isnetworkdetectionenabled-struct-member"></a>isNetworkDetectionEnabled 结构成员
如果已设置，遥测组件会 ping 后台线程上的网络状态
  
##### <a name="islocalcachingenabled-struct-member"></a>isLocalCachingEnabled 结构成员
如果设置，遥测组件将使用磁盘上的缓存
  
##### <a name="istraceloggingenabled-struct-member"></a>isTraceLoggingEnabled 结构成员
如果已设置，遥测组件会将警告/错误日志写入磁盘
  
##### <a name="istelemetryoptedout-struct-member"></a>isTelemetryOptedOut 结构成员
如果已设置，则仅发送必要的服务数据遥测
  
##### <a name="isfastshutdownenabled-struct-member"></a>isFastShutdownEnabled 结构成员
如果设置此设置，则在关闭时不会上载任何事件，在日志记录后将立即上载审核事件
  
##### <a name="customsettings-struct-member"></a>customSettings 结构成员
自定义遥测设置 >

## <a name="namespace-mipauditmetadatakeys"></a>命名空间 mip：： auditmetadatakeys
  
### <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string Sender （）       |  审核字符串表示形式的元数据密钥。
public std：： string 接收者（）       | 尚未记录。
public std：： string LastModifiedBy （）       | 尚未记录。
public std：： string LastModifiedDate （）       | 尚未记录。
  
### <a name="members"></a>成員
  
#### <a name="sender-function"></a>Sender 函数
审核字符串表示形式的元数据密钥。
  
#### <a name="recipients-function"></a>收件人函数
_尚无记录。_

  
#### <a name="lastmodifiedby-function"></a>LastModifiedBy 函数
_尚无记录。_

  
#### <a name="lastmodifieddate-function"></a>LastModifiedDate 函数
_尚无记录。_

## <a name="namespace-miprights"></a>命名空间 mip：：权限
  
### <a name="summary"></a>“摘要”
 
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string Owner()       |  获取“所有者”权限的字符串标识符。
public std::string View()       |  获取“查看”权限的字符串标识符。
public std::string AuditedExtract()       |  获取“已审核的提取”权限的字符串标识符。
public std::string Edit()       |  获取“编辑”权限的字符串标识符。
public std::string Export()       |  获取“导出”权限的字符串标识符。
public std::string Extract()       |  获取“提取”权限的字符串标识符。
public std::string Print()       |  获取“打印”权限的字符串标识符。
public std::string Comment()       |  获取“注释”权限的字符串标识符。
public std::string Reply()       |  获取“回复”权限的字符串标识符。
public std::string ReplyAll()       |  获取“全部回复”权限的字符串标识符。
public std::string Forward()       |  获取“转发”权限的字符串标识符。
public std：： vector\<std：： string\> EmailRights （）       |  获取适用于电子邮件的权限列表。
public std：： vector\<std：： string\> EditableDocumentRights （）       |  获取适用于文档的权限列表。
public std：： vector\<std：： string\> CommonRights （）       |  获取适用于所有方案的权限列表。
  
### <a name="members"></a>成員
  
#### <a name="owner-function"></a>所有者函数
获取“所有者”权限的字符串标识符。

  
**返回结果**：“所有者”权限的字符串标识符
  
#### <a name="view-function"></a>查看函数
获取“查看”权限的字符串标识符。

  
**返回结果**：“查看”权限的字符串标识符
  
#### <a name="auditedextract-function"></a>AuditedExtract 函数
获取“已审核的提取”权限的字符串标识符。

  
**返回结果**：“已审核的提取”权限的字符串标识符
  
#### <a name="edit-function"></a>编辑函数
获取“编辑”权限的字符串标识符。

  
**返回结果**：“编辑”权限的字符串标识符
  
#### <a name="export-function"></a>导出函数
获取“导出”权限的字符串标识符。

  
**返回结果**：“导出”权限的字符串标识符
  
#### <a name="extract-function"></a>Extract 函数
获取“提取”权限的字符串标识符。

  
**返回结果**：“提取”权限的字符串标识符
  
#### <a name="print-function"></a>Print 函数
获取“打印”权限的字符串标识符。

  
**返回结果**：“打印”权限的字符串标识符
  
#### <a name="comment-function"></a>Comment 函数
获取“注释”权限的字符串标识符。

  
**返回结果**：“注释”权限的字符串标识符
  
#### <a name="reply-function"></a>Reply 函数
获取“回复”权限的字符串标识符。

  
**返回结果**：“回复”权限的字符串标识符
  
#### <a name="replyall-function"></a>ReplyAll 函数
获取“全部回复”权限的字符串标识符。

  
**返回结果**：“全部回复”权限的字符串标识符
  
#### <a name="forward-function"></a>Forward 函数
获取“转发”权限的字符串标识符。

  
**返回结果**：“转发”权限的字符串标识符
  
#### <a name="emailrights-function"></a>EmailRights 函数
获取适用于电子邮件的权限列表。

  
**返回结果**：适用于电子邮件的权限列表
  
#### <a name="editabledocumentrights-function"></a>EditableDocumentRights 函数
获取适用于文档的权限列表。

  
**返回结果**：适用于文档的权限列表
  
#### <a name="commonrights-function"></a>CommonRights 函数
获取适用于所有方案的权限列表。

  
**返回结果**：适用于所有方案的权限列表

## <a name="namespace-miproles"></a>命名空间 mip：： roles
  
### <a name="summary"></a>“摘要”
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  获取“查看者”角色的字符串标识符。
public std::string Reviewer()       |  获取“审阅者”角色的字符串标识符。
public std::string Author()       |  获取“作者”角色的字符串标识符。
public std::string CoOwner()       |  获取“共有者”角色的字符串标识符。
  
### <a name="members"></a>成員
  
#### <a name="viewer-function"></a>查看器函数
获取“查看者”角色的字符串标识符。

  
**返回结果**：“查看者”的字符串标识符。查看者只能查看内容， 无法编辑、复制或打印内容。
  
#### <a name="reviewer-function"></a>审校函数
获取“审阅者”角色的字符串标识符。

  
**返回结果**：“审阅者”的字符串标识符。审阅者可以查看和编辑内容， 但无法复制或打印内容。
  
#### <a name="author-function"></a>Author 函数
获取“作者”角色的字符串标识符。

  
**返回结果**：“作者”角色的字符串标识符。作者可以查看、编辑、复制和打印内容。
  
#### <a name="coowner-function"></a>CoOwner 函数
获取“共有者”角色的字符串标识符。

  
**返回结果**：“共有者”角色的字符串标识符。共有者拥有全部权限

