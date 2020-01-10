---
title: 使用 Azure 信息保护配置可靠的文档协作
description: 用于在受 Azure 信息保护保护的文档上进行协作的端到端工作流。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4895c429-959f-47c7-9007-b8f032f6df6f
ms.subservice: aiplabels
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 57e40899f3c386b076a8642c17f019ea0767ab22
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75743782"
---
# <a name="configuring-secure-document-collaboration-by-using-azure-information-protection"></a>使用 Azure 信息保护配置可靠的文档协作

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

当你使用 Azure 信息保护时，你可以保护你的文档，而无需牺牲授权用户的协作。 一个用户创建并与他人共享以进行查看和编辑的大多数文档将是 Word、Excel 和 PowerPoint 等 Office 文档。 这些文档支持本地保护，这意味着除了授权和加密的保护功能外，它们还支持受限权限以实现更细化的控制。 

这些权限被称为使用权限，并包含查看、编辑、打印等权限。 你可以在文档受到保护时定义个人使用权限，也可以定义一组使用权限，这被称为权限级别。 通过权限级别，你可以更轻松地选择通常一起使用的使用权限，例如审阅者和合著者。 有关使用权限和权限级别的详细信息，请参阅[配置 Azure 信息保护的使用权限](configure-usage-rights.md)。

配置这些权限时，可以指定向哪些用户授予它们：

- **对于你自己的组织或使用 Azure Active Directory 的另一组织中的用户**：可以指定 Azure AD 用户帐户、Azure AD 组或该组织中的所有用户。 

- **对于没有 Azure Active Directory 帐户的用户**：指定将与 Microsoft 帐户一起使用的电子邮件地址。 此帐户可能已经存在，或者用户可以在打开受保护文档时进行创建。 
    
    若要使用 Microsoft 帐户打开文档，用户必须使用 Office 365 应用（即点即用）。 其他 Office 版本尚不支持使用 Microsoft 帐户打开受 Office 保护的文档。

- **对于任何身份已验证的用户**：此选项适用于不需要控制谁能访问受保护文档的情况，前提是可以验证用户身份。 如果内容受 Office 365 邮件加密的新功能保护，可以通过 Azure AD（使用 Microsoft 帐户），甚至是联合社交提供程序或一次性密码进行身份验证。 

作为管理员，你可以配置 Azure 信息保护标签以应用权限和授权用户。 此配置使用户和其他管理员应用正确的保护设置变得非常简单，因为他们只需应用标签而无需指定任何详细信息。 以下部分提供了一个演练示例，用于保护支持与内外部用户进行安全协作的文档。


## <a name="example-configuration-for-a-label-to-apply-protection-to-support-internal-and-external-collaboration"></a>让标签应用保护以支持外部协作的配置示例


此示例演示了如何配置现有标签以应用保护，以便组织中的用户可以与另一个拥有 Office 365 或 Azure AD 的组织中的所有用户、其他具有 Office 365 或 Azure AD 的组织中的组以及在 Azure AD 中没有帐户而是使用 Gmail 电子邮件地址的用户就文档进行协作。

由于方案限制为只有特定人员拥有访问权限，因此不包括任何身份已验证的用户的设置。 有关如何使用此设置配置标签的示例，请参阅[示例 5：加密内容但不限制谁能访问内容的标签](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)。  

1. 选择已在全局策略中或指定了作用域的策略中的标签。 在“保护”窗格，确保选中“Azure (云密钥)”。
    
2. 务必选中“设置权限”，然后选择“添加权限”。

3. 在“添加权限”窗格： 
    
   - 对于内部组：选择“浏览目录”以选择组，而其必须启用电子邮件。
    
   - 对于第一个外部组织中的所有用户：选择“输入详细信息”，然后在组织的租户中键入域名。 例如，fabrikam.com。
    
   - 对于第二个外部组织中的组：仍在“输入详细信息”选项卡上，键入组织租户中的组的电子邮件地址。 例如， sales@contoso.com。
    
   - 对于没有 Azure AD 帐户的用户：仍在“输入详细信息”选项卡上，键入用户的电子邮件地址。 例如， bengi.turan@gmail.com。 

4. 若要向所有这些用户授予相同的权限：对于“从预设中选择权限”，可选择“共有者”、“合著者”、“审阅者”或“自定义”，以选择希望授予的权限。
    
    例如，你配置的权限可能与以下内容相似：
        
    ![为安全协作配置权限](./media/collaboration-permissions.png)

5. 在“添加权限”窗格上单击“确定”。

6. 在 "**保护**" 窗格上，单击 **"确定"** 。

7. 在“标签”窗格上，选择“保存”。 

## <a name="applying-the-label-that-supports-secure-collaboration"></a>应用支持安全协作的标签

现在此标签已配置好，它可以通过好多种方式（包括以下几种）应用于文档：

