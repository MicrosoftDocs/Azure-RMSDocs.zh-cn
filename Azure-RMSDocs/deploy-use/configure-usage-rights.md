---
title: 为 Azure Rights Management 配置使用权限 - AIP
description: 了解和确定在使用 Azure 信息保护中的 Azure 权限管理服务保护文件或电子邮件时使用的特定权限。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f632acdb4091967b0d8f5aebab97464d69b0b2e3
ms.sourcegitcommit: 752368caff1bf5bff64a5d262e7bc4105d906827
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2018
ms.locfileid: "39270601"
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>为 Azure Rights Management 配置使用权限

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

在文件或电子邮件上使用 Azure 信息保护中的 Azure 权限管理服务设置保护并且不使用模板时，必须自行配置使用权限。 此外，在为 Azure 权限管理保护配置模板或标签时，可以选择随后在用户、管理员或配置的服务选择模板或标签时会自动应用的使用权限。 例如，在 Azure 门户中，可以选择配置使用权限逻辑分组的角色，或者可以配置单个权限。

使用本文章可帮助为当前使用的应用程序配置所需的使用权限，并了解应用程序如何解释这些权限。

> [!NOTE] 
> 为保持完整性，本文包括已在 2018 年 1 月 8 日停用的 Azure 经典门户中的值。
>
> 为帮助用户迁移到新的门户，可参阅[曾使用 Azure 经典门户执行的任务](migrate-portal.md)。

## <a name="usage-rights-and-descriptions"></a>使用权限和说明
下表列出并说明了 Rights Management 支持的使用权限，以及它们的使用和解释方式。 它们按公用名列出，公用名通常是你看待使用权限作为在代码中使用的单字值（策略中的编码值）的更友好版本进行显示或引用的方式。 

**API 常量或值**是 MSIPC API 调用的 SDK 名称，在你编写检查使用权限的启用 RMS 的应用程序，或向策略添加使用权限时使用。


