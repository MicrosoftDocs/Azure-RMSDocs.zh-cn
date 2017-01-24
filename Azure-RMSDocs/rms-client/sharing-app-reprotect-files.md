---
title: "更改受 Rights Management 保护的文件的权限 | Azure 信息保护"
description: "当文件已由 Rights Management 保护时，你可以更改其权限，方法是重新保护它，然后指定有权访问它的所有用户，以及你要给予他们哪些权限。"
keywords: 
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5ac121b3-d7a0-40e4-8fe7-90bf4cf796f1
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: c0bfd99229e4d93c91fe8f9efafd887aa7562328


---

# <a name="change-permissions-on-files-that-have-been-protected-by-rights-management"></a>更改受 Rights Management 保护的文件的权限

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、具有 SP1 的 Windows 7、Windows 8、Windows 8.1*

当文件已由 Rights Management 保护时，你可以更改其权限，方法是重新保护它，然后指定有权访问它的所有用户，以及你要给予他们哪些权限。

> [!IMPORTANT]
> 这不是增量更改，而是完全替换。 你可以使用你需要的完整权限集有效地重新保护文件。
> 
>  例如，如果某个文件受到保护，只有市场营销部门的人员才可以打开它，而你想让销售部门的人员也能打开它，则必须重新保护该文件，以便销售和市场营销部门的人员都可以打开它。
>
> 同样，如果你想要添加或删除权限，则不能只指定要添加或删除的权限，而必须指定你希望所指定用户拥有的所有权限。

如果你是想要重新保护的文件的所有者（例如，你最初使用共享应用程序保护该文件），则你将自动拥有重新保护该文件的权限。 如果你不是所有者，那么你可能有或没有重新保护该文件的权限，具体取决于当前受保护文件具有的权限。 若要重新保护文件，则需要[完全控制使用权限](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions)。

例如，如果其他人使用 Rights Management 共享应用程序保护了该文件，并且指定了你所属的组和**共同所有者**作为自定义权限，那么你将能够重新保护该文件。 但是，如果他们没有指定你的名称或你所属的组，或者如果他们选择**审阅者 - 查看和编辑**或者是不允许你删除权限的模板，则你将不能重新保护该文件。 弄清自己是否具有相应权限的最简单的办法是尝试重新保护该文件。

如果你想要完全删除所有权限，以便不再保护文件，请参阅[《Remove protection from a file》](sharing-app-remove-protection.md)（删除文件保护）。

## <a name="to-re-protect-a-file-in-place"></a>若要重新保护现有文件，请执行以下操作

1.  选择文件资源管理器中要保护的文件。 右键单击该文件，选择“使用 RMS 保护”，然后选择“就地保护”。 例如：

    ![“就地保护”菜单选项](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > 如果没有看到“使用 RMS 保护”  选项，可能是计算机上没有安装 RMS 共享应用程序，或者是必须重新启动计算机以完成安装。 有关如何安装 RMS 共享应用程序的详细信息，请参阅[下载和安装 Rights Management 共享应用程序](install-sharing-app.md)。

2.  执行以下操作之一：

    -   选择策略模板：一般而言，它们是将访问权限和使用限制给你的组织成员的预定义权限。 例如，如果组织名称为“Contoso, Ltd”，你可能会看到“Contoso, Ltd - 机密，仅供查阅”。 如果这是你首次在此电脑上保护文件，将需要首先选择“公司定义的保护”以下载模板。

        下次单击“就地保护”选项时，你会看到多达 10 个可供选择的模板。 如果可用模板超过 10 个，但没有显示你所需要的模板，则可单击“公司定义的保护”以下载和查看所有模板。

        选择策略模板时，也可以保护多个文件和某个文件夹。 选择某个文件夹时，将自动选择该文件夹中的所有文件进行保护，但不会自动保护在该文件夹中创建的新文件。

    -   选择“自定义权限” ：如果模板没有提供所需的保护级别，或你想要自己显式设置保护选项，请选择此选项。 在[添加保护](sharing-app-dialog-box.md)对话框中指定此文件所需的选项，然后单击“应用”。

3. 如果你没有重新保护文件的权限，你将看到“无法保护内容”消息，其中包含要联系的人（文档所有者）的电子邮件地址，以便他们可以更改你的权限。

    如果你有重新保护文件的权限，你可能很快就会看到一个对话框，告诉你文件处于受保护状态，然后焦点返回到文件资源管理器。 现在，已使用你的更改保护所选的一个或多个文件。 

> [!NOTE]
> 在你可以重新保护文件之前，Rights Management 服务必须首先确认你有权对该文件执行该操作，方法是检查你的用户名和密码。 在某些情况下，此信息会被缓存下来，所以你不会看到要求出示凭据的提示。 在其他情况下，将提示你提供凭据。
>
> 如果你的组织不使用 Azure 信息保护或 AD RMS，你可以申请会接受你的凭据的免费帐户，以便可以使用受 RMS 保护的文件：
>
> -   若要申请此帐户，请单击链接以申请 [个人 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)。
>
>     注册时，使用公司的电子邮件地址，而不是个人电子邮件地址。 如果注册的原因是要使用电子邮件发送受保护附件，请使用与用于发送电子邮件相同的电子邮件地址。
> -   有关详细信息，请参阅[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

## <a name="to-re-protect-a-file-that-you-have-emailed"></a>重新保护已通过电子邮件发送的文件

如果想要更改已通过电子邮件发送的文件的权限：

- **要让更多的人阅读该文件**：按照[《Protect a file that you share by email》](sharing-app-protect-by-email.md)（保护使用电子邮件共享的文件）中的说明，将文件通过电子邮件发送给他们。

- **要更改文件的权限**：按照[《Protect a file that you share by email》](sharing-app-protect-by-email.md)（保护使用电子邮件共享的文件）中的说明，选择所需的新权限，通过电子邮件再次发送该文件。 

    因为不能删除最初通过电子邮件发送的文件的以前的权限，仅将其替换为新版本，所以考虑撤销以前通过电子邮件发送的文件，以便收件人不再能够打开该版本的文档。 如果需要使权限的限制性更强（例如，删除不应访问文件的用户，或者使他们不再能够编辑文件），那么撤销文件是合适的做法。

    若要撤销已通过电子邮件发送的文件，请参阅[《Track and revoke your documents》](sharing-app-track-revoke.md)（跟踪和撤销文档）。


## <a name="examples-and-other-instructions"></a>示例和其他说明
有关如何使用 Rights Management 共享应用程序以及操作说明的示例，请参阅以下 Rights Management 共享应用程序用户指南部分：

-   [使用 RMS 共享应用程序的示例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [要执行什么操作？](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>另请参阅
[权限管理共享应用程序用户指南](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