|应用标签的不同方式|更多信息|
|---------------|----------|
|用户在 Office 应用程序中创建文档时，手动选择标签。|用户从 Office 功能区上的“保护”按钮或从 Azure 信息保护栏选择标签。|
|系统提示用户在保存新文档时选择一个标签。|你已配置名为“所有文档和电子邮件必须具有标签”的 Azure 信息保护[策略设置](configure-policy-settings.md)。|
|用户通过电子邮件共享文档并在 Outlook 中手动选择标签。|用户从 Office 功能区上的“保护”按钮或从 Azure 信息保护栏选择标签，并使用相同的设置自动保护附加的文档。|
|管理员使用 PowerShell 将标签应用于文档。|使用 [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) cmdlet 将标签应用于特定文档或文件夹中的所有文档。|
|你还额外配置了标签以应用自动分类，而现在可以使用 Azure 信息保护扫描程序或 PowerShell 应用自动分类。|请参阅[如何配置 Azure 信息保护的自动和建议分类条件](configure-policy-classification.md)。|

若要完成本演练，请在 Office 应用程序中创建文档时手动应用标签： 

1. 在客户端计算机上，如果你已打开 Office 应用程序，请先关闭，然后再重新打开，以获取包含新配置的标签的最新策略更改。 

2. 将标签应用于文档并保存。

通过将受保护的文档附加到电子邮件中来实现共享，并将其发送给你授权编辑该文档的人员。

## <a name="opening-and-editing-the-protected-document"></a>打开并编辑受保护的文档

当你授权的用户打开文档进行编辑时，文档会在打开时出现一个信息横幅，提示他们权限受限。 例如：

![Azure 信息保护权限信息横幅示例](./media/example-restricted-access-banner.png)

如果他们选择“查看权限”按钮，将看到他们拥有的权限。 在以下示例中，用户可以查看和编辑文档：

![Azure 信息保护权限对话框示例](./media/example-permisisons-popup.png)

注意：如果文档由同时使用 Azure 信息保护的外部用户打开，Office 应用程序不会显示文档的分类标签，尽管仍保留标签中的任何视觉标记。 相反，外部用户可以根据组织的分类来应用自己的标签。 如果这些外部用户随后将编辑过的文档发回给你，Office 会在文档重新打开时显示原始分类标签。

在受保护文档打开前，将会发生以下身份验证流之一：

- 对于拥有 Azure AD 帐户的用户，他们使用自己的 Azure AD 凭据由 Azure AD 进行身份验证，随后文档打开。 

- 对于没有 Azure AD 帐户的用户，如果他们未使用有权打开文档的帐户登录 Office，则会看到“帐户”页面。 
    
   在“帐户”页面上，选择“添加帐户”：
   
    ![添加 Microsoft 帐户以打开受保护的文档](./media/add-account-msa.png)

   在“登录”页面上，选择“创建一个!”， 并按照提示使用用于授予权限的电子邮件地址创建一个新的 Microsoft 帐户：
    
    ![创建 Microsoft 帐户以打开受保护的文档](./media/create-account-msa.png)
    
    当创建新的 Microsoft 帐户时，本地帐户切换会到这个新的 Microsoft 帐户，然后用户可以打开文档。


### <a name="supported-scenarios-for-opening-protected-documents"></a>用于打开受保护的文档的受支持场景

下表总结了不同的身份验证方法，支持使用这些方法来查看和编辑受保护文档。

此外，以下方案也支持查看文档：

- 适用于 Windows、iOS 和 Android 的 Azure 信息保护查看器可以使用 Microsoft 帐户打开文件。 

- 如果社交提供程序和一次性密码与 Exchange Online 和 Office 365 邮件加密的新功能一起用于执行身份验证，浏览器可以打开受保护附件。 

|用于查看和编辑文档的平台： <br />Word、Excel、PowerPoint|身份验证方法：<br />Azure AD|身份验证方法：<br />Microsoft 帐户|
|---------------|----------|-----------|-----------|
|Windows|是 [[1]](#footnote-1)|是 [[2]](#footnote-2)|
|iOS|是 [[1]](#footnote-1)|否|
|Android|是 [[1]](#footnote-1)|否|
|MacOS|是 [[1]](#footnote-1)|否|

###### <a name="footnote-1"></a>脚注 1
支持用户帐户、启用电子邮件的组、所有成员。 用户帐户和启用电子邮件的组可以包括来宾帐户。 除来宾帐户外的所有成员。

###### <a name="footnote-2"></a>脚注 2
当前仅受 Office 365 应用（即点即用）支持。




## <a name="next-steps"></a>后续步骤

有关要将保护应用于常见场景的标签，请参阅其他[配置示例](configure-policy-protection.md#example-configurations)。 本文还包含有关保护设置的更多详细信息。

有关可以为标签配置的其他选项和设置的详细信息，请参阅[配置 Azure 信息保护策略](configure-policy.md)。 

本文中配置的标签也通过相同的名称创建保护模板。 如果你拥有的应用程序和服务与 Azure 信息保护的保护模板相集成，则可以应用此模板。 例如，DLP 解决方案和邮件流规则。 Web 上的 Outlook 自动显示 Azure 信息保护全局策略中的保护模板。 