|使用权限|描述|实现|
|-------------------------------|---------------------------|-----------------|
|公用名：**编辑内容，编辑** <br /><br />策略中的编码：**DOCEDIT**|允许用户对应用程序中的内容进行修改、重新排列、设置格式或排序。 它不会授权保存编辑过的副本。<br /><br />在 Word 中，除非 Office 365 专业增强版的最低版本为 1807（最低生成号为 10325.20000），否则此权限不足，无法启用或禁用“跟踪更改”，也无法以审阅者身份使用所有跟踪更改功能。 必须拥有“完全控制”权限，才能使用所有跟踪更改选项。 |Office 自定义权限：作为“更改”和“完全控制”选项的一部分。 <br /><br />Azure 经典门户中的名称：**编辑内容**<br /><br />Azure 门户中的名称：**编辑内容、编辑(DOCEDIT)**<br /><br />AD RMS 模板中的名称：**编辑** <br /><br />API 常量或值：不适用。|
|公用名：**保存** <br /><br />策略中的编码：**EDIT**|允许用户将文档保存到当前位置。<br /><br />在 Office 应用程序中，如果所选文件格式以本机方式支持 Rights Management 保护，则此权限还允许用户修改文档并以新名称将其保存到新位置。 文件格式限制可确保无法从文件中删除原始保护。|Office 自定义权限：作为“更改”和“完全控制”选项的一部分。 <br /><br />Azure 经典门户中的名称：**保存文件**<br /><br />Azure 门户中的名称：**保存(EDIT)**<br /><br />AD RMS 模板中的名称：**保存** <br /><br />API 常量或值：`IPC_GENERIC_WRITE L"EDIT"`|
|公用名：**注释** <br /><br />策略中的编码：**COMMENT**|启用向内容添加批注或注释的选项。<br /><br />此权限可用于 SDK、在 AzureInformationProtection 和适用于 Windows PowerShell 的 RMS 保护模块中作为即席策略提供，并且已在一些软件供应商应用程序中实现。 但是，它尚未广泛使用，并且当前也不受 Office 应用程序支持。|Office 自定义权限：未实现。 <br /><br />Azure 经典门户中的名称：未实现。<br /><br />Azure 门户中的名称：未实现。<br /><br />AD RMS 模板中的名称：未实现。 <br /><br />API 常量或值：`IPC_GENERIC_COMMENT L"COMMENT`|
|公用名：**另存为，导出** <br /><br />策略中的编码：**EXPORT**|启用将内容保存到其他文件名的选项（另存为）。 <br /><br />对于 Office 文档和 Azure 信息保护客户端，文件可在不受保护的情况下进行保存，也可使用新设置和权限重新保护。 这些允许的操作意味着，具有此权限的用户可以从受保护的文档或电子邮件对 Azure 信息保护标签进行更改或删除。 <br /><br />此权限还允许用户在应用程序中执行其他导出选项，如“发送至 OneNote” 。<br /><br /> 注意：如果未授予此权限，并且所选的文件格式以本机方式支持 Rights Management 保护，则 Office 应用程序允许用户将文档另存为一个新的名称。|Office 自定义权限：作为“更改”和“完全控制”选项的一部分。 <br /><br />Azure 经典门户中的名称：**导出内容(另存为)** <br /><br />Azure 门户中的名称：**另存为、导出(EXPORT)**<br /><br />AD RMS 模板中的名称：**导出(另存为)** <br /><br />API 常量或值：`IPC_GENERIC_EXPORT L"EXPORT"`|
|公用名：**转发** <br /><br />策略中的编码：**FORWARD**|启用此选项以转发电子邮件，并将收件人添加到“收件人”  和“抄送”  行。 此权限不适用于文档；仅适用于电子邮件。<br /><br />不允许转发器授予其他用户权限作为转发操作的一部分。 <br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），以确保原始电子邮件包含在转发的电子邮件中，且不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要此权限。 或者，对于组织内无需使用 Azure Rights Management 服务的用户来说，也需要此权限，因为你已实施了[载入控件](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)。|Office 自定义权限：使用“不要转发”标准策略时拒绝。<br /><br />Azure 经典门户中的名称：**转发**<br /><br />Azure 门户中的名称：**转发(FORWARD)**<br /><br />AD RMS 模板中的名称：**转发** <br /><br />API 常量或值：`IPC_EMAIL_FORWARD L"FORWARD"`|
|公用名：**完全控制** <br /><br />策略中的编码：**OWNER**|授予对文档的所有权限，并且所有可用操作都可以执行。<br /><br />包括删除保护和重新保护文档的功能。 <br /><br />请注意，此使用权限不等同于[权限管理所有者](#rights-management-issuer-and-rights-management-owner)。|Office 自定义权限：作为“完全控制”自定义选项。<br /><br />Azure 经典门户中的名称：**完全控制**<br /><br />Azure 门户中的名称：**完全控制(OWNER)**<br /><br />AD RMS 模板中的名称：**完全控制** <br /><br />API 常量或值：`IPC_GENERIC_ALL L"OWNER"`|
|公用名：**打印** <br /><br />策略中的编码：**PRINT**|启用打印内容的选项。|Office 自定义权限：作为自定义权限中的“打印内容”选项。 不是特定于收件人的设置。<br /><br />Azure 经典门户中的名称：**打印**<br /><br />Azure 门户中的名称：**打印(PRINT)**<br /><br />AD RMS 模板中的名称：**打印** <br /><br />API 常量或值：`IPC_GENERIC_PRINT L"PRINT"`|
|公用名：**答复** <br /><br />策略中的编码：**REPLY**|启用邮件客户端中的“答复”选项，但不允许更改“收件人”或“抄送”行。<br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），以确保原始电子邮件包含在转发的电子邮件中，且不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要此权限。 或者，对于组织内无需使用 Azure Rights Management 服务的用户来说，也需要此权限，因为你已实施了[载入控件](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)。|Office 自定义权限：不适用。<br /><br />Azure 经典门户中的名称：**答复**<br /><br />Azure 经典门户中的名称：**答复(REPLY)**<br /><br />AD RMS 模板中的名称：**答复** <br /><br />API 常量或值：`IPC_EMAIL_REPLY`|
|公用名：**全部答复** <br /><br />策略中的编码：**REPLYALL**|启用邮件客户端中的“全部答复”  选项，但不允许用户将收件人添加到“收件人”  或“抄送”  行。<br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），以确保原始电子邮件包含在转发的电子邮件中，且不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要此权限。 或者，对于组织内无需使用 Azure Rights Management 服务的用户来说，也需要此权限，因为你已实施了[载入控件](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)。|Office 自定义权限：不适用。<br /><br />Azure 经典门户中的名称：**全部答复**<br /><br />Azure 门户中的名称：**全部答复(REPLY ALL)**<br /><br />AD RMS 模板中的名称：**全部答复** <br /><br />API 常量或值：`IPC_EMAIL_REPLYALL L"REPLYALL"`|
|公用名：**查看，打开，读取** <br /><br />策略中的编码：**VIEW**|允许用户打开文档，并查看内容。<br /><br /> 在 Excel 中，此权限不足，无法对数据进行排序。必须拥有“编辑内容、编辑”权限，才能执行此操作。 必须拥有“编辑内容、编辑”和“复制”这两项权限，才能在 Excel 中筛选数据。|Office 自定义权限：作为“读取”自定义策略的“查看”选项。<br /><br />Azure 经典门户中的名称：**查看**<br /><br />Azure 门户中的名称：**查看、打开、读取(VIEW)**<br /><br />AD RMS 模板中的名称：读取 <br /><br />API 常量或值：`IPC_GENERIC_READ L"VIEW"`|
|公用名：**复制** <br /><br />策略中的编码：**EXTRACT**|启用将数据（包括屏幕捕获）从文档复制到同一文档或其他文档的选项。<br /><br />在某些应用程序中，它还允许以不受保护的形式保存整个文档。<br /><br />在 Skype for Business 和类似屏幕共享应用程序中，演示者必须拥有此权限，才能成功展示受保护文档。 如果演示者没有此权限，与会者便无法查看文档，且文档显示为对与会者禁用。|Office 自定义权限：作为“允许具有读取权限的用户复制内容”自定义策略选项。<br /><br />Azure 经典门户中的名称：**复制并提取内容**<br /><br />Azure 门户中的名称：**复制(EXTRACT)**<br /><br />AD RMS 模板中的名称：**提取** <br /><br />API 常量或值：`IPC_GENERIC_EXTRACT L"EXTRACT"`|
|公用名：**查看权限** <br /><br />策略中的编码：**VIEWRIGHTSDATA**|允许用户查看应用于文档的策略。|Office 自定义权限：未实现。<br /><br />Azure 经典门户中的名称：**查看分配的权限**<br /><br />Azure 门户中的名称：**查看权限(VIEWRIGHTSDATA)**。<br /><br />AD RMS 模板中的名称：**查看权限** <br /><br />API 常量或值：`IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|公用名：**更改权限** <br /><br />策略中的编码：**EDITRIGHTSDATA**|允许用户更改应用于文档的策略。 包括删除的保护。|Office 自定义权限：未实现。<br /><br />Azure 经典门户中的名称：**更改权限**<br /><br />Azure 门户中的名称：**编辑权限(EDITRIGHTSDATA)**。<br /><br />AD RMS 模板中的名称：**编辑权限** <br /><br />API 常量或值：`PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|公用名：**允许宏** <br /><br />策略中的编码：**OBJMODEL**|启用运行宏或执行其他编程或远程访问文档内容的选项。|Office 自定义权限：作为“允许编程访问”自定义策略选项。 不是特定于收件人的设置。<br /><br />Azure 经典门户中的名称：**允许宏**<br /><br />Azure 门户中的名称：**允许宏(OBJMODEL)**<br /><br />AD RMS 模板中的名称：**允许宏** <br /><br />API 常量或值：未实现。|

## <a name="rights-included-in-permissions-levels"></a>权限级别中包括的权限

某些应用程序会将使用权限组合成不同的权限级别，这样可以更容易地选择那些通常在一起使用的使用权限。 这些权限级别可帮助减少用户操作的复杂性，用户只需按角色选择相应选项即可。  例如，**审阅者**和**合著者**。 虽然这些选项通常会向用户显示这些权限的摘要，但可能并不包括前一表中列出的每个权限。

可通过下表查看这些权限级别的列表，以及这些权限级别所含使用权限的完整列表。 使用权限按各自的[公用名](#usage-rights-and-descriptions)列出。

|权限级别|应用程序|包含的使用权限|
|---------------------|----------------|---------------------------------|
|查看器|Azure 经典门户 <br /><br />Azure 门户<br /><br /> 适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；查看权限；答复 [[1]](#footnote-1)；全部答复 [[1]](#footnote-1)；允许宏 [[2]](#footnote-2)<br /><br />注意：对于电子邮件，请使用审阅者级别而不是此权限级别，确保接收到的电子邮件答复为电子邮件而不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要审阅者权限。 或者，对于组织内无需使用 Azure Rights Management 服务的用户来说，也需要此权限，因为你已实施了[载入控件](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)。|
|审阅者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；查看权限；答复：全部答复 [[3]](#footnote-3)；转发 [[3]](#footnote-3)；允许宏 [[2]](#footnote-2)|
|合著者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；复制；查看权限；允许宏；另存为、导出 [[4]](#footnote-4)；打印；答复 [[3]](#footnote-3)；全部答复 [[3]](#footnote-3)；转发 [[3]](#footnote-3)|
|共有者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；复制；查看权限；更改权限；允许宏；另存为、导出；打印；答复 [[3]](#footnote-3)；全部答复 [[3]](#footnote-3)；转发 [[3]](#footnote-3)；完全控制|

----

###### <a name="footnote-1"></a>脚注 1

未包括在 Azure 门户中。

###### <a name="footnote-2"></a>脚注 2

对于适用于 Windows 的 Azure 信息保护客户端，目前 Office 应用程序中的信息保护栏需要此权限。

###### <a name="footnote-3"></a>脚注 3
不适用项：适用于 Windows 的 Azure 信息保护客户端或适用于 Windows 的 Rights Management 共享应用程序。

###### <a name="footnote-4"></a>脚注 4
不包括在 Azure 门户或适用于 Windows 的 Azure 信息保护客户端中。

## <a name="rights-included-in-the-default-templates"></a>默认模板中包括的权限
下表列出了创建默认模板时包含的使用权限。 使用权限按各自的[公用名](#usage-rights-and-descriptions)列出。

这些默认模板在购买订阅时进行创建，并且名称和使用权限可在 Azure 门户中[更改](configure-policy-templates.md)。 

|模板的显示名称|2017 年 10 月 6 日到当前日期的使用权限|2017 年 10 月 6 日之前的使用权限|
|----------------|--------------------|----------|
|\<组织名称> - 机密，仅供查阅 <br /><br />或<br /><br /> *高度机密\所有员工*|查看、打开、读取；复制；查看权限；允许宏；打印；转发；答复；全部 答复；保存；编辑内容、编辑|查看、打开、读取|
|\<组织名称> - 机密 <br /><br />或 <br /><br />*机密\所有员工*|查看、打开、读取；另存为、导出；复制；查看权限；更改权限；允许宏；打印；转发；答复；全部答复；保存；编辑内容、编辑；完全控制|查看、打开、读取；另存为、导出；编辑内容、编辑；查看权限；允许宏；转发；答复；全部答复|

## <a name="do-not-forward-option-for-emails"></a>电子邮件的“不得转发”选项

Exchange 客户端和服务（例如 Outlook 客户端、Outlook Web Access 应用和 Exchange 邮件流规则）有一个针对电子邮件的附加信息权限保护选项：“不得转发”。 

尽管**不得转发**看似用户（和 Exchange 管理员）可选择的默认权限管理模板，但此选项并不是模板。 因此在 Azure 门户中查看和管理保护模板时，你看不到此选项。 相反，“不得转发”选项是用户对其电子邮件收件人动态应用的一组使用权限。

当“不要转发”选项应用于一封电子邮件后，此电子邮件会被加密，且收件人必须要进行身份验证。 收件人无法转发、打印或从此电子邮件中进行复制，也无法保存附件或另存为其他名称。 例如，在 Outlook 客户端中，“转发”按钮和“另存为”、“保存附件”和“打印”菜单选项将不可用，并且无法添加或更改“收件人”、“抄送”或“密件抄送”框中的收件人。

附加到该电子邮件的未受保护 [Office 文档](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)自动继承相同的限制。 应用于这些文档的使用权限是“编辑内容，编辑”、“保存”、“查看，打开，读取”和“允许使用宏”。 如果附件需要不同的使用权限或者你的附件不是支持此继承保护的 Office 文档，请先保护文件，然后再将其附加到电子邮件。 然后，你可以为该文件分配所需的特定使用权限。 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>“不得转发”与不授予使用权限之间的区别

应用“不得转发”选项和应用不授予电子邮件“转发”权限的模板有重要区别：“不得转发”选项使用基于原始电子邮件用户所选收件人的授权用户动态列表；而模板中的权限使用由管理员事先指定的授权用户静态列表。 区别是什么？ 让我们举个例子： 

某名用户想要通过电子邮件向营销部门的特定人员发送不应与其他任何人共享的信息。 她应该使用将（查看、答复和保存）权限限制于营销部门的模板来保护邮件吗？  还是她应该选择**不得转发**选项？ 这两种选择都将使收件人无法转发电子邮件。 

- 如果她应用模板，收件人仍可与营销部门中的其他人共享该信息。 例如，收件人可使用资源管理器将电子邮件拖放到共享位置或 U 盘。 现在，营销部门中有权访问此位置的任何人（和电子邮件所有者）都可以查看该电子邮件中的信息。
 
- 如果她应用了**不得转发**选项，则收件人将无法通过将电子邮件移动到其他位置来与营销部门中的其他任何人共享信息。 在这种情况下，将只有原始收件人（和电子邮件所有者）能够查看该电子邮件中的信息。

> [!NOTE] 
> 当要求只有发件人选择的收件人才能看到电子邮件中的信息时，请使用**不得转发**。 使用模板，使电子邮件将权限限制于管理员提前指定的、与发件人所选收件人相互独立的一组人员。

## <a name="encrypt-only-option-for-emails"></a>电子邮件的“仅加密”选项

当 Exchange Online 使用 Office 365 邮件加密的新功能后，一项新的电子邮件选项将变为可用：“仅加密”。

此选项会被部署到使用 Exchange Online 的租户，最初只适用于 Outlook 网页版，以及作为适用于邮件流规则的一个权限保护选项。 有关详细信息，请参阅来自 office 团队的下列博客文章公告：[Office 365 邮件加密即将推出“仅加密”](https://aka.ms/omefeb2018)。

选择此选项后，电子邮件会被加密，且收件人必须要进行身份验证。 收件人将具有除“另存为，导出”和“完全控制”以外的所有使用权限。 此使用权限的组合意味着除了无法删除保护外，收件人不会有任何限制。 例如，收件人可以复制、打印和转发此电子邮件。 

同样，默认情况下，附加到电子邮件的未受保护 [Office 文档](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)也会继承相同的权限。 这些文档会自动受到保护，收件人可以在 Office 应用程序中保存、编辑、复制和打印已下载的这些文档。 当收件人保存文档时，可以将其保存为新的名称，甚至保存为不同的格式。 但是，只有支持保护的文件格式才可用，以确保在没有原始保护的情况下无法保存文档。 如果附件需要不同的使用权限或者你的附件不是支持此继承保护的 Office 文档，请先保护文件，然后再将其附加到电子邮件。 然后，你可以为该文件分配所需的特定使用权限。

也可以对在浏览器中查看文档的收件人更改文档的这种加密继承。 如果无需在用户通过身份验证后保留文档的原始保护，建议使用这种配置。 若要执行此更改，请运行 Exchange Online PowerShell 命令 `Set-IRMConfiguration -DecryptAttachmentFromPortal $true`。 然后，保护设置会在这些收件人下载文档后遭删除。 有关详细信息，请参阅 Office 博客文章 [Office 365 邮件加密中现在提供的附件管理控制](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Admin-control-for-attachments-now-available-in-Office-365/ba-p/204007)。 如果确实需要在下载文档后保留原始保护，请参阅[使用 Azure 信息保护来保护文档协作](../get-started/secure-collaboration-documents.md)。      

## <a name="rights-management-issuer-and-rights-management-owner"></a>权限管理颁发者和权限管理所有者

使用 Azure 权限管理服务保护文档或电子邮件时，保护该内容的帐户自动成为该内容的权限管理颁发者。 在[使用情况日志](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs)中，此帐户记录为“颁发者”字段。 

始终向权限管理颁发者授予文档或电子邮件的“完全控制”使用权，此外：

- 如果保护设置中包括过期日期，该日期到期后，权限管理颁发者仍然可以打开和编辑文档或电子邮件。

- 权限管理颁发者可始终脱机访问文档或电子邮件。

- 撤消权限后，权限管理颁发者仍可打开文档。 

默认情况下，此帐户也是该内容的“权限管理所有者”，当创建文档或电子邮件的用户启动保护时便是如此。 但是，某些情况下，管理员或服务可以代表用户保护内容。 例如：

- 管理员批量保护文件共享上的文件：Azure AD 中的管理员帐户保护用户文档。

- 权限管理连接器保护 Windows Server 文件夹上的 Office 文档：Azure AD 中为 RMS 连接器创建的服务主体帐户保护用户文档。

在这些情况下，权限管理颁发者可使用 Azure 信息保护 SDK 或 PowerShell 将权限管理所有者分配给另一个帐户。 例如，将 [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) PowerShell cmdlet 与 Azure 信息保护客户端配合使用时，可以指定 OwnerEmail 参数将权限管理所有者分配给另一个帐户。 

如果权利管理颁发者代表用户提供保护，分配权限管理所有者可确保原始文档或电子邮件所有者对其受保护内容拥有同一级别的控制，就如同由其自己启动保护一样。 

例如，即使文档现在受不含打印使用权限的模板的保护，创建该文档的用户仍可打印文档。 同一用户始终可访问其文档，而无需考虑离线访问设置或可能在该模板中配置的到期日期。 此外，由于 Rights Management 所有者具有完全控制使用权限，因此该用户还可以重新保护文档以向更多用户授予访问权限（此时该用户成为 Rights Management 颁发者以及 Rights Management 所有者），甚至可以删除保护。 但是，只有权限管理颁发者可跟踪和撤销文档。

在[使用情况日志](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs)中，文档或电子邮件的权限管理所有者记录为“所有者-电子邮件”字段。

请注意，权限管理所有者独立于 Windows 文件系统所有者。 两者通常是相同的，但也可以不同，即使不使用 SDK 或 PowerShell 也是如此。

## <a name="rights-management-use-license"></a>Rights Management 使用许可证

用户打开已受 Azure Rights Management 保护的文档或电子邮件时，会向该用户授予 Rights Management 使用许可证。 此使用许可证是一个证书，它包含用户对文档或电子邮件的使用权限，以及用于加密内容的加密密钥。 此使用许可证还包含一个到期日期（如果已设置）及其有效时长。

除了权限帐户证书 (RAC)，用户还必须具有一个有效的使用许可证才能打开内容，这是在[初始化用户环境](../understand-explore/how-does-it-work.md#initializing-the-user-environment)时授予的证书，然后每隔 31 天续订一次。

使用许可证有效期内，无需对用户重新进行身份验证或重新授权即可获取内容。 这样即使没有 Internet 连接，用户也能够打开受保护的文档或电子邮件。 使用许可证有效期到期后，用户下次访问受保护的文档或电子邮件时就必须重新进行身份验证并重新进行授权。 

如果文档和电子邮件是通过标签或定义保护设置的模板进行保护，可更改标签或模板中的这些设置，而无需重新保护内容。 如果用户已访问过内容，则所做的更改将在他们的使用许可证过期后生效。 但如果用户应用了自定义权限（也称为临时权限策略），且这些权限需要在保护文档或电子邮件后更改，则必须使用新权限再次保护该内容。 通过“不转发”选项实现电子邮件的自定义权限。

租户使用许可证的默认有效期为 30 天，可使用 PowerShell cmdlet [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime) 配置该值。 可使用标签或模板，为何时应用保护配置限制性更强的设置：

- 在 Azure 门户中配置标签或模板时，使用许可证有效期从“允许脱机访问设置”取得其值。 
    
    有关在 Azure 门户中配置此设置的详细信息和指导，请参阅如何为 Rights Management 保护配置标签的说明中的[保护设置相关信息](../deploy-use/configure-policy-protection.md#information-about-the-protection-settings)表。

- 使用 PowerShell 配置模板时，使用许可证有效期从 [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) 和 [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate) cmdlet 中的 LicenseValidityDuration 参数中取得其值。
    
    有关使用 PowerShell 配置此设置的详细信息和指南，请参阅每个 cmdlet 的帮助。

## <a name="see-also"></a>另请参阅
[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)

[为 Azure 权限管理和发现服务或数据恢复配置超级用户](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

