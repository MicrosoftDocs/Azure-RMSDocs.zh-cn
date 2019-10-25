---
title: 配置 Azure 信息保护策略设置 - AIP
description: 在 Azure 信息保护策略中配置适用于所有用户、所有设备的设置。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/29/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 9d4d3dfe2ccba6bf3f1f2aa46098e02e6a9a514d
ms.sourcegitcommit: afc3b5a5823c79873c822ef9274db0d29ccd5c13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72447159"
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>如何为 Azure 信息保护配置策略设置

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> *适用于[Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

> [!NOTE]
> 这些说明适用于 Azure 信息保护客户端（经典版），而不是 Azure 信息保护统一标记客户端。 不确定这些客户端之间有何区别？ 请参见[常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)。
> 
> 如果你正在寻找信息来为统一标签客户端配置策略设置，请参阅 Office 文档。 例如，[敏感度标签概述](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)。

除了信息保护栏标题和工具提示，Azure 信息保护策略中还有一些可以在标签中单独配置的设置：

![Azure 信息保护策略全局设置](./media/defaultsettings-aip.png)

请注意，策略设置的默认值可能不同，具体取决于购买 Azure 信息保护订阅的时间。 还可以使用[自定义客户端设置](./rms-client/client-admin-guide-customizations.md)进行某些设置。

配置这些设置：

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“分类” > “策略”菜单选项：在“Azure 信息保护 - 策略”边栏选项卡上，如果要配置的设置将应用于所有用户，请选择“全局”。
    
    如果要配置的设置位于[作用域内策略](configure-policy-scope.md)中，为了使其仅应用于所选用户，请改为选择你的作用域内策略。

3. 在“策略”边栏选项卡上，配置以下设置：
    
   - **选择默认标签**：当设置此选项时，选择标签以分配给没有标签的文档和电子邮件。 如果具有子标签，则不能将标签设置为默认标签。
        
        此设置适用于 Office 应用和扫描程序。 不适用于文件资源管理器或 PowerShell。
    
    - **将审核数据发送到 Azure 信息保护分析**：创建 azure[信息分析](reports-aip.md)的 azure Log Analytics 工作区之前，此设置的值显示为 "已**关闭**" 和 "**未配置**"。 创建工作区时，值将更改为“关闭”和“打开”。
        
        当设置为**On**时，支持集中报表的客户端将数据发送到 Azure 信息保护服务。 此信息包括应用的标签、用户选择具有较低分类的标签或删除标签。 有关发送和存储的信息的详细信息，请参阅中央报表文档中的[收集和发送到 Microsoft](reports-aip.md#information-collected-and-sent-to-microsoft)部分。 将此策略设置设置为 "**关闭**" 可阻止发送此数据。
    
    - **所有文档和电子邮件都必须有标签**：此选项设置为“**打开**”时，所有已保存的文档和发送的电子邮件都必须应用标签。 标记可能由用户手动分配，或因[条件](configure-policy-classification.md)自动分配，或（通过设置“**选择默认标签**”选项）默认分配。
        
       如果在用户保存文档或发送电子邮件时未分配标签，系统会提示用户选择一个标签。 例如：
        
       ![Azure 信息保护提示（如果强制实施了标记）](./media/info-protect-enforce-labelv2.png)
        
       使用带有 RemoveLabel 参数的 [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) PowerShell cmdlet 删除标签时，此选项不适用。
        
   - **用户必须提供理由以设置较低分类标签、删除标签或删除保护**：此选项设置为“开”时，如果用户执行下列任一操作（例如，将“公共”标签更改为“个人”），则系统会提示用户提供此操作的理由。 例如，用户可能会解释该文档不再包含敏感信息。 操作和相应的理由会记录在其本地 Windows 事件日志中：“应用程序和服务日志” > “Azure 信息保护”。  
        
       ![Azure 信息保护提示新分类是否较低](./media/info-protect-lower-justification.png)
        
       此选项不适用于降低同一父标签下子标签的分类。
        
   - **对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签**：将此选项设置为“推荐”时，系统会提示用户将标签应用到其电子邮件中。 将基于应用于附件的分类标签动态选择标签，并选择最高等级的标签。 附件必须是物理文件，并且不能是指向文件的链接（例如，指向 SharePoint 或 OneDrive for Business 文件的链接）。 用户可接受或忽略该建议。 将此选项设置为“自动”时，将自动应用该标签，但用户可以在发送电子邮件之前删除该标签或选择另一个标签。
        
        要在使用此策略设置时考虑子标签的排序，必须[配置高级客户端设置](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)。
        
        如果将具有最高分类标签的附件配置为通过用户定义的权限的预览设置进行保护，则为; 如果标签的用户定义权限包括 Outlook （不要转发），则应用该标签且不转发保护应用于电子邮件。 当标签的用户定义权限仅适用于 Word、Excel、PowerPoint 和文件资源管理器时，该标签不会应用于电子邮件，也不会受到保护。
    
   - **在 Office 应用中显示信息保护栏**：关闭此设置后，用户无法在 Word、Excel、PowerPoint 和 Outlook 中从信息保护栏选择标签。 在此情况下，用户必须通过功能区上的“保护”按钮选择标签。 打开此设置后，用户可以通过信息保护栏或“保护”按钮选择标签。
        
       打开此设置后，可以将其与高级客户端设置配合使用，因此如果用户选择不显示该栏，可以[永久隐藏 Azure 信息保护栏](./rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)。 从“保护”按钮清除“显示信息保护栏”选项，即可实现此操作。
    
   - **向 Outlook 功能区添加“不转发”按钮**：打开此设置后，除了从 Outlook 菜单中选择“不转发”按钮之外，用户也可以从 Outlook 功能区上的“保护”组中选择此按钮。 为了帮助确保用户对电子邮件进行分类并对其进行保护，你可能更倾向于不添加此按钮，而是[配置一个用于保护的标签](configure-policy-protection.md)和一个适用于 Outlook 的用户定义权限。 此保护设置的功能与选择“不转发”按钮相同，但当此功能附带标签时，意味着对电子邮件进行了分类和保护。
    
       也可以使用高级客户端设置将此策略设置配置为[客户端自定义](./rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)。
    
   - **让自定义权限选项可供用户使用**：启用此设置后，用户会看到用于自行设定保护设置的选项，这些设置能够替代标签配置可能自带的任何保护设置。 用户还能看到一个用于删除保护的选项。 关闭此设置后，用户不再看到这些选项。
        
       请注意，此策略设置对用户可以通过 Office 菜单选项配置的自定义权限没有任何影响。 但是，也可以使用高级客户端设置将其配置为[客户端自定义](./rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)。
        
       自定义权限选项位于以下位置：
        
       - 在 Office 应用程序中：功能区中的“开始”选项卡 >“保护”组 >“保护” > “自定义权限”
        
       - 在文件资源管理器中：右键单击 >“分类并保护” > “自定义权限”
    
   - **为 Azure 信息保护客户端“告诉我详细信息”网页提供自定义 URL**：当用户在其 Office 应用程序中从“开始”选项卡选择“保护” > “帮助和反馈”时，将在“帮助和反馈”部分的“Microsoft Azure 信息保护”对话框中看到此链接。 默认情况下，此链接将转到 [Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection)网站。 如果希望此链接转到备选网页，可输入 HTTP 或 HTTPS（推荐）URL。 不进行检查来验证输入的自定义 URL 是否可供访问或是否可在所有设备上正确显示。
        
       例如，对于技术支持，你可以输入 Microsoft 文档页，其中包含有关安装和使用客户端的信息： `https://docs.microsoft.com/information-protection/rms-client/info-protect-client`。 或发布版本信息： `https://docs.microsoft.com/information-protection/rms-client/client-version-release-history`。 另外，可以发布自己的网页，提供供用户联系支持人员的信息，或提供指导用户如何使用已配置标签的视频。

4. 若要保存所做的更改并将它们提供给用户，请单击“保存”。

单击“保存”时，更改将会自动提供给用户和服务。 不再提供单独发布选项。

## <a name="next-steps"></a>后续步骤

若要查看其中某些策略设置如何协同工作，请尝试学习[配置协同工作的 Azure 信息保护策略设置](infoprotect-settings-tutorial.md)教程。

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。

