---
title: "为 Azure Rights Management 配置使用权限 - AIP"
description: "了解和确定在使用 Azure 信息保护中的 Azure 权限管理服务保护文件或电子邮件时使用的特定权限。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ed06deca76ed1241f0c9b3f104fd922263c5a6cd
ms.sourcegitcommit: dd5a63bfee309c8b68ee9f8cd071a574ab0f6b4a
ms.translationtype: HT
ms.contentlocale: zh-CN
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>为 Azure Rights Management 配置使用权限

>*适用于：Azure 信息保护、Office 365*

在文件或电子邮件上使用 Azure 信息保护中的 Azure 权限管理服务设置保护并且不使用模板时，必须自行配置使用权限。 此外，在为 Azure 权限管理配置自定义模板时，可以选择随后在用户、管理员或配置的服务选择模板时会自动应用的使用权限。 例如，在 Azure 经典门户中，可以选择配置使用权限逻辑分组的角色，也可以配置单个权限。

使用本文章可帮助为当前使用的应用程序配置所需的使用权限，并了解应用程序如何解释这些权限。

## <a name="usage-rights-and-descriptions"></a>使用权限和说明
下表列出并说明了 Rights Management 支持的使用权限，以及它们的使用和解释方式。 它们按**公用名**列出，公用名通常是你看待使用权限作为在代码中使用的单字值（**策略中的编码**值）的更友好版本进行显示或引用的方式。 

**API 常量或值**是 MSIPC API 调用的 SDK 名称，在你编写检查使用权限的启用 RMS 的应用程序，或向策略添加使用权限时使用。


