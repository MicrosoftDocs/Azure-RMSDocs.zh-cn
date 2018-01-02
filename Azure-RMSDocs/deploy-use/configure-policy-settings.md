---
title: "配置 Azure 信息保护策略设置"
description: "在 Azure 信息保护策略中配置适用于所有用户、所有设备的设置。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: 49eb10a999f541cb9979576faac55ca28ff35a0b
ms.sourcegitcommit: e089661f23f199b122b0ca9ba4748792b349bc27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2017
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>如何为 Azure 信息保护配置策略设置

>*适用于：Azure 信息保护*

除了信息保护栏标题和工具提示，Azure 信息保护策略中还有一些可以在标签中单独配置的设置：

![Azure 信息保护策略全局设置](../media/info-protect-policy-default-settingsv3.png)

请注意，策略设置的默认值可能不同，具体取决于购买 Azure 信息保护订阅的时间。 还可以使用[自定义客户端设置](../rms-client/client-admin-guide-customizations.md)进行某些设置。

配置这些设置：

1. 如果尚未执行此操作，请在新浏览器窗口中，以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要配置的设置将应用于所有用户，请选择“Azure 信息保护 - 全局策略”边栏选项卡。
    
    如果要配置的设置位于[作用域内策略](configure-policy-scope.md)中，仅应用于所选用户，请从“策略”菜单选项中选择“作用域内策略”。 然后从“Azure 信息保护 - 作用域内策略”边栏选项卡选择作用域内策略。

3. 从“Azure 信息保护 - 全局策略”边栏选项卡或“策略: \<名称>”边栏选项卡中，配置以下设置：
    
    - **选择默认标签**：当设置此选项时，选择标签以分配给没有标签的文档和电子邮件。 如果具有子标签，不能将标签设置为默认标签。 
    
    - **所有文档和电子邮件都必须有标签**：此选项设置为“**打开**”时，所有已保存的文档和发送的电子邮件都必须应用标签。 标记可能由用户手动分配，或因[条件](configure-policy-classification.md)自动分配，或（通过设置“**选择默认标签**”选项）默认分配。
        
        如果在用户保存文档或发送电子邮件时未分配标签，系统会提示用户选择一个标签。 例如：
        
        ![Azure 信息保护提示（如果强制实施了标记）](../media/info-protect-enforce-labelv2.png)
        
    - **用户必须提供理由以设置较低分类标签、删除标签或删除保护**：此选项设置为“开”时，如果用户执行下列任一操作（例如，将“公共”标签更改为“个人”），则系统会提示用户提供此操作的理由。 例如，用户可能会解释该文档不再包含敏感信息。 在其本地 Windows 事件日志中记录他们的操作和理由：“应用程序和服务日志” > “Azure 信息保护”。  
        
        ![Azure 信息保护提示新分类是否较低](../media/info-protect-lower-justification.png)
        
        此选项不适用于子标签。
        
    - **对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签**：将此选项设置为“推荐”时，系统会提示用户将标签应用到其电子邮件中。 将基于应用于附件的分类标签动态选择标签，并选择最高等级的标签。 附件必须是物理文件，并且不能是指向文件的链接（例如，指向 SharePoint 或 OneDrive for Business 文件的链接）。 用户可接受或忽略该建议。 将此选项设置为“开”时，将自动应用该标签，但用户可以在发送电子邮件之前删除该标签或选择另一个标签。  
    
    - **在 Office 应用中显示信息保护栏**：关闭此设置后，用户无法在 Word、Excel、PowerPoint 和 Outlook 中从信息保护栏选择标签。 在此情况下，用户必须通过功能区上的“保护”按钮选择标签。 打开此设置后，用户可以通过信息保护栏或“保护”按钮选择标签。
        
        > [!IMPORTANT]
        > 此设置在预览版中，且需要 Azure 信息保护客户端的当前预览版本。
        
        打开此设置后，可以将其与高级客户端设置配合使用，因此如果用户选择不显示该栏，可以[永久隐藏 Azure 信息保护栏](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)。 从“保护”按钮清除“显示信息保护栏”选项，即可实现此操作。
    
    - **向 Outlook 功能区添加“不转发”按钮**：打开此设置后，除了从 Outlook 菜单中选择“不转发”按钮之外，用户也可以从 Outlook 功能区上的“保护”组中选择此按钮。 若要帮助确保用户对其电子邮件进行分类和保护，可以首选不添加此标签，并改为[配置用于保护的标签](configure-policy-protection.md)和 Outlook 的用户定义权限。 此保护设置的功能与选择“不转发”按钮相同，但当此功能附带标签时，意味着对电子邮件进行了分类和保护。
    
        也可以使用高级客户端设置将此策略设置配置为[客户端自定义](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)。
    
    - **使用户可以使用自定义权限选项**：打开此设置后，用户可以设置自己的保护设置并替代标签配置所包括的任何保护设置。 关闭此设置后，用户无法选择自定义权限选项。
        
        > [!IMPORTANT]
        > 如果具有为 Word、Excel、PowerPoint 和文件资源管理器的用户定义权限配置的标签，除非使用当前预览版本的客户端，否则请勿使用“关闭”设置。 如果使用此选项，应用标签时，系统不会提示用户配置自定义权限。 结果是：标记文档，但并未按预期保护文档。
        
        请注意，此策略设置对用户可以通过 Office 菜单选项配置的自定义权限没有任何影响。 但是，也可以使用高级客户端设置将其配置为[客户端自定义](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)。
        
        自定义权限选项位于以下位置：
        
        - 在 Office 应用程序中：功能区中的“开始”选项卡 >“保护”组 >“保护” > “自定义权限”
        
        - 在文件资源管理器中：右键单击 >“分类并保护” > “自定义权限”
    
    - **为 Azure 信息保护客户端“告诉我详细信息”网页提供自定义 URL**：当用户在其 Office 应用程序中从“开始”选项卡选择“保护” > “帮助和反馈”时，将在“帮助和反馈”部分的“Microsoft Azure 信息保护”对话框中看到此链接。 默认情况下，此链接将转到 [Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection)网站。 如果希望此链接转到备选网页，可输入 HTTP 或 HTTPS（推荐）URL。 不进行检查来验证输入的自定义 URL 是否可供访问或是否可在所有设备上正确显示。
        
        例如，对于支持人员，输入的 Microsoft 文档页可包含有关安装和使用客户端的信息 (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) 或者有关发布版本的信息 (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**)。 另外，可以发布自己的网页，提供供用户联系支持人员的信息，或提供指导用户如何使用已配置标签的视频。

3. 单击“**保存**”以保存更改。

4. 若要使所做的更改适用于用户，请在初始“Azure 信息保护”边栏选项卡，单击“发布”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
