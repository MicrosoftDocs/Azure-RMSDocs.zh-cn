---
title: MIP SDK for C++ Reference
description: MIP SDK for C++ Reference
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: f1e5e06332cac6c0f8beba089d92654781ff6f71
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560438"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C++ Reference

Microsoft 信息保护（MIP） SDK C++允许开发人员管理数据保护策略并将其应用于数据和其他数字资产。

MIP SDK for C++ 包括：

- [枚举和结构](mip-enums-and-structs.md)
- [函数](mip-functions.md)
- 下列类：

 类                         | 描述                                
--------------------------------|---------------------------------------------
[类 mip：： AccessDeniedError](class_mip_accessdeniederror.md)  |  用户无法访问内容。 例如，无权限、内容已撤销。
[类 mip：： Action](class_mip_action.md)  |  操作的接口。 每个操作都转换为，出于应用标签目的，应用程序需要执行的步骤（如策略所定义）
[类 mip：： ActionData](class_mip_actiondata.md)  | 尚未记录。
[类 mip：： AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  指定向文档添加内容脚注的操作类。
[类 mip：： AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  指定添加内容头的操作类。
[类 mip：： AddWatermarkAction](class_mip_addwatermarkaction.md)  |  指定添加水印的操作类。
[类 mip：： AddWatermarkActionData](class_mip_addwatermarkactiondata.md)  | 尚未记录。
[类 mip：： AdhocProtectionRequiredError](class_mip_adhocprotectionrequirederror.md)  |  应设置即席保护来完成对文件的操作。
[类 mip：： ApplicationActionState](class_mip_applicationactionstate.md)  | 尚未记录。
[类 mip：： ApplyLabelAction](class_mip_applylabelaction.md)  |  应用标签操作要求，必须调用应用程序，才能应用特定标签。
[类 mip：： ArgumentData](class_mip_argumentdata.md)  | 尚未记录。
[类 mip：： AuthDelegate](class_mip_authdelegate.md)  |  用于身份验证相关操作的委托。
[类 mip：： AuthDelegate：： OAuth2Challenge](class_mip_authdelegate_oauth2challenge.md)  |  一个类，其中包含调用应用程序所需的所有信息，以便生成 oauth2 标记。
[类 mip：： AuthDelegate：： OAuth2Token](class_mip_authdelegate_oauth2token.md)  |  定义 MIP SDK 期望将 oauth2 标记传回 SDK 的方式的类。
[类 mip：： BadInputError](class_mip_badinputerror.md)  |  输入不正确的错误，在 SDK API 输入无效时引发。
[类 mip：： ClassificationData](class_mip_classificationdata.md)  | 尚未记录。
[类 mip：： ClassificationRequest](class_mip_classificationrequest.md)  |  包含执行状态的分类调用请求的类。
[类 mip：： ClassificationResult](class_mip_classificationresult.md)  |  包含对执行状态进行分类调用的结果的类。
[类 mip：： ComputeEngine](class_mip_computeengine.md)  | 尚未记录。
[类 mip：： ComputeEngine：： Settings](class_mip_computeengine_settings.md)  | 尚未记录。
[类 mip：： ComputeEngineContext](class_mip_computeenginecontext.md)  | 尚未记录。
[类 mip：： ConditionData](class_mip_conditiondata.md)  | 尚未记录。
[类 mip：： ConsentDelegate](class_mip_consentdelegate.md)  |  执行许可相关操作的委托。
[类 mip：： ConsentDeniedError](class_mip_consentdeniederror.md)  |  需要用户同意的操作未获得同意。
[类 mip：： ContentLabel](class_mip_contentlabel.md)  |  Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
[类 mip：： ContentMarkingActionData](class_mip_contentmarkingactiondata.md)  | 尚未记录。
[类 mip：： CustomAction](class_mip_customaction.md)  |  CustomAction 是一个通用操作类，它捕获操作的所有子属性作为属性包。 调用方负责理解操作的含义。
[类 mip：:D eprecatedApiError](class_mip_deprecatedapierror.md)  |  调用方调用了已弃用的 API。
[类 mip：:D ocumentState](class_mip_documentstate.md)  | 尚未记录。
[类 mip：： Error](class_mip_error.md)  |  将从 MIP SDK 报告（引发或返回）的所有错误的基类。
[类 mip：： Executionstate&](class_mip_executionstate.md)  |  执行引擎所需的所有状态的接口。
[类 mip：： FileEngine](class_mip_fileengine.md)  |  此类提供适用于所有引擎功能的接口。
[类 mip：： FileEngine：： Settings](class_mip_fileengine_settings.md)  | 尚未记录。
[类 mip：： FileExecutionState](class_mip_fileexecutionstate.md)  | 尚未记录。
[类 mip：： FileHandler](class_mip_filehandler.md)  |  适用于所有文件处理函数的接口。
[类 mip：： FileHandler：： Observer](class_mip_filehandler_observer.md)  |  观察者接口，使客户端能够获取与文件处理程序相关的通知事件。
[类 mip：： FileInspector](class_mip_fileinspector.md)  | 尚未记录。
[类 mip：： FileIOError](class_mip_fileioerror.md)  |  文件 IO 错误。
[类 mip：： FileProfile](class_mip_fileprofile.md)  |  FileProfile 类是用于使用 Microsoft 信息保护操作的根类。
[类 mip：： FileProfile：： Observer](class_mip_fileprofile_observer.md)  |  观察者接口，供客户端获取配置文件相关事件的通知。
[类 mip：： FileProfile：： Settings](class_mip_fileprofile_settings.md)  |  FileProfile 在其创建期间及其整个生存期内使用的设置。
[类 mip：： HttpDelegate](class_mip_httpdelegate.md)  |  用于重写 HTTP 处理的接口。
[类 mip：： HttpOperation](class_mip_httpoperation.md)  |  一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 操作。
[类 mip：： HttpRequest](class_mip_httprequest.md)  |  描述单个 HTTP 请求的接口。
[类 mip：： Httpresponse.cache](class_mip_httpresponse.md)  |  一个接口，该接口描述在重写 HttpDelegate 时由客户端应用程序实现的单个 HTTP 响应。
[类 mip：： Identity](class_mip_identity.md)  |  标识的抽象。
[类 mip：： InternalError](class_mip_internalerror.md)  |  内部错误。 如果在执行期间出现意外，就会抛出此错误。
[类 mip：： JustificationRequiredError](class_mip_justificationrequirederror.md)  | 尚未记录。
[类 mip：： JustifyAction](class_mip_justifyaction.md)  |  调整操作要求对标签进行降级并在执行状态中设置响应。
[类 mip：： Label](class_mip_label.md)  |  单个 Microsoft 信息保护标签的抽象。
[类 mip：： LabelActionData](class_mip_labelactiondata.md)  | 尚未记录。
[类 mip：： LabelDisabledError](class_mip_labeldisablederror.md)  |  标签已禁用或处于非活动状态。
[类 mip：： LabelGroupData](class_mip_labelgroupdata.md)  | 尚未记录。
[类 mip：： LabelingOptions](class_mip_labelingoptions.md)  |  用于为 SetLabel/DeleteLabel 方法配置标记选项的接口。
[类 mip：： LabelNotFoundError](class_mip_labelnotfounderror.md)  |  标签 ID 无法识别。
[类 mip：： LoggerDelegate](class_mip_loggerdelegate.md)  |  定义 MIP SDK 记录器接口的类。
[类 mip：： MetadataAction](class_mip_metadataaction.md)  |  向内容添加元数据信息的操作。
[类 mip：： MipContext](class_mip_mipcontext.md)  |  MipContext 表示在所有配置文件、引擎和处理程序之间共享的状态。
[类 mip：： MsgAttachmentData](class_mip_msgattachmentdata.md)  | 尚未记录。
[类 mip：： MsgInspector](class_mip_msginspector.md)  | 尚未记录。
[类 mip：： NetworkError](class_mip_networkerror.md)  |  网络错误。 对服务终结点执行网络调用时，由于意外行为所致。
[类 mip：： NoAuthTokenError](class_mip_noauthtokenerror.md)  |  由于缺少身份验证令牌，用户无法访问内容。
[类 mip：： NoPermissionsError](class_mip_nopermissionserror.md)  |  用户无法访问内容。 例如，无权限、内容已撤销。
[类 mip：： NoPolicyError](class_mip_nopolicyerror.md)  |  租户策略未配置为分类/标签。
[类 mip：： NotSupportedError](class_mip_notsupportederror.md)  |  SDK 不支持应用程序请求执行的操作。
[类 mip：： OperationCancelledError](class_mip_operationcancellederror.md)  |  已取消操作。
[类 mip：:P olicyEngine](class_mip_policyengine.md)  |  此类提供适用于所有引擎功能的接口。
[类 mip：:P olicyEngine：： Settings](class_mip_policyengine_settings.md)  |  定义与 PolicyEngine 关联的设置。
[类 mip：:P olicyHandler](class_mip_policyhandler.md)  |  此类为文件上的所有策略处理程序函数提供一个接口。
[类 mip：:P olicyPackageData](class_mip_policypackagedata.md)  | 尚未记录。
[类 mip：:P olicyProfile](class_mip_policyprofile.md)  |  PolicyProfile 类是用于使用 Microsoft 信息保护操作的根类。 典型的应用程序只需要一个 PolicyProfile，但可以根据需要创建多个配置文件。
[类 mip：:P olicyProfile：：观察程序](class_mip_policyprofile_observer.md)  |  观察者接口，供客户端获取配置文件相关事件的通知。
[类 mip：:P olicyProfile：： Settings](class_mip_policyprofile_settings.md)  |  PolicyProfile 在其创建期间及其整个生存期内使用的设置。
[类 mip：:P olicyRuleData](class_mip_policyruledata.md)  | 尚未记录。
[类 mip：:P olicySyncError](class_mip_policysyncerror.md)  |  同步策略数据尝试失败。
[类 mip：:P rivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  由于当前标签被指定为特权操作（相当于管理员操作），因此无法替代。
[类 mip：:P ropertyData](class_mip_propertydata.md)  | 尚未记录。
[类 mip：:P rotectAdhocAction](class_mip_protectadhocaction.md)  |  指定向文档添加临时保护的操作类。
[类 mip：:P rotectByTemplateAction](class_mip_protectbytemplateaction.md)  |  指定向文档添加模板保护的操作类。
[类 mip：:P rotectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  指定向文档添加不转发保护的操作类。
[类 mip：:P rotectionActionData](class_mip_protectionactiondata.md)  | 尚未记录。
[类 mip：:P rotectionDescriptor](class_mip_protectiondescriptor.md)  |  与某段内容相关的保护说明。
[类 mip：:P rotectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  构造描述与一段内容相关联的保护的 ProtectionDescriptor。
[类 mip：:P rotectionEngine](class_mip_protectionengine.md)  |  管理与特定标识有关的保护相关操作。
[类 mip：:P rotectionEngine：：观察程序](class_mip_protectionengine_observer.md)  |  接收与 ProtectionEngine 相关的通知的接口。
[类 mip：:P rotectionEngine：： Settings](class_mip_protectionengine_settings.md)  |  ProtectionEngine 在其创建期间及其整个生存期内使用的设置。
[类 mip：:P rotectionHandler](class_mip_protectionhandler.md)  |  管理特定保护配置的保护相关操作。
[类 mip：:P rotectionHandler：： ConsumptionSettings](class_mip_protectionhandler_consumptionsettings.md)  |  用于创建 ProtectionHandler 以使用现有内容的设置。
[类 mip：:P rotectionHandler：：观察程序](class_mip_protectionhandler_observer.md)  |  接收与 ProtectionHandler 相关的通知的接口。
[类 mip：:P rotectionHandler：:P ublishingSettings](class_mip_protectionhandler_publishingsettings.md)  |  用于创建 ProtectionHandler 以保护新内容的设置。
[类 mip：:P rotectionProfile](class_mip_protectionprofile.md)  |  ProtectionProfile 是用于执行保护操作的根类。
[类 mip：:P rotectionProfile：：观察程序](class_mip_protectionprofile_observer.md)  |  接收与 ProtectionProfile 相关的通知的接口。
[类 mip：:P rotectionProfile：： Settings](class_mip_protectionprofile_settings.md)  |  ProtectionProfile 在其创建期间及其整个生存期内使用的设置。
[类 mip：:P rotectionSettings](class_mip_protectionsettings.md)  |  用于为 SetLabel 方法配置保护选项的接口。
[类 mip：:P roxyAuthenticationError](class_mip_proxyauthenticationerror.md)  |  代理身份验证失败。
[类 mip：:P ublishingLicenseInfo](class_mip_publishinglicenseinfo.md)  |  保存用于创建保护处理程序的发布许可证的详细信息。
[类 mip：： RecommendLabelAction](class_mip_recommendlabelaction.md)  |  建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
[类 mip：： RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  指定从文档中删除内容脚注的操作类。
[类 mip：： RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  指定从文档中删除内容头的操作类。
[类 mip：： RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  指定从文档中删除保护的操作类。
[类 mip：： RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  指定从文档中删除水印的操作类。
[类 mip：： RulePackageData](class_mip_rulepackagedata.md)  | 尚未记录。
[类 mip：： SensitivityConditionData](class_mip_sensitivityconditiondata.md)  | 尚未记录。
[类 mip：： SensitivityTypesRulePackage](class_mip_sensitivitytypesrulepackage.md)  | 尚未记录。
[类 mip：： ServiceDisabledError](class_mip_servicedisablederror.md)  |  由于服务被禁用，用户无法访问内容。
[类 mip：： Stream](class_mip_stream.md)  |  一个类，它定义 MIP SDK 和基于流的内容之间的接口。
[类 mip：： SyncFileBaseData](class_mip_syncfilebasedata.md)  | 尚未记录。
[类 mip：： SyncFilePolicyData](class_mip_syncfilepolicydata.md)  | 尚未记录。
[类 mip：： SyncFileSensitivityData](class_mip_syncfilesensitivitydata.md)  | 尚未记录。
[类 mip：： TaskDispatcherDelegate](class_mip_taskdispatcherdelegate.md)  |  定义 MIP SDK 任务调度程序接口的类。
[类 mip：： TemplateNotFoundError](class_mip_templatenotfounderror.md)  |  RMS 服务无法识别模板 ID。
[类 mip：： TransientNetworkError](class_mip_transientnetworkerror.md)  |  暂时性网络错误。 对服务终结点执行网络调用时，由于意外行为所致。 此错误是暂时性错误，因此可重试该操作。
[类 mip：： UserRights](class_mip_userrights.md)  |  一组用户以及与之关联的权限。
[类 mip：： UserRoles](class_mip_userroles.md)  |  一组用户以及与之关联的角色。