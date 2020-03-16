---
title: 配置 Azure 信息保护的使用权限
description: 了解和确定在使用 Azure 信息保护中的 Rights Management 保护来保护文件或电子邮件时使用的特定权限。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 74e76f9e15c81a187c602b6e546a3a89620d9200
ms.sourcegitcommit: 2917e822a5d1b21bf465f2cb93cfe46937b1faa7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2020
ms.locfileid: "79404651"
---
# <a name="configuring-usage-rights-for-azure-information-protection"></a>配置 Azure 信息保护的使用权限

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

当你为加密配置敏感度标签或保护模板时，你可以选择在用户、管理员或配置的服务选择标签或模板时将自动应用的使用权限。 例如，在 Azure 门户中，可以选择配置使用权限逻辑分组的角色，或者可以配置单个权限。 另外，用户还可以选择并应用使用权限本身。

本文介绍如何为所使用的应用程序配置所需的使用权限，并了解这些权限是如何由应用程序进行解释的。 但是，应用程序在实现权限的方式上可能会有所不同，因此请始终查阅其文档，并使用用户对应用程序进行测试，以便在生产环境中进行部署之前查看行为。

> [!NOTE] 
> 为保持完整性，本文包括已在 2018 年 1 月 8 日停用的 Azure 经典门户中的值。

## <a name="usage-rights-and-descriptions"></a>使用权限和说明
下表列出并说明了 Rights Management 支持的使用权限，以及它们的使用和解释方式。 它们按公用名列出，公用名通常是你看待使用权限作为在代码中使用的单字值（策略中的编码值）的更友好版本进行显示或引用的方式。 

在此表中：

- **Api 常量或值**是 MSIPC API 调用的 SDK 名称，可在编写用于检查使用权限的应用程序时使用，也可将使用权限添加到策略。

- **标签管理中心**是指配置敏感度标签的位置，可以是 Microsoft 365 符合性中心、Microsoft 365 安全中心或 Office 365 安全与合规中心。


