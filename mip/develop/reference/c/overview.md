---
title: MIP SDK for C 参考
description: MIP SDK for C 参考
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 4/16/2020
ms.openlocfilehash: 438cdc93989ffbd5b294adb24175c443aeaf1024
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763861"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C 参考

适用于 C 语言的 Microsoft 信息保护（MIP） SDK 允许开发人员管理数据保护策略并将其应用于数据和其他数字资产。

适用于 C 的 MIP SDK 包括

- [枚举](enumerations.md)
- [结构](structures.md)
- 以下功能：

函数 | 简要描述 |
|---|---|
| [mip_cc_auth_callback](functions.md#mip_cc_auth_callback) | 用于获取 OAuth2 标记的回调函数定义 |
| [mip_cc_consent_callback](functions.md#mip_cc_consent_callback) | 允许用户访问外部服务终结点的回调函数定义 |
| [MIP_CC_CreateDictionary](functions.md#mip_cc_createdictionary) | 创建字符串键/值的字典 |
| [MIP_CC_Dictionary_GetEntries](functions.md#mip_cc_dictionary_getentries) | 获取构成字典的键/值对 |
| [MIP_CC_ReleaseDictionary](functions.md#mip_cc_releasedictionary) | 释放与字典关联的资源 |
| [mip_cc_http_send_callback_fn](functions.md#mip_cc_http_send_callback_fn) | 发出 HTTP 请求的回调函数定义 |
| [mip_cc_http_cancel_callback_fn](functions.md#mip_cc_http_cancel_callback_fn) | 用于取消 HTTP 请求的回调函数定义 |
| [MIP_CC_CreateHttpDelegate](functions.md#mip_cc_createhttpdelegate) | 创建可用于重写 MIP 的默认 HTTP 堆栈的 HTTP 委托 |
| [MIP_CC_NotifyHttpDelegateResponse](functions.md#mip_cc_notifyhttpdelegateresponse) | 通知 HTTP 委托 HTTP 响应已准备就绪 |
| [MIP_CC_ReleaseHttpDelegate](functions.md#mip_cc_releasehttpdelegate) | 释放与 HTTP 委托句柄关联的资源 |
| [mip_cc_logger_init_callback_fn](functions.md#mip_cc_logger_init_callback_fn) | 记录器初始化的回调函数定义 |
| [mip_cc_logger_write_callback_fn](functions.md#mip_cc_logger_write_callback_fn) | 用于写入 log 语句的回调函数定义 |
| [MIP_CC_CreateLoggerDelegate](functions.md#mip_cc_createloggerdelegate) | 创建一个记录器委托，该委托可用于重写 MIP 的默认记录器 |
| [MIP_CC_ReleaseLoggerDelegate](functions.md#mip_cc_releaseloggerdelegate) | 释放与记录器委托句柄关联的资源 |
| [MIP_CC_CreateMipContext](functions.md#mip_cc_createmipcontext) | 创建 MIP 上下文以管理所有配置文件实例中共享的状态 |
| [MIP_CC_CreateMipContextWithCustomFeatureSettings](functions.md#mip_cc_createmipcontextwithcustomfeaturesettings) | 创建 MIP 上下文以管理所有配置文件实例中共享的状态 |
| [MIP_CC_ReleaseMipContext](functions.md#mip_cc_releasemipcontext) | 释放与 MIP 上下文关联的资源 |
| [MIP_CC_ProtectionDescriptor_GetProtectionType](functions.md#mip_cc_protectiondescriptor_getprotectiontype) | 获取保护类型，无论其是否由 RMS 模板定义 |
| [MIP_CC_ProtectionDescriptor_GetOwnerSize](functions.md#mip_cc_protectiondescriptor_getownersize) | 获取存储所有者所需的缓冲区大小 |
| [MIP_CC_ProtectionDescriptor_GetOwner](functions.md#mip_cc_protectiondescriptor_getowner) | 获取保护所有者 |
| [MIP_CC_ProtectionDescriptor_GetNameSize](functions.md#mip_cc_protectiondescriptor_getnamesize) | 获取存储名称所需的缓冲区大小 |
| [MIP_CC_ProtectionDescriptor_GetName](functions.md#mip_cc_protectiondescriptor_getname) | 获取保护名称 |
| [MIP_CC_ProtectionDescriptor_GetDescriptionSize](functions.md#mip_cc_protectiondescriptor_getdescriptionsize) | 获取存储说明所需的缓冲区大小 |
| [MIP_CC_ProtectionDescriptor_GetDescription](functions.md#mip_cc_protectiondescriptor_getdescription) | 获取保护说明 |
| [MIP_CC_ProtectionDescriptor_GetTemplateId](functions.md#mip_cc_protectiondescriptor_gettemplateid) | 获取模板 ID |
| [MIP_CC_ProtectionDescriptor_GetLabelId](functions.md#mip_cc_protectiondescriptor_getlabelid) | 获取标签 ID |
| [MIP_CC_ProtectionDescriptor_GetContentId](functions.md#mip_cc_protectiondescriptor_getcontentid) | 获取内容 ID |
| [MIP_CC_ProtectionDescriptor_DoesContentExpire](functions.md#mip_cc_protectiondescriptor_doescontentexpire) | 获取内容是否具有过期时间 |
| [MIP_CC_ProtectionDescriptor_GetContentValidUntil](functions.md#mip_cc_protectiondescriptor_getcontentvaliduntil) | 获取保护过期时间（以秒计） |
| [MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess](functions.md#mip_cc_protectiondescriptor_doesallowofflineaccess) | 获取是否允许脱机访问 |
| [MIP_CC_ProtectionDescriptor_GetReferrerSize](functions.md#mip_cc_protectiondescriptor_getreferrersize) | 获取存储引用站点所需的缓冲区大小 |
| [MIP_CC_ProtectionDescriptor_GetReferrer](functions.md#mip_cc_protectiondescriptor_getreferrer) | 获取保护引用 |
| [MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize](functions.md#mip_cc_protectiondescriptor_getdoublekeyurlsize) | 获取存储双关键字 URL 所需的缓冲区大小 |
| [MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl](functions.md#mip_cc_protectiondescriptor_getdoublekeyurl) | 获取双键 URL |
| [MIP_CC_ReleaseProtectionDescriptor](functions.md#mip_cc_releaseprotectiondescriptor) | 释放与保护描述符关联的资源 |
| [MIP_CC_CreateStringList](functions.md#mip_cc_createstringlist) | 创建字符串列表 |
| [MIP_CC_StringList_GetStrings](functions.md#mip_cc_stringlist_getstrings) | 获取组成字符串列表的字符串 |
| [MIP_CC_ReleaseStringList](functions.md#mip_cc_releasestringlist) | 释放与字符串列表关联的资源 |
| [mip_cc_dispatch_task_callback_fn](functions.md#mip_cc_dispatch_task_callback_fn) | 用于调度异步任务的回调函数定义 |
| [mip_cc_cancel_task_callback_fn](functions.md#mip_cc_cancel_task_callback_fn) | 用于取消后台任务的回调函数 |
| [MIP_CC_CreateTaskDispatcherDelegate](functions.md#mip_cc_createtaskdispatcherdelegate) | 创建可用于重写 MIP 的默认异步任务处理的任务调度程序委托 |
| [MIP_CC_ExecuteDispatchedTask](functions.md#mip_cc_executedispatchedtask) | 通知 TaskDispatcher 委托任务计划立即在当前线程上执行 |
| [MIP_CC_ReleaseTaskDispatcherDelegate](functions.md#mip_cc_releasetaskdispatcherdelegate) | 释放与任务调度程序委托句柄关联的资源 |
| [MIP_CC_CreateTelemetryConfiguration](functions.md#mip_cc_createtelemetryconfiguration) | 创建用于创建保护配置文件的设置对象 |
| [MIP_CC_TelemetryConfiguration_SetHostName](functions.md#mip_cc_telemetryconfiguration_sethostname) | 设置将替代内部遥测设置的遥测主机名 |
| [MIP_CC_TelemetryConfiguration_SetLibraryName](functions.md#mip_cc_telemetryconfiguration_setlibraryname) | 设置遥测共享库替代 |
| [MIP_CC_TelemetryConfiguration_SetHttpDelegate](functions.md#mip_cc_telemetryconfiguration_sethttpdelegate) | 重写客户端自己的默认遥测 HTTP 堆栈 |
| [MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate](functions.md#mip_cc_telemetryconfiguration_settaskdispatcherdelegate) | 用客户端自己的替换默认的异步任务调度程序 |
| [MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled](functions.md#mip_cc_telemetryconfiguration_setisnetworkdetectionenabled) | 设置是否允许遥测组件在后台线程上 ping 网络状态 |
| [MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled](functions.md#mip_cc_telemetryconfiguration_setislocalcachingenabled) | 设置是否允许遥测组件将缓存写入磁盘 |
| [MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled](functions.md#mip_cc_telemetryconfiguration_setistraceloggingenabled) | 设置是否允许遥测组件将日志写入磁盘 |
| [MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut](functions.md#mip_cc_telemetryconfiguration_setistelemetryoptedout) | 设置应用程序/用户是否已选择不使用可选遥测 |
| [MIP_CC_TelemetryConfiguration_SetCustomSettings](functions.md#mip_cc_telemetryconfiguration_setcustomsettings) | 设置自定义遥测设置 |
| [MIP_CC_TelemetryConfiguration_AddMaskedProperty](functions.md#mip_cc_telemetryconfiguration_addmaskedproperty) | 将遥测属性设置为屏蔽 |
| [MIP_CC_ReleaseTelemetryConfiguration](functions.md#mip_cc_releasetelemetryconfiguration) | 释放与保护配置文件设置关联的资源 |
| [MIP_CC_ReleaseProtectionEngine](functions.md#mip_cc_releaseprotectionengine) | 释放与保护引擎关联的资源 |
| [MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing](functions.md#mip_cc_protectionengine_createprotectionhandlerforpublishing) | 创建用于发布新内容的保护处理程序 |
| [MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption](functions.md#mip_cc_protectionengine_createprotectionhandlerforconsumption) | 创建用于使用现有内容的保护处理程序 |
| [MIP_CC_ProtectionEngine_GetEngineIdSize](functions.md#mip_cc_protectionengine_getengineidsize) | 获取引擎 ID 所需的缓冲区大小 |
| [MIP_CC_ProtectionEngine_GetEngineId](functions.md#mip_cc_protectionengine_getengineid) | 获取引擎 ID |
| [MIP_CC_ProtectionEngine_GetTemplatesSize](functions.md#mip_cc_protectionengine_gettemplatessize) | 获取与保护引擎关联的 RMS 模板的数目 |
| [MIP_CC_ProtectionEngine_GetTemplates](functions.md#mip_cc_protectionengine_gettemplates) | 获取可供用户使用的模板集合 |
| [MIP_CC_ProtectionEngine_GetRightsForLabelId](functions.md#mip_cc_protectionengine_getrightsforlabelid) | 获取向用户授予的标签 ID 的权限列表 |
| [MIP_CC_ProtectionEngine_GetClientDataSize](functions.md#mip_cc_protectionengine_getclientdatasize) | 获取与保护引擎关联的客户端数据的大小 |
| [MIP_CC_ProtectionEngine_GetClientData](functions.md#mip_cc_protectionengine_getclientdata) | 获取与保护引擎关联的客户端数据 |
| [MIP_CC_CreateProtectionEngineSettingsWithIdentity](functions.md#mip_cc_createprotectionenginesettingswithidentity) | 创建用于创建全新保护引擎的设置对象 |
| [MIP_CC_ProtectionEngineSettings_SetClientData](functions.md#mip_cc_protectionenginesettings_setclientdata) | 设置客户端数据，该数据将与此引擎透明存储并跨会话保存 |
| [MIP_CC_ProtectionEngineSettings_SetCustomSettings](functions.md#mip_cc_protectionenginesettings_setcustomsettings) | 配置自定义设置，用于功能的门和测试。 |
| [MIP_CC_ProtectionEngineSettings_SetSessionId](functions.md#mip_cc_protectionenginesettings_setsessionid) | 设置可用于关联日志和遥测的会话 ID |
| [MIP_CC_ProtectionEngineSettings_SetCloud](functions.md#mip_cc_protectionenginesettings_setcloud) | 设置影响所有服务请求的终结点 Url 的云 |
| [MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl](functions.md#mip_cc_protectionenginesettings_setcloudendpointbaseurl) | 设置所有服务请求的基 URL |
| [MIP_CC_ReleaseProtectionEngineSettings](functions.md#mip_cc_releaseprotectionenginesettings) | 释放与保护引擎设置关联的资源 |
| [MIP_CC_CreateProtectionHandlerPublishingSettings](functions.md#mip_cc_createprotectionhandlerpublishingsettings) | 创建用于创建用于发布新内容的保护处理程序的设置对象 |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred](functions.md#mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred) | 设置是否首选不推荐使用的加密算法（ECB）以实现向后兼容性 |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed](functions.md#mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed) | 设置是否允许非 MIP 感知应用程序打开受保护的内容 |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson](functions.md#mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson) | 设置 PL 是否为 JSON 格式（默认值为 XML） |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail](functions.md#mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail) | 设置委派的用户 |
| [MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail](functions.md#mip_cc_protectionhandlerpublishingsettings_setprelicenseuseremail) | 设置许可前用户 |
| [MIP_CC_CreateProtectionHandlerConsumptionSettings](functions.md#mip_cc_createprotectionhandlerconsumptionsettings) | 创建用于创建保护处理程序以使用现有内容的设置对象 |
| [MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense](functions.md#mip_cc_createprotectionhandlerconsumptionsettingswithprelicense) | 创建用于创建保护处理程序以使用现有内容的设置对象 |
| [MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly](functions.md#mip_cc_protectionhandlerconsumptionsettings_setisofflineonly) | 设置保护处理程序创建是否允许联机 HTTP 操作 |
| [MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail](functions.md#mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail) | 设置委派的用户 |
| [MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize](functions.md#mip_cc_protectionhandler_getserializedpublishinglicensesize) | 获取发布许可证的大小（以字节为单位） |
| [MIP_CC_ProtectionHandler_GetSerializedPublishingLicense](functions.md#mip_cc_protectionhandler_getserializedpublishinglicense) | 获取发布许可证 |
| [MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize](functions.md#mip_cc_protectionhandler_getserializedprelicensesize) | 获取预许可证的大小（以字节为单位） |
| [MIP_CC_ProtectionHandler_GetSerializedPreLicense](functions.md#mip_cc_protectionhandler_getserializedprelicense) | 获取预许可 |
| [MIP_CC_ProtectionHandler_GetProtectionDescriptor](functions.md#mip_cc_protectionhandler_getprotectiondescriptor) | 获取保护描述符 |
| [MIP_CC_ProtectionHandler_GetRights](functions.md#mip_cc_protectionhandler_getrights) | 获取授予用户的权限的列表 |
| [MIP_CC_ProtectionHandler_GetProtectedContentSize](functions.md#mip_cc_protectionhandler_getprotectedcontentsize) | 计算受保护内容的大小，在填充中进行因式分解，等等。 |
| [MIP_CC_ProtectionHandler_GetBlockSize](functions.md#mip_cc_protectionhandler_getblocksize) | 获取保护处理程序所使用的密码模式的块大小（以字节为单位） |
| [MIP_CC_ProtectionHandler_GetIssuedUserSize](functions.md#mip_cc_protectionhandler_getissuedusersize) | 获取存储已被授予对受保护内容的访问权限的用户所需的缓冲区大小 |
| [MIP_CC_ProtectionHandler_GetIssuedUser](functions.md#mip_cc_protectionhandler_getissueduser) | 获取已被授予对受保护内容的访问权限的用户 |
| [MIP_CC_ProtectionHandler_GetOwnerSize](functions.md#mip_cc_protectionhandler_getownersize) | 获取存储受保护内容的所有者所需的缓冲区大小 |
| [MIP_CC_ProtectionHandler_GetOwner](functions.md#mip_cc_protectionhandler_getowner) | 获取受保护内容的所有者 |
| [MIP_CC_ProtectionHandler_GetContentId](functions.md#mip_cc_protectionhandler_getcontentid) | 获取受保护内容的 IE 内容 |
| [MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm](functions.md#mip_cc_protectionhandler_doesusedeprecatedalgorithm) | 获取保护处理程序是否使用不推荐使用的加密算法（ECB）来实现向后兼容性 |
| [MIP_CC_ProtectionHandler_DecryptBuffer](functions.md#mip_cc_protectionhandler_decryptbuffer) | 解密缓冲区 |
| [MIP_CC_ReleaseProtectionHandlerPublishingSettings](functions.md#mip_cc_releaseprotectionhandlerpublishingsettings) | 释放与保护处理程序设置关联的资源 |
| [MIP_CC_ReleaseProtectionHandlerConsumptionSettings](functions.md#mip_cc_releaseprotectionhandlerconsumptionsettings) | 释放与保护处理程序设置关联的资源 |
| [MIP_CC_ReleaseProtectionHandler](functions.md#mip_cc_releaseprotectionhandler) | 释放与保护处理程序关联的资源 |
| [MIP_CC_LoadProtectionProfile](functions.md#mip_cc_loadprotectionprofile) | 加载配置文件 |
| [MIP_CC_ReleaseProtectionProfile](functions.md#mip_cc_releaseprotectionprofile) | 释放与保护配置文件关联的资源 |
| [MIP_CC_CreateProtectionProfileSettings](functions.md#mip_cc_createprotectionprofilesettings) | 创建用于创建保护配置文件的设置对象 |
| [MIP_CC_ProtectionProfileSettings_SetSessionId](functions.md#mip_cc_protectionprofilesettings_setsessionid) | 设置可用于关联日志和遥测的会话 ID |
| [MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses](functions.md#mip_cc_protectionprofilesettings_setcancachelicenses) | 配置最终用户许可证（Eul）是否将缓存在本地 |
| [MIP_CC_ProtectionProfileSettings_SetHttpDelegate](functions.md#mip_cc_protectionprofilesettings_sethttpdelegate) | 用客户端自己的替换默认的 HTTP 堆栈 |
| [MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate](functions.md#mip_cc_protectionprofilesettings_settaskdispatcherdelegate) | 用客户端自己的替换默认的异步任务调度程序 |
| [MIP_CC_ProtectionProfileSettings_SetCustomSettings](functions.md#mip_cc_protectionprofilesettings_setcustomsettings) | 配置自定义设置，用于功能的门和测试。 |
| [MIP_CC_ReleaseProtectionProfileSettings](functions.md#mip_cc_releaseprotectionprofilesettings) | 释放与保护配置文件设置关联的资源 |
| [MIP_CC_TemplateDescriptor_GetId](functions.md#mip_cc_templatedescriptor_getid) | 获取模板 ID |
| [MIP_CC_TemplateDescriptor_GetNameSize](functions.md#mip_cc_templatedescriptor_getnamesize) | 获取存储名称所需的缓冲区大小 |
| [MIP_CC_TemplateDescriptor_GetName](functions.md#mip_cc_templatedescriptor_getname) | 获取模板名称 |
| [MIP_CC_TemplateDescriptor_GetDescriptionSize](functions.md#mip_cc_templatedescriptor_getdescriptionsize) | 获取存储说明所需的缓冲区大小 |
| [MIP_CC_TemplateDescriptor_GetDescription](functions.md#mip_cc_templatedescriptor_getdescription) | 获取模板说明 |
| [MIP_CC_ReleaseTemplateDescriptor](functions.md#mip_cc_releasetemplatedescriptor) | 释放与模板描述符关联的资源 |
| [MIP_CC_Action_GetType](functions.md#mip_cc_action_gettype) | 获取操作的类型 |
| [MIP_CC_Action_GetId](functions.md#mip_cc_action_getid) | 获取操作的 ID |
| [MIP_CC_ActionResult_GetActions](functions.md#mip_cc_actionresult_getactions) | 获取构成操作结果的操作 |
| [MIP_CC_ReleaseActionResult](functions.md#mip_cc_releaseactionresult) | 释放与操作结果关联的资源 |
| [MIP_CC_AddContentFooterAction_GetUIElementNameSize](functions.md#mip_cc_addcontentfooteraction_getuielementnamesize) | 获取存储 "添加内容脚注" 操作的 UI 元素名称所需的缓冲区大小 |
| [MIP_CC_AddContentFooterAction_GetUIElementName](functions.md#mip_cc_addcontentfooteraction_getuielementname) | 获取 "添加内容脚注" 操作的 UI 元素名称 |
| [MIP_CC_AddContentFooterAction_GetTextSize](functions.md#mip_cc_addcontentfooteraction_gettextsize) | 获取存储 "添加内容脚注" 操作文本所需的缓冲区大小 |
| [MIP_CC_AddContentFooterAction_GetText](functions.md#mip_cc_addcontentfooteraction_gettext) | 获取 "添加内容脚注" 操作的文本 |
| [MIP_CC_AddContentFooterAction_GetFontNameSize](functions.md#mip_cc_addcontentfooteraction_getfontnamesize) | 获取存储 "添加内容脚注" 操作字体名称所需的缓冲区大小 |
| [MIP_CC_AddContentFooterAction_GetFontName](functions.md#mip_cc_addcontentfooteraction_getfontname) | 获取 "添加内容脚注" 操作的字体名称 |
| [MIP_CC_AddContentFooterAction_GetFontSize](functions.md#mip_cc_addcontentfooteraction_getfontsize) | 获取整数字号 |
| [MIP_CC_AddContentFooterAction_GetFontColorSize](functions.md#mip_cc_addcontentfooteraction_getfontcolorsize) | 获取存储 "添加内容脚注" 操作字体颜色所需的缓冲区大小 |
| [MIP_CC_AddContentFooterAction_GetFontColor](functions.md#mip_cc_addcontentfooteraction_getfontcolor) | 获取 "添加内容脚注" 操作的字体颜色（例如，"#000000"） |
| [MIP_CC_AddContentFooterAction_GetAlignment](functions.md#mip_cc_addcontentfooteraction_getalignment) | 获取对齐方式 |
| [MIP_CC_AddContentFooterAction_GetMargin](functions.md#mip_cc_addcontentfooteraction_getmargin) | 获取边距大小 |
| [MIP_CC_AddContentHeaderAction_GetUIElementNameSize](functions.md#mip_cc_addcontentheaderaction_getuielementnamesize) | 获取存储 "添加内容标头" 操作的 UI 元素名称所需的缓冲区大小 |
| [MIP_CC_AddContentHeaderAction_GetUIElementName](functions.md#mip_cc_addcontentheaderaction_getuielementname) | 获取 "添加内容标头" 操作的 UI 元素名称 |
| [MIP_CC_AddContentHeaderAction_GetTextSize](functions.md#mip_cc_addcontentheaderaction_gettextsize) | 获取存储 "添加内容标头" 操作文本所需的缓冲区大小 |
| [MIP_CC_AddContentHeaderAction_GetText](functions.md#mip_cc_addcontentheaderaction_gettext) | 获取 "添加内容标头" 操作的文本 |
| [MIP_CC_AddContentHeaderAction_GetFontNameSize](functions.md#mip_cc_addcontentheaderaction_getfontnamesize) | 获取存储 "添加内容标头" 操作字体名称所需的缓冲区大小 |
| [MIP_CC_AddContentHeaderAction_GetFontName](functions.md#mip_cc_addcontentheaderaction_getfontname) | 获取 "添加内容标头" 操作的字体名称 |
| [MIP_CC_AddContentHeaderAction_GetFontSize](functions.md#mip_cc_addcontentheaderaction_getfontsize) | 获取整数字号 |
| [MIP_CC_AddContentHeaderAction_GetFontColorSize](functions.md#mip_cc_addcontentheaderaction_getfontcolorsize) | 获取存储 "添加内容标头" 操作字体颜色所需的缓冲区大小 |
| [MIP_CC_AddContentHeaderAction_GetFontColor](functions.md#mip_cc_addcontentheaderaction_getfontcolor) | 获取 "添加内容标头" 操作的字体颜色（例如，"#000000"） |
| [MIP_CC_AddContentHeaderAction_GetAlignment](functions.md#mip_cc_addcontentheaderaction_getalignment) | 获取对齐方式 |
| [MIP_CC_AddContentHeaderAction_GetMargin](functions.md#mip_cc_addcontentheaderaction_getmargin) | 获取边距大小 |
| [MIP_CC_AddWatermarkAction_GetUIElementNameSize](functions.md#mip_cc_addwatermarkaction_getuielementnamesize) | 获取存储 "添加水印" 操作的 UI 元素名称所需的缓冲区大小 |
| [MIP_CC_AddWatermarkAction_GetUIElementName](functions.md#mip_cc_addwatermarkaction_getuielementname) | 获取 "添加水印" 操作的 UI 元素名称 |
| [MIP_CC_AddWatermarkAction_GetLayout](functions.md#mip_cc_addwatermarkaction_getlayout) | 获取水印布局 |
| [MIP_CC_AddWatermarkAction_GetTextSize](functions.md#mip_cc_addwatermarkaction_gettextsize) | 获取存储 "添加水印" 操作文本所需的缓冲区大小 |
| [MIP_CC_AddWatermarkAction_GetText](functions.md#mip_cc_addwatermarkaction_gettext) | 获取 "添加水印" 操作的文本 |
| [MIP_CC_AddWatermarkAction_GetFontNameSize](functions.md#mip_cc_addwatermarkaction_getfontnamesize) | 获取存储 "添加水印" 操作字体名称所需的缓冲区大小 |
| [MIP_CC_AddWatermarkAction_GetFontName](functions.md#mip_cc_addwatermarkaction_getfontname) | 获取 "添加水印" 操作的字体名称 |
| [MIP_CC_AddWatermarkAction_GetFontSize](functions.md#mip_cc_addwatermarkaction_getfontsize) | 获取整数字号 |
| [MIP_CC_AddWatermarkAction_GetFontColorSize](functions.md#mip_cc_addwatermarkaction_getfontcolorsize) | 获取存储 "添加水印" 操作字体颜色所需的缓冲区大小 |
| [MIP_CC_AddWatermarkAction_GetFontColor](functions.md#mip_cc_addwatermarkaction_getfontcolor) | 获取 "添加水印" 操作的字体颜色（例如，"#000000"） |
| [MIP_CC_ReleaseContentLabel](functions.md#mip_cc_releasecontentlabel) | 释放与内容标签关联的资源 |
| [MIP_CC_ContentLabel_GetCreationTime](functions.md#mip_cc_contentlabel_getcreationtime) | 获取应用标签的时间 |
| [MIP_CC_ContentLabel_GetAssignmentMethod](functions.md#mip_cc_contentlabel_getassignmentmethod) | 获取标签分配方法 |
| [MIP_CC_ContentLabel_GetExtendedProperties](functions.md#mip_cc_contentlabel_getextendedproperties) | 获取扩展属性 |
| [MIP_CC_ContentLabel_IsProtectionAppliedFromLabel](functions.md#mip_cc_contentlabel_isprotectionappliedfromlabel) | 获取一个标签是否应用了保护。 |
| [MIP_CC_ContentLabel_GetLabel](functions.md#mip_cc_contentlabel_getlabel) | 从内容标签实例获取一般标签属性 |
| [MIP_CC_CustomAction_GetNameSize](functions.md#mip_cc_customaction_getnamesize) | 获取存储 "自定义" 操作名称所需的缓冲区大小 |
| [MIP_CC_CustomAction_GetName](functions.md#mip_cc_customaction_getname) | 获取 "自定义" 操作的名称 |
| [MIP_CC_CustomAction_GetProperties](functions.md#mip_cc_customaction_getproperties) | 获取 "自定义" 操作的属性 |
| [mip_cc_metadata_callback](functions.md#mip_cc_metadata_callback) | 用于检索文档元数据的回调函数定义，按名称/前缀筛选 |
| [MIP_CC_ReleaseLabel](functions.md#mip_cc_releaselabel) | 释放与标签关联的资源 |
| [MIP_CC_Label_GetId](functions.md#mip_cc_label_getid) | 获取标签 ID |
| [MIP_CC_Label_GetNameSize](functions.md#mip_cc_label_getnamesize) | 获取存储名称所需的缓冲区大小 |
| [MIP_CC_Label_GetName](functions.md#mip_cc_label_getname) | 获取标签名称 |
| [MIP_CC_Label_GetDescriptionSize](functions.md#mip_cc_label_getdescriptionsize) | 获取存储说明所需的缓冲区大小 |
| [MIP_CC_Label_GetDescription](functions.md#mip_cc_label_getdescription) | 获取标签说明 |
| [MIP_CC_Label_GetColorSize](functions.md#mip_cc_label_getcolorsize) | 获取存储颜色所需的缓冲区大小 |
| [MIP_CC_Label_GetColor](functions.md#mip_cc_label_getcolor) | 获取标签颜色 |
| [MIP_CC_Label_GetSensitivity](functions.md#mip_cc_label_getsensitivity) | 获取标签的敏感度级别。 较高的值意味着更敏感。 |
| [MIP_CC_Label_GetTooltipSize](functions.md#mip_cc_label_gettooltipsize) | 获取存储工具提示所需的缓冲区大小 |
| [MIP_CC_Label_GetTooltip](functions.md#mip_cc_label_gettooltip) | 获取标签工具提示 |
| [MIP_CC_Label_GetAutoTooltipSize](functions.md#mip_cc_label_getautotooltipsize) | 获取存储自动分类工具提示所需的缓冲区大小 |
| [MIP_CC_Label_GetAutoTooltip](functions.md#mip_cc_label_getautotooltip) | 获取标签自动分类工具提示 |
| [MIP_CC_Label_IsActive](functions.md#mip_cc_label_isactive) | 获取一个标签是否处于活动状态 |
| [MIP_CC_Label_GetParent](functions.md#mip_cc_label_getparent) | 获取父标签（如果有） |
| [MIP_CC_Label_GetChildrenSize](functions.md#mip_cc_label_getchildrensize) | 获取子标签的数目 |
| [MIP_CC_Label_GetChildren](functions.md#mip_cc_label_getchildren) | 获取子标签 |
| [MIP_CC_Label_GetCustomSettings](functions.md#mip_cc_label_getcustomsettings) | 获取标签的策略定义的自定义设置 |
| [MIP_CC_MetadataAction_GetMetadataToRemove](functions.md#mip_cc_metadataaction_getmetadatatoremove) | 获取要移除的 "元数据" 操作的元数据 |
| [MIP_CC_MetadataAction_GetMetadataToAdd](functions.md#mip_cc_metadataaction_getmetadatatoadd) | 获取要添加的 "元数据" 操作的元数据 |
| [MIP_CC_CreateMetadataDictionary](functions.md#mip_cc_createmetadatadictionary) | 创建字符串键/值的字典 |
| [MIP_CC_MetadataDictionary_GetEntries](functions.md#mip_cc_metadatadictionary_getentries) | 获取构成字典的元数据项 |
| [MIP_CC_ReleaseMetadataDictionary](functions.md#mip_cc_releasemetadatadictionary) | 释放与字典关联的资源 |
| [MIP_CC_ReleasePolicyEngine](functions.md#mip_cc_releasepolicyengine) | 释放与策略引擎关联的资源 |
| [MIP_CC_PolicyEngine_GetEngineIdSize](functions.md#mip_cc_policyengine_getengineidsize) | 获取引擎 ID 所需的缓冲区大小 |
| [MIP_CC_PolicyEngine_GetEngineId](functions.md#mip_cc_policyengine_getengineid) | 获取引擎 ID |
| [MIP_CC_PolicyEngine_GetMoreInfoUrlSize](functions.md#mip_cc_policyengine_getmoreinfourlsize) | 获取与策略引擎关联的客户端数据的大小 |
| [MIP_CC_PolicyEngine_GetMoreInfoUrl](functions.md#mip_cc_policyengine_getmoreinfourl) | 获取与策略引擎关联的客户端数据 |
| [MIP_CC_PolicyEngine_IsLabelingRequired](functions.md#mip_cc_policyengine_islabelingrequired) | 获取策略是否指示必须标记文档。 |
| [MIP_CC_PolicyEngine_GetPolicyFileIdSize](functions.md#mip_cc_policyengine_getpolicyfileidsize) | 获取与策略引擎关联的客户端数据的大小 |
| [MIP_CC_PolicyEngine_GetPolicyFileId](functions.md#mip_cc_policyengine_getpolicyfileid) | 获取与策略引擎关联的客户端数据 |
| [MIP_CC_PolicyEngine_GetSensitivityFileIdSize](functions.md#mip_cc_policyengine_getsensitivityfileidsize) | 获取与策略引擎关联的客户端数据的大小 |
| [MIP_CC_PolicyEngine_GetSensitivityFileId](functions.md#mip_cc_policyengine_getsensitivityfileid) | 获取与策略引擎关联的客户端数据 |
| [MIP_CC_PolicyEngine_HasClassificationRules](functions.md#mip_cc_policyengine_hasclassificationrules) | 获取策略是否具有自动或建议规则 |
| [MIP_CC_PolicyEngine_GetLastPolicyFetchTime](functions.md#mip_cc_policyengine_getlastpolicyfetchtime) | 获取上次提取策略的时间 |
| [MIP_CC_PolicyEngine_GetSensitivityLabelsSize](functions.md#mip_cc_policyengine_getsensitivitylabelssize) | 获取与策略引擎关联的敏感度标签的数目 |
| [MIP_CC_PolicyEngine_GetSensitivityLabels](functions.md#mip_cc_policyengine_getsensitivitylabels) | 获取与策略引擎关联的敏感度标签 |
| [MIP_CC_PolicyEngine_GetLabelById](functions.md#mip_cc_policyengine_getlabelbyid) | 按 ID 获取敏感度标签 |
| [MIP_CC_PolicyEngine_GetSensitivityTypesSize](functions.md#mip_cc_policyengine_getsensitivitytypessize) | 获取与策略引擎关联的敏感度类型的数目 |
| [MIP_CC_PolicyEngine_GetSensitivityTypes](functions.md#mip_cc_policyengine_getsensitivitytypes) | 获取与策略引擎关联的敏感度类型 |
| [MIP_CC_PolicyEngine_CreatePolicyHandler](functions.md#mip_cc_policyengine_createpolicyhandler) | 创建策略处理程序以执行策略相关的函数 |
| [MIP_CC_PolicyEngine_SendApplicationAuditEvent](functions.md#mip_cc_policyengine_sendapplicationauditevent) | 将特定于应用程序的事件记录到审核管道 |
| [MIP_CC_PolicyEngine_GetTenantIdSize](functions.md#mip_cc_policyengine_gettenantidsize) | 获取租户 ID 的大小 |
| [MIP_CC_PolicyEngine_GetTenantId](functions.md#mip_cc_policyengine_gettenantid) | 获取租户 ID |
| [MIP_CC_PolicyEngine_GetPolicyDataXmlSize](functions.md#mip_cc_policyengine_getpolicydataxmlsize) | 获取策略数据 xml 的大小 |
| [MIP_CC_PolicyEngine_GetPolicyDataXml](functions.md#mip_cc_policyengine_getpolicydataxml) | 获取策略数据 xml |
| [MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize](functions.md#mip_cc_policyengine_getsensitivitytypesdataxmlsize) | 获取敏感类型数据 xml 的大小 |
| [MIP_CC_PolicyEngine_GetSensitivityTypesDataXml](functions.md#mip_cc_policyengine_getsensitivitytypesdataxml) | 获取敏感类型数据 xml |
| [MIP_CC_PolicyEngine_GetClientDataSize](functions.md#mip_cc_policyengine_getclientdatasize) | 获取与策略引擎关联的客户端数据的大小 |
| [MIP_CC_PolicyEngine_GetClientData](functions.md#mip_cc_policyengine_getclientdata) | 获取与策略引擎关联的客户端数据 |
| [MIP_CC_CreatePolicyEngineSettingsWithIdentity](functions.md#mip_cc_createpolicyenginesettingswithidentity) | 创建用于创建全新策略引擎的设置对象 |
| [MIP_CC_PolicyEngineSettings_SetClientData](functions.md#mip_cc_policyenginesettings_setclientdata) | 设置客户端数据，该数据将与此引擎透明存储并跨会话保存 |
| [MIP_CC_PolicyEngineSettings_SetCustomSettings](functions.md#mip_cc_policyenginesettings_setcustomsettings) | 配置自定义设置，用于功能的门和测试。 |
| [MIP_CC_PolicyEngineSettings_SetSessionId](functions.md#mip_cc_policyenginesettings_setsessionid) | 设置可用于关联日志和遥测的会话 ID |
| [MIP_CC_PolicyEngineSettings_SetCloud](functions.md#mip_cc_policyenginesettings_setcloud) | 设置影响所有服务请求的终结点 Url 的云 |
| [MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl](functions.md#mip_cc_policyenginesettings_setcloudendpointbaseurl) | 设置所有服务请求的基 URL |
| [MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail](functions.md#mip_cc_policyenginesettings_setdelegateduseremail) | 设置委派的用户 |
| [MIP_CC_PolicyEngineSettings_SetLabelFilter](functions.md#mip_cc_policyenginesettings_setlabelfilter) | 设置标签筛选器 |
| [MIP_CC_ReleasePolicyEngineSettings](functions.md#mip_cc_releasepolicyenginesettings) | 释放与策略引擎设置关联的资源 |
| [MIP_CC_ReleasePolicyHandler](functions.md#mip_cc_releasepolicyhandler) | 释放与策略处理程序关联的资源 |
| [MIP_CC_PolicyHandler_GetSensitivityLabel](functions.md#mip_cc_policyhandler_getsensitivitylabel) | 获取文档的当前标签 |
| [MIP_CC_PolicyHandler_ComputeActions](functions.md#mip_cc_policyhandler_computeactions) | 根据所提供的状态执行策略规则并确定相应的操作 |
| [MIP_CC_PolicyHandler_NotifyCommittedActions](functions.md#mip_cc_policyhandler_notifycommittedactions) | 应用计算的操作并将数据提交到磁盘后，由应用程序调用 |
| [MIP_CC_PolicyProfile_AcquireAuthToken](functions.md#mip_cc_policyprofile_acquireauthtoken) | 触发身份验证回拨 |
| [MIP_CC_LoadPolicyProfile](functions.md#mip_cc_loadpolicyprofile) | 加载配置文件 |
| [MIP_CC_ReleasePolicyProfile](functions.md#mip_cc_releasepolicyprofile) | 释放与策略配置文件关联的资源 |
| [MIP_CC_CreatePolicyProfileSettings](functions.md#mip_cc_createpolicyprofilesettings) | 创建用于创建策略配置文件的设置对象 |
| [MIP_CC_PolicyProfileSettings_SetSessionId](functions.md#mip_cc_policyprofilesettings_setsessionid) | 设置可用于关联日志和遥测的会话 ID |
| [MIP_CC_PolicyProfileSettings_SetHttpDelegate](functions.md#mip_cc_policyprofilesettings_sethttpdelegate) | 用客户端自己的替换默认的 HTTP 堆栈 |
| [MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate](functions.md#mip_cc_policyprofilesettings_settaskdispatcherdelegate) | 用客户端自己的替换默认的异步任务调度程序 |
| [MIP_CC_PolicyProfileSettings_SetCustomSettings](functions.md#mip_cc_policyprofilesettings_setcustomsettings) | 配置自定义设置，用于功能的门和测试。 |
| [MIP_CC_ReleasePolicyProfileSettings](functions.md#mip_cc_releasepolicyprofilesettings) | 释放与策略配置文件设置关联的资源 |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize) | 获取存储双密钥加密 url 所需的缓冲区大小。 |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurl) | 获取双密钥加密 url |
| [MIP_CC_ProtectByTemplateAction_GetTemplateId](functions.md#mip_cc_protectbytemplateaction_gettemplateid) | 获取 "按模板保护" 操作的模板 ID |
| [MIP_CC_ProtectByTemplateDkAction_GetTemplateId](functions.md#mip_cc_protectbytemplatedkaction_gettemplateid) | 获取 "使用双键保护模板" 操作的模板 ID |
| [MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurlsize) | 获取存储双密钥加密 url 所需的缓冲区大小。 |
| [MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurl) | 获取双密钥加密 url |
| [MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize) | 获取存储双密钥加密 url 所需的缓冲区大小。 |
| [MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl) | 获取双密钥加密 url |
| [MIP_CC_RemoveContentFooterAction_GetUIElementNames](functions.md#mip_cc_removecontentfooteraction_getuielementnames) | 获取要移除的 "删除内容脚注" 操作的 UI 元素名称 |
| [MIP_CC_RemoveContentHeaderAction_GetUIElementNames](functions.md#mip_cc_removecontentheaderaction_getuielementnames) | 获取要移除的 "删除内容标头" 操作的 UI 元素名称 |
| [MIP_CC_RemoveWatermarkAction_GetUIElementNames](functions.md#mip_cc_removewatermarkaction_getuielementnames) | 获取要移除的 "删除水印" 操作的 UI 元素名称 |
| [MIP_CC_ReleaseSensitivityType](functions.md#mip_cc_releasesensitivitytype) | 释放与敏感度类型关联的资源 |
| [MIP_CC_SensitivityType_GetRulePackageIdSize](functions.md#mip_cc_sensitivitytype_getrulepackageidsize) | 获取存储敏感度类型的规则包 ID 所需的缓冲区大小 |
| [MIP_CC_SensitivityType_GetRulePackageId](functions.md#mip_cc_sensitivitytype_getrulepackageid) | 获取敏感度类型的规则包 ID |
| [MIP_CC_SensitivityType_GetRulePackageSize](functions.md#mip_cc_sensitivitytype_getrulepackagesize) | 获取存储敏感度类型的规则包所需的缓冲区大小 |
| [MIP_CC_SensitivityType_GetRulePackage](functions.md#mip_cc_sensitivitytype_getrulepackage) | 获取敏感度类型的规则包 |
