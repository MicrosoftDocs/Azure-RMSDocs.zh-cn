---
title: MIP SDK for C 参考
description: MIP SDK for C 参考
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 6269921c14b0ac284aab501253d07bea416ef137
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565254"
---
# <a name="mip-sdk-for-c-reference"></a>MIP SDK for C 参考

Microsoft 信息保护 (适用于 C 的 MIP) SDK，开发人员可使用它来管理数据保护策略并将其应用到数据和其他数字资产。

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
| [MIP_CC_ProtectionDescriptor_GetContentValidUntil](functions.md#mip_cc_protectiondescriptor_getcontentvaliduntil) | 从 epoch 开始，获取保护过期时间 (秒)  |
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
| [MIP_CC_TemplateDescriptor_GetId](functions.md#mip_cc_templatedescriptor_getid) | 获取模板 ID |
| [MIP_CC_TemplateDescriptor_GetNameSize](functions.md#mip_cc_templatedescriptor_getnamesize) | 获取存储名称所需的缓冲区大小 |
| [MIP_CC_TemplateDescriptor_GetName](functions.md#mip_cc_templatedescriptor_getname) | 获取模板名称 |
| [MIP_CC_TemplateDescriptor_GetDescriptionSize](functions.md#mip_cc_templatedescriptor_getdescriptionsize) | 获取存储说明所需的缓冲区大小 |
| [MIP_CC_TemplateDescriptor_GetDescription](functions.md#mip_cc_templatedescriptor_getdescription) | 获取模板说明 |
| [MIP_CC_ReleaseTemplateDescriptor](functions.md#mip_cc_releasetemplatedescriptor) | 释放与模板描述符关联的资源 |
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
| [MIP_CC_AddContentFooterAction_GetFontColor](functions.md#mip_cc_addcontentfooteraction_getfontcolor) | 获取 "添加内容脚注" 操作的字体颜色 (例如 "#000000" )  |
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
| [MIP_CC_AddContentHeaderAction_GetFontColor](functions.md#mip_cc_addcontentheaderaction_getfontcolor) | 获取 "添加内容标头" 操作的字体颜色 (例如 "#000000" )  |
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
| [MIP_CC_AddWatermarkAction_GetFontColor](functions.md#mip_cc_addwatermarkaction_getfontcolor) | 获取 "添加水印" 操作的字体颜色 (例如 "#000000" )  |
| [MIP_CC_ReleaseContentLabel](functions.md#mip_cc_releasecontentlabel) | 释放与内容标签关联的资源 |
| [MIP_CC_ContentLabel_GetCreationTime](functions.md#mip_cc_contentlabel_getcreationtime) | 获取应用标签的时间 |
| [MIP_CC_ContentLabel_GetAssignmentMethod](functions.md#mip_cc_contentlabel_getassignmentmethod) | 获取标签分配方法 |
| [MIP_CC_ContentLabel_GetExtendedProperties](functions.md#mip_cc_contentlabel_getextendedproperties) | 获取扩展属性 |
| [MIP_CC_ContentLabel_IsProtectionAppliedFromLabel](functions.md#mip_cc_contentlabel_isprotectionappliedfromlabel) | 获取一个标签是否应用了保护。 |
| [MIP_CC_ContentLabel_GetLabel](functions.md#mip_cc_contentlabel_getlabel) | 从内容标签实例获取一般标签属性 |
| [MIP_CC_CustomAction_GetNameSize](functions.md#mip_cc_customaction_getnamesize) | 获取存储 "自定义" 操作名称所需的缓冲区大小 |
| [MIP_CC_CustomAction_GetName](functions.md#mip_cc_customaction_getname) | 获取 "自定义" 操作的名称 |
| [MIP_CC_CustomAction_GetProperties](functions.md#mip_cc_customaction_getproperties) | 获取 "自定义" 操作的属性 |
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
| [MIP_CC_ReleasePolicyHandler](functions.md#mip_cc_releasepolicyhandler) | 释放与策略处理程序关联的资源 |
| [MIP_CC_PolicyHandler_GetSensitivityLabel](functions.md#mip_cc_policyhandler_getsensitivitylabel) | 获取文档的当前标签 |
| [MIP_CC_PolicyHandler_ComputeActions](functions.md#mip_cc_policyhandler_computeactions) | 根据所提供的状态执行策略规则并确定相应的操作 |
| [MIP_CC_PolicyHandler_NotifyCommittedActions](functions.md#mip_cc_policyhandler_notifycommittedactions) | 应用计算的操作并将数据提交到磁盘后，由应用程序调用 |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize) | 获取存储双密钥加密 url 所需的缓冲区大小。 |
| [MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl](functions.md#mip_cc_protectadhocdkaction_getdoublekeyencryptionurl) | 获取双密钥加密 url |
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
