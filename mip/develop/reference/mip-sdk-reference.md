---
title: MIP SDK for c + + 参考
description: MIP SDK for c + + 参考
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cae7955684d0fae0f61e2a7319cbb036263e129b
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650575"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for c + + 参考

Microsoft 信息保护 (MIP) SDK for c + + 允许开发人员来管理和数据保护策略应用到数据和其他数字资产。  

MIP SDK for C++ 包括：

- [枚举和结构](mip-enums-and-structs.md)
- [函数](mip-functions.md)
- 下列类：

| Namespace::Class 名称 | 描述 |
| :----------|:------------|
[mip::AccessDeniedError](class_mip_AccessDeniedError.md)  |  用户无法访问内容。 例如，无权限、内容已撤销。
[mip::Action](class_mip_Action.md)  |  操作的接口。 每个操作都转换为，出于应用标签目的，应用程序需要执行的步骤（如策略所定义）
[mip::AddContentFooterAction](class_mip_AddContentFooterAction.md)  |  指定向文档添加内容脚注的操作类。
[mip::AddContentHeaderAction](class_mip_AddContentHeaderAction.md)  |  指定添加内容头的操作类。
[mip::AddWatermarkAction](class_mip_AddWatermarkAction.md)  |  指定添加水印的操作类。
[mip::ApplyLabelAction](class_mip_ApplyLabelAction.md)  |  应用标签操作要求，必须调用应用程序，才能应用特定标签。
[mip::AuthDelegate](class_mip_AuthDelegate.md)  |  委托身份验证相关的操作。
[mip::BadInputError](class_mip_BadInputError.md)  |  输入不正确的错误，在 SDK API 输入无效时引发。
[mip::ClassificationRequest](class_mip_ClassificationRequest.md)  |  包含请求的执行状态的一个分类调用的类。
[mip::ClassificationResult](class_mip_ClassificationResult.md)  |  包含对执行状态进行分类调用的结果的类。
[mip::ConsentDelegate](class_mip_ConsentDelegate.md)  |  执行许可相关操作的委托。
[mip::ConsentDeniedError](class_mip_ConsentDeniedError.md)  |  需要用户同意的操作未获得同意。
[mip::ContentLabel](class_mip_ContentLabel.md)  |  Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
[mip::CustomAction](class_mip_CustomAction.md)  |  [CustomAction](class_mip_customaction.md) 是一个泛型操作类，它捕获操作的所有子属性作为一个属性包。 调用方负责理解操作的含义。
[mip::Error](class_mip_Error.md)  |  将从 MIP SDK 报告（引发或返回）的所有错误的基类。
[mip::ExecutionState](class_mip_ExecutionState.md)  |  执行引擎所需的所有状态的接口。
[mip::FileEngine](class_mip_FileEngine.md)  |  此类提供适用于所有引擎功能的接口。
[mip::FileExecutionState](class_mip_FileExecutionState.md)  | _尚无记录。_
[mip::FileHandler](class_mip_FileHandler.md)  |  适用于所有文件处理函数的接口。
[mip::FileIOError](class_mip_FileIOError.md)  |  文件 IO 错误。
[mip::FileProfile](class_mip_FileProfile.md)  |  [FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
[mip::HttpDelegate](class_mip_HttpDelegate.md)  |  用于重写 HTTP 处理的接口。
[mip::HttpRequest](class_mip_HttpRequest.md)  |  描述单个 HTTP 请求的接口。
[mip::HttpResponse](class_mip_HttpResponse.md)  |  描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
[mip::Identity](class_mip_Identity.md)  |  标识抽象。
[mip::InternalError](class_mip_InternalError.md)  |  内部错误。 如果在执行期间出现意外，就会抛出此错误。
[mip::JustificationRequiredError](class_mip_JustificationRequiredError.md)  | _尚无记录。_
[mip::JustifyAction](class_mip_JustifyAction.md)  |  Justify[Action](class_mip_action.md) 要求必须合理解释标签降级，并设置执行状态下的响应。
[mip::Label](class_mip_Label.md)  |  单个 Microsoft 信息保护标签的抽象。
[mip::LabelingOptions](class_mip_LabelingOptions.md)  |  用于为 SetLabel/DeleteLabel 方法配置标记选项的接口。
[mip::LoggerDelegate](class_mip_LoggerDelegate.md)  |  定义 MIP SDK 记录器接口的类。
[mip::MetadataAction](class_mip_MetadataAction.md)  |  将元数据信息添加到内容的 [Action](class_mip_action.md)。
[mip::NetworkError](class_mip_NetworkError.md)  |  网络错误。 对服务终结点执行网络调用时，由于意外行为所致。
[mip::NoAuthTokenError](class_mip_NoAuthTokenError.md)  |  用户无法获取由于缺少身份验证令牌内容的访问权限。
[mip::NoPermissionsError](class_mip_NoPermissionsError.md)  |  用户无法访问内容。 例如，无权限、内容已撤销。
[mip::NoPolicyError](class_mip_NoPolicyError.md)  |  租户策略未配置的分类/标签。
[mip::NotSupportedError](class_mip_NotSupportedError.md)  |  SDK 不支持应用程序请求执行的操作。
[mip::PolicyEngine](class_mip_PolicyEngine.md)  |  此类提供适用于所有引擎功能的接口。
[mip::PolicyHandler](class_mip_PolicyHandler.md)  |  此类为文件上的所有策略处理程序函数提供一个接口。
[mip::PolicyProfile](class_mip_PolicyProfile.md)  |  [PolicyProfile](class_mip_policyprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个 [PolicyProfile](class_mip_policyprofile.md)，但它可以按需创建多个配置文件。
[mip::PolicySyncError](class_mip_PolicySyncError.md)  |  同步策略数据尝试失败。
[mip::PrivilegedRequiredError](class_mip_PrivilegedRequiredError.md)  |  由于当前标签被指定为特权操作（相当于管理员操作），因此无法替代。
[mip::ProtectAdhocAction](class_mip_ProtectAdhocAction.md)  |  指定向文档添加临时保护的操作类。
[mip::ProtectByTemplateAction](class_mip_ProtectByTemplateAction.md)  |  指定向文档添加模板保护的操作类。
[mip::ProtectDoNotForwardAction](class_mip_ProtectDoNotForwardAction.md)  |  指定向文档添加不转发保护的操作类。
[mip::ProtectionDescriptor](class_mip_ProtectionDescriptor.md)  |  与某段内容相关的保护说明。
[mip::ProtectionDescriptorBuilder](class_mip_ProtectionDescriptorBuilder.md)  |  构造 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，用于描述与一段内容相关的保护。
[mip::ProtectionEngine](class_mip_ProtectionEngine.md)  |  管理与特定标识有关的保护相关操作。
[mip::ProtectionHandler](class_mip_ProtectionHandler.md)  |  管理特定保护配置的保护相关操作。
[mip::ProtectionProfile](class_mip_ProtectionProfile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
[mip::ProxyAuthenticationError](class_mip_ProxyAuthenticationError.md)  |  代理身份验证失败。
[mip::RecommendLabelAction](class_mip_RecommendLabelAction.md)  |  建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
[mip::RemoveContentFooterAction](class_mip_RemoveContentFooterAction.md)  |  指定从文档中删除内容脚注的操作类。
[mip::RemoveContentHeaderAction](class_mip_RemoveContentHeaderAction.md)  |  指定从文档中删除内容头的操作类。
[mip::RemoveProtectionAction](class_mip_RemoveProtectionAction.md)  |  指定从文档中删除保护的操作类。
[mip::RemoveWatermarkAction](class_mip_RemoveWatermarkAction.md)  |  指定从文档中删除水印的操作类。
[mip::SensitivityTypesRulePackage](class_mip_SensitivityTypesRulePackage.md)  | _尚无记录。_
[mip::ServiceDisabledError](class_mip_ServiceDisabledError.md)  |  用户无法获取访问内容，因为服务被禁用。
[mip::Stream](class_mip_Stream.md)  |  一个类，它定义 MIP SDK 和基于流的内容之间的接口。
[mip::TransientNetworkError](class_mip_TransientNetworkError.md)  |  暂时性网络错误。 对服务终结点执行网络调用时，由于意外行为所致。 此错误是暂时性错误，因此可重试该操作。
[mip::UserRights](class_mip_UserRights.md)  |  一组用户以及与之关联的权限。
[mip::UserRoles](class_mip_UserRoles.md)  |  一组用户以及与之关联的角色。