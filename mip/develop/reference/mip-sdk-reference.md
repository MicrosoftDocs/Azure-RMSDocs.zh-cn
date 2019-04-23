---
title: MIP SDK forC++引用
description: MIP SDK forC++引用
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1db2faeca6c2ff00a0053a7d65d16872190d306f
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60172787"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK forC++引用

适用于的 Microsoft 信息保护 (MIP) SDKC++允许开发人员来管理和数据保护策略应用到数据和其他数字资产。

MIP SDK for C++ 包括：

- [枚举和结构](mip-enums-and-structs.md)
- [函数](mip-functions.md)
- 下列类：

 类                         | 描述                                
--------------------------------|---------------------------------------------
class mip::AccessDeniedError  |  用户无法访问内容。 例如，无权限、内容已撤销。
class mip::Action  |  操作的接口。 每个操作都转换为，出于应用标签目的，应用程序需要执行的步骤（如策略所定义）
class mip::AddContentFooterAction  |  指定向文档添加内容脚注的操作类。
class mip::AddContentHeaderAction  |  指定添加内容头的操作类。
class mip::AddWatermarkAction  |  指定添加水印的操作类。
类 mip::AdhocProtectionRequiredError  |  临时保护应设置为完成文件上的操作。
class mip::ApplyLabelAction  |  应用标签操作要求，必须调用应用程序，才能应用特定标签。
类 mip::AuthDelegate  |  委托身份验证相关的操作。
类 mip::AuthDelegate::OAuth2Challenge  |  包含从调用应用程序，以便生成 oauth2 令牌所需的所有信息的类。
类 mip::AuthDelegate::OAuth2Token  |  定义 MIP SDK 如何要求要传递到 SDK 的 oauth2 令牌的类。
class mip::BadInputError  |  输入不正确的错误，在 SDK API 输入无效时引发。
类 mip::ClassificationRequest  |  包含请求的执行状态的一个分类调用的类。
类 mip::ClassificationResult  |  包含对执行状态进行分类调用的结果的类。
类 mip::ConsentDelegate  |  执行许可相关操作的委托。
类 mip::ConsentDeniedError  |  需要用户同意的操作未获得同意。
class mip::ContentLabel  |  Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
class mip::CustomAction  |  [CustomAction](class_mip_customaction.md) 是一个泛型操作类，它捕获操作的所有子属性作为一个属性包。 调用方负责理解操作的含义。
class mip::Error  |  将从 MIP SDK 报告（引发或返回）的所有错误的基类。
class mip::ExecutionState  |  执行引擎所需的所有状态的接口。
class mip::FileEngine  |  此类提供适用于所有引擎功能的接口。
class mip::FileEngine::Settings  | _尚无记录。_
类 mip::FileExecutionState  | _尚无记录。_
class mip::FileHandler  |  适用于所有文件处理函数的接口。
class mip::FileHandler::Observer  |  [Observer](class_mip_filehandler_observer.md) 接口，供客户端获取文件处理程序相关事件的通知。
class mip::FileIOError  |  文件 IO 错误。
class mip::FileProfile  |  [FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
class mip::FileProfile::Observer  |  [Observer](class_mip_fileprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
class mip::FileProfile::Settings  |  [FileProfile](class_mip_fileprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_fileprofile_settings.md)。
类 mip::HttpDelegate  |  用于重写 HTTP 处理的接口。
类 mip::HttpOperation  |  描述单个 HTTP 操作，重写时，由客户端应用程序实现的接口[HttpDelegate](class_mip_httpdelegate.md)。
class mip::HttpRequest  |  描述单个 HTTP 请求的接口。
类 mip::HttpResponse  |  描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
类 mip::Identity  |  标识抽象。
class mip::InternalError  |  内部错误。 如果在执行期间出现意外，就会抛出此错误。
class mip::JustificationRequiredError  | _尚无记录。_
class mip::JustifyAction  |  Justify[Action](class_mip_action.md) 要求必须合理解释标签降级，并设置执行状态下的响应。
class mip::Label  |  单个 Microsoft 信息保护标签的抽象。
class mip::LabelingOptions  |  用于为 SetLabel/DeleteLabel 方法配置标记选项的接口。
class mip::LoggerDelegate  |  定义 MIP SDK 记录器接口的类。
class mip::MetadataAction  |  将元数据信息添加到内容的 [Action](class_mip_action.md)。
class mip::NetworkError  |  网络错误。 对服务终结点执行网络调用时，由于意外行为所致。
类 mip::NoAuthTokenError  |  用户无法获取由于缺少身份验证令牌内容的访问权限。
类 mip::NoPermissionsError  |  用户无法访问内容。 例如，无权限、内容已撤销。
类 mip::NoPolicyError  |  租户策略未配置的分类/标签。
class mip::NotSupportedError  |  SDK 不支持应用程序请求执行的操作。
类 mip::OperationCancelledError  |  已取消操作。
class mip::PolicyEngine  |  此类提供适用于所有引擎功能的接口。
class mip::PolicyEngine::Settings  |  定义与 [PolicyEngine](class_mip_policyengine.md) 关联的设置。
类 mip::PolicyHandler  |  此类为文件上的所有策略处理程序函数提供一个接口。
class mip::PolicyProfile  |  [PolicyProfile](class_mip_policyprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个 [PolicyProfile](class_mip_policyprofile.md)，但它可以按需创建多个配置文件。
class mip::PolicyProfile::Observer  |  [Observer](class_mip_policyprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
class mip::PolicyProfile::Settings  |  [PolicyProfile](class_mip_policyprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_policyprofile_settings.md)。
class mip::PolicySyncError  |  同步策略数据尝试失败。
class mip::PrivilegedRequiredError  |  由于当前标签被指定为特权操作（相当于管理员操作），因此无法替代。
class mip::ProtectAdhocAction  |  指定向文档添加临时保护的操作类。
class mip::ProtectByTemplateAction  |  指定向文档添加模板保护的操作类。
class mip::ProtectDoNotForwardAction  |  指定向文档添加不转发保护的操作类。
类 mip::ProtectionDescriptor  |  与某段内容相关的保护说明。
类 mip::ProtectionDescriptorBuilder  |  构造 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，用于描述与一段内容相关的保护。
类 mip::ProtectionEngine  |  管理与特定标识有关的保护相关操作。
类 mip::ProtectionEngine::Observer  |  接收 [ProtectionEngine](class_mip_protectionengine.md) 相关通知的接口。
类 mip::ProtectionEngine::Settings  |  [ProtectionEngine](class_mip_protectionengine.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_protectionengine_settings.md)。
类 mip::ProtectionHandler  |  管理特定保护配置的保护相关操作。
类 mip::ProtectionHandler::Observer  |  接收 [ProtectionHandler](class_mip_protectionhandler.md) 相关通知的接口。
class mip::ProtectionProfile  |  [ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
class mip::ProtectionProfile::Observer  |  接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关通知的接口。
class mip::ProtectionProfile::Settings  |  由 [ProtectionProfile](class_mip_protectionprofile.md) 在创建期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)。
类 mip::ProxyAuthenticationError  |  代理身份验证失败。
类 mip::RecommendLabelAction  |  建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
class mip::RemoveContentFooterAction  |  指定从文档中删除内容脚注的操作类。
class mip::RemoveContentHeaderAction  |  指定从文档中删除内容头的操作类。
class mip::RemoveProtectionAction  |  指定从文档中删除保护的操作类。
class mip::RemoveWatermarkAction  |  指定从文档中删除水印的操作类。
类 mip::SensitivityTypesRulePackage  | _尚无记录。_
类 mip::ServiceDisabledError  |  用户无法获取访问内容，因为服务被禁用。
class mip::Stream  |  一个类，它定义 MIP SDK 和基于流的内容之间的接口。
类 mip::TaskDispatcherDelegate  |  定义 MIP SDK 任务调度程序的接口的类。
class mip::TransientNetworkError  |  暂时性网络错误。 对服务终结点执行网络调用时，由于意外行为所致。 此错误是暂时性错误，因此可重试该操作。
class mip::UserRights  |  一组用户以及与之关联的权限。
class mip::UserRoles  |  一组用户以及与之关联的角色。