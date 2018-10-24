---
title: MIP SDK for C++（预览版）参考
description: MIP SDK for C++（预览版）参考
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 06d8bb26a8e3026562006d68d4ae8d1630eba81c
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446322"
---
# <a name="mip-sdk-for-c-preview-reference"></a>MIP SDK for C++（预览版）参考

Microsoft 信息保护 (MIP) SDK for C++（预览版）允许开发人员管理数据保护策略，并将其应用于数据和其他数字资产。  

要了解详细信息，请参阅 [MIP 开发人员博客](https://aka.ms/MIPDevelopers)<!-- and [MIP samples](https://aka.ms/mipsdksamples)-->。

MIP SDK for C++ 包括：

- [枚举和结构](mip-enums-and-structs.md)
- [函数](mip-functions.md)
- 下列类：

| 类名称 | 描述 |
| :----------|:------------|
[AccessDeniedError](class_mip_accessdeniederror.md)  |  用户无法访问内容。 例如，无权限、内容已撤销。
[操作](class_mip_action.md)  |  操作的接口。 每个操作都转换为，出于应用标签目的，应用程序需要执行的步骤（如策略所定义）
[AddContentFooterAction](class_mip_addcontentfooteraction.md)  |  指定向文档添加内容脚注的操作类。
[AddContentHeaderAction](class_mip_addcontentheaderaction.md)  |  指定添加内容头的操作类。
[AddWatermarkAction](class_mip_addwatermarkaction.md)  |  指定添加水印的操作类。
[ApplyLabelAction](class_mip_applylabelaction.md)  |  应用标签操作要求，必须调用应用程序，才能应用特定标签。
[BadInputError](class_mip_badinputerror.md)  |  输入不正确的错误，在 SDK API 输入无效时引发。
[ClassificationResult](class_mip_classificationresult.md)  |  包含对执行状态进行分类调用的结果的类。
[ConsentDelegate](class_consentdelegate.md)  |  执行许可相关操作的委托。
[ConsentDeniedError](class_mip_consentdeniederror.md)  |  需要用户同意的操作未获得同意。
[ContentLabel](class_mip_contentlabel.md)  |  Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
[CustomAction](class_mip_customaction.md)  |  [CustomAction](class_mip_customaction.md) 是一个泛型操作类，它捕获操作的所有子属性作为一个属性包。 调用方负责理解操作的含义。
[错误](class_mip_error.md)  |  将从 MIP SDK 报告（引发或返回）的所有错误的基类。
[ExecutionState](class_mip_executionstate.md)  |  执行引擎所需的所有状态的接口。
[FileEngine::Settings](class_mip_fileengine_settings.md)  | _尚无记录。_
[FileEngine](class_mip_fileengine.md)  |  此类提供适用于所有引擎功能的接口。
[FileHandler::Observer](class_mip_filehandler_observer.md)  |  [Observer](class_mip_filehandler_observer.md) 接口，供客户端获取文件处理程序相关事件的通知。
[FileHandler](class_mip_filehandler.md)  |  适用于所有文件处理函数的接口。
[FileIOError](class_mip_fileioerror.md)  |  文件 IO 错误。
[FileProfile::Observer](class_mip_fileprofile_observer.md)  |  [Observer](class_mip_fileprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
[FileProfile::Settings](class_mip_fileprofile_settings.md)  |  [FileProfile](class_mip_fileprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_fileprofile_settings.md)。
[FileProfile](class_mip_fileprofile.md)  |  [FileProfile](class_mip_fileprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。
[HttpDelegate](class_mip_httpdelegate.md)  |  用于重写 HTTP 处理的接口。
[HttpRequest](class_mip_httprequest.md)  |  描述单个 HTTP 请求的接口。
[HttpResponse](class_mip_httpresponse.md)  |  描述单个 HTTP 响应的接口，由客户端应用在重写 [HttpDelegate](class_mip_httpdelegate.md) 时实现。
[InternalError](class_mip_internalerror.md)  |  内部错误。 如果在执行期间出现意外，就会抛出此错误。
[JustificationRequiredError](class_mip_justificationrequirederror.md)  | _尚无记录。_
[JustifyAction](class_mip_justifyaction.md)  |  Justify[Action](class_mip_action.md) 要求必须合理解释标签降级，并设置执行状态下的响应。
[Label](class_mip_label.md)  |  单个 Microsoft 信息保护标签的抽象。
[LabelingOptions](class_mip_labelingoptions.md)  |  用于为 SetLabel/DeleteLabel 方法配置标记选项的接口。
[LoggerDelegate](class_mip_loggerdelegate.md)  |  定义 MIP SDK 记录器接口的类。
[MetadataAction](class_mip_metadataaction.md)  |  将元数据信息添加到内容的 [Action](class_mip_action.md)。
[NetworkError](class_mip_networkerror.md)  |  网络错误。 对服务终结点执行网络调用时，由于意外行为所致。
[NotSupportedError](class_mip_notsupportederror.md)  |  SDK 不支持应用程序请求执行的操作。
[PolicyEngine::Settings](class_mip_policyengine_settings.md)  |  定义与 [PolicyEngine](class_mip_policyengine.md) 关联的设置。
[PolicyEngine](class_mip_policyengine.md)  |  此类提供适用于所有引擎功能的接口。
[PolicyHandler](class_mip_policyhandler.md)  |  此类为文件上的所有策略处理程序函数提供一个接口。
[PolicyProfile::Observer](class_mip_policyprofile_observer.md)  |  [Observer](class_mip_policyprofile_observer.md) 接口，供客户端获取配置文件相关事件的通知。
[PolicyProfile::Settings](class_mip_policyprofile_settings.md)  |  [PolicyProfile](class_mip_policyprofile.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_policyprofile_settings.md)。
[PolicyProfile](class_mip_policyprofile.md)  |  [PolicyProfile](class_mip_policyprofile.md) 类是用于使用 Microsoft 信息保护操作的根类。 一个典型的应用程序只需要一个 [PolicyProfile](class_mip_policyprofile.md)，但它可以按需创建多个配置文件。
[PolicySyncError](class_mip_policysyncerror.md)  |  同步策略数据尝试失败。
[PrivilegedRequiredError](class_mip_privilegedrequirederror.md)  |  由于当前标签被指定为特权操作（相当于管理员操作），因此无法替代。
[ProtectAdhocAction](class_mip_protectadhocaction.md)  |  指定向文档添加临时保护的操作类。
[ProtectByTemplateAction](class_mip_protectbytemplateaction.md)  |  指定向文档添加模板保护的操作类。
[ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md)  |  指定向文档添加不转发保护的操作类。
[ProtectionDescriptor](class_mip_protectiondescriptor.md)  |  与某段内容相关的保护说明。
[ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md)  |  构造 [ProtectionDescriptor](class_mip_protectiondescriptor.md)，用于描述与一段内容相关的保护。
[ProtectionEngine::Observer](class_mip_protectionengine_observer.md)  |  接收 [ProtectionEngine](class_mip_protectionengine.md) 相关通知的接口。
[ProtectionEngine::Settings](class_mip_protectionengine_settings.md)  |  [ProtectionEngine](class_mip_protectionengine.md) 在其创建期间及其整个生存期内使用的 [Settings](class_mip_protectionengine_settings.md)。
[ProtectionEngine](class_mip_protectionengine.md)  |  管理与特定标识有关的保护相关操作。
[ProtectionHandler::Observer](class_mip_protectionhandler.md)  |  接收 [ProtectionHandler](class_mip_protectionhandler.md) 相关通知的接口。
[ProtectionHandler](class_mip_protectionhandler.md)  |  管理特定保护配置的保护相关操作。
[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md)  |  接收与 [ProtectionProfile](class_mip_protectionprofile.md) 相关通知的接口。
[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md)  |  由 [ProtectionProfile](class_mip_protectionprofile.md) 在创建期间及其整个生存期内使用的[设置](class_mip_protectionprofile_settings.md)。
[ProtectionProfile](class_mip_protectionprofile.md)  |  [ProtectionProfile](class_mip_protectionprofile.md) 是用于执行保护操作的根类。
[RecommendLabelAction](class_mip_recommendlabelaction.md)  |  建议标签操作是向用户建议标签。 在用户忽略建议标签后，应通过对执行状态采取受支持的操作来取消此调用。
[RemoveContentFooterAction](class_mip_removecontentfooteraction.md)  |  指定从文档中删除内容脚注的操作类。
[RemoveContentHeaderAction](class_mip_removecontentheaderaction.md)  |  指定从文档中删除内容头的操作类。
[RemoveProtectionAction](class_mip_removeprotectionaction.md)  |  指定从文档中删除保护的操作类。
[RemoveWatermarkAction](class_mip_removewatermarkaction.md)  |  指定从文档中删除水印的操作类。
[Stream](class_mip_stream.md)  |  一个类，它定义 MIP SDK 和基于流的内容之间的接口。
[TransientNetworkError](class_mip_transientnetworkerror.md)  |  暂时性网络错误。 对服务终结点执行网络调用时，由于意外行为所致。 此错误是暂时性错误，因此可重试该操作。
[UserRights](class_mip_userrights.md)  |  一组用户以及与之关联的权限。
[UserRoles](class_mip_userroles.md)  |  一组用户以及与之关联的角色。
