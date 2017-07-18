---
title: "使用 Azure 信息保护进行分类和保护"
description: "说明如何对文档和电子邮件进行分类和保护。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 960fe1abf2fa4f5b8976f190454d31849736298a
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>使用 Azure 信息保护对文件或电子邮件进行分类和保护

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

在 Office 桌面应用中（**Word**、**Excel**、**PowerPoint**、**Outlook**）创建和编辑文档和电子邮件时对其进行分类和保护最为简单。 

但是，你也可以使用**文件资源管理器**对文件进行分类和保护，此方法支持其他文件类型，并且是一次性分类和保护多个文件的便捷方式。 此方法支持保护 Office 文档、PDF 文件、文本和图像文件，以及各种其他文件。 

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>与组织外部人员安全共享文件

受保护文件可安全地与他人共享。 例如，将文件附加到电子邮件，或从你的 SharePoint 站点发送邀请。

如果你定期与组织外部人员共享文件，管理员可能为你配置了设置保护的标签，以便这些人员可以读取它。 此外，也可以在共享前使用 [Office 应用程序来设置自定义权限](#set-custom-permissions-for-a-document)，或使用[文件资源管理器设置文件的自定义权限](#using-file-explorer-to-classify-and-protect-files)。 

如果设置你自己的自定义权限，并且文件已受到保护以供内部使用，请先创建一个副本来保留原始权限。 然后，使用此副本设置自定义权限。  

如果使用自定义权限保护文件，请使用标准共享机制共享文件。 如果你要与之共享的人员是第一次接收受保护文件，他们可能需要阅读说明才能查看。 对于这些人，你可以复制并粘贴以下消息：**我已使用 Microsoft Azure 信息保护对此文件提供保护。若是首次使用，请参阅这些[说明](https://aka.ms/rms-signup)。**


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>使用 Office 应用对文档和电子邮件进行分类和保护

使用 Azure 信息保护栏并选择其中一个已为你配置的标签。 

例如，在下图中，因为“敏感度”显示“未设置”，因此尚未标记文档。 若要设置标签，例如“内部”，请单击“内部”。 如果你不确定要将哪种标签应用于当前文档或电子邮件，请使用标签工具提示详细了解每种标签及其应用情况。

![Azure 信息保护栏示例](../media/info-protect-bar-not-set-callout.png)

如果已将某种标签应用于文档，并且想要进行更改，可以选择其他标签。 如果标签没有显示在栏上，请首先单击当前标签值旁边的“编辑标签”图标。

除了手动选择标签，还可通过以下方式应用标签：

- 管理员配置了默认标签，你可保留或更改该标签。

- 管理员配置了建议提示，当检测到敏感数据时将提示选择特定标签。 你可以接受此建议（应用标签），或拒绝建议（不应用建议标签）。

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Azure 信息保护栏的异常 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>你的 Office 应用程序中看不到此信息保护栏？

- 你可能没有[安装](install-client-app.md) Azure 信息保护客户端，或客户端正以[仅保护模式](client-protection-only-mode.md)运行。
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>你希望看到的标签没有显示在栏上？ 

- 如果管理员最近为你配置了新标签，请尝试关闭 Office 应用程序的所有实例，然后重新打开。 此操作将检查对你的标签所做的更改。

- 如果缺少应用保护的标签，那么可能你使用的 Office 版本不支持应用 Rights Management 保护。 若要验证，请依次单击“**保护**” > “**帮助和反馈**”，检查“**客户端状态**”部分中是否显示消息“**此客户端未获许可使用 Office Professional Plus**”。 

- 此标签采用的作用域策略可能不包括你的帐户。 请与你的技术支持或管理员一起检查。

### <a name="set-custom-permissions-for-a-document"></a>设置文档的自定义权限

可以指定你自己的文档保护设置，而不使用管理员可能与选定标签一起添加的保护设置。

1. 在“**开始**”选项卡上的“**保护**”组中，依次单击“**保护**” > “**自定义权限**”：

    ![“自定义权限”选项](../media/custom-permissions-callout.png)
    
    请注意，你指定的任何自定义权限将替换（而不是补充）管理员可能已为选定标签定义的保护设置。  

2. 在“**Microsoft Azure 信息保护**”对话框中，指定以下内容：

    - **使用自定义权限进行保护**：请务必选中此选项，这样才能指定并应用自定义权限。 取消选中此选项即撤销任何自定义权限。
    
    - **选择权限**：如果要保护文件，以便只有你可以访问，请选中“**仅限自己访问**”。 否则，请选中“希望对象拥有的访问级别”。

    - **选择用户、组或组织**：指定哪些人应拥有你为一个或多个文件选择的权限。 键入他们的完整电子邮件地址、组电子邮件地址或相应组织中所有用户的组织域名。 请注意，暂不支持个人电子邮件地址。
        
    - 过期访问：仅为时间敏感文件选择此选项，以便你指定的人员在你设定的日期后无法打开所选文件。你仍然可以打开原始文件，但是在所设定日期的午夜后（当前时区），你指定的用户将无法打开文件。

5. 单击“**应用**”，然后等待“**已应用自定义权限**”消息。 然后单击 **“关闭”**。


### <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Azure 信息保护栏的键盘快捷方式

若要使用键盘快捷方式访问 Azure 信息保护栏，请使用以下组合键：

- 按 **Ctrl** + **Shift** + **~** 

然后，使用 Tab 键选择标签和保护栏上的其他控件（“隐藏标签”图标和“删除标签”图标），按 Enter 键以将其选中。

## <a name="using-file-explorer-to-classify-and-protect-files"></a>使用文件资源管理器对文件进行分类和保护

使用文件资源管理器时，可快速对单个文件、多个文件或文件夹进行分类和保护。 

选择文件夹时，将自动为你设置的分类和保护选项选择该文件夹及其所有子文件夹中的所有文件。 但是，在该文件夹或子文件夹中创建的新文件不会自动配置这些选项。

使用文件资源管理器对文件进行分类和保护时，如果一个或多个标签显示为灰色，则你选择的文件不支持分类。 对于这些文件，只有在管理员已将标签配置为应用保护时，你才能选择标签。 或者，你可以指定自己的保护设置。 

分类和保护会自动排除一些文件，因为更改这些文件可能会导致电脑停止运行。 尽管你可以选择这些文件，但系统会将其作为排除的文件夹或文件跳过。 示例包括可执行文件和你的 Windows 文件夹。

管理员指南包含受支持文件类型的完整列表以及自动排除的文件和文件夹的完整列表：[受 Azure 信息保护客户端支持的文件类型](client-admin-guide-file-types.md)。


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>使用文件资源管理器对文件进行分类和保护

1. 在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”。 例如：
    
    ![在文件资源管理器中，右键单击“使用 Azure 信息保护进行分类和保护”](../media/right-click-classify-protect-folder.png)

2. 在“分类和保护 - Azure信息保护”对话框中，请像在 Office 应用程序中那样使用标签，这样可以按管理员定义的方式设置分类和保护。 

    - 如果无法选择标签（它们显示为灰色）：则所选文件不支持分类，但你可以通过自定义权限保护它（步骤 3）。 例如：

    ![“分类和保护 - Azure 信息保护”对话框中无可用标签](../media/info-protect-dialog-labels-dimmed.png)
    
    - 如果你看不到标签，但是“公司预定义的保护”选项出现在此对话框中，表明：客户端正以[仅保护模式](client-protection-only-mode.md)运行。 选择模板以应用管理员为你配置的保护，或者选择“自定义权限”指定自己的保护设置，然后转到步骤 4.
    
    ![“分类和保护 - Azure 信息保护”对话框中无任何标签](../media/info-protect-dialog-labels-protection-only.png)
    
3. 如果想要指定自己的保护设置，而不使用管理员可能已包含在所选标签中的保护设置，请选择“使用自定义权限保护”。
    
    指定的任何自定义权限将替换而不是补充管理员可能已为所选标签定义的保护设置。  

4. 如果已选择自定义权限选项，此时指定以下项：

    - **选择权限**：选择你希望用户在保护所选文件时具有的访问级别。
    
    - **选择用户**：指定应对文件具有选定权限的人员。 可以从通讯簿中进行选择（例如，来自组织的人员和来自其他组织的联系人）。 对于其他人员，键入他们的完整电子邮件地址、组电子邮件地址或相应组织中所有用户的组织域名。 请注意，暂不支持个人电子邮件地址。
        
    - 过期访问：仅为时间敏感文件选择此选项，以便你指定的人员在你设定的日期后无法打开所选文件。你仍然可以打开原始文件，但是在所设定日期的午夜后（当前时区），你指定的用户将无法打开文件。
    
    请注意，如果此设置此前通过 Office 2010 应用的自定义权限配置，则指定到期日期不会显示在此对话框中，但仍然会设置到期日期。 此显示问题仅适用于在 Office 2010 中配置了到期日期的情况。

5. 单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。

根据你的选择，现已对所选择的一个或多个文件进行分类和保护。 在某些情况下（添加的保护更改了文件扩展名时），文件资源管理器中的原始文件将替换为具有 Azure 信息保护锁状图标的新文件。 例如：

![Azure 信息保护中具有锁状图标的受保护文件](../media/Pfile.png)

如果改变了有关分类和保护的想法，或稍后需要更改设置，仅需通过重复此过程进行新的设置。

指定的分类和保护会保留在文件中，即使你通过电子邮件发送文件或将其保存到其他位置也是如此。 如果已保护该文件，则可跟踪用户如何使用它，如果有必要，还可撤销对它的访问。 有关详细信息，请参阅[使用 Azure 信息保护时跟踪和撤销已保护的文档](client-track-revoke.md)。 


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

-   [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