|使用权限|说明|实现|
|-------------------------------|---------------------------|-----------------|
|公用名称：**编辑内容、编辑** <br /><br />策略中的编码：**DOCEDIT**|允许用户对应用程序中的内容进行修改、重新排列、设置格式或排序。 它不会授权保存编辑过的副本。<br /><br />在 Word 中，除非 Office 365 专业增强版的最低版本为 [1807](https://docs.microsoft.com/officeupdates/monthly-channel-2018#version-1807-july-25)，否则此权限不足，无法启用或禁用“跟踪更改”，也无法以审阅者身份使用所有跟踪更改功能。 相反，必须具有以下权限才能使用所有跟踪更改选项：**完全控制**。 |Office 自定义权限：作为“更改” 和“完全控制” 选项的一部分。 <br /><br />Azure 经典门户中的名称：**编辑内容**<br /><br />标记管理中心和 Azure 门户中的名称：**编辑内容、编辑 (DOCEDIT)**<br /><br />AD RMS 模板中的名称：**编辑** <br /><br />API 常量或值：不适用。|
|公用名称：**保存** <br /><br />策略中的编码：**EDIT**|允许用户将文档保存到当前位置。<br /><br />在 Office 应用程序中，如果所选文件格式以本机方式支持 Rights Management 保护，则此权限还允许用户修改文档并以新名称将其保存到新位置。 文件格式限制可确保无法从文件中删除原始保护。|Office 自定义权限：作为“更改” 和“完全控制” 选项的一部分。 <br /><br />Azure 经典门户中的名称：**保存文件**<br /><br />标记管理中心和 Azure 门户中的名称：**保存 (EDIT)**<br /><br />AD RMS 模板中的名称：**保存** <br /><br />API 常量或值：`IPC_GENERIC_WRITE L"EDIT"`|
|公用名称：**注释** <br /><br />策略中的编码：**COMMENT**|启用向内容添加批注或注释的选项。<br /><br />此权限可用于 SDK、在 AzureInformationProtection 和适用于 Windows PowerShell 的 RMS 保护模块中作为即席策略提供，并且已在一些软件供应商应用程序中实现。 但是，它并未广泛使用，并且不受 Office 应用程序支持。|Office 自定义权限：未实现。 <br /><br />Azure 经典门户中的名称：未实现。<br /><br />标记管理中心和 Azure 门户中的名称：未实现。<br /><br />AD RMS 模板中的名称：未实现。 <br /><br />API 常量或值：`IPC_GENERIC_COMMENT L"COMMENT`|
|公用名称：**另存为、导出** <br /><br />策略中的编码：**EXPORT**|启用将内容保存到其他文件名的选项（另存为）。 <br /><br />对于 Azure 信息保护客户端，文件可在不受保护的情况下进行保存，也可使用新设置和权限重新保护。 这些允许的操作意味着，具有此权限的用户可以从受保护的文档或电子邮件对 Azure 信息保护标签进行更改或删除。 <br /><br />此权限还允许用户在应用程序中执行其他导出选项，如“发送至 OneNote”。|Office 自定义权限：作为“完全控制”选项的一部分。 <br /><br />Azure 经典门户中的名称：**导出内容（另存为）** <br /><br />标记管理中心和 Azure 门户中的名称：**另存为、导出 (EXPORT)**<br /><br />AD RMS 模板中的名称：**导出（另存为）** <br /><br />API 常量或值：`IPC_GENERIC_EXPORT L"EXPORT"`|
|公用名称：**转发** <br /><br />策略中的编码：**FORWARD**|启用此选项以转发电子邮件，并将收件人添加到“收件人” 和“抄送” 行。 此权限不适用于文档；仅适用于电子邮件。<br /><br />不允许转发器授予其他用户权限作为转发操作的一部分。 <br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），另外授予“保存”权限（通用名称），以确保受保护的电子邮件不作为附件发送。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也指定这些权限。 或者，对于组织中免于使用 Rights Management 保护的用户，因为你已实现了[载入控件](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)。|Office 自定义权限：使用“不得转发” 标准策略时拒绝。<br /><br />Azure 经典门户中的名称：**转发**<br /><br />标记管理中心和 Azure 门户中的名称：**转发 (FORWARD)**<br /><br />AD RMS 模板中的名称：**转发** <br /><br />API 常量或值：`IPC_EMAIL_FORWARD L"FORWARD"`|
|公用名称：**完全控制** <br /><br />策略中的编码：**OWNER**|授予对文档的所有权限，并且所有可用操作都可以执行。<br /><br />包括删除保护和重新保护文档的功能。 <br /><br />请注意，此使用权限不等同于[权限管理所有者](#rights-management-issuer-and-rights-management-owner)。|Office 自定义权限：作为“完全控制” 自定义选项。<br /><br />Azure 经典门户中的名称：**完全控制**<br /><br />标记管理中心和 Azure 门户中的名称：**完全控制 (OWNER)**<br /><br />AD RMS 模板中的名称：**完全控制** <br /><br />API 常量或值：`IPC_GENERIC_ALL L"OWNER"`|
|公用名称：**打印** <br /><br />策略中的编码：**PRINT**|启用打印内容的选项。|Office 自定义权限：作为自定义权限中的“打印内容” 选项。 不是特定于收件人的设置。<br /><br />Azure 经典门户中的名称：**打印**<br /><br />标记管理中心和 Azure 门户中的名称：**打印 (PRINT)**<br /><br />AD RMS 模板中的名称：**打印** <br /><br />API 常量或值：`IPC_GENERIC_PRINT L"PRINT"`|
|公用名称：**答复** <br /><br />策略中的编码：**REPLY**|启用邮件客户端中的“答复”选项，但不允许更改“收件人”或“抄送”行。<br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），另外授予“保存”权限（通用名称），以确保受保护的电子邮件不作为附件发送。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也指定这些权限。 或者，对于组织中免于使用 Rights Management 保护的用户，因为你已实现了[载入控件](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)。|Office 自定义权限：不适用。<br /><br />Azure 经典门户中的名称：**答复**<br /><br />Azure 经典门户中的名称：**答复 (REPLY)**<br /><br />AD RMS 模板中的名称：**答复** <br /><br />API 常量或值：`IPC_EMAIL_REPLY`|
|公用名称：**全部答复** <br /><br />策略中的编码：**REPLYALL**|启用邮件客户端中的“全部答复” 选项，但不允许用户将收件人添加到“收件人” 或“抄送” 行。<br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），另外授予“保存”权限（通用名称），以确保受保护的电子邮件不作为附件发送。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也指定这些权限。 或者，对于组织中免于使用 Rights Management 保护的用户，因为你已实现了[载入控件](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)。|Office 自定义权限：不适用。<br /><br />Azure 经典门户中的名称：**全部答复**<br /><br />标记管理中心和 Azure 门户中的名称：**全部答复 (REPLY ALL)**<br /><br />AD RMS 模板中的名称：**全部答复** <br /><br />API 常量或值：`IPC_EMAIL_REPLYALL L"REPLYALL"`|
|公用名称：**查看、打开、读取** <br /><br />策略中的编码：**VIEW**|允许用户打开文档，并查看内容。<br /><br /> 在 Excel 中，此权限不足，无法对数据进行排序，必须拥有以下权限：“编辑内容、编辑”。 若要在 Excel 中筛选数据，需要拥有以下两项权限：“编辑内容、编辑”和“复制”。|Office 自定义权限：作为“读取” 自定义策略，“查看” 选项。<br /><br />Azure 经典门户中的名称：**视图**<br /><br />标记管理中心和 Azure 门户中的名称：**查看、打开、读取 (VIEW)**<br /><br />AD RMS 模板中的名称：**读取** <br /><br />API 常量或值：`IPC_GENERIC_READ L"VIEW"`|
|公用名称：**复制** <br /><br />策略中的编码：**EXTRACT**|启用将数据（包括屏幕捕获）从文档复制到同一文档或其他文档的选项。<br /><br />在某些应用程序中，它还允许以不受保护的形式保存整个文档。<br /><br />在 Skype for Business 和类似屏幕共享应用程序中，演示者必须拥有此权限，才能成功展示受保护文档。 如果演示者没有此权限，与会者便无法查看文档，且文档显示为对与会者禁用。|Office 自定义权限：作为“允许具有读取权限的用户复制内容” 自定义策略选项。<br /><br />Azure 经典门户中的名称：**复制和提取内容**<br /><br />标记管理中心和 Azure 门户中的名称：**复制 (EXTRACT)**<br /><br />AD RMS 模板中的名称：**提取** <br /><br />API 常量或值：`IPC_GENERIC_EXTRACT L"EXTRACT"`|
|公用名称：**查看权限** <br /><br />策略中的编码：**VIEWRIGHTSDATA**|允许用户查看应用于文档的策略。 <br /><br /> 不受 Office 应用或 Azure 信息保护客户端支持。|Office 自定义权限：未实现。<br /><br />Azure 经典门户中的名称：**查看已分配的权限**<br /><br />标记管理中心和 Azure 门户中的名称：**查看权限 (VIEWRIGHTSDATA)** 。<br /><br />AD RMS 模板中的名称：**查看权限** <br /><br />API 常量或值：`IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|公用名称：**更改权限** <br /><br />策略中的编码：**EDITRIGHTSDATA**|允许用户更改应用于文档的策略。 包括删除的保护。 <br /><br /> 不受 Office 应用或 Azure 信息保护客户端支持。|Office 自定义权限：未实现。<br /><br />Azure 经典门户中的名称：**更改权限**<br /><br />标记管理中心和 Azure 门户中的名称：**编辑权限 (EDITRIGHTSDATA)** 。<br /><br />AD RMS 模板中的名称：**编辑权限** <br /><br />API 常量或值：`PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|公用名称：**允许宏** <br /><br />策略中的编码：**OBJMODEL**|启用运行宏或执行其他编程或远程访问文档内容的选项。|Office 自定义权限：作为“允许编程访问” 自定义策略选项。 不是特定于收件人的设置。<br /><br />Azure 经典门户中的名称：**允许宏**<br /><br />标记管理中心和 Azure 门户中的名称：**允许宏 (OBJMODEL)**<br /><br />AD RMS 模板中的名称：**允许宏** <br /><br />API 常量或值：未实现。|

## <a name="rights-included-in-permissions-levels"></a>权限级别中包括的权限

某些应用程序会将使用权限组合成不同的权限级别，这样可以更容易地选择那些通常在一起使用的使用权限。 这些权限级别可帮助减少用户操作的复杂性，用户只需按角色选择相应选项即可。  例如，**审阅者**和**合著者**。 虽然这些选项通常会向用户显示这些权限的摘要，但可能并不包括前一表中列出的每个权限。

可通过下表查看这些权限级别的列表，以及这些权限级别所含使用权限的完整列表。 使用权限按各自的[公用名](#usage-rights-and-descriptions)列出。

|权限级别|应用程序|包含的使用权限|
|---------------------|----------------|---------------------------------|
|查看器|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；查看权限；答复 [[1]](#footnote-1)；全部答复 [[1]](#footnote-1)；允许宏 [[2]](#footnote-2)<br /><br />注意:对于电子邮件，请使用“审阅者”级别而不是此权限级别来确保接收到的电子邮件答复为电子邮件而不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要审阅者权限。 或者，对于组织内无需使用 Azure Rights Management 服务的用户来说，也需要此权限，因为你已实施了[载入控件](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)。|
|审阅者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；查看权限；答复：全部答复 [[3]](#footnote-3)；转发 [[3]](#footnote-3)；允许宏 [[2]](#footnote-2)|
|合著者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；复制；查看权限；允许宏；另存为、导出 [[4]](#footnote-4)；打印；答复 [[3]](#footnote-3)；全部答复 [[3]](#footnote-3)；转发 [[3]](#footnote-3)|
|共有者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；复制；查看权限；更改权限；允许宏；另存为、导出；打印；答复 [[3]](#footnote-3)；全部答复 [[3]](#footnote-3)；转发 [[3]](#footnote-3)；完全控制|

----

###### <a name="footnote-1"></a>脚注 1

不包括在标签管理中心或 Azure 门户中。

###### <a name="footnote-2"></a>脚注 2

对于适用于 Windows 的 Azure 信息保护客户端，Office 应用中的信息保护栏需要此权限。

###### <a name="footnote-3"></a>脚注 3
对适用于 Windows 的 Azure 信息保护客户端不适用。

###### <a name="footnote-4"></a>脚注 4
不包括在标签管理中心、Azure 门户或适用于 Windows 的 Azure 信息保护客户端中。

## <a name="rights-included-in-the-default-templates"></a>默认模板中包括的权限
下表列出了创建默认模板时包含的使用权限。 使用权限按各自的[公用名](#usage-rights-and-descriptions)列出。

这些默认模板是在购买订阅时创建的，并且可以在 Azure 门户和[PowerShell](https://docs.microsoft.com/powershell/module/aipservice/set-aipservicetemplateproperty)中[更改](configure-policy-templates.md)名称和使用权限。 

|模板的显示名称|2017 年 10 月 6 日到当前日期的使用权限|2017 年 10 月 6 日之前的使用权限|
|----------------|--------------------|----------|
|\<组织名称> - 机密，仅供查阅 <br /><br />或<br /><br /> *高度机密\所有员工*|查看、打开、读取；复制；查看权限；允许宏；打印；转发；答复；全部 答复；保存；编辑内容、编辑|查看、打开、读取|
|\<组织名称> - 机密 <br /><br />或 <br /><br />*机密\所有员工*|查看、打开、读取；另存为、导出；复制；查看权限；更改权限；允许宏；打印；转发；答复；全部答复；保存；编辑内容、编辑；完全控制|查看、打开、读取；另存为、导出；编辑内容、编辑；查看权限；允许宏；转发；答复；全部答复|

## <a name="do-not-forward-option-for-emails"></a>电子邮件的“不得转发”选项

Exchange 客户端和服务（例如，Outlook 客户端、网页版 Outlook、Exchange 邮件流规则和 Exchange 的 DLP 操作）具有电子邮件的附加信息权限保护选项：“不得转发”。 

尽管**不得转发**看似用户（和 Exchange 管理员）可选择的默认权限管理模板，但此选项并不是模板。 因此在 Azure 门户中查看和管理保护模板时，你看不到此选项。 相反，“不得转发”选项是用户对其电子邮件收件人动态应用的一组使用权限。

当“不要转发”选项应用于一封电子邮件后，此电子邮件会被加密，且收件人必须要进行身份验证。 然后，收件人将无法转发、打印它或从中进行复制。 例如，在 Outlook 客户端中，“转发”按钮将不可用，“另存为”和“打印”菜单选项将不可用，并且无法添加或更改“收件人”、“抄送”或“密件抄送”框中的收件人。

附加到该电子邮件的未受保护 [Office 文档](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)自动继承相同的限制。 应用于这些文档的使用权限是“编辑内容，编辑”、“保存”、“查看，打开，读取”和“允许使用宏”。 如果附件需要不同的使用权限或者你的附件不是支持此继承保护的 Office 文档，请先保护文件，然后再将其附加到电子邮件。 然后，你可以为该文件分配所需的特定使用权限。 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>“不得转发”与不授予使用权限之间的区别

应用“不得转发”选项和应用不授予对电子邮件进行“转发”的使用权限的模板之间有重要区别：“不得转发”选项使用基于原始邮件用户所选收件人的授权用户动态列表；而模板中的权限具有由管理员事先指定的授权用户的静态列表。 区别是什么？ 让我们举个例子： 

某名用户想要通过电子邮件向营销部门的特定人员发送不应与其他任何人共享的信息。 她应该使用将（查看、答复和保存）权限限制于营销部门的模板来保护邮件吗？  还是她应该选择**不得转发**选项？ 这两种选择都将使收件人无法转发电子邮件。 

- 如果她应用模板，收件人仍可与营销部门中的其他人共享该信息。 例如，收件人可使用资源管理器将电子邮件拖放到共享位置或 U 盘。 现在，营销部门中有权访问此位置的任何人（和电子邮件所有者）都可以查看该电子邮件中的信息。
 
- 如果她应用了**不得转发**选项，则收件人将无法通过将电子邮件移动到其他位置来与营销部门中的其他任何人共享信息。 在这种情况下，将只有原始收件人（和电子邮件所有者）能够查看该电子邮件中的信息。

> [!NOTE] 
> 当要求只有发件人选择的收件人才能看到电子邮件中的信息时，请使用**不得转发**。 使用模板，使电子邮件将权限限制于管理员提前指定的、与发件人所选收件人相互独立的一组人员。

## <a name="encrypt-only-option-for-emails"></a>电子邮件的“仅加密”选项

当 Exchange Online 使用 Office 365 邮件加密的新功能后，一个新的电子邮件选项将变为可用：“仅加密”。

此选项可供使用 Exchange Online 的租户使用，可以在网页版 Outlook 中作为邮件流规则的另一个权限保护选项（作为 Office 365 DLP 操作）选择，如果安装了最低版本为 [1804](/officeupdates/monthly-channel-2018#outlook-feature-updates-4) 的 Office 365 专业增强版，且具有[支持 Azure RMS 的 Office 365 应用](requirements-applications.md#windows-computers-for-information-rights-management-irm)的最低版本为 1805 时，还可以从 Outlook 中选择。 有关“仅加密”选项的详细信息，请参阅来自 office 团队的以下博客文章公告：[Office 365 邮件加密中推出“仅加密”](https://aka.ms/omefeb2018)。

选择此选项后，电子邮件会被加密，且收件人必须要进行身份验证。 收件人将具有除“另存为，导出”和“完全控制”以外的所有使用权限。 此使用权限的组合意味着除了无法删除保护外，收件人不会有任何限制。 例如，收件人可以复制、打印和转发此电子邮件。 

同样，默认情况下，附加到电子邮件的未受保护 [Office 文档](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)也会继承相同的权限。 这些文档会自动受到保护，收件人可以在 Office 应用程序中保存、编辑、复制和打印已下载的这些文档。 当收件人保存文档时，可以将其保存为新的名称，甚至保存为不同的格式。 但是，只有支持保护的文件格式才可用，以确保在没有原始保护的情况下无法保存文档。 如果附件需要不同的使用权限或者你的附件不是支持此继承保护的 Office 文档，请先保护文件，然后再将其附加到电子邮件。 然后，你可以为该文件分配所需的特定使用权限。

或者，也可以通过使用 [Exchange Online PowerShell](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell?view=exchange-ps) 指定 `Set-IRMConfiguration -DecryptAttachmentForEncryptOnly $true` 来更改文档的此保护继承。 如果无需在用户通过身份验证后保留文档的原始保护，请使用这种配置。 当收件人打开电子邮件时，文档将不受保护。

如果确实需要附加的文档以保留原始保护，请参阅[使用 Azure 信息保护来保护文档协作](secure-collaboration-documents.md)。

注意:如果看到了对 DecryptAttachmentFromPortal 的引用，请注意对于 [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration?view=exchange-ps)现已弃用此参数。 除非之前设置了此参数，否则它不可用。

## <a name="automatically-encrypt-pdf-documents-with-exchange-online"></a>通过 Exchange Online 自动加密 PDF 文档

当 Exchange Online 使用 Office 365 邮件加密的新功能时，如果将未受保护的 PDF 文档附加到加密电子邮件，则可以自动对其进行加密。 该文档继承了电子邮件的相同权限。 若要启用此配置，请使用[set-irmconfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration?view=exchange-ps)设置**EnablePdfEncryption $True** 。

如果收件人没有安装支持 PDF 加密 ISO 标准的读取器，则可以安装 Pdf 读取器中列出的一个[支持 Microsoft 信息保护](./rms-client/protected-pdf-readers.md)的读取器。 或者，收件人可以阅读 OME 门户中受保护的 PDF 文档。

## <a name="rights-management-issuer-and-rights-management-owner"></a>权限管理颁发者和权限管理所有者

使用 Azure 权限管理服务保护文档或电子邮件时，保护该内容的帐户自动成为该内容的权限管理颁发者。 在[使用情况日志](log-analyze-usage.md#how-to-interpret-your-usage-logs)中，此帐户记录为“颁发者”字段。 

始终向权限管理颁发者授予文档或电子邮件的“完全控制”使用权，此外：

- 如果保护设置中包括过期日期，该日期到期后，权限管理颁发者仍然可以打开和编辑文档或电子邮件。

- 权限管理颁发者可始终脱机访问文档或电子邮件。

- 撤消权限后，权限管理颁发者仍可打开文档。 

默认情况下，此帐户也是该内容的“权限管理所有者”，当创建文档或电子邮件的用户启动保护时便是如此。 但是，某些情况下，管理员或服务可以代表用户保护内容。 例如：

- 管理员批量保护文件共享上的文件：Azure AD 中的管理员帐户保护用户的文档。

- Rights Management 连接器保护 Windows Server 文件夹上的 Office 文档：Azure AD 中为 RMS 连接器创建的服务主体帐户可以保护用户的文档。

在这些情况下，权限管理颁发者可使用 Azure 信息保护 SDK 或 PowerShell 将权限管理所有者分配给另一个帐户。 例如，将 [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) PowerShell cmdlet 与 Azure 信息保护客户端配合使用时，可以指定 OwnerEmail参数将权限管理所有者分配给另一个帐户。 

如果权利管理颁发者代表用户提供保护，分配权限管理所有者可确保原始文档或电子邮件所有者对其受保护内容拥有同一级别的控制，就如同由其自己启动保护一样。 

例如，即使文档现在受不含打印使用权限的模板的保护，创建该文档的用户仍可打印文档。 同一用户始终可访问其文档，而无需考虑离线访问设置或可能在该模板中配置的到期日期。 此外，由于 Rights Management 所有者具有完全控制使用权限，因此该用户还可以重新保护文档以向更多用户授予访问权限（此时该用户成为 Rights Management 颁发者以及 Rights Management 所有者），甚至可以删除保护。 但是，只有权限管理颁发者可跟踪和撤销文档。

在[使用情况日志](log-analyze-usage.md#how-to-interpret-your-usage-logs)中，文档或电子邮件的权限管理所有者记录为“所有者-电子邮件”字段。

请注意，权限管理所有者独立于 Windows 文件系统所有者。 两者通常是相同的，但也可以不同，即使不使用 SDK 或 PowerShell 也是如此。

## <a name="rights-management-use-license"></a>Rights Management 使用许可证

用户打开已受 Azure Rights Management 保护的文档或电子邮件时，会向该用户授予 Rights Management 使用许可证。 此使用许可证是一个证书，它包含用户对文档或电子邮件的使用权限，以及用于加密内容的加密密钥。 此使用许可证还包含一个到期日期（如果已设置）及其有效时长。

除了权限帐户证书 (RAC)，用户还必须具有一个有效的使用许可证才能打开内容，这是在[初始化用户环境](how-does-it-work.md#initializing-the-user-environment)时授予的证书，然后每隔 31 天续订一次。

使用许可证有效期内，无需对用户重新进行身份验证或重新授权即可获取内容。 这样，用户就可以在没有 internet 连接的情况下继续打开受保护的文档或电子邮件。 使用许可证有效期到期后，用户下次访问受保护的文档或电子邮件时就必须重新进行身份验证并重新进行授权。 

如果文档和电子邮件是通过标签或定义保护设置的模板进行保护，可更改标签或模板中的这些设置，而无需重新保护内容。 如果用户已访问过内容，则所做的更改将在他们的使用许可证过期后生效。 但如果用户应用了自定义权限（也称为临时权限策略），且这些权限需要在保护文档或电子邮件后更改，则必须使用新权限再次保护该内容。 通过“不转发”选项实现电子邮件的自定义权限。

租户的默认使用许可证有效期为30天，你可以使用 PowerShell cmdlet [AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)来配置此值。 可使用标签或模板，为何时应用保护配置限制性更强的设置：

- 在 Azure 门户中配置标签或模板时，使用许可证有效期从“允许脱机访问设置”取得其值。 
    
    有关在 Azure 门户中配置此设置的详细信息和指导，请参阅如何为 Rights Management 保护配置标签的说明中的[保护设置相关信息](configure-policy-protection.md#information-about-the-protection-settings)表。

- 使用 PowerShell 配置模板时，使用许可证有效期从[AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)和[AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate) cmdlet 中的*LicenseValidityDuration*参数获取其值。
    
    有关使用 PowerShell 配置此设置的详细信息和指南，请参阅每个 cmdlet 的帮助。

## <a name="see-also"></a>另请参阅
[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)

[为 Azure 信息保护和发现服务或数据恢复配置超级用户](configure-super-users.md)
