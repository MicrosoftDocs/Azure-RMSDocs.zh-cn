---
title: '& 保护分类-Azure 信息保护经典客户端'
description: 有关使用适用于 Windows 的 Azure 信息保护经典客户端时如何对文档和电子邮件进行分类和保护的说明。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: b3fe9b0cbe0a709ffd5a256abf1d65af4ec4b535
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98808626"
---
# <a name="user-guide-classify-and-protect-with-the-azure-information-protection-classic-client"></a>用户指南：通过 Azure 信息保护经典客户端进行分类和保护

>***适用于**： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标记客户端，请参阅 [统一标签客户端用户指南](clientv2-classify-protect.md)。

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

> [!TIP]
> 借助这些说明，对文档和电子邮件进行分类和保护。 如果只需对文档和电子邮件进行分类（但不保护），请参阅[仅分类说明](client-classify.md)。 如果不确定应使用哪组说明，请与管理员或支持人员核实。

在 Office 桌面应用中（**Word**、**Excel**、**PowerPoint**、**Outlook**）创建和编辑文档和电子邮件时对其进行分类和保护最为简单。 

但是，还可以使用文件资源管理器对文件进行分类和保护。 此方法支持其他文件类型，此方法是一种一次性对多个文件进行分类和保护的便捷方法。 此方法支持保护 Office 文档、PDF 文件、文本和图像文件，以及各种其他文件。 

如果标签将保护应用于文档，则受保护的文档不适合保存在 SharePoint 或 OneDrive 中。 对于受保护的文件，这些位置不支持以下内容：共同创作、Office for web、搜索、文档预览、缩略图和电子数据展示。

> [!TIP]
> 如果为 [敏感标签启用了 SharePoint](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)，请询问管理员是否将标签迁移到这些位置支持的统一敏感度标签。

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>与组织外部人员安全共享文件

受保护文件可安全地与他人共享。 例如，你将受保护的文档附加到一封电子邮件。

在与组织外部人员共享文件之前，请咨询你的支持人员或管理员如何为外部用户保护文件。

例如，如果你的组织定期与另一组织中的用户通信，则你的管理员可能已配置了标签，以便这些用户可以读取和使用受保护的文档。 如果是这种情况，请选择这些标签来分类和保护要共享的文档。

