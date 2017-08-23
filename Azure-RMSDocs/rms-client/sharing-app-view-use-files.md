---
title: "使用 RMS 共享应用打开 RMS 保护的文件 - AIP"
description: "有关查看和使用受保护文件（需要安装 Rights Management (RMS) 共享应用程序）的说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0a510d559573e942b8a2bf392f36a1300dfbfb7a
ms.sourcegitcommit: 1c3ebf4ad64b55db4fec3ad007fca71ab7d38c02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2017
---
# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>查看和使用受权限管理保护的文件

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

如果[计算机安装了权限管理 (RMS) 共享应用程序](install-sharing-app.md)，你只需双击受保护文件即可查看它。 此文件也许是电子邮件中的附件，或者你可能在使用文件资源管理器时看到它。

> [!NOTE]
> 在你可以查看受保护文件之前，Rights Management 服务必须首先确认你有权查看该文件，方法是检查你的用户名和密码。 在某些情况下，此信息会被缓存下来，所以你不会看到要求出示凭据的提示。 在其他情况下，将提示你提供凭据。
>
> 如果你的组织不使用 Azure 信息保护或 AD RMS，你可以申请会接受你的凭据的免费帐户，以便可以使用 RMS 打开受保护文件：
>
> -   若要申请此帐户，请单击链接以申请 [个人 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)。
>
>     注册时，使用公司的电子邮件地址，而不是个人电子邮件地址。 如果注册的原因是要使用电子邮件发送受保护附件，请使用与用于发送电子邮件相同的电子邮件地址。
> -   有关详细信息，请参阅[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

## <a name="to-view-a-protected-file"></a>查看受保护文件
通过使用文件资源管理器或包含附件的电子邮件，双击受保护文件，然后在收到提示时输入凭据。

如果你看到两个版本的文件，但具有不同的文件扩展名，仅在不打开另一个文件的情况下打开具有 .ppdf 文件扩展名的文件。 如果 .ppdf 版本也无法打开，请首先安装 [RMS 共享应用程序](install-sharing-app.md)，因为该程序知道如何打开具有 .ppdf 文件扩展名的文件。

> [!NOTE]
> 有关详细信息，请参阅[自动创建的 .ppdf 文件是什么文件？](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)

文件的打开方式取决于保护方式，此保护方式你可以通过查看文件扩展名得知。 在每种情况下，只要文件受到保护，打开它就需要审核并将处于审核状态。 此外，如果文件以电子邮件附件的形式发送，则每次你打开文件时，发件人都会收到电子邮件通知。

- **文件具有*.pfile* 文件扩展名**

    文件受到一般性保护。

    打开文件时，你将看到共享应用程序中的“受保护文件”对话框，告知你此文件由谁保护，并且希望你遵守共同所有者权限。 单击“打开”  ，读取文件。

    ![使用 RMS 共享应用程序时通过电子邮件共享的 pfile 的对话框](../media/ADRMS_MSRMSApp_PfilePermission.png)

- **文件具有 .ppdf 文件扩展名，或者是受保护的文本或图像文件（如 .ptxt 或 .pjpg）**

    该文件已本机保护为只读副本。

    使用 RMS 共享应用程序安装的查看器，打开该文件。 此文件是只读文件，即使你将其保存到其他位置或将其重命名也是如此。

- **其他文件扩展名**

    该文件已受到本机保护。

    使用与原始文件扩展名关联的应用程序打开文件，并且文件顶部会显示限制横幅。 该横幅可能显示适用于文件的权限，或者提供显示权限的链接。 例如，你可能会看到以下内容，要求你单击“权限当前受限”  以查看适用于文件和可以访问文件的用户的实际权限：

    ![文件受保护时的受限访问横幅](../media/ADRMS_MSRMSApp_RestrictedAccess.png)



对于 Rights Management 服务支持的文件扩展名的完整列表，请参阅 [Rights Management 共享应用程序管理员指南](sharing-app-admin-guide.md)中的[支持的文件类型和文件扩展名](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)部分。 如果你的文件扩展名未列出，则可进行 Web 搜索，看它是否是其他应用程序支持的文件扩展名。

## <a name="to-use-files-that-have-been-protected-for-example-edit-and-print-the-file"></a>使用受保护的文件（例如，编辑和打印文件）
如果在打开受保护文件后，你想要执行除读取之外的其他操作（例如编辑、复制和打印），请根据文件扩展名按照说明执行操作：

- **文件具有*.pfile* 文件扩展名**

    保存已打开文件，并赋予其与所要使用的应用程序关联的新文件扩展名。

    例如，如果某个文件使用文件名 document.vsdx.pfile 保护，请查看该文件并在文件资源管理器中将文件作为 document.vsdx 进行保存。

    新文件从此不受保护。 如果你想要保护该文件，必须手动执行此操作。 有关说明，请参阅[使用 Rights Management 共享应用程序保护设备上的文件（就地保护）](sharing-app-protect-in-place.md)。

- **文件具有 .ppdf 文件扩展名，或者是受保护的文本或图像文件（如 .ptxt 或 .pjpg）**

    你仅可以查看文件，并且如果重命名或移动文件，保护将保留在文件上。

- **其他文件扩展名**

    若要使用这些文件，你的设备必须具有了解 Rights Management 保护的应用程序。 这些应用程序称为启用 RMS 的应用程序。 Office 2016、Office 2013 和 Office 2010 应用程序（如 Word、Excel、PowerPoint 和 Outlook）即是为 Rights Management 启用的应用程序的示例。 但是非 Microsoft 应用程序（如其他软件公司的应用程序或你自己的业务线应用程序）也要为 Rights Management 而启用。

    为 Rights Management 而启用的应用程序知道如何打开由其他权限管理启用的应用程序保护的文件。 它们还保留了应用到它们的保护，即使你编辑该文件、将其按其他文件名保存或将其保存到其他位置。 这些应用程序允许你根据当前应用到文件的权限使用文件，以便在你得到授权的情况下可以使用该文件。 例如，你可能能够编辑文件，但不能打印文件。


## <a name="examples-and-other-instructions"></a>示例和其他说明
有关如何使用 Rights Management 共享应用程序以及操作说明的示例，请参阅以下 Rights Management 共享应用程序用户指南部分：

-   [使用 RMS 共享应用程序的示例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [要执行什么操作？](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>另请参阅
[权限管理共享应用程序用户指南](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]