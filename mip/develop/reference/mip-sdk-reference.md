---
title: MIP SDK for C++ Reference
description: MIP SDK for C++ Reference
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2fab85dfd5b5d0d1103f9c3ee4b0d3725a10cb8f
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884823"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C++ Reference

Microsoft 信息保护 (MIP) SDK C++允许开发人员管理数据保护策略并将其应用于数据和其他数字资产。

MIP SDK for C++ 包括：

- [枚举和结构](mip-enums-and-structs.md)
- [函数](mip-functions.md)
- 下列类：

 类                         | 描述                                
--------------------------------|---------------------------------------------
class mip::AccessDeniedError  |  用户无法访问内容。 例如，无权限、内容已撤销。
class mip::Action  |  操作的接口。 每个操作都转换为，出于应用标签目的，应用程序需要执行的步骤（如策略所定义）
类 mip:: ActionData  | _尚无记录。_
class mip::AddContentFooterAction  |  指定向文档添加内容脚注的操作类。
class mip::AddContentHeaderAction  |  指定添加内容头的操作类。
class mip::AddWatermarkAction  |  指定添加水印的操作类。
类 mip:: AddWatermarkActionData  | _尚无记录。_
类 mip:: AdhocProtectionRequiredError  |  应设置即席保护来完成对文件的操作。
类 mip:: ApplicationActionState  | _尚无记录。_
class mip::ApplyLabelAction  |  应用标签操作要求，必须调用应用程序，才能应用特定标签。
类 mip:: ArgumentData  | _尚无记录。_
类 mip:: AuthDelegate  |  用于身份验证相关操作的委托。
class mip::BadInputError  |  输入不正确的错误，在 SDK API 输入无效时引发。
类 mip:: ClassificationData  | _尚无记录。_
类 mip:: ClassificationRequest  |  包含执行状态的分类调用请求的类。
类 mip::ClassificationResult  |  包含对执行状态进行分类调用的结果的类。
类 mip:: ComputeEngine  | _尚无记录。_
类 mip:: ComputeEngineContext  | _尚无记录。_
类 mip:: ConditionData  | _尚无记录。_
类 mip:: ConsentDelegate  |  执行许可相关操作的委托。
类 mip::ConsentDeniedError  |  需要用户同意的操作未获得同意。
class mip::ContentLabel  |  Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
类 mip:: ContentMarkingActionData  | _尚无记录。_
class mip::CustomAction  |  [CustomAction](class_mip_customaction.md) 是一个泛型操作类，它捕获操作的所有子属性作为一个属性包。 调用方负责理解操作的含义。
类 mip::D eprecatedApiError  |  调用方调用了已弃用的 API。
类 mip::D ocumentState  | _尚无记录。_
class mip::Error  |  将从 MIP SDK 报告（引发或返回）的所有错误的基类。
class mip::ExecutionState  |  执行引擎所需的所有状态的接口。
class mip::FileEngine  |  此类提供适用于所有引擎功能的接口。
类 mip:: FileExecutionState  | _尚无记录。_
class mip::FileHandler  |  适用于所有文件处理函数的接口。
类 mip:: FileInspector  | _尚无记录。_
class mip::FileIOError  |  文件 IO 错误。
class mip::FileProfile  |  [FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
类 mip::HttpDelegate  |  用于重写 HTTP 处理的接口。
类 mip:: HttpOperation  |  一个接口, 该接口描述在重写[HttpDelegate](class_mip_httpdelegate.md)时由客户端应用程序实现的单个 HTTP 操作。
class mip::HttpRequest  |  描述单个 HTTP 请求的接口。
类 mip::HttpResponse  |  描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
类 mip:: Identity  |  标识的抽象。
class mip::InternalError  |  内部错误。 如果在执行期间出现意外，就会抛出此错误。
class mip::JustificationRequiredError  | _尚无记录。_
class mip::JustifyAction  |  Justify[Action](class_mip_action.md) 要求必须合理解释标签降级，并设置执行状态下的响应。
class mip::Label  |  单个 Microsoft 信息保护标签的抽象。
类 mip:: LabelActionData  | _尚无记录。_
类 mip:: LabelDisabledError  |  [标签](class_mip_label.md)已禁用或处于非活动状态。
类 mip:: LabelGroupData  | _尚无记录。_
class mip::LabelingOptions  |  用于为 SetLabel/DeleteLabel 方法配置标记选项的接口。
类 mip:: LabelNotFoundError  |  [标签](class_mip_label.md)ID 无法识别。
class mip::LoggerDelegate  |  定义 MIP SDK 记录器接口的类。
class mip::MetadataAction  |  将元数据信息添加到内容的 [Action](class_mip_action.md)。
类 mip:: MipContext  | MipContext 表示在所有配置文件、引擎和处理程序之间共享的状态。
类 mip:: MsgAttachmentData  | _尚无记录。_
类 mip:: MsgInspector  | _尚无记录。_
class mip::NetworkError  |  网络错误。 对服务终结点执行网络调用时，由于意外行为所致。
类 mip:: NoAuthTokenError  |  由于缺少身份验证令牌, 用户无法访问内容。
类 mip:: NoPermissionsError  |  用户无法访问内容。 例如，无权限、内容已撤销。
类 mip:: NoPolicyError  |  租户策略未配置为分类/标签。
class mip::NotSupportedError  |  SDK 不支持应用程序请求执行的操作。
类 mip:: OperationCancelledError  |  操作已取消。
class mip::PolicyEngine  |  此类提供适用于所有引擎功能的接口。
类 mip::PolicyHandler  |  此类为文件上的所有策略处理程序函数提供一个接口。
类 mip::P olicyPackageData  | _尚无记录。_
class mip::PolicyProfile  |  [PolicyProfile](class_mip_policyprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个 [PolicyProfile](class_mip_policyprofile.md)，但它可以按需创建多个配置文件。
类 mip::P olicyRuleData  | _尚无记录。_
class mip::PolicySyncError  |  同步策略数据尝试失败。
class mip::PrivilegedRequiredError  |  由于当前标签被指定为特权操作（相当于管理员操作），因此无法替代。
类 mip::P ropertyData  | _尚无记录。_
class mip::ProtectAdhocAction  |  指定向文档添加临时保护的操作类。
class mip::ProtectByTemplateAction  |  指定向文档添加模板保护的操作类。
class mip::ProtectDoNotForwardAction  |  指定向文档添加不转发保护的操作类。
类 mip::P rotectionActionData  | _尚无记录。_
类 mip::ProtectionDescriptor  |  与某段内容相关的保护说明。
类 mip::ProtectionDescriptorBuilder  |  构造 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，用于描述与一段内容相关的保护。
类 mip::ProtectionEngine  |  管理与特定标识有关的保护相关操作。
类 mip::ProtectionHandler  |  管理特定保护配置的保护相关操作。
class mip::ProtectionProfile  |  [ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
类 mip::P rotectionSettings  |  用于为 SetLabel 方法配置保护选项的接口。
类 mip::P roxyAuthenticationError  |  代理身份验证失败。
类 mip::P ublishingLicenseInfo  |  保存用于创建保护处理程序的发布许可证的详细信息。
类 mip::RecommendLabelAction  |  建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
class mip::RemoveContentFooterAction  |  指定从文档中删除内容脚注的操作类。
class mip::RemoveContentHeaderAction  |  指定从文档中删除内容头的操作类。
class mip::RemoveProtectionAction  |  指定从文档中删除保护的操作类。
class mip::RemoveWatermarkAction  |  指定从文档中删除水印的操作类。
类 mip:: RulePackageData  | _尚无记录。_
类 mip:: SensitivityConditionData  | _尚无记录。_
类 mip:: SensitivityTypesRulePackage  | _尚无记录。_
类 mip:: ServiceDisabledError  |  由于服务被禁用, 用户无法访问内容。
class mip::Stream  |  一个类，它定义 MIP SDK 和基于流的内容之间的接口。
类 mip:: SyncFileBaseData  | _尚无记录。_
类 mip:: SyncFilePolicyData  | _尚无记录。_
类 mip:: SyncFileSensitivityData  | _尚无记录。_
类 mip:: TaskDispatcherDelegate  |  定义 MIP SDK 任务调度程序接口的类。
类 mip:: TemplateNotFoundError  |  RMS 服务无法识别模板 ID。
class mip::TransientNetworkError  |  暂时性网络错误。 对服务终结点执行网络调用时，由于意外行为所致。 此错误是暂时性错误，因此可重试该操作。
class mip::UserRights  |  一组用户以及与之关联的权限。
class mip::UserRoles  |  一组用户以及与之关联的角色。
