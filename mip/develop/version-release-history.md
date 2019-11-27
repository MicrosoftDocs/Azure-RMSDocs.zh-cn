---
title: Microsoft 信息保护（MIP） SDK 版本发行历史记录和支持策略
description: MIP SDK 的版本发行历史记录和更改注释。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/25/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: a678765835785dcb40aaf65e7f92e78fba67c73a
ms.sourcegitcommit: 487e681c9683b8adb7ae6fcfb374830bf0e5ad72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74479116"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Microsoft 信息保护（MIP） SDK 版本发行历史记录和支持策略

## <a name="servicing"></a>服务 

每个正式发布（GA）版本在下一正式发行版发布后的六个月内受支持。 文档可能不包含有关不支持的版本的信息。 修补程序和新功能仅适用于最新的 GA 版本。

不应在生产中部署预览版本。 请改用最新的预览版本来测试新功能或即将推出的新功能或修补程序。 仅支持最新的预览版本。

## <a name="release-history"></a>版本历史

使用以下信息可查看受支持版本的新增功能或更改内容。 最新版本会最先列出。 

> [!NOTE]
> 不会列出小修补程序，因此，如果您在使用 SDK 时遇到问题，我们建议您检查是否已通过最新的 GA 版本修复了此问题。 如果问题仍然存在，请检查当前预览版。
>  
> 若要获得技术支持，请访问[Microsoft 信息保护论坛 Stack Overflow](https://stackoverflow.com/questions/tagged/microsoft-information-protection)。 

## <a name="version-140"></a>版本1.4。0 

**发布日期**：2019年11月6日

此版本引入了对 .NET 包（InformationProtection）中的保护 API 的支持。

### <a name="sdk-changes"></a>SDK 更改
- 性能改进和 bug 修复
- 将 StorageType 枚举重命名为 CacheStorageType
- Android 链接到 libc + + 而不是 gnustl
- 删除以前不推荐使用的 Api
  - 文件/策略/配置文件：：设置必须使用 MipContext 进行初始化
  - 已删除 "文件/策略/配置文件：：设置路径"、"应用程序信息"、"记录器委托"、"遥测" 和 "日志级别 getter/setter"。 这些属性由 MipContext 管理
- Apple 平台上更好的静态库支持
  - 单一静态库
    - libmip_file_sdk_static。
    - libmip_upe_sdk_static。
    - libmip_protection_sdk_static。
    - libmip_upe_and_protection_sdk_static。
  - 提取到不同库中的第三方依赖项
    - libsqlite3
    - libssl1.0。0
- 删除 mip_telemetry .dll （合并到 mip_core .dll）

### <a name="file-api"></a>文件 API

- .RPMSG
  - 加密
  - 添加了对 string8 解密的支持
- 可配置的 .PFILE 扩展行为（默认 <EXT>.PFILE 或 P<EXT>）
  - ProtectionSettings::SetPFileExtensionBehavior

### <a name="policy-api"></a>策略 API

- 完成 C API
- 配置与保护关联的标签的筛选
  - PolicyEngine：：设置也：： SetLabelFilter （）

### <a name="protection-api"></a>保护 API

- 删除以前不推荐使用的 Api
  - 已删除 ProtectionEngine：： CreateProtectionHandlerFromDescriptor [Async] （使用 ProtectionEngine：： CreateProtectionHandlerForPublishing [Async]）
  - 已删除 ProtectionEngine：： CreateProtectionHandlerFromPublishingLicense [Async] （使用 ProtectionEngine：： CreateProtectionHandlerForConsumption [Async]）
- 完整C# API
- 完成 C API
  - C 版本 C api 预览版中的 C API 规范化更改：
    - 将 mip_cc_storage_type 重命名为 mip_cc_cache_storage_type
    - 将 MIP_CC_AddProtectionProfileEngine 重命名为 MIP_CC_ProtectionProfile_AddEngine
    - 将 MIP_CC_CreateProtectionEngineSettingsForExistingEngine 重命名为 MIP_CC_CreateProtectionEngineSettingsWithEng
    - 将 MIP_CC_CreateProtectionEngineSettingsForNewEngine 重命名为 MIP_CC_CreateProtectionEngineSettingsWithIdentity
    - 将 MIP_CC_SetProtectionProfileSettingsHttpDelegate 重命名为 MIP_CC_ProtectionProfileSettings_SetHttpDelegate
    - 将 MIP_CC_CreateProtectionHandlerForConsumption 重命名为 MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption
    - 将 MIP_CC_CreateProtectionHandlerForPublishing 重命名为 MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing
    - 将 MIP_CC_GetProtectionEngineId 重命名为 MIP_CC_ProtectionEngine_GetEngineId
    - 将 MIP_CC_GetProtectionEngineTemplates 重命名为 MIP_CC_ProtectionEngine_GetTemplates
    - 将 MIP_CC_GetProtectionEngineTemplatesSize 重命名为 MIP_CC_ProtectionEngine_GetTemplatesSize
    - 将 MIP_CC_SetTelemetryConfigurationHttpDelegate 重命名为 MIP_CC_TelemetryConfiguration_SetHttpDelegate
    - 将 MIP_CC_SetTelemetryConfigurationHostName 重命名为 MIP_CC_TelemetryConfiguration_SetHostName
    - 将 MIP_CC_SetTelemetryConfigurationIsLocalCachingEnabled 重命名为 MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled
    - 将 MIP_CC_SetTelemetryConfigurationIsNetworkDetectionEnabled 重命名为 MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled
    - 将 MIP_CC_SetTelemetryConfigurationIsTelemetryOptedOut 重命名为 MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut
    - 将 MIP_CC_SetTelemetryConfigurationLibraryName 重命名为 MIP_CC_TelemetryConfiguration_SetLibraryName
    - 删除 MIP_CC_ProtectionEngine_GetRightsForLabelIdSize 并更新 MIP_CC_ProtectionEngine_GetRightsForLabelId 以填充 mip_cc_string_list，而不是以逗号分隔的字符串缓冲区
    - 删除 MIP_CC_ProtectionHandler_GetRightsSize 并更新 MIP_CC_ProtectionHandler_GetRights 以填充 mip_cc_string_list，而不是以逗号分隔的字符串缓冲区
    - 添加了 MIP_CC_ProtectionEngine_GetEngineIdSize 并更新了 MIP_CC_ProtectionEngine_GetEngineId 来填充字符串缓冲区而不是 mip_cc_guid
    - MIP_CC_CreateProtectionDescriptorFromUserRights 现在使用 "mip_cc_dictionary" 参数，而不是 "mip_cc_dictionary"
    - MIP_CC_ProtectionEngineSettings_SetCustomSettings 现在使用 "mip_cc_dictionary" 参数，而不是 "mip_cc_dictionary"
    - MIP_CC_ProtectionProfileSettings_SetCustomSettings 现在使用 "mip_cc_dictionary" 参数，而不是 "mip_cc_dictionary"
    - MIP_CC_TelemetryConfiguration_SetCustomSettings 现在使用 "mip_cc_dictionary" 参数，而不是 "mip_cc_dictionary"
    - MIP_CC_CreateMipContext 采用 "isOfflineOnly" 和 "loggerDelegateOverride" 参数


## <a name="version-130"></a>版本1.3。0

**发布日期**：2019年8月22日

### <a name="new-features"></a>新功能

- `mip::MipContext` 是新的最高级别的对象。
- 现在支持解密受保护的消息文件。
- 通过 `mip::FileInspector` 和 `mip::FileHandler::InspectAsync()`来支持检查 .rpmsg 文件。
- 磁盘上的缓存现在可以有选择性地加密。
- 保护 API 现在支持中国主权 cloud。
- Android 上的 Arm64 支持。
- IOS 上的 Arm64e 支持。
- 最终用户许可证（EUL）缓存现在可以禁用。
- 。可以通过 `mip::FileEngine::EnablePFile` 禁用 .pfile 加密
- 通过减少 HTTP 调用数提高了保护操作的性能
- 已从 `mip::Identity` 中删除委托的标识详细信息，并将 `DelegatedUserEmail` 添加到 `mip::FileEngine::Settings`、`mip::ProtectionSettings`、`mip::PolicyEngine::Settings`和 `mip::ProtectionHandler``PublishingSettings` 和 `ConsumptionSettings`。
- 先前返回面部的函数现在返回 `mip::Label` 对象。

### <a name="changes"></a>更改

* 在以前的版本中，我们要求你调用 `mip::ReleaseAllResources`。 版本1.3 将此替换为 `mip::MipContext::~MipContext` 或 `mip::MipContext::Shutdown`。
* 从 `mip::LabelingOptions` 和 `mip::ExecutionState::GetNewLabelActionSource` 中删除了 `ActionSource`
* 已将 `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` 替换为 `mip::ProtectionEngine::CreateProtectionHandlerForPublishing`。
* 已将 `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` 替换为 `mip::ProtectionEngine::CreateProtectionHandlerForConsumption`。
* 将 `mip::PublishingLicenseContext` 重命名为 `mip::PublishingLicenseInfo` 并更新为包含丰富的字段，而不是原始序列化的字节。
* `mip::PublishingLicenseInfo` 包含在分析发布许可证（PL）之后与 MIP 相关的数据。
* 当应用程序通过 MIP 时，将引发 `mip::TemplateNotFoundError` 和 `mip::LabelNotFoundError` 无法识别的模板 ID 或标签 ID。
* 通过 `AcquireToken()` 和 `mip::AuthDelegate::OAuth2Challenge()`的声明参数添加了对基于标签的条件性访问的支持。 尚未通过安全和合规中心门户公开此功能。


## <a name="version-120"></a>版本1.2。0

**发布日期**：2019年4月15日

### <a name="new-features"></a>新功能

 - 遥测组件现在使用与 MIP 的其余部分相同的 HTTP stack，即使客户端应用程序已使用 HttpDelegate 重写它也是如此。
 - 客户端应用程序可以通过重写配置文件中的 TaskDispatcherDelegate 来控制异步任务的线程行为。
 - .RPMSG 加密现为预览版。
 - 与保护 SDK 协调文件/策略 SDK 异常处理行为：
    - 如果代理配置为要求身份验证，则所有 Sdk 引发的 ProxyAuthError。
    - 当应用程序的 mip：： AuthDelegate：： AcquireOAuth2Token 的实现提供空的身份验证令牌时，所有 Sdk 引发的 NoAuthTokenError。
 - 改进了策略 SDK 的 HTTP 缓存，减少了一半的所需 HTTP 调用数。
 - 更丰富的日志/审核/遥测，用于改进的故障检测和调试。
 - 支持外部/外部标签，以便迁移到 AIP 标签。
 - 支持第三方应用程序从 SCC 下载敏感类型。
 - 公开更多遥测设置，并可配置（缓存/线程行为等）。
 
### <a name="sdk-changes"></a>SDK 更改

 - mip_common 拆分为 mip_core .dll 和 mip_telemetry。
 - 将 mip：： ContentState 重命名为 mip：:D ataState 以说明应用程序如何与高级别的数据交互。
 - mip：： AdhocProtectionRequiredError 异常由 FileHandler：： SetLabel 引发，用于通知应用程序它必须先应用即席保护，然后才能应用标签。
 - 当取消了某个操作（例如由于关闭或 HTTP 取消操作）时，将引发 mip：： OperationCancelledError 异常。
 - 新 Api：
    - mip：： ClassificationResult：： GetSensitiveInformationDetections
    - mip：： FileEngine：： GetLastPolicyFetchTime
    - mip：： FileEngine：： GetDefaultSensitivityLabel
    - mip：： FileEngine：： GetPolicyId
    - mip：： FileEngine：： HasClassificationRules
    - mip：： FileEngine：： Settings：： SetPolicyCloudEndpointBaseUrl
    - mip：： FileHandler：： GetDecryptedTemporaryFileAsync
    - mip：： FileHandler：： Observer：： OnGetDecryptedTemporaryFileFailure
    - mip：： FileHandler：： Observer：： OnGetDecryptedTemporaryFileSuccess
    - mip：： File/Policy/ProtectionProfile：： SetTaskDispatcherDelegate
    - mip：： File/Policy/ProtectionProfile：： SetTelemetryConfiguration
    - mip：： HttpRequest：： GetBody 返回 std：： vector < uint8_t > 而不是 std：： string
    - mip：： HttpRequest：： GetId
    - mip：:P olicyEngine：： GetLastPolicyFetchTime
    - mip：:P olicyEngine：： GetPolicyId
    - mip：:P olicyEngine：： HasClassificationRules
    - mip：:P olicyEngine：： Settings：： SetCloudEndpointBaseUrl
    - mip：:P rotectionDescriptor：： GetContentId
    - （接口） mip：： TaskDispatcherDelegate
 
### <a name="new-requirements"></a>新要求
 - 必须在处理终止之前调用 mip：： ReleaseAllResources （清除对所有配置文件、引擎和处理程序的引用后）
 - （interface） mip：： Executionstate&：： GetClassificationResults 返回类型，而 "classificationIds" 参数已更改
 - （接口） mip：： FileExecutionState：： GetAuditMetadata 可以由应用程序实现，以指定详细信息以与租户管理员的审核仪表板（例如发件人、收件人、上次修改时间等）进行呈现。
 - （接口） mip：： FileExecutionState：： GetClassificationResults 返回类型已更改，它现在需要 FileHandler 参数
 - （接口） mip：： FileExecutionState：： GetDataState 应由应用程序实现，以指定应用程序如何与 contentIdentifier 交互
 - （接口） mip：： HttpDelegate 接口需要 "CancelOperation" 和 "CancelAllOperations" 方法
 - （接口） mip：： HttpDelegate 接口 "Send" 和 "SendAsync" 返回 mip：： HttpOperation，而不是 mip：： Httpresponse.cache
 - （接口） mip：： Httpresponse.cache：： GetBody 返回 std：： vector < uint8_t > 而不是 std：： string
 - （接口） mip：： Httpresponse.cache 接口需要 "GetId" 方法实现
 - mip：： ContentLabel：： GetCreationTime 返回 std：： chrono：： time_point 而不是 std：： string
 - mip：： FileEngine：： CreateFileHandlerAsync 不再接受 "contentIdentifier" 参数
 - mip：:P olicyHandler：： NotifyCommitedActions 重命名为 mip：:P olicyHandler：： NotifyCommittedActions


## <a name="version-110"></a>版本1.1。0

**发布日期**：2019年1月15日

此版本引入了对以下平台的支持：

  - .NET
  - iOS SDK （策略 API）
  - Android SDK （策略 API 和保护 API）

### <a name="new-features"></a>新功能

- ADRMS 支持
- 保护 API 操作真正是异步的（在 Win32 上），允许同时进行非阻塞加密/解密操作
  - 现在可以在任何后台线程上调用应用程序回调（AuthDelegate、HTTPDelegate 等）
- IT 管理员设置的自定义标签属性现在可以通过 mip：： Label：： GetCustomSettings 进行读取
- 现在可以直接从文件中检索序列化发布许可证，无需通过 mip：： FileHandler：： GetSerializedPublishingLicense 进行任何 HTTP 操作
- 当完成通过 mip：： FileProfile：：:P FileEngine olicyEngine via mip：：：： Observer：： OnAddPolicyEngineStarting/mip：:P olicyProfile：： Observer：： OnAddEngineStarting 创建 mip：：：：时，将通知应用程序是否需要 HTTP 操作
- 检测到受保护的内容是否有过期日期，或未使用便利方法 mip 进行简化：:P rotectionDescriptor：:D oesContentExpire
- 分类
  - 可从 SCC 服务获取敏感度类型（用于 CC #、passport # 等的正则表达式）
    - 通过设置 mip：： FileEngine：： Settings/mip：:P olicyEngine：： Settings 标志来启用功能
    - 通过 mip：： FileEngine：： ListSensitivityTypes/mip：:P olicyEngine：： ListSensitivityTypes 读取类型
  - 可以将外部文档扫描程序实用工具的分类结果送入到 MIP，以根据文档内容来驱动推荐/必需的标签
    - 通过 mip：： FileExecutionState：： GetClassificationResults/MIP：： Executionstate&：： GetClassificationResults 将结果传递给 MIP
    - 当分类结果与指示必需/推荐标签的策略规则匹配时，mip：： ApplyLabelAction 和 mip：： RecommendLabelAction 可以由 mip：:P olicyEngine：： ComputeActions 返回

### <a name="new-requirements"></a>新要求 

  - 已强制填充 ID/名称/版本字段 mip：： ApplicationInfo 创建 mip：： FileProfile、mip：:P olicyProfile 和 mip：:P rotectionProfile
  - 创建 mip：： FileHandlers 时，应用程序必须实现新的 mip：： FileExecutionState 接口
  
### <a name="new-exceptions"></a>新异常 

  - mip：： NoAuthTokenError 在应用程序的 AuthDelegate 返回空标记时引发（因为取消）
    - 适用于创建：
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - 如果未为标签配置租户，则引发 mip：： NoPolicyError
    - 适用于创建：
      - mip::FileEngine
      - mip::PolicyEngine
  - 如果为特定用户/设备/平台/租户禁用了 RMS 服务，则引发 mip：： ServiceDisabledError
    - 适用于创建：
      - mip::FileHandler
      - mip::ProtectionHandler
  - 如果用户无权解密文档或内容已过期，则引发 mip：： NoPermissionsError
    - 适用于创建：
      - mip::FileHandler
      - mip::ProtectionHandler

## <a name="next-steps"></a>后续步骤

- 有关支持的平台等的信息，请参阅[MIP SDK faq 和问题](faqs-known-issues.md)。
- 有关如何开始利用 MIP SDK 的信息，请参阅[MIP sdk 设置和配置](setup-configure-mip.md)。
