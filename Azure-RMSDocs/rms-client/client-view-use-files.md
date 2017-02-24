---
title: "查看和使用受保护文件 | Azure 信息保护"
description: "查看和使用要求安装 Azure 信息保护客户端的受保护文件的说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/10/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5fcd31a570fbd22a488d0a016dd3d3887918f755
ms.openlocfilehash: 123fc7078e29ca59174d349efb2366df2f39e023


---

# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>查看和使用受权限管理保护的文件

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

通常，你可以直接打开受保护文件进行查看。 例如，可双击电子邮件中的附件、双击文件资源管理器中的文件或单击文件的链接。

如果文件未打开，可以使用 **Azure 信息保护查看器**将其打开。 此查看器会作为 Azure 信息保护客户端的一部分自动安装，或者可以单独安装。 你可以从 Microsoft 网站的 [Microsoft Azure 信息保护](https://go.microsoft.com/fwlink/?LinkId=303970)页面中同时安装客户端和查看器。 有关安装客户端的详细信息，请参阅[下载和安装 Azure 信息保护客户端](install-client-app.md)。

> [!NOTE]
> 虽然安装客户端可提供更多功能，但它需要本地管理员权限，并且完整功能需要组织的相应服务：
> 
> - Azure 信息保护
> 
> - Azure 权限管理
> 
> - Active Directory 权限管理服务 
> 
> 如果另一组织中的某人向你发送了受保护文档，或者你没有访问你的电脑的本地管理员权限，请安装查看器。

## <a name="prompts-for-authentication"></a>身份验证提示

在你可以查看受保护文件之前，用于保护文件的 Rights Management 服务必须首先确认你有权查看该文件。 该服务通过检查你的用户名和密码来完成此操作。 在某些情况下，此信息会被缓存下来，所以你不会看到要求出示凭据的提示。 在其他情况下，将提示你提供凭据。

如果你的组织没有基于云的帐户供你使用（用于 Office 365 或 Azure），并且未使用等效的本地版本 (AD RMS)，你可以申请一个用于接受凭据的免费帐户，以便打开 Rights Management 保护的文件：

-   若要申请此帐户，请单击链接以申请 [个人 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)。
    
    注册时，使用公司的电子邮件地址，而不是个人电子邮件地址。 如果注册的原因是要使用电子邮件发送受保护附件，请使用与用于发送电子邮件相同的电子邮件地址。
    
-   有关详细信息，请参阅[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

## <a name="to-view-and-use-a-protected-file"></a>查看和使用受保护的文件

1. 打开受保护的文件（例如，双击文件或附件，或单击文件的链接）。 如果系统提示你选择应用，请选择“Azure 信息保护查看器”。 

2. 如果看到“登录”或“注册”页面：请点击“登录”并输入凭据。 如果受保护的文件是以附件形式发送给你的，请务必指定用于向你发送该文件的同一电子邮件地址。
    
    如果没有被接受的帐户，请参阅本页中的[身份验证提示](#prompts-for-authentication)部分。 注册一个免费帐户，然后返回到这些说明。

3. 该文件的只读版本会在 **Azure 信息保护查看器**中打开。 如果有足够的权限，你可以打印该文件，并对其进行编辑。 

    可通过单击“权限”来检查你对该文件的权限。 如果要请求具有其他权限的新版本文件，在“权限”对话框中，你还可以标识要联系的文件所有者。
    
    有关每个权限级别中包含的权限和使用情况权限的详细信息，请参阅[权限级别中包含的权限](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels)。

4. 若要编辑文件，请单击“另存为”，这样就可以在不保护原始文件扩展名的情况下保存文件。 然后，可使用与该文件类型相关联的应用程序来编辑该文件。

5. 如果要打开其他受保护的文件，可以使用“打开”选项从查看器中直接浏览它们。 所选文件将替换查看器中的原始文件。 

> [!TIP]
> 如果未打开受保护的文件，请下载并使用 [RMS分析工具](https://www.microsoft.com/en-us/download/details.aspx?id=46437)。 按照工具中的说明进行操作，看你的计算机中是否存在妨碍受保护文档打开的问题。


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

-   [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


