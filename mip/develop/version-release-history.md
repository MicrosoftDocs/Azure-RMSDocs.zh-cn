---
title: Microsoft 信息保护 (MIP) SDK 版本发行历史记录和支持策略
description: 适用于 MIP SDK 的版本发行历史记录和更改注释。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/25/2019
ms.author: mbaldwin
ms.openlocfilehash: 1b34606abcf9093bc082d11b576d5d521e4d7777
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844194"
---
# <a name="microsoft-information-protection-mip-software-development-kit-sdk-version-release-history-and-support-policy"></a>Microsoft 信息保护 (MIP) 软件开发工具包 (SDK) 版本发行历史记录和支持策略

## <a name="servicing"></a>维护

发布下一个 GA 版本后，每年支持 (GA) 版本。 文档可能不包含有关不支持的版本的信息。 修补程序和新功能仅适用于最新的 GA 版本。

不应在生产中部署预览版本。 请改用最新的预览版本来测试新功能或即将推出的新功能或修补程序。 仅支持最新的预览版本。

## <a name="release-history"></a>版本历史记录

使用以下信息可查看受支持版本的新增功能或更改内容。 最新版本会最先列出。

> [!NOTE]
> 未列出次要修补程序。 如果 SDK 出现问题，我们建议你检查是否已通过最新的 GA 版本修复了此问题。 如果问题仍然存在，请检查当前预览版。
>  
> 若要获得技术支持，请访问 [Microsoft 信息保护论坛 Stack Overflow](https://stackoverflow.com/questions/tagged/microsoft-information-protection)。

## <a name="version-1897"></a>版本1.8.97

**发布日期：** 2021年2月24日

- 修复了一个 bug，其中子标签未正确筛选并包含所有类型的标签，即使未请求也是如此。 
- 修复了标签 `RemoveProtection()` 元数据不完整时标签未在其上保留的 bug。 

## <a name="version-1894"></a>版本1.8.94

**发布日期：** 2021年2月8日

- 修复了 NuGet 包中的 bug，其中 c + + 项目的调试配置部署了版本二进制文件。 版本1.8.86 可能会导致本机 c + + 应用崩溃。 请确保更新到1.8.94 或更高版本。
- 修复了一个 bug，要求策略引擎才能删除保护。 
  - 如果策略引擎无法加载并且存在标签元数据，则会在删除保护后丢弃该策略。 
- 修复了在 `labelInfo.xml` 将文件更改为另一个受保护的标签时生成了空的 bug。 

## <a name="version-1886"></a>版本1.8.86

**发布日期：** 2021年1月13日

### <a name="general-changes"></a>常规更改

- 添加了对 ARM 上 Mac 的支持。
- 已签署 Mac 的所有 .dylib 文件。
- 所有三个 Sdk 完全支持所有云。
- 将 `TelemetryConfiguration` 重命名为 `DiagnosticConfiguration`。
- 更新 `MipContext` 为接受 `DiagnosticConfiguration` 而不是 `TelemetryConfiguration` 。
- 公开 `AuditDelegate` 的新。
- 几个自定义设置的名称已更改，并将在1.9 版中删除。 它们将继续与版本1.8 中的更新名称并行工作。 

| 新名称          | 旧名称                   |
| ----------------- | -------------------------- |
| is_debug_audit    | is_debug_telemetry         |
| is_audit_disabled | is_built_in_audit_disabled |

### <a name="file-sdk"></a>文件 SDK

- 添加了对具有双重密钥加密的用户定义标签的支持。
- 添加了一个 API， `MsgInspector.BodyType` 用于公开 MSG 文件的正文编码类型。
- 添加了 Api 以支持 User-Defined 权限的双密钥加密。
- 为添加了标志，该标志 `mip::FileHandler` 允许调用方禁用审核发现事件发送。 这修复了使用 `ClassifyAsync()` API 会导致重复发现事件的情况。
- 修复了以下错误： 
  - 设置对 XPS 文件的保护失败。
  - 从 SharePoint Online 上传/下载并删除自定义权限后，不能打开文件。
  - `RemoveProtection()` 函数将接受 .rpmsg 输入。 现在只接受 MSG 文件。
  - 尝试跟踪或撤消未保护的文件时出现故障。

### <a name="policy-sdk"></a>策略 SDK

- `ActionId`从默认的元数据属性中删除，以确保 Microsoft Office 和 SharePoint Online 标记的文档之间的一致性。
- 添加了对 Azure 监控范围特定标签的支持。
- 添加了通过委托重写遥测和审核的功能。
  - 审核委派提供将 AIP 审核事件发送到 AIP Analytics 以外的目标的功能，或除 AIP 分析以外的其他功能。
- 为添加了标志，该标志 `mip::PolicyHandler` 允许调用方发现审核发现事件发送。 这修复了使用 `ClassifyAsync()` API 会导致重复发现事件的情况。
- 修复了在某些情况下无法打开加密的策略数据库的 bug。
- 公开 `AuditDelegate` 的新，允许开发人员覆盖默认的 MIP SDK 审核管道并将事件发送到其自己的基础结构。 
- `mip::ClassifierUniqueIdsAndContentFormats``GetContentFormat()`现在返回， `std::string` 而不是 `mip::ContentFormat` 。 此更改将在 .NET 和 Java 包装器中复制。 
- `ContentFormat.Default` 现在为 `ContentFormat.File` 。

### <a name="protection-sdk"></a>保护 SDK

- 添加了一个 `ProtectionEngineSettings.SetAllowCloudServiceOnly` 属性，该属性将在为 true 时禁止任何与 Active Directory Rights Management Services 群集的连接。 仅使用云环境。
- 添加了获取委派许可证的支持。
  - 委托许可证允许服务代表用户提取内容许可证。
  - 这允许服务查看权限数据并代表用户解密，而无需对服务进行其他调用。  

### <a name="java-wrapper-public-preview"></a>Java 包装 (公共预览版) 

- 添加了对跟踪和撤消到 Java 包装器的支持。
- 已将流支持添加到 Java 包装器

### <a name="c-api"></a>C API

- 已从 C API 删除 **MIP_FLIGHTING_FEATURE_KEEP_PDF_LINEARIZATION** 标志。

## <a name="version-17147"></a>版本1.7.147

### <a name="file-sdk"></a>文件 SDK

- .PBIX 文件格式的次要 bug 修复。 

## <a name="version-17145"></a>版本1.7.145

**发布日期：** 2020年11月13日

### <a name="general-changes"></a>常规更改

- 更新了 NuGet 包以仅复制更新而不是始终复制依赖项。
- .NET 上的调试配置将使用本机库的发行版。 我们发现，在调试模式下向远程服务器部署 .NET 解决方案的客户需要安装 VC + + 调试运行时，这并不是很简单。 如果需要在中调试到本机库，请将 SDK 可再发行版本中的 Dll 复制到项目文件夹中 (https://ala.ms/mipsdkbins)
- 修复了一个为 .NET Core 项目生成警告的 bug。

## <a name="version-17133"></a>版本1.7.133

**发布日期**：2020年9月23日

### <a name="general-sdk-changes"></a>常规 SDK 更改

- 适用于 Windows 和 Ubuntu 18.04 的 Java 公开预览版。
- Windows 上现在支持 .NET Core。
- Ubuntu 18.04 上的公共预览版支持 .NET Core。
- 当存储缓存类型设置为时，改进了密钥存储的本地日志记录 `OnDiskEncrypted.`
- 已启用 .NET 包装上的功能试验
- 已将 SDK 遥测行为恢复为1.6。 仅当选择 "仅限最小遥测" 时，才会发送一组最小的使用情况事件。

### <a name="file-sdk"></a>文件 SDK

- 修复了中的 UTF-16/UTF-8 正文转换 `MSGInspector` 。
- 将文件 SDK 保护的文件的默认最大文件大小限制设置为6GB。
  - 由于在可用内存中 *至少* 需要文件大小的大型文件进行解密而造成的更改。
  - 可以通过自定义设置重写 `max_file_size_for_protection` 。
- 添加了对线性 Pdf 的支持。
- 修复了更改事件中未更新 LastModifiedDate 的 bug。
- 修复了受保护的 PDF 创建中的内存泄漏。
- 文件 SDK 支持吊销跟踪的文件。
- `FileEngine::Settings::SetLabelFilter` 已弃用，请 `ConfigureFunctionality` 改用。

### <a name="policy-sdk"></a>策略 SDK

- 策略 SDK 现在支持仅加密标记操作。
- 修复了 `mip::Identity` 从缓存引擎中未正确加载的 bug。
- 修复了分类 GUID 比较在分类 API 中区分大小写的 bug。
- 通过添加新字段增加了审核事件。

### <a name="protection-sdk"></a>保护 SDK

- 修复了 `mip::Identity` 从缓存引擎中未正确加载的 bug。
- 添加了针对新创建的发布许可证的隐式注册。
- 添加了对用于在 Office 文件中支持 DKE 的加密算法的支持。
- 已使 `documentId` 和 `owner` 参数成为可选参数。

### <a name="c-apis"></a>C Api

- 添加了缺少的标识和 DKE Api。
- `AuthDelegate`从配置文件移动到跨所有 sdk 的引擎。
- 适用于 C 的发布策略 SDK 示例
- `MIP_CC_CreateProtectionEngineSettingsWithIdentity` 已弃用，请 `MIP_CC_CreateProtectionEngineSettingsWithIdentityAndAuthCallback` 改用。
- `MIP_CC_CreateProtectionEngineSettingsWithEngineId` 已弃用，请 `MIP_CC_CreateProtectionEngineSettingsWithEngineIdAndAuthCallback` 改用。
- `MIP_CC_CreateProtectionProfileSettings` 签名已更改。
- `MIP_CC_CreatePolicyEngineSettingsWithIdentity` 已弃用，请使用 `MIP_CC_CreatePolicyEngineSettingsWithIdentityAndAuthCallback` 。
- `MIP_CC_CreatePolicyEngineSettingsWithEngineId` 已弃用，请使用 `MIP_CC_CreatePolicyEngineSettingsWithEngineIdAndAuthCallback` 。
- `MIP_CC_PolicyEngineSettings_SetLabelFilter` 已弃用，请使用 `MIP_CC_PolicyEngineSettings_ConfigureFunctionality` 。
- `MIP_CC_CreatePolicyProfileSettings` 签名已更改。

### <a name="breaking-changes"></a>重大更改

#### <a name="common"></a>通用

- `TelemetryConfiguration::isTelemetryOptedOut` 已重命名为 `isMinimalTelemetryEnabled`。 

#### <a name="c-api"></a>C API

- `mip_cc_document_state` 已使用新值 `mip_cc_metadata_version_format` contentMetadataVersionFormat 更新

## <a name="version-16103"></a>版本1.6.103

**发布日期**：2020年4月16日

### <a name="general-sdk-changes"></a>常规 SDK 更改

- 为所有非 ADRMS HTTP 通信强制执行 TLS 1.2。
- 已将 iOS/macOS HTTP 实现从 NSURLConnection 迁移到 NSURLSession。
- 已将 iOS 遥测组件从 Aria SDK 迁移到 1DS SDK。
- 遥测组件现在使用适用于 iOS、macOS 和 Linux 的 MIP HttpDelegate。  (以前仅) win32。
- 提高了 C API 的类型安全性。
- 将 AuthDelegate 从配置文件移动到 c + +、c # 和 Java Api 中的引擎。
- AuthDelegate 从的构造函数移 `Profile::Settings` 到 `Engine::Settings` 。
- 向 NoPolicyError 添加了类别，以提供有关策略同步失败的原因的详细信息。
- 已添加 `PolicyEngine::GetTenantId` 方法。
- 为所有云添加了显式支持。
  - `Engine::Settings::SetCloud`用于设置目标云 (GCC 高、21-Vianet 等的新方法 ) 。
  - `Engine::Settings::SetCloudEndpointBaseUrl`已识别的云不再需要现有的方法调用。
- 已为 iOS 二进制文件启用 bitcode。

### <a name="file-sdk"></a>文件 SDK

- 添加 `IFileHandler::InspectAsync` 到 c # 和 Java 包装器
- 通过 `FileProfile::AcquirePolicyAuthToken` 触发策略令牌获取的新支持，使应用程序能够使其令牌缓存更热。    
- `MsgInspector::GetAttachments` 返回 `vector<shared_ptr<MsgAttachmentData>>` 而不是 `vector<unique_ptr<MsgAttachmentData>>`
- `TelemetryConfiguration::isOptedOut` 设置现在完全禁用遥测。 以前发送了一组最小遥测数据。

### <a name="policy-sdk"></a>策略 SDK

- 新支持触发令牌采集，使应用程序能够通过使其令牌缓存更热 `PolicyProfile::AcquireAuthToken` 。
- 默认情况下，筛选 HYOK 标签。
- 与已删除标签关联的元数据现在将被删除。
- 如果缓存的标签策略与敏感度策略之间出现不匹配，则将清除策略缓存。
- 版本控制元数据的新支持：
  - 文件格式可能会采用其标签元数据的位置/格式。 在这种情况下，应用程序应提供所有元数据的 MIP，而 MIP 将确定哪些元数据为 "true"。
  - `ContentLabel::GetExtendedProperties` 现在返回 `vector<MetadataEntry>` 而不是 `vector<pair<string, string>>` 。
  - `MetadataAction::GetMetadataToAdd` 现在返回 `vector<MetadataEntry>` 而不是 `vector<pair<string, string>>` 。
  - `ExecutionState::GetContentMetadata` 现在应返回 `vector<MetadataEntry>` 而不是 `vector<pair<string, string>>` 。
  - `ExecutionState::GetContentMetadataVersion` 应返回应用程序为当前文件格式识别的最高版本的元数据 (通常为 0) 。
  - `PolicyEngine::GetWxpMetadataVersion` 返回租户管理员配置的 Office 文档的元数据版本 (0 = 默认值，1 = 启用 coauth 格式) 。
  - C API 中的等效更改：
    - `MIP_CC_ContentLabel_GetExtendedProperties`
    - `MIP_CC_MetadataAction_GetMetadataToAdd`
    - `mip_cc_metadata_callback`
    - `mip_cc_document_state`
    - `MIP_CC_PolicyEngine_GetWxpMetadataVersion`
- `TelemetryConfiguration::isOptedOut` 设置现在完全禁用遥测。 以前发送了一组最小遥测数据。 

### <a name="protection-sdk"></a>保护 SDK

- 支持对文档跟踪进行注册和吊销。
- 新支持在发布时生成预许可证。
- 公开了保护服务使用的公共 Microsoft TLS 证书。
   - `GetMsftCert` 和 `GetMsftCertPEM`
   - 如果应用程序覆盖 `HttpDelegate` 接口，则它必须信任此 CA 颁发的服务器证书。
   - 此要求在2020中应延迟删除。    

## <a name="version-15124"></a>版本1.5.124

**发布日期**：2020年3月2日

### <a name="general-sdk-changes"></a>常规 SDK 更改

- Java API (仅限 Windows 的) 
- 异步 MIP 任务的取消
  - 所有异步调用都使用取消 () 方法返回 mip：： AsyncControl 对象
- 延迟-加载相关二进制文件
- 选择性地屏蔽特定遥测/审核属性
   - 可通过 mip：： TelemetryConfiguration：： maskedProperties 配置
- 改进的异常：
  - 所有错误都包括说明字符串中的可操作相关 Id
  - 网络错误具有 "Category"、"BaseUrl"、"RequestId" 和 "StatusCode" 字段
- 改进的 C API 结果/错误详细信息

### <a name="file-sdk"></a>文件 SDK

- 无网络检查文件是否已标记或受保护
  - mip：： FileHandler：： IsLabeledOrProtected () 
  - 如果文件包含僵尸标签元数据，则为误报 (的小风险) 
- 与特定保护类型关联的筛选标签
  - 可通过 mip：： FileEngine：： Settings：： SetLabelFilter () 配置
- 向文件 API 公开策略数据
  - mip：： FileEngine：： GetPolicyDataXml () 

### <a name="policy-sdk"></a>策略 SDK

- 水印/页眉/页脚操作的动态内容标记：
  - MIP 将自动填充 $ {Item. Label}、$ {Item.Name}、$ {User.Name}、$ {}、$ {} 等字段
  - mip：： Identity 可使用用户友好的 "name" 字段进行构造，该字段由动态内容标记使用
  - 可通过 mip 配置：:P olicyEngine：： Settings：： SetVariableTextMarkingType () 
- 无网络检查是否标记内容
  - mip：:P olicyHandler：： IsLabeled () 
  - 如果 content 包含僵尸标签元数据，则为误报 (的小风险) 
- 标签策略缓存 TTL
  - 默认值：30天
  - 可通过 mip 配置：:P olicyProfile：： SetCustomSettings () 
- **重大更改**
  - 已将 PolicyEngine 的列表中的 LabelFilter 更新为可为 null 的位域。

### <a name="protection-sdk"></a>保护 SDK

- 预许可
  - 与以前检索到的用户证书相同，与加密的内容一起存在，允许对内容进行脱机解密
  - mip：:P rotectionHandler：： ConsumptionSettings 可以使用预许可
  - mip：:P rotectionEngine：： LoadUserCert |Async () 获取根据 mip：:P rotectionProfile 的缓存策略存储的用户证书
- 服务器特定的功能检查
  - 检查用户的租户是否支持 "仅加密" 功能 (仅在 Azure RMS 中可用) 
  - mip：:P rotectionEngine：： IsFeatureSupported () 
- 提取 RMS 模板时更丰富的详细信息
- **重大更改**
  - `mip::ProtectionEngine::GetTemplates()``vector<shared_ptr<string>>` `vector<shared_ptr<mip::TemplateDescriptor>>` (c + +) 替换的返回值
  - `mip::ProtectionEngine::Observer::OnGetTemplatesSuccess()` 回调 `shared_ptr<vector<string>>` 参数替换为 `vector<shared_ptr<mip::TemplateDescriptor>>` (c + +) 
  - IProtectionEngine. Templatedescriptor.gettemplates |Async () 返回值 `List<string>` 已替换为 `List<TemplateDescriptor>` 。 (C#)
  - MIP_CC_ProtectionEngine_GetTemplates () mip_cc_guid * 参数替换为 mip_cc_template_descriptor * (C API) 

### <a name="c-api"></a>C API

- **重大更改**：更新了大多数函数以包括 mip_cc_error * 参数，可以为 NULL
  

### <a name="errorexception-updates"></a>错误/异常更新

- 错误处理摘要：
  - AccessDeniedError：用户无权访问内容
      - NoAuthTokenError：应用未提供身份验证令牌
      - NoPermissionsError：尚未向用户授予对特定内容的权限，但提供了引用者/所有者
      - ServiceDisabledError：已对用户/设备/平台/租户禁用服务
  - AdhocProtectionRequiredError：设置标签之前必须设置即席保护
  - BadInputError：用户/应用的输入无效
      - InsufficientBufferError：来自用户/应用的无效缓冲区输入
      - LabelDisabledError：标识 ID 已被识别，但被禁用以供使用
      - LabelNotFoundError：无法识别的标签 ID
      - TemplateNotFoundError：无法识别的模板 ID
  - ConsentDeniedError：未向用户/应用授予许可许可的操作
  - DeprecatedApiError：此 API 已弃用
  - FileIOError：读取/写入文件失败
  - InternalError：意外的内部错误
  - NetworkError
      - ProxyAuthenticationError：需要代理身份验证
    - 类别 = BadResponse：服务器返回了不可读的 HTTP 响应 (重试可能会成功) 
    - 类别 = 已取消：无法建立 HTTP 连接，因为用户/应用取消了操作 (重试可能会成功) 
    - Category = FailureResponseCode： Server 返回了一般失败响应 (重试可能会成功) 
    - 类别 = NoConnection：无法建立 HTTP 连接 (重试可能会成功) 
    - 类别 = 脱机：无法建立 HTTP 连接，因为应用程序处于脱机模式 (重试不会成功) 
    - 类别 = 代理：由于代理问题而无法建立 HTTP 连接 (重试可能不会成功) 
    - 类别 = SSL：由于 SSL 问题而无法建立 HTTP 连接 (重试可能不会成功) 
    - 类别 = 限制：服务器返回了 "限制" 响应 (回退/重试可能会成功) 
    - 类别 = 超时：无法在超时后建立 HTTP 连接 (重试可能会成功) 
    - 类别 = UnexpectedResponse：服务器返回了意外数据 (重试可能会成功) 
  - NoPolicyError：没有为标签配置租户或用户
  - NotSupportedError：操作在当前状态中不受支持
  - OperationCancelledError：操作已取消
  - PrivilegedRequiredError：除非分配方法 = 特权，否则不能修改标签
- 更改
  - 删除未使用的 PolicySyncError。 替换为 NetworkError
  - 删除未使用的 TransientNetworkError。 替换为 NetworkError 类别

## <a name="version-140"></a>版本1.4。0 

**发布日期**：2019年11月6日

此版本引入了对 .NET 包中 (保护 SDK 的支持) 。

### <a name="sdk-changes"></a>SDK 更改
- 性能改进和 bug 修复
- 将 StorageType 枚举重命名为 CacheStorageType
- Android 链接到 libc + + 而不是 gnustl
- 删除了以前不推荐使用的 Api
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
- 已删除 mip_telemetry.dll (合并到 mip_core.dll) 

### <a name="file-sdk"></a>文件 SDK

- .RPMSG
  - 加密
  - 添加了对 string8 解密的支持
- 可配置的 .PFILE 扩展行为 (默认值 <EXT> 。.PFILE 或 P <EXT>) 
  - ProtectionSettings::SetPFileExtensionBehavior

### <a name="policy-sdk"></a>策略 SDK

- 完成 C API
- 配置与保护关联的标签的筛选
  - PolicyEngine：：设置也：： SetLabelFilter () 

### <a name="protection-sdk"></a>保护 SDK

- 删除了以前不推荐使用的 Api
  - 已删除 ProtectionEngine：： CreateProtectionHandlerFromDescriptor [Async] (使用 ProtectionEngine：： CreateProtectionHandlerForPublishing [Async] ) 
  - 已删除 ProtectionEngine：： CreateProtectionHandlerFromPublishingLicense [Async] (使用 ProtectionEngine：： CreateProtectionHandlerForConsumption [Async] ) 
- 完成 c # API
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


## <a name="version-130"></a>版本 1.3.0

**发布日期**：2019年8月22日

### <a name="new-features"></a>新功能

- `mip::MipContext` 是新的最高级别的对象。
- 现在支持解密受保护的消息文件。
- 检查 .rpmsg 文件是通过和支持的。 `mip::FileInspector` `mip::FileHandler::InspectAsync()`
- 磁盘上的缓存现在可以有选择性地加密。
- 保护 SDK 现在支持中文云客户。
- Android 上的 Arm64 支持。
- IOS 上的 Arm64e 支持。
- 现在可以禁用 (EUL) 缓存的最终用户许可证。
- 。 .pfile 加密可能会通过 `mip::FileEngine::EnablePFile`
- 通过减少 HTTP 调用数提高了保护操作的性能
- 从中移除委托标识详细信息， `mip::Identity` 并 `DelegatedUserEmail` 将其添加到 `mip::FileEngine::Settings` 、、 `mip::ProtectionSettings` `mip::PolicyEngine::Settings` 和 `mip::ProtectionHandler` 的 `PublishingSettings` 和 `ConsumptionSettings` 。
- 先前返回面部的函数现在返回一个 `mip::Label` 对象。

### <a name="changes"></a>更改

* 在以前的版本中，我们需要你调用 `mip::ReleaseAllResources` 。 版本1.3 将此替换为 `mip::MipContext::~MipContext` 或 `mip::MipContext::Shutdown` 。
* 已 `ActionSource` 从 `mip::LabelingOptions` 和删除 `mip::ExecutionState::GetNewLabelActionSource`
* 替换 `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptor` 为 `mip::ProtectionEngine::CreateProtectionHandlerForPublishing` 。
* 替换 `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicense` 为 `mip::ProtectionEngine::CreateProtectionHandlerForConsumption` 。
* 重命名 `mip::PublishingLicenseContext` 为 `mip::PublishingLicenseInfo` ，并更新为包含丰富的字段，而不是原始序列化的字节。
* `mip::PublishingLicenseInfo` 在分析发布许可证 (PL) 后，包含与 MIP 相关的数据。
* `mip::TemplateNotFoundError``mip::LabelNotFoundError`当应用程序通过 MIP 找不到的模板 id 或标签 id 时引发。
* 通过和的声明参数添加了对基于标签的条件性访问的支持 `AcquireToken()` `mip::AuthDelegate::OAuth2Challenge()` 。 尚未通过安全和合规中心门户公开此功能。


## <a name="version-120"></a>版本 1.2.0

**发布日期**：2019年4月15日

### <a name="new-features"></a>新功能

 - 遥测组件现在使用与 MIP 的其余部分相同的 HTTP stack，即使客户端应用程序已使用 HttpDelegate 重写它也是如此。
 - 客户端应用程序可以通过重写配置文件中的 TaskDispatcherDelegate 来控制异步任务的线程行为。
 - .RPMSG 加密现为预览版。
 - 与保护 SDK 协调文件/策略 SDK 异常处理行为：
    - 如果代理配置为要求身份验证，则所有 Sdk 引发的 ProxyAuthError。
    - 当应用程序的 mip：： AuthDelegate：： AcquireOAuth2Token 的实现提供空的身份验证令牌时，所有 Sdk 引发的 NoAuthTokenError。
 - 改进了策略 SDK 的 HTTP 缓存，减少了半个所需 HTTP 调用数。
 - 更丰富的日志/审核/遥测，用于改进的故障检测和调试。
 - 支持外部/外部标签，以便迁移到 AIP 标签。
 - 支持第三方应用程序从 SCC 下载敏感类型。
 - 更多遥测设置公开并可配置 (缓存/线程行为等 ) 。
 
### <a name="sdk-changes"></a>SDK 更改

 - mip_common.dll 拆分为 mip_core.dll 和 mip_telemetry.dll。
 - 将 mip：： ContentState 重命名为 mip：:D ataState 以说明应用程序如何与高级别的数据交互。
 - mip：： AdhocProtectionRequiredError 异常由 FileHandler：： SetLabel 引发，用于通知应用程序它必须首先应用即席保护，然后才能应用标签。
 - 当取消了某个操作 (例如因关闭或) HTTP 取消而引发时，将引发 mip：： OperationCancelledError 异常。
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
    - mip：： HttpRequest：： GetBody 返回 std：： vector<uint8_t> 而不是 std：： string
    - mip：： HttpRequest：： GetId
    - mip：:P olicyEngine：： GetLastPolicyFetchTime
    - mip：:P olicyEngine：： GetPolicyId
    - mip：:P olicyEngine：： HasClassificationRules
    - mip：:P olicyEngine：： Settings：： SetCloudEndpointBaseUrl
    - mip：:P rotectionDescriptor：： GetContentId
    -  (接口) mip：： TaskDispatcherDelegate
 
### <a name="new-requirements"></a>新要求
 - 在清除对所有配置文件、引擎和处理程序的引用后 (必须在处理终止之前调用 mip：： ReleaseAllResources) 
 -  (接口) mip：： Executionstate&：： GetClassificationResults 返回类型，而 "classificationIds" 参数已更改
 -  (接口) mip：： FileExecutionState：： GetAuditMetadata 可以由应用程序实现，以指定详细信息以面向租户管理员的审核仪表板 (例如发件人、收件人、上次修改的等。 ) 
 -  (接口) mip：： FileExecutionState：： GetClassificationResults 返回类型已更改，它现在需要 FileHandler 参数
 -  (接口) mip：： FileExecutionState：： GetDataState 应由应用程序实现，以指定应用程序如何与 contentIdentifier 交互
 -  (接口) mip：： HttpDelegate 接口需要 "CancelOperation" 和 "CancelAllOperations" 方法
 -  (接口) mip：： HttpDelegate 接口 "Send" 和 "SendAsync" 返回 mip：： HttpOperation，而不是 mip：： Httpresponse.cache
 -  (接口) mip：： Httpresponse.cache：： GetBody 返回 std：： vector<uint8_t> 而不是 std：： string
 -  (接口) mip：： Httpresponse.cache 接口需要 "GetId" 方法实现
 - mip：： ContentLabel：： GetCreationTime 返回 std：： chrono：： time_point 而不是 std：： string
 - mip：： FileEngine：： CreateFileHandlerAsync 不再接受 "contentIdentifier" 参数
 - mip：:P olicyHandler：： NotifyCommitedActions 重命名为 mip：:P olicyHandler：： NotifyCommittedActions


## <a name="version-110"></a>版本 1.1.0 

**发布日期**：2019年1月15日

此版本引入了对以下平台的支持：

  - .NET
  - iOS SDK (策略 SDK) 
  - Android SDK (策略 SDK 和保护 SDK) 

### <a name="new-features"></a>新功能

- ADRMS 支持
- 保护 SDK 操作是 Win32) 上真正的异步 (，允许同时进行非阻塞加密/解密操作
  -  (AuthDelegate、HTTPDelegate 等的应用程序回调现在可以在任何后台线程上调用 ) 
- IT 管理员设置的自定义标签属性现在可以通过 mip：： Label：： GetCustomSettings 进行读取
- 现在可以直接从文件中检索序列化发布许可证，无需通过 mip：： FileHandler：： GetSerializedPublishingLicense 进行任何 HTTP 操作
- 当完成通过 mip：： FileProfile：：:P FileEngine olicyEngine via mip：：：： Observer：： OnAddPolicyEngineStarting/mip：:P olicyProfile：： Observer：： OnAddEngineStarting 创建 mip：：：：时，将通知应用程序是否需要 HTTP 操作
- 检测到受保护的内容是否有过期日期，或未使用便利方法 mip 进行简化：:P rotectionDescriptor：:D oesContentExpire
- 分类
  - 对于 CC #、passport # 等， (regex 表达式的敏感度类型 ) 可从 SCC 服务获取
    - 通过设置 mip：： FileEngine：： Settings/mip：:P olicyEngine：： Settings 标志来启用功能
    - 通过 mip：： FileEngine：： ListSensitivityTypes/mip：:P olicyEngine：： ListSensitivityTypes 读取类型
  - 可以将外部文档扫描程序实用工具的分类结果送入到 MIP，以根据文档内容来驱动推荐/必需的标签
    - 通过 mip：： FileExecutionState：： GetClassificationResults/MIP：： Executionstate&：： GetClassificationResults 将结果传递给 MIP
    - 当分类结果与指示必需/推荐标签的策略规则匹配时，mip：： ApplyLabelAction 和 mip：： RecommendLabelAction 可以由 mip：:P olicyEngine：： ComputeActions 返回

### <a name="new-requirements"></a>新要求 

  - 已强制填充 ID/名称/版本字段 mip：： ApplicationInfo 创建 mip：： FileProfile、mip：:P olicyProfile 和 mip：:P rotectionProfile
  - 创建 mip：： FileHandlers 时，应用程序必须实现新的 mip：： FileExecutionState 接口
  
### <a name="new-exceptions"></a>新异常 

  - 如果应用程序的 AuthDelegate 由于取消 (返回空令牌引发了 mip：： NoAuthTokenError) 
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

- 有关支持的平台等的信息，请参阅 [MIP SDK faq 和问题](faqs-known-issues.md) 。
- 有关如何开始利用 MIP SDK 的信息，请参阅 [MIP sdk 设置和配置](setup-configure-mip.md) 。
