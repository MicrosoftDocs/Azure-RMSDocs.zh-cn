---
title: 如何&#58;使用内置权限 | Azure RMS
description: 概述了 RMS SDK 4.2 提供的内置权限以及应用为遵守这些限制而强制执行的使用限制。
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 3fd505e8e692cfacafbfec7b65d6e6ac37d539f5
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071261"
---
# <a name="how-to-use-built-in-rights"></a>如何：使用内置权限

本主题概述了 Microsoft Rights Management SDK 4.2 提供的内置权限以及应用为遵守这些限制而强制执行的使用限制。 以下显示内置权限；常见权限、可编辑文档权限和电子邮件权限，之后有描述和操作系统中相应的值。

**请注意** -对于 Linux SDK，请参阅 *rights.h* 源文件了解详细信息。

## <a name="common-rights"></a>常见权限

**所有** - 所有常见权限的集合。
- Android：[CommonRights.All](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS 和 OS X：[MSCommonRights](https://msdn.microsoft.com/library/dn758314.aspx) - 实现“所有”权限的用户所有者和视图
- Windows Store 和 Windows Phone：[CommonRights.All</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.all.aspx)
- Linux:[CommonRights:All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**所有者** - 所有者权限授予对受保护的内容的完全控制。
- Android：[<strong>CommonRights.Owner](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS 和 OS X：[MSCommonRights owner](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store 和 Windows Phone：[CommonRights.Owner](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.owner.aspx)
- Linux:[CommonRights:Owner](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**查看** - 查看受保护内容的权限。 通常情况下，授予此权限时，应用程序使用户能够打开并查看受保护的内容；但是，若要修改、提取、转发或保存内容，还需要其他权限。

- Android：[CommonRights.View](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS 和 OS X：[MSCommonRights view](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows Store 和 Windows Phone：[CommonRights.View](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.view.aspx)
- Linux:[CommonRights:View](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>可编辑文档的权限
**所有** - 包含所有可编辑文档权限的集合。
- Android：[EditableDocumentRights.All](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights all](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store 和 Windows Phone：[EditableDocumentRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.all.aspx)
- Linux:[EditableDocumentRights:All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**注释** - 对文档进行注释的权限。
- Android：[EditableDocumentRights.Comment](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights comment](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store 和 Windows Phone：[EditableDocumentRights.Comment](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.comment.aspx)
- Linux:[EditableDocumentRights:Comment](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**编辑** - 编辑受保护的内容并将其以相同的受保护格式保存。 通常情况下，授予权限后，应用允许用户更改受保护内容并将其保存到相同文件。
- Android：[EditableDocumentRights.Edit](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights edit](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store 和 Windows Phone：[EditableDocumentRights.Edit](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.edit.aspx)
- Linux:[EditableDocumentRights:Edit](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**导出** - 从受保护的格式中提取内容并将其置于不同的 AD 受 RMS 保护的格式中。 通常情况下，授予此权限后，应用使用户可将受保护内容保存到其他 AD 受 RMS 保护的格式；例如，如果应用程序实施“另存为”功能。

- Android：[EditableDocumentRights.Export](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights exportable](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store 和 Windows Phone：[EditableDocumentRights.Export](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.export.aspx)
- Linux:[EditableDocumentRights:Export](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**提取** - 从受保护的格式中提取内容并将其置于不受保护的格式中。 通常情况下，授予权限后，应用使用户可从受保护内容复制和粘贴信息。 如果应用实施“另存为”功能，应用程序可能也会使用户将受保护内容保存到不受保护的格式以及其他受保护的格式。 此权限与电子邮件的“提取”权限具有相同的值。

- Android：[EditableDocumentRights.Extract](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights extract](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store 和 Windows Phone：[EditableDocumentRights.Extract](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.extract.aspx)
- Linux:[EditableDocumentRights:Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**打印** - 打印受保护内容的权限。 通常情况下，授予权限后，应用允许用户打印受保护内容。 此权限与电子邮件的“打印”权限具有相同的值。

- Android：[EditableDocumentRights.Print](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights print](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows Store 和 Windows Phone：[EditableDocumentRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.print.aspx)
- Linux:[EditableDocumentRights:Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>电子邮件权限

**所有** - 包含所有电子邮件权限的集合。
- Android：[EmailRights.All](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights all](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store 和 Windows Phone：[EmailRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.all.aspx)
- Linux:[EmailRights:All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**提取** - 从受保护的格式中提取内容并将其置于不受保护的格式中。 通常情况下，授予权限后，应用允许电子邮件收件人从受保护电子邮件复制和粘贴信息。 如果应用实施“另存为”功能，应用程序可能也会允许收件人将受保护内容保存为不受保护的格式以及其他受保护的格式。 此权限与可编辑文档的“提取”权限具有相同的值。

- Android：[EmailRights.Extract](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights extract](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store 和 Windows Phone：[EmailRights.Extract</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.extract.aspx)
- Linux:[EmailRights:Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**转发** - 转发受保护电子邮件的权限。 通常情况下，授予权限后，应用允许电子邮件收件人转发受保护电子邮件。
- Android：[<strong>EmailRights.Forward</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights forward](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store 和 Windows Phone：[EmailRights.Forward](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.forward.aspx)
- Linux:[EmailRights:Forward](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**打印** - 打印受保护内容的权限。 通常情况下，授予权限后，应用允许电子邮件收件人打印受保护电子邮件。 此权限与可编辑文档的“打印”权限具有相同的值。

- Android：[EmailRights.Print](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights print](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store 和 Windows Phone：[EmailRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.print.aspx)
- Linux:[EmailRights:Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**回复** - 通常情况下，授予此权限后，应用允许电子邮件收件人回复受保护电子邮件并附上原始电子邮件的副本。

- Android：[EmailRights.Reply](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights reply](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store 和 Windows Phone：[EmailRights.Reply](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.reply.aspx)
- Linux:[EmailRights:Reply](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**回复所有** - 通常情况下，授予此权限后，应用允许电子邮件收件人回复受保护电子邮件的所有收件人并附上原始电子邮件的副本。

- Android：[EmailRights.ReplyAll</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights replyAll](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows Store 和 Windows Phone：[EmailRights.ReplyAll](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.replyall.aspx)
- Linux:[EmailRights:ReplyAll](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)