或者，如果外部用户具有为其创建的 [企业到企业 (B2B) 帐户](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)，你可以在共享文档之前，使用 [Office 应用设置自定义权限](#set-custom-permissions-for-a-document)或使用[文件资源管理器设置自定义权限](#using-file-explorer-to-classify-and-protect-files) 如果设置你自己的自定义权限，并且文档已受到保护以供内部使用，请先创建一个副本来保留原始权限。 然后，使用此副本设置自定义权限。


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>使用 Office 应用对文档和电子邮件进行分类和保护

使用 Azure 信息保护栏或功能区上的“保护”按钮，选择已为你配置的某一个标签。 

例如，在下图中，因为 Azure 信息保护栏上的“敏感度”显示“未设置”，因此尚未标记文档。 要设置标签，例如“常规”，请单击“常规”。 如果你不确定要将哪种标签应用于当前文档或电子邮件，请使用标签工具提示详细了解每种标签及其应用情况。 

![Azure 信息保护栏示例](../media/info-protect-bar-not-set-callout.png)

如果已将某种标签应用于文档，并且想要进行更改，可以选择其他标签。 如果标签没有显示在栏上，请首先单击当前标签值旁边的“编辑标签”图标。

除了手动选择标签，还可通过以下方式应用标签：

- 管理员配置了默认标签，你可保留或更改该标签。

- 管理员配置了建议提示，当检测到敏感数据时将提示选择特定标签。 你可以接受此建议（应用标签），或拒绝建议（不应用建议标签）。

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Azure 信息保护栏的异常 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>你的 Office 应用程序中看不到此信息保护栏？

可能的原因：

- 未[安装](install-client-app.md) Azure 信息保护客户端。

- 安装了客户端，但管理员配置的设置不显示信息保护栏。 可改为从 Office 功能区“文件”选项卡上的“保护”按钮选择标签。 

- 客户端正以[仅保护模式](client-protection-only-mode.md)运行。
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>没有显示希望看到的标签？ 

可能的原因：

- 如果管理员最近为你配置了新标签，请尝试关闭 Office 应用程序的所有实例，然后重新打开。 此操作将检查对你的标签所做的更改。

- 如果缺少应用保护的标签，那么可能你使用的 Office 版本不支持应用 Rights Management 保护。 若要验证，请单击 "**保护**  >  **帮助和反馈**"。 在对话框中，检查“客户端状态”部分中是否显示消息“此客户端未获许可使用 Office Professional Plus”。 
    
    如果你的 Office 应用 Microsoft 365 适用于企业的应用程序，Microsoft 365 商业版或者在为用户分配了 Azure (Rights Management 的许可证（也称为 Azure 信息保护 for Office 365) ），则不需要 Office Professional Plus。

- 此标签采用的作用域策略可能不包括你的帐户。 请与你的技术支持或管理员一起检查。

### <a name="set-custom-permissions-for-a-document"></a>设置文档的自定义权限

如果得到管理员的允许，可以指定你自己的文档保护设置，而不使用管理员可能已包含在所选标签中的保护设置。 此选项特定于文档，不适用于 Outlook。

1. 在“**开始**”选项卡上的“**保护**”组中，依次单击“**保护**” > “**自定义权限**”：

    ![自定义权限选项](../media/custom-permissions-callout.png)
    
    如果看不到“自定义权限”，则表示管理员禁止你使用此选项。
    
    请注意，你指定的任何自定义权限将替换（而不是补充）管理员可能已为选定标签定义的保护设置。  

2. 在“**Microsoft Azure 信息保护**”对话框中，指定以下内容：

    - **使用自定义权限进行保护**：请务必选中此选项，这样才能指定并应用自定义权限。 取消选中此选项即撤销任何自定义权限。
    
    - **选择权限**：如果要保护文件，以便只有你可以访问，请选中“**仅限自己访问**”。 否则，请选中“希望对象拥有的访问级别”。
    
    - **选择用户、组或组织**：指定哪些人应拥有你为一个或多个文件选择的权限。 键入他们的完整电子邮件地址、组电子邮件地址或相应组织中所有用户的组织域名。 
        
        此外，还可以使用“通讯簿”图标从 Outlook 通讯簿选择用户或组。
    
    - **过期访问**：仅为时间敏感的文件选择此选项，以使指定的人员无法在设置日期后打开选定的文件。 仍可以打开原始文件，但在设置日期的午夜（当前时区）过后，指定的人员将无法打开该文件。

5. 单击“**应用**”，然后等待“**已应用自定义权限**”消息。 然后单击 **“关闭”**。

### <a name="safely-sharing-by-email"></a>通过电子邮件实现安全共享

通过电子邮件共享 Office 文档时，可将文档附加到所保护的电子邮件中，应用到此电子邮件的相同限制会自动保护此文档。 

但是，我们建议首先保护文档，然后再将它附加到电子邮件中。 如果电子邮件中包含敏感信息，也需要保护电子邮件。 将文档附加到电子邮件前保护它有两个好处：

- 通过电子邮件发送文档后可以跟踪并根据需要撤消此文档。

- 可以对文档应用不同于电子邮件的权限。

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
    
3. 如果得到管理员的准许，则可自行指定保护设置，而不使用管理员可能在所选标签中随附的保护设置。 若要执行此操作，请选择“使用自定义权限进行保护”。
    
    如果看不到“使用自定义权限进行保护”，则表示管理员禁止你使用此选项。
    
    指定的任何自定义权限将替换而不是补充管理员可能已为所选标签定义的保护设置。  

4. 如果选择了 "自定义权限" 选项，请指定以下选项
    
    |选项  |说明  |
    |---------|---------|
    |**选择权限**     |    在保护所选文件时选择希望用户具有的访问级别。     |
    |**选择用户、组或组织**     |  指定应对文件具有选定权限的人员。 键入他们的完整电子邮件地址、组电子邮件地址或相应组织中所有用户的组织域名。 </br>或者，可以使用“通讯簿”图标从 Outlook 通讯簿选择用户或组。       |
    |**访问权限过期**     |  仅对具有时效性的文件选择此选项，使指定的人员无法在你设置的日期后打开所选的一个文件或多个文件。你仍然可以打开原始文件，但是在所设定日期的午夜后（当前时区），你指定的人员将无法打开文件。  <br><br>**注意**：如果以前使用 Office 2010 应用中的自定义权限配置此设置，则不会在此对话框中显示指定的到期日期，但仍会设置到期日期。 此显示问题仅适用于在 Office 2010 中配置了到期日期的情况。 <br><br>**重要提示**： Office 2010 扩展支持于2020年10月13日结束。 有关详细信息，请参阅 [AIP 和旧版 Windows 和 Office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。     |
    |     |         |


5. 单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。

根据你的选择，现已对所选择的一个或多个文件进行分类和保护。 在某些情况下（添加的保护更改了文件扩展名时），文件资源管理器中的原始文件将替换为具有 Azure 信息保护锁状图标的新文件。 例如：

![Azure 信息保护中具有锁状图标的受保护文件](../media/Pfile.png)

如果改变了有关分类和保护的想法，或稍后需要更改设置，仅需通过重复此过程进行新的设置。

指定的分类和保护会保留在文件中，即使你通过电子邮件发送文件或将其保存到其他位置也是如此。 如果已保护该文件，则可跟踪用户如何使用它，如果有必要，还可撤销对它的访问。 有关详细信息，请参阅[使用 Azure 信息保护时跟踪和撤销已保护的文档](client-track-revoke.md)。 


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

-   [您希望做什么？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
有关启用“让自定义权限选项可供用户使用”策略设置的配置说明，请参阅[配置 Azure 信息保护策略设置](../configure-policy-settings.md)。

其他配置说明：[配置 Azure 信息保护策略](../configure-policy.md)。