---
title: 用于操作 RMS 共享应用程序的任务 - AIP
description: 适用于从 RMS 共享应用程序升级到 Azure 信息保护客户端的用户的说明。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: cc1d3c3d64d6c8b51d355fd870c48138a6ed4d33
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117521"
---
# <a name="user-guide-tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>用户指南：用于操作 RMS 共享应用程序的任务

>*适用于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、带 SP1 的 windows 7、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> *适用于[Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

最近从 Rights Management 共享应用程序（也称为“RMS 共享应用”）升级到 Azure 信息保护客户端？ 

使用以下信息可帮助你快速启动和运行。

|RMS 共享应用|如何使用 Azure 信息保护客户端进行操作
|-----------|--------------------|
|保护设备上的文件 <br /><br />也称为“就地保护”|对于 Office 应用程序：选择应用所需保护的标签，或设置自定义权限。<br /><br />对于其他文件：使用文件资源管理器菜单选项“**分类和保护**”打开“**分类和保护 - Azure 信息保护**”对话框。 然后选择应用所需保护的标签，或指定你自己的自定义权限。 <br /><br />有关详细信息，请参阅[对文件或电子邮件进行分类和保护](client-classify-protect.md)。
|保护你通过电子邮件共享的文件 <br /><br />也称为“共享保护项”|通过使用 Outlook，对电子邮件应用具有所需保护的标签，或选择 Outlook 中的“不要转发”选项。 具有[受支持文件类型](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)的未受保护附件会自动受到保护。<br /><br />注意：若要跟踪通过电子邮件发送的受保护文档，请首先保护此文档，然后再将它附加到电子邮件中。<br /><br />有关详细信息，请参阅[对文件或电子邮件进行分类和保护](client-classify-protect.md)。
|更改受保护的文件的权限 <br /><br />也称为“重新保护”|对于显示 Azure 信息保护栏的 Office 应用程序：选择应用所需保护的标签。<br /><br />对于其他文件，如果 Azure 信息保护客户端处于[仅保护模式](client-protection-only-mode.md)：使用文件资源管理器菜单选项“分类和保护”来打开“分类和保护 - Azure 信息保护”对话框。 然后选择应用所需保护的标签，或指定你自己的自定义权限。<br /><br />有关详细信息，请参阅[对文件或电子邮件进行分类和保护](client-classify-protect.md)。
|跟踪和撤销文档|在 Word、Excel 和 PowerPoint 中：打开文档，再依次选择“开始”选项卡>“保护”组>“保护” > “跟踪和撤销”<br /><br />从文件资源管理器：右键单击文件或文件夹 > 选择“分类和保护”。 然后在“分类和保护 - Azure 信息保护”对话框中，单击“跟踪和撤销”。 <br /><br />将 PowerShell 用于 Azure 信息保护客户端时：将*bre-walkthrough-enabletracking*参数与[set-aipfilelabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) cmdlet 一起用于注册要跟踪的标记文档。<br /><br />有关详细信息，请参阅[跟踪和撤销文档](client-track-revoke.md)。
|查看和使用受保护的文件|对于受保护的 Office 文档，必须安装 Office。 Azure 信息保护查看器可以打开许多其他受保护的文件，使你可以阅读它们，而且在你有相关权限的情况下还可以打印和保存这些文件。 此查看器随客户端自动安装，也可以单独安装。<br /><br />有关详细信息，请参阅[打开受保护的文件](client-view-use-files.md)。
|删除对文件的保护|使用文件资源管理器菜单选项“分类并保护”打开“分类和保护 - Azure 信息保护”对话框。 <br /><br />然后对于单个文件，清除“使用自定义权限保护”选项。 对于多个文件或文件夹，单击“删除自定义权限”。<br /><br />有关详细信息，请参阅[删除文件和电子邮件中的标签和保护](client-remove-label-protection.md)。|

## <a name="cant-find-the-option-youre-looking-for"></a>找不到要查找的选项？

如果你正在查找通常在 RMS共享应用程序中选择的特定选项，请查看下表。

|RMS 共享应用中的选项|信息
|-----------|--------------------|
|**共享保护项**|Office 功能区不再提供此选项。 不要直接在 Office 应用程序中共享，请使用文件资源管理器的右键单击选项“分类和保护”来通过自定义权限保护文档副本，然后使用所选电子邮件客户端或共享位置来共享文件。 <br /><br /> 还可以将未受保护的 Office 文档附加到保护的电子邮件，文档会自动受到相同限制带来的保护。 但是，如此便无法跟踪和撤消此文档。
|**当有人尝试打开这些文档时，给我送发电子邮件**|使用文档跟踪站点配置首选电子邮件通知设置：找到你共享的受保护文档>“设置” > “电子邮件通知”
|**允许我立即撤消对这些文档的访问权限**|此选项不再可用。 使用不允许脱机访问的管理员定义的保护设置。 此外，管理员可以通过运行[AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)来减少租户的使用许可证有效期。
|Outlook 中的“跟踪使用情况”|无法再通过 Outlook 访问文档跟踪网站。 请改用 Word、PowerPoint、Excel 或文件资源管理器中的“跟踪和撤销选项。 也可以使用浏览器直接转到[文档跟踪网站](https://go.microsoft.com/fwlink/?LinkId=529562)。

## <a name="next-steps"></a>后续步骤
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅 [Azure 信息保护客户端管理员指南](client-admin-guide.md)。

  
