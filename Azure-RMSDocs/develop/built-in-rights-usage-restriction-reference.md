---
# required metadata

title: 如何&#58;使用内置权限 | Azure RMS
description: 概述了 RMS SDK 4.2 提供的内置权限以及应用为遵守这些限制而强制执行的使用限制。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 如何：使用内置权限

本主题概述了 Microsoft Rights Management SDK 4.2 提供的内置权限以及应用为遵守这些限制而强制执行的使用限制。 以下显示内置权限；常见权限、可编辑文档权限和电子邮件权限，之后有描述和操作系统中相应的值。

**请注意** -对于 Linux SDK，请参阅 *rights.h* 源文件了解详细信息。

## 常见权限 ##

**所有** - 所有常见权限的集合。
- Android：[CommonRights.All](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL)
- iOS 和 OS X：[MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows 应用商店和 Windows Phone：[CommonRights.All</strong>](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)
- Linux：[CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**所有者** - 所有者权限授予对受保护的内容的完全控制。
- Android：[<strong>CommonRights.Owner](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner)
- iOS 和 OS X：[MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows 应用商店和 Windows Phone：[CommonRights.Owner](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner)
- Linux：[CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**查看** - 查看受保护内容的权限。 通常情况下，授予此权限时，应用程序使用户能够打开并查看受保护的内容；但是，若要修改、提取、转发或保存内容，还需要其他权限。

- Android：[CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- iOS 和 OS X：[MSCommonRights view](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows 应用商店和 Windows Phone：[CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- Linux：[CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## 可编辑文档的权限 ##
**所有** - 包含所有可编辑文档权限的集合。
- Android：[EditableDocumentRights.All](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL)
- iOS 和 OS X：[MSEditableDocumentRights all](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EditableDocumentRights.All](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all)
- Linux：[EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**注释** - 对文档进行注释的权限。
- Android：[EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)
- iOS 和 OS X：[MSEditableDocumentRights comment](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)
- Linux：[EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**编辑** - 编辑受保护的内容并将其以相同的受保护格式保存。 通常情况下，授予权限后，应用允许用户更改受保护内容并将其保存到相同文件。
- Android：[EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit)
- iOS 和 OS X：[MSEditableDocumentRights edit](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit)
- Linux：[EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**导出** - 从受保护的格式中提取内容并将其置于不同的 AD 受 RMS 保护的格式中。 通常情况下，授予此权限后，应用使用户可将受保护内容保存到其他 AD 受 RMS 保护的格式；例如，如果应用程序实施“另存为”功能。

- Android：[EditableDocumentRights.Export](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export)
- iOS 和 OS X：[MSEditableDocumentRights exportable](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EditableDocumentRights.Export](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export)
- Linux：[EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**提取** - 从受保护的格式中提取内容并将其置于不受保护的格式中。 通常情况下，授予权限后，应用使用户可从受保护内容复制和粘贴信息。 如果应用实施“另存为”<em></em>功能，应用程序可能也会使用户将受保护内容保存到不受保护的格式以及其他受保护的格式。 此权限与电子邮件的“提取”权限具有相同的值。

- Android：[EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract)
- iOS 和 OS X：[MSEditableDocumentRights extract](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract)
- Linux：[EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**打印** - 打印受保护内容的权限。 通常情况下，授予权限后，应用允许用户打印受保护内容。 此权限与电子邮件的“打印”权限具有相同的值。

- Android：[EditableDocumentRights.Print](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print)
- iOS 和 OS X：[MSEditableDocumentRights print](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EditableDocumentRights.Print](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print)
- Linux：[EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## 电子邮件权限 ##

**所有** - 包含所有电子邮件权限的集合。
- Android：[EmailRights.All](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL)
- iOS 和 OS X：[MSEmailRights all](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EmailRights.All](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)
- Linux：[EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**提取** - 从受保护的格式中提取内容并将其置于不受保护的格式中。 通常情况下，授予权限后，应用允许电子邮件收件人从受保护电子邮件复制和粘贴信息。 如果应用实施“另存为”<em></em>功能，应用程序可能也会允许收件人将受保护内容保存为不受保护的格式以及其他受保护的格式。 此权限与可编辑文档的“提取”权限具有相同的值。

- Android：[EmailRights.Extract](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract)
- iOS 和 OS X：[MSEmailRights extract](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EmailRights.Extract</strong>](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract)
- Linux：[EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**转发** - 转发受保护电子邮件的权限。 通常情况下，授予权限后，应用允许电子邮件收件人转发受保护电子邮件。
- Android：[<strong>EmailRights.Forward</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward)
- iOS 和 OS X：[MSEmailRights forward](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EmailRights.Forward](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward)
- Linux：[EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**打印** - 打印受保护内容的权限。 通常情况下，授予权限后，应用允许电子邮件收件人打印受保护电子邮件。 此权限与可编辑文档的“打印”权限具有相同的值。

- Android：[EmailRights.Print](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print)
- iOS 和 OS X：[MSEmailRights print](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EmailRights.Print](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print)
- Linux：[EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**回复** - 通常情况下，授予此权限后，应用允许电子邮件收件人回复受保护电子邮件并附上原始电子邮件的副本。

- Android：[EmailRights.Reply](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply)
- iOS 和 OS X：[MSEmailRights reply](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EmailRights.Reply](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply)
- Linux：[EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**回复所有** - 通常情况下，授予此权限后，应用允许电子邮件收件人回复受保护电子邮件的所有收件人并附上原始电子邮件的副本。

- Android：[EmailRights.ReplyAll</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll)
- iOS 和 OS X：[MSEmailRights replyAll](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 应用商店和 Windows Phone：[EmailRights.ReplyAll](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall)
- Linux：[EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

 

 

 


<!--HONumber=Apr16_HO4-->


