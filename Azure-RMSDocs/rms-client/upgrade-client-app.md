---
title: "用于操作 RMS 共享应用程序的任务 - AIP"
description: "适用于从 RMS 共享应用程序升级到 Azure 信息保护客户端的用户的说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 9d955866337fc050cd6025a9c7cdb3384f598976
ms.sourcegitcommit: 02e860196efca306ef9d1e61c1d89c4d8593c912
translationtype: HT
---
# <a name="tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>用于操作 RMS 共享应用程序的任务

最近从 Rights Management 共享应用程序（也称为“RMS 共享应用”）升级到 Azure 信息保护客户端？ 

使用以下信息可帮助你快速启动和运行。

|RMS 共享应用|如何使用 Azure 信息保护客户端进行操作
|-----------|--------------------|
|保护设备上的文件 <br /><br />也称为“就地保护”|对于 Office 应用程序：选择应用所需保护的标签，或设置自定义权限。<br /><br />对于其他文件：使用文件资源管理器菜单选项“**分类和保护**”打开“**分类和保护 - Azure 信息保护**”对话框。 然后选择应用所需保护的标签，或指定你自己的自定义权限。 <br /><br />有关详细信息，请参阅[对文件或电子邮件进行分类和保护](client-classify-protect.md)。
|保护通过电子邮件共享的文件 <br /><br />也称为“共享保护项”|如果在内部共享：对文档或电子邮件应用具有必需保护的标签，或选择 Outlook 中的“不要转发”选项。 <br /><br /> 如果要与外部共享：使用文件副本和自定义权限在 Office 应用程序或文件资源管理器内保护文件。 然后使用标准共享机制共享文件，例如电子邮件的附件或 SharePoint Online 文档的邀请。 请考虑附带 https://aka.ms/rms-signup 链接，以提供首次使用的说明。 <br /><br />有关外部共享的详细信息，请参阅用户指南中的[与组织外部人员安全共享文件](client-classify-protect.md#safely-share-a-file-with-people-outside-your-organization)部分。
|更改受保护的文件的权限 <br /><br />也称为“重新保护”|对于显示 Azure 信息保护栏的 Office 应用程序：选择应用所需保护的标签。<br /><br />对于其他文件，如果 Azure 信息保护客户端处于[仅保护模式](client-protection-only-mode.md)：使用文件资源管理器菜单选项“分类和保护”来打开“分类和保护 - Azure 信息保护”对话框。 然后选择应用所需保护的标签，或指定你自己的自定义权限。<br /><br />有关详细信息，请参阅[对文件或电子邮件进行分类和保护](client-classify-protect.md)。
|跟踪和撤销文档|对于 Office 应用程序：打开文档，然后选择“开始”选项卡>“保护”组>“保护” > “跟踪和撤销”<br /><br />从文件资源管理器：右键单击文件或文件夹 > 选择“分类和保护”。 然后在“分类和保护 - Azure 信息保护”对话框中，单击“跟踪和撤销”。 <br /><br />有关详细信息，请参阅[跟踪和撤销文档](client-track-revoke.md)。
|保护你通过电子邮件共享的文件|Azure 信息保护查看器可以打开受保护的文件，以便你可以读取它们，而且如果你有权限执行这些操作，还可以打印和保存这些文件。 此查看器随客户端自动安装，也可以单独安装。<br /><br />有关详细信息，请参阅[打开受保护的文件](client-view-use-files.md)。
|删除对文件的保护|使用文件资源管理器菜单选项“分类并保护”打开“分类和保护 - Azure 信息保护”对话框。 <br /><br />然后对于单个文件，清除“使用自定义权限保护”选项。 对于多个文件或文件夹，单击“删除自定义权限”。<br /><br />有关详细信息，请参阅[删除文件和电子邮件中的标签和保护](client-remove-label-protection.md)。|

## <a name="cant-find-the-option-youre-looking-for"></a>找不到要查找的选项？

如果你正在查找通常在 RMS共享应用程序中选择的特定选项，请查看下表。

|RMS 共享应用中的选项|信息
|-----------|--------------------|
|**共享保护项**|Office 功能区不再提供此选项。 不要直接在 Office 应用程序中共享，请使用文件资源管理器的右键单击选项“分类和保护”来通过自定义权限保护文档副本，然后使用所选电子邮件客户端或共享位置来共享文件。 请考虑附带 https://aka.ms/rms-signup 链接，以提供首次使用的说明。 <br /><br />有关外部共享的详细信息，请参阅用户指南中的[与组织外部人员安全共享文件](#safely-share-a-file-with-people-outside-your-organization)部分。
|**当有人尝试打开这些文档时，给我送发电子邮件**|使用文档跟踪站点配置首选电子邮件通知设置：找到你共享的受保护文档>“设置” > “电子邮件通知”
|**允许我立即撤消对这些文档的访问权限**|此选项不再可用。 配置不允许脱机访问的模板。 此外，请考虑是否需要通过运行 [Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime) 来减少租户的使用许可证有效期。







[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
