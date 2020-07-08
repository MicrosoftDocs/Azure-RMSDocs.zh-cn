---
title: 通过 Azure 信息保护查看器查看受保护的文件
description: 说明如何查看和使用要求安装 Azure 信息保护查看器的受保护文件。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: f5b0ab0eacd7c95edf53135c81fe3184e9f3c46d
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047280"
---
# <a name="user-guide-view-protected-files-with-the-azure-information-protection-viewer"></a>用户指南：通过 Azure 信息保护查看器查看受保护的文件

>*适用于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8*
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

通常，你可以直接打开受保护文件进行查看。 例如，可双击电子邮件中的附件、双击文件资源管理器中的文件或单击文件的链接。

如果没有立即打开文件，Azure 信息保护查看器**** 可能会将其打开。 此查看器可以打开受保护的文本文件、受保护的图像文件、受保护的 PDF 文件，以及具有 .pfile**** 文件扩展名的所有文件。

此查看器作为 Azure 信息保护客户端的一部分自动安装，你也可以单独进行安装。 你可以从 Microsoft 网站的 [Microsoft Azure 信息保护](https://go.microsoft.com/fwlink/?LinkId=303970)页面中同时安装客户端和查看器。 有关安装客户端的详细信息，请参阅[下载和安装 Azure 信息保护客户端](install-client-app.md)。

> [!NOTE]
> 虽然安装客户端可提供更多功能，但它需要本地管理员权限，并且完整功能需要组织的相应服务。 例如，Azure 信息保护或 Active Directory Rights Management Services。
> 
> 如果另一组织中的某人向你发送了受保护文档，或者你没有访问你的电脑的本地管理员权限，请安装查看器。

必须是“已启用 RMS”的应用程序才能打开受保护的文档。 例如，Office 应用和 Azure 信息保护查看器是已启用 RMS 的应用程序。 要按类型和受支持的设备查看应用程序列表，请参阅[启用 RMS 的应用程序](../requirements-applications.md#rms-enlightened-applications)表格。  
## <a name="messagerpmsg-as-an-email-attachment"></a>作为电子邮件附件的 Message.rpmsg

如果在电子邮件中看到 message.rpmsg**** 文件附件，表明此文件不是受保护文档，而是作为附件显示的受保护电子邮件。 不能使用适用于 Windows 的 Azure 信息保护查看器来查看 Windows 电脑上受保护的电子邮件。 而是需要一个支持 Rights Management 保护的 Windows 电子邮件应用程序，如 Office Outlook。 或者可以使用 Outlook 网页版。

但是，如果你有 iOS 或 Android 设备，可以使用 Azure 信息保护应用来打开这些受保护的电子邮件。 可以从 Microsoft 网站的 [Microsoft Azure 信息保护](https://go.microsoft.com/fwlink/?LinkId=303970)页中为这些移动设备下载此应用。

## <a name="prompts-for-authentication"></a>身份验证提示

在你可以查看受保护文件之前，用于保护文件的 Rights Management 服务必须首先确认你有权查看该文件。 该服务通过检查你的用户名和密码来进行此项确认。 在某些情况下，这些凭据可能会被缓存，所以你不会看到要求登陆的提示。 在其他情况下，会提示你提供凭据。

如果你的组织没有基于云的帐户供你使用（用于 Office 365 或 Azure），并且没有使用等效的本地版本 (AD RMS)，则有两个选择：

- 如果他人向你发送受保护的电子邮件，请按照说明使用社交标识提供者登录（例如对于 Gmail 帐户使用 Google）或申请一次性密码。

- 可以申请一个接受你的凭据的免费帐户，使你能够打开受 Rights Management 保护的文档。 若要申请此帐户，请单击链接以申请[个人 RMS](https://go.microsoft.com/fwlink/?LinkId=309469)，然后使用公司电子邮件地址而不是个人电子邮件地址。 

## <a name="to-view-and-use-a-protected-document"></a>查看和使用受保护的文档

1. 打开受保护的文件（例如，双击文件或附件，或单击文件的链接）。 如果系统提示你选择应用，请选择“Azure 信息保护查看器”****。 

2. 如果看到“登录”**** 或“注册”**** 页面：请点击“登录”**** 并输入凭据。 如果受保护的文件是以附件形式发送给你的，请务必指定用于向你发送该文件的同一电子邮件地址。
    
    如果没有被接受的帐户，请参阅本页中的[身份验证提示](#prompts-for-authentication)部分。

3. 该文件的只读版本会在 **Azure 信息保护查看器**中打开。 如果有足够的权限，你可以打印该文件，并对其进行编辑。 

    可通过单击“权限”**** 来检查你对该文件的权限。 如果要请求具有其他权限的新版本文件，在“权限”**** 对话框中，你还可以标识要联系的文件所有者。
    
    有关每个权限级别中包含的权限和使用情况权限的详细信息，请参阅[权限级别中包含的权限](../configure-usage-rights.md#rights-included-in-permissions-levels)。

4. 要编辑文件，请单击“另存为”，这样可以将受保护的文件保存为其原始文件扩展名****。 然后，可使用与该文件类型相关联的应用程序来编辑该文件。 此时，文件的标签和保护将被删除。
    
    请注意，由于查看器是受保护的文件，因此仅对受保护的文件启用“另存为”按钮****。
    
5. 编辑完文件后，在“文件资源管理器”中，右键单击该文件以重新应用标签。 此操作会重新应用保护。

6. 如果要打开其他受保护的文件，可以使用“打开”**** 选项从查看器中直接浏览它们。 所选文件将替换查看器中的原始文件。 

> [!TIP]
> 如果受保护的文件未打开，并且已安装完整的 Azure 信息保护客户端，请尝试“重置设置”**** 选项。 要访问此选项，请从 Office 应用中依次选择“保护”按钮 >“帮助和反馈” > “重置设置”************。 
> 
> [有关“重置设置”选项的详细信息](client-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

-   [你希望做什么？](client-user-guide.md#what-do-you-want-to-do)