|Right|说明|实现|
|-------------------------------|---------------------------|-----------------|
|公用名：**编辑内容，编辑** <br /><br />策略中的编码：**DOCEDIT**|允许用户对应用程序中的内容进行修改、重新排列、设置格式或筛选。 它不会授权保存编辑过的副本。|Office 自定义权限：作为“更改”和“完全控制”选项的一部分。 <br /><br />Azure 经典门户中的名称：**编辑内容**<br /><br />Azure 门户中的名称：包含在“编辑和保存”中<br /><br />AD RMS 模板中的名称：**编辑** <br /><br />API 常量或值：不适用。|
|公用名：**保存** <br /><br />策略中的编码：**EDIT**|允许用户将文档保存到当前位置。<br /><br />在 Office 应用程序中，此权限还允许用户修改文档。|Office 自定义权限：作为“更改”和“完全控制”选项的一部分。 <br /><br />Azure 经典门户中的名称：**保存文件**<br /><br />Azure 门户中的名称：包含在“编辑和保存”中<br /><br />AD RMS 模板中的名称：**保存** <br /><br />API 常量或值：`IPC_GENERIC_WRITE L"EDIT"`|
|公用名：**注释** <br /><br />策略中的编码：**COMMENT**|启用向内容添加批注或注释的选项。<br /><br />此权限可用于 SDK、在 AzureInformationProtection 和适用于 Windows PowerShell 的 RMS 保护模块中作为即席策略提供，并且已在一些软件供应商应用程序中实现。 但是，它尚未广泛使用，并且当前也不受 Office 应用程序支持。|Office 自定义权限：未实现。 <br /><br />Azure 经典门户中的名称：未实现。<br /><br />Azure 门户中的名称：未实现。<br /><br />AD RMS 模板中的名称：未实现。 <br /><br />API 常量或值：`IPC_GENERIC_COMMENT L"COMMENT`|
|公用名：**另存为，导出** <br /><br />策略中的编码：**EXPORT**|启用将内容保存到其他文件名的选项（另存为）。 对于 Office 文档和 Azure 信息保护客户端，该文件可在不受保护的情况下进行保存。<br /><br />此权限还允许用户在应用程序中执行其他导出选项，如“发送至 OneNote” 。<br /><br /> 注意：如果未授予此权限，并且所选的文件格式以本机方式支持 Rights Management 保护，则 Office 应用程序允许用户将文档另存为一个新的名称。|Office 自定义权限：作为“更改”和“完全控制”选项的一部分。 <br /><br />Azure 经典门户中的名称：**导出内容(另存为)** <br /><br />Azure 门户中的名称：包含在“完全控制”中<br /><br />AD RMS 模板中的名称：**导出(另存为)** <br /><br />API 常量或值：`IPC_GENERIC_EXPORT L"EXPORT"`|
|公用名：**转发** <br /><br />策略中的编码：**FORWARD**|启用此选项以转发电子邮件，并将收件人添加到“收件人”  和“抄送”  行。 此权限不适用于文档；仅适用于电子邮件。<br /><br />不允许转发器授予其他用户权限作为转发操作的一部分。 <br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），以确保原始电子邮件包含在转发的电子邮件中，且不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要此权限。|Office 自定义权限：使用“不要转发”标准策略时拒绝。<br /><br />Azure 经典门户中的名称：**转发**<br /><br />Azure 门户中的名称：“转发”<br /><br />AD RMS 模板中的名称：**转发** <br /><br />API 常量或值：`IPC_EMAIL_FORWARD L"FORWARD"`|
|公用名：**完全控制** <br /><br />策略中的编码：**OWNER**|授予对文档的所有权限，并且所有可用操作都可以执行。<br /><br />包括删除保护和重新保护文档的功能。 <br /><br />请注意，此使用权限不等同于[权限管理所有者](#rights-management-issuer-and-rights-management-owner)。|Office 自定义权限：作为“完全控制”自定义选项。<br /><br />Azure 经典门户中的名称：**完全控制**<br /><br />Azure 门户中的名称：“完全控制”<br /><br />AD RMS 模板中的名称：**完全控制** <br /><br />API 常量或值：`IPC_GENERIC_ALL L"OWNER"`|
|公用名：**打印** <br /><br />策略中的编码：**PRINT**|启用打印内容的选项。|Office 自定义权限：作为自定义权限中的“打印内容”选项。 不是特定于收件人的设置。<br /><br />Azure 经典门户中的名称：**打印**<br /><br />Azure 门户中的名称：“打印”<br /><br />AD RMS 模板中的名称：**打印** <br /><br />API 常量或值：`IPC_GENERIC_PRINT L"PRINT"`|
|公用名：**答复** <br /><br />策略中的编码：**REPLY**|启用邮件客户端中的“答复”选项，但不允许更改“收件人”或“抄送”行。<br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），以确保原始电子邮件包含在转发的电子邮件中，且不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要此权限。|Office 自定义权限：不适用。<br /><br />Azure 经典门户中的名称：**答复**<br /><br />AD RMS 模板中的名称：**答复** <br /><br />API 常量或值：`IPC_EMAIL_REPLY`|
|公用名：**全部答复** <br /><br />策略中的编码：**REPLYALL**|启用邮件客户端中的“全部答复”  选项，但不允许用户将收件人添加到“收件人”  或“抄送”  行。<br /><br />授予此权限时，同时授予“编辑内容，编辑”权限（通用名称），以确保原始电子邮件包含在转发的电子邮件中，且不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要此权限。|Office 自定义权限：不适用。<br /><br />Azure 经典门户中的名称：**全部答复**<br /><br />Azure 门户中的名称：“全部答复”<br /><br />AD RMS 模板中的名称：**全部答复** <br /><br />API 常量或值：`IPC_EMAIL_REPLYALL L"REPLYALL"`|
|公用名：**查看，打开，读取** <br /><br />策略中的编码：**VIEW**|允许用户打开文档，并查看内容。|Office 自定义权限：作为“读取”自定义策略的“查看”选项。<br /><br />Azure 经典门户中的名称：**查看**<br /><br />Azure 门户中的名称：“查看内容”<br /><br />AD RMS 模板中的名称：**全部答复** <br /><br />API 常量或值：`IPC_GENERIC_READ L"VIEW"`|
|公用名：**复制** <br /><br />策略中的编码：**EXTRACT**|启用将数据（包括屏幕捕获）从文档复制到同一文档或其他文档的选项。<br /><br />在某些应用程序中，它还允许以不受保护的形式保存整个文档。|Office 自定义权限：作为“允许具有读取权限的用户复制内容”自定义策略选项。<br /><br />Azure 经典门户中的名称：**复制并提取内容**<br /><br />Azure 门户中的名称：“复制并提取内容”<br /><br />AD RMS 模板中的名称：**提取** <br /><br />API 常量或值：`IPC_GENERIC_EXTRACT L"EXTRACT"`|
|公用名：**允许宏** <br /><br />策略中的编码：**OBJMODEL**|启用运行宏或执行其他编程或远程访问文档内容的选项。|Office 自定义权限：作为“允许编程访问”自定义策略选项。 不是特定于收件人的设置。<br /><br />Azure 经典门户中的名称：**允许宏**<br /><br />Azure 门户中的名称：包含在可选择的所有权限中，因为 Office 应用中的 Azure 信息保护栏需要此权限。<br /><br />AD RMS 模板中的名称：**允许宏** <br /><br />API 常量或值：未实现。|

## <a name="rights-included-in-permissions-levels"></a>权限级别中包括的权限

某些应用程序会将使用权限组合成不同的权限级别，这样可以更容易地选择那些通常在一起使用的使用权限。 这些权限级别可帮助减少用户操作的复杂性，用户只需按角色选择相应选项即可。  例如，**审阅者**和**合著者**。 虽然这些选项通常会向用户显示这些权限的摘要，但可能并不包括前一表中列出的每个权限。

可通过下表查看这些权限级别的列表，以及这些权限级别所含权限的完整列表。

|权限级别|应用程序|包括的权限（通用名称）|
|---------------------|----------------|---------------------------------|
|查看器|Azure 经典门户 <br /><br />Azure 门户<br /><br /> 适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；答复；全部答复；允许宏 [[1]](#footnote-1)<br /><br />注意：对于电子邮件，请使用审阅者级别而不是此权限级别，确保接收到的电子邮件答复为电子邮件而不是附件。 向使用 Outlook 客户端或 Outlook Web App 的其他组织发送电子邮件时，也需要审阅者权限。|
|审阅者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；答复：全部答复 [[2]](#footnote-2)；转发 [[2]](#footnote-2)；允许宏 [[1]](#footnote-1)|
|合著者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；复制；查看权限；允许宏；另存为、导出 [[3]](#footnote-3)；打印；答复 [[2]](#footnote-2)；全部答复 [[2]](#footnote-2)；转发 [[2]](#footnote-2)|
|共有者|Azure 经典门户 <br /><br />Azure 门户<br /><br />适用于 Windows 的 Rights Management 共享应用程序<br /><br />适用于 Windows 的 Azure 信息保护客户端|查看、打开、读取；保存；编辑内容、编辑；复制；查看权限；允许宏；另存为、导出；打印；答复 [[2]](#footnote-2)；全部答复 [[2]](#footnote-2)；转发 [[2]](#footnote-2)；完全控制|

----

###### <a name="footnote-1"></a>脚注 1

对于适用于 Windows 的 Azure 信息保护客户端，目前 Office 应用程序中的信息保护栏需要此权限。

###### <a name="footnote-2"></a>脚注 2
不适用项：适用于 Windows 的 Azure 信息保护客户端或适用于 Windows 的 Rights Management 共享应用程序。

###### <a name="footnote-3"></a>脚注 3
不包括在适用于 Windows 的 Azure 信息保护客户端中。 在此客户端中，导出使用权限包括删除保护的功能。


## <a name="rights-included-in-the-default-templates"></a>默认模板中包括的权限
默认模板中包括的权限如下：

|显示名称|包括的权限（通用名称）|
|----------------|---------------------------------|
|&lt;组织名称&gt; - 机密信息，仅供查阅|查看、打开、读取|
|&lt;组织名称&gt; - 机密信息|查看、打开、读取；保存；编辑内容、编辑；查看权限；允许宏；转发；答复；全部答复|

## <a name="do-not-forward-option-for-emails"></a>电子邮件的“不得转发”选项

Exchange 客户端和服务（例如 Outlook 客户端、Outlook Web Access 应用和 Exchange 传输规则）有一个附加的电子邮件信息权限保护选项：**不得转发**。 

尽管**不得转发**看似用户（和 Exchange 管理员）可选择的默认权限管理模板，但此选项并不是模板。 因此在 Azure 经典门户中查看和管理 Azure 权限管理模板时，你看不到此选项。 相反，**不得转发**选项是用户对其电子邮件收件人动态应用的一组权限。

对电子邮件应用**不得转发**选项时，收件人将无法转发、打印或复制电子邮件，也无法保存附件或另存为其他名称。 例如，在 Outlook 客户端中，“转发”按钮和**另存为**、**保存附件**和**打印**菜单选项将不可用，并且无法添加或更改**收件人**、**抄送**或**密件抄送**框中的收件人。

应用**不得转发**选项和应用不授予电子邮件“转发”权限的模板有重要区别：**不得转发**选项使用基于原始邮件用户所选收件人的授权用户动态列表；而模板中的权限使用由管理员事先指定的授权用户静态列表。 区别是什么？ 让我们举个例子： 

某名用户想要通过电子邮件向营销部门的特定人员发送不应与其他任何人共享的信息。 她应该使用将（查看、答复和保存）权限限制于营销部门的模板来保护邮件吗？  还是她应该选择**不得转发**选项？ 这两种选择都将使收件人无法转发电子邮件。 

- 如果她应用模板，收件人仍可与营销部门中的其他人共享该信息。 例如，收件人可使用资源管理器将电子邮件拖放到共享位置或 U 盘。 现在，营销部门中有权访问此位置的任何人（和电子邮件所有者）都可以查看该电子邮件中的信息。
 
- 如果她应用了**不得转发**选项，则收件人将无法通过将电子邮件移动到其他位置来与营销部门中的其他任何人共享信息。 在这种情况下，将只有原始收件人（和电子邮件所有者）能够查看该电子邮件中的信息。

> [!NOTE] 
> 当要求只有发件人选择的收件人才能看到电子邮件中的信息时，请使用**不得转发**。 使用模板，使电子邮件将权限限制于管理员提前指定的、与发件人所选收件人相互独立的一组人员。

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

例如，即使文档现在受不含打印使用权限的模板的保护，创建该文档的用户仍可打印文档。 同一用户始终可访问其文档，而无需考虑离线访问设置或可能在该模板中配置的到期日期。 此外，由于权限管理所有者具有完全控制使用权限，因此该用户还可以重新保护文档以向更多用户授予访问权限（此时该用户成为权限管理颁发者以及权限管理所有者），甚至可以删除保护。 但是，只有权限管理颁发者可跟踪和撤销文档。

在[使用情况日志](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs)中，文档或电子邮件的权限管理所有者记录为“所有者-电子邮件”字段。

请注意，权限管理所有者独立于 Windows 文件系统所有者。 两者通常是相同的，但也可以不同，即使不使用 SDK 或 PowerShell 也是如此。

## <a name="see-also"></a>另请参阅
[为 Azure Rights Management 服务配置自定义模板](configure-custom-templates.md)

[为 Azure 权限管理和发现服务或数据恢复配置超级用户](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

