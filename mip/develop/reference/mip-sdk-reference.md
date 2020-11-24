---
title: MIP SDK for c + + 参考
description: MIP SDK for c + + 参考
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: da5ee17fbb177fe9b6e37461a5d35425a3945e59
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565084"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for c + + 参考

Microsoft 信息保护 (MIP) SDK for c + + 允许开发人员管理数据保护策略并将其应用到数据和其他数字资产。

MIP SDK for C++ 包括：

- [枚举和结构](mip-enums-and-structs.md)
- [函数](mip-functions.md)
- 下列类：

## <a name="namespace-mip-classes"></a>命名空间 mip 类

 类                         | 说明                                
--------------------------------|---------------------------------------------
[类 AccessDeniedError](class_mip_accessdeniederror.md)  |  用户无法访问内容。 例如，无权限、内容已撤销。
[类操作](class_mip_action.md)  |  操作的接口。 每个操作都转换为，出于应用标签目的，应用程序需要执行的步骤（如策略所定义）
[类 ActionData](class_mip_actiondata.md)  | 尚无记录。
[类 AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  指定向文档添加内容脚注的操作类。
[类 AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  指定添加内容头的操作类。
[类 AddWatermarkAction](class_mip_addwatermarkaction.md)  |  指定添加水印的操作类。
[类 AddWatermarkActionData](class_mip_addwatermarkactiondata.md)  | 尚无记录。
[类 AdhocProtectionRequiredError](class_mip_adhocprotectionrequirederror.md)  |  应设置即席保护来完成对文件的操作。
[类 ApplicationActionState](class_mip_applicationactionstate.md)  | 尚无记录。
[类 ApplyLabelAction](class_mip_applylabelaction.md)  |  应用标签操作要求，必须调用应用程序，才能应用特定标签。
[类 ArgumentData](class_mip_argumentdata.md)  | 尚无记录。
[类 AsyncControl](class_mip_asynccontrol.md)  |  用于取消异步操作的类。
[类 AuthDelegate](class_mip_authdelegate.md)  |  用于身份验证相关操作的委托。
[类 BadInputError](class_mip_badinputerror.md)  |  输入不正确的错误，在 SDK API 输入无效时引发。
[类 ClassificationData](class_mip_classificationdata.md)  | 尚无记录。
[类 ClassificationRequest](class_mip_classificationrequest.md)  |  包含执行状态的分类调用请求的类。
[类 ClassificationResult](class_mip_classificationresult.md)  |  包含对执行状态进行分类调用的结果的类。
[类 ComputeEngine](class_mip_computeengine.md)  | 尚无记录。
[类 ComputeEngineContext](class_mip_computeenginecontext.md)  | 尚无记录。
[类 ConditionData](class_mip_conditiondata.md)  | 尚无记录。
[类 ConsentDelegate](class_mip_consentdelegate.md)  |  执行许可相关操作的委托。
[类 ConsentDeniedError](class_mip_consentdeniederror.md)  |  需要用户同意的操作未获得同意。
[类 ProtectionHandler：： ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  用于创建 ProtectionHandler 以使用现有内容的设置。
[类 ContentLabel](class_mip_contentlabel.md)  |  Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
[类 ContentMarkingActionData](class_mip_contentmarkingactiondata.md)  | 尚无记录。
[类 CustomAction](class_mip_customaction.md)  |  CustomAction 是一个通用操作类，它捕获操作的所有子属性作为属性包。 调用方负责理解操作的含义。
[类 DeprecatedApiError](class_mip_deprecatedapierror.md)  |  调用方调用了已弃用的 API。
[类 DetailedClassificationResult](class_mip_detailedclassificationresult.md)  |  包含对执行状态进行分类调用的结果的类。
[类 DocumentState](class_mip_documentstate.md)  | 尚无记录。
[类错误](class_mip_error.md)  |  将从 MIP SDK 报告（引发或返回）的所有错误的基类。
[类 Executionstate&](class_mip_executionstate.md)  |  执行引擎所需的所有状态的接口。
[类 FileEngine](class_mip_fileengine.md)  |  此类提供适用于所有引擎功能的接口。
[类 FileExecutionState](class_mip_fileexecutionstate.md)  | 尚无记录。
[类 FileHandler](class_mip_filehandler.md)  |  适用于所有文件处理函数的接口。
[类 FileInspector](class_mip_fileinspector.md)  | 尚无记录。
[类 FileIOError](class_mip_fileioerror.md)  |  文件 IO 错误。
[类 FileProfile](class_mip_fileprofile.md)  |  FileProfile 类是用于使用 Microsoft 信息保护操作的根类。
[类 HttpDelegate](class_mip_httpdelegate.md)  |  用于重写 HTTP 处理的接口。
[类 HttpOperation](class_mip_httpoperation.md)  |  一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 操作。
[类 HttpRequest](class_mip_httprequest.md)  |  描述单个 HTTP 请求的接口。
[类 Httpresponse.cache](class_mip_httpresponse.md)  |  描述单个 HTTP 响应的接口，由客户端应用在重写 HttpDelegate 时实现。
[类标识](class_mip_identity.md)  |  标识的抽象。
[类 InsufficientBufferError](class_mip_insufficientbuffererror.md)  |  缓冲区不足错误。
[类 InternalError](class_mip_internalerror.md)  |  内部错误。 如果在执行期间出现意外，就会抛出此错误。
[类 JustificationRequiredError](class_mip_justificationrequirederror.md)  | 尚无记录。
[类 JustifyAction](class_mip_justifyaction.md)  |  JustifyAction 要求必须合理解释标签降级，并设置执行状态下的响应。
[类标签](class_mip_label.md)  |  单个 Microsoft 信息保护标签的抽象。
[类 LabelActionData](class_mip_labelactiondata.md)  | 尚无记录。
[类 LabelDisabledError](class_mip_labeldisablederror.md)  |  标签已禁用或处于非活动状态。
[类 LabelGroupData](class_mip_labelgroupdata.md)  | 尚无记录。
[类 LabelingOptions](class_mip_labelingoptions.md)  |  用于为 SetLabel/DeleteLabel 方法配置标记选项的接口。
[类 LabelNotFoundError](class_mip_labelnotfounderror.md)  |  标签 ID 无法识别。
[类 LicenseNotRegisteredError](class_mip_licensenotregisterederror.md)  |  未注册许可证。
[类 LoggerDelegate](class_mip_loggerdelegate.md)  |  定义 MIP SDK 记录器接口的类。
[类 MetadataAction](class_mip_metadataaction.md)  |  将元数据信息添加到内容的 Action。
[类 MetadataEntry](class_mip_metadataentry.md)  |  元数据项的抽象类。
[类 MetadataVersion](class_mip_metadataversion.md)  |  MetadataVersion 的接口。 MetadataVersion 确定哪些元数据是活动的，以及如何对其进行处理。
[类 MipContext](class_mip_mipcontext.md)  |  MipContext 表示在所有配置文件、引擎和处理程序之间共享的状态。
[类 MsgAttachmentData](class_mip_msgattachmentdata.md)  | 尚无记录。
[类 MsgInspector](class_mip_msginspector.md)  | 尚无记录。
[类 NetworkError](class_mip_networkerror.md)  |  网络错误。 对服务终结点执行网络调用时，由于意外行为所致。
[类 NoAuthTokenError](class_mip_noauthtokenerror.md)  |  由于缺少身份验证令牌，用户无法访问内容。
[类 NoPermissionsError](class_mip_nopermissionserror.md)  |  用户无法访问内容。 例如，无权限、内容已撤销。
[类 NoPolicyError](class_mip_nopolicyerror.md)  |  租户策略未配置为分类/标签。
[类 NotSupportedError](class_mip_notsupportederror.md)  |  SDK 不支持应用程序请求执行的操作。
[类 AuthDelegate：： OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)  |  一个类，其中包含调用应用程序所需的所有信息，以便生成 oauth2 标记。
[类 AuthDelegate：： OAuth2Token](class_mip_authdelegate_oauth2token.md)  |  一个类，其中包含应用程序提供的访问令牌信息。
[类 FileHandler：：观察程序](class_mip_filehandler_observer.md)  |  Observer 接口，供客户端获取文件处理程序相关事件的通知。
[类 ProtectionEngine：：观察程序](class_mip_protectionengine_observer.md)  |  接收 ProtectionEngine 相关通知的接口。
[类 FileProfile：：观察程序](class_mip_fileprofile_observer.md)  |  Observer 接口，供客户端获取配置文件相关事件的通知。
[类 PolicyProfile：：观察程序](class_mip_policyprofile_observer.md)  |  Observer 接口，供客户端获取配置文件相关事件的通知。
[类 ProtectionHandler：：观察程序](class_mip_protectionhandler_observer.md)  |  接收 ProtectionHandler 相关通知的接口。
[类 ProtectionProfile：：观察程序](class_mip_protectionprofile_observer.md)  |  接收与 ProtectionProfile 相关通知的接口。
[类 OperationCancelledError](class_mip_operationcancellederror.md)  |  已取消操作。
[类 PolicyEngine](class_mip_policyengine.md)  |  此类提供适用于所有引擎功能的接口。
[类 PolicyHandler](class_mip_policyhandler.md)  |  此类为文件上的所有策略处理程序函数提供一个接口。
[类 PolicyPackageData](class_mip_policypackagedata.md)  | 尚无记录。
[类 PolicyProfile](class_mip_policyprofile.md)  |  PolicyProfile 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个 PolicyProfile，但它可以按需创建多个配置文件。
[类 PolicyRuleData](class_mip_policyruledata.md)  | 尚无记录。
[类 PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  由于当前标签被指定为特权操作（相当于管理员操作），因此无法替代。
[类 PropertyData](class_mip_propertydata.md)  | 尚无记录。
[类 ProtectAdhocAction](class_mip_protectadhocaction.md)  |  指定向文档添加临时保护的操作类。
[类 ProtectAdhocDkAction](class_mip_protectadhocdkaction.md)  |  指定向文档添加即席双重密钥保护的操作类。
[类 ProtectByEncryptOnlyAction](class_mip_protectbyencryptonlyaction.md)  |  指定仅对文档添加加密保护的操作类。
[类 ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  指定向文档添加模板保护的操作类。
[类 ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  指定向文档添加不转发保护的操作类。
[类 ProtectDoNotForwardDkAction](class_mip_protectdonotforwarddkaction.md)  |  一个操作类，该操作类指定对文档添加 "不向双重密钥保护"。
[类 ProtectionActionData](class_mip_protectionactiondata.md)  | 尚无记录。
[类 ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  与某段内容相关的保护说明。
[类 ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  构造 ProtectionDescriptor，用于描述与一段内容相关的保护。
[类 ProtectionEngine](class_mip_protectionengine.md)  |  管理与特定标识有关的保护相关操作。
[类 ProtectionHandler](class_mip_protectionhandler.md)  |  管理特定保护配置的保护相关操作。
[类 ProtectionProfile](class_mip_protectionprofile.md)  |  ProtectionProfile 是用于执行保护操作的根类。
[类 ProtectionSettings](class_mip_protectionsettings.md)  |  用于为 SetLabel 方法配置保护选项的接口。
[类 ProxyAuthenticationError](class_mip_proxyauthenticationerror.md)  |  代理身份验证失败。
[类 PublishingLicenseInfo](class_mip_publishinglicenseinfo.md)  |  保存用于创建保护处理程序的发布许可证的详细信息。
[类 ProtectionHandler：:P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  用于创建 ProtectionHandler 以保护新内容的设置。
[类 RecommendLabelAction](class_mip_recommendlabelaction.md)  |  建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
[类 RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  指定从文档中删除内容脚注的操作类。
[类 RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  指定从文档中删除内容头的操作类。
[类 RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  指定从文档中删除保护的操作类。
[类 RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  指定从文档中删除水印的操作类。
[类 RulePackageData](class_mip_rulepackagedata.md)  | 尚无记录。
[类 SensitiveTypeClassificationData](class_mip_sensitivetypeclassificationdata.md)  | 尚无记录。
[类 SensitivityConditionData](class_mip_sensitivityconditiondata.md)  | 尚无记录。
[类 SensitivityTypesRulePackage](class_mip_sensitivitytypesrulepackage.md)  | 尚无记录。
[类 ServiceDisabledError](class_mip_servicedisablederror.md)  |  由于服务被禁用，用户无法访问内容。
[类 FileEngine：： Settings](class_mip_fileengine_settings.md)  | 尚无记录。
[类 PolicyEngine：： Settings](class_mip_policyengine_settings.md)  |  定义与 PolicyEngine 关联的设置。
[类 PolicyProfile：： Settings](class_mip_policyprofile_settings.md)  |  PolicyProfile 在其创建期间及其整个生存期内使用的 Settings。
[类 ProtectionProfile：： Settings](class_mip_protectionprofile_settings.md)  |  由 ProtectionProfile 在创建期间及其整个生存期内使用的设置。
[类 FileProfile：： Settings](class_mip_fileprofile_settings.md)  |  FileProfile 在其创建期间及其整个生存期内使用的 Settings。
[类 ComputeEngine：： Settings](class_mip_computeengine_settings.md)  | 尚无记录。
[类 ProtectionEngine：： Settings](class_mip_protectionengine_settings.md)  |  ProtectionEngine 在其创建期间及其整个生存期内使用的 Settings。
[类流](class_mip_stream.md)  |  一个类，它定义 MIP SDK 和基于流的内容之间的接口。
[类 SyncFileBaseData](class_mip_syncfilebasedata.md)  | 尚无记录。
[类 SyncFilePolicyData](class_mip_syncfilepolicydata.md)  | 尚无记录。
[类 SyncFileSensitivityData](class_mip_syncfilesensitivitydata.md)  | 尚无记录。
[类 TaskDispatcherDelegate](class_mip_taskdispatcherdelegate.md)  |  定义 MIP SDK 任务调度程序接口的类。
[类 TemplateDescriptor](class_mip_templatedescriptor.md)  | 尚无记录。
[类 TemplateNotFoundError](class_mip_templatenotfounderror.md)  |  RMS 服务无法识别模板 ID。
[类 UserRights](class_mip_userrights.md)  |  一组用户以及与之关联的权限。
[类 UserRoles](class_mip_userroles.md)  |  一组用户以及与之关联的角色。