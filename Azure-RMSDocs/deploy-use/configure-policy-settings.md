---
title: "配置 Azure 信息保护策略设置"
description: "在 Azure 信息保护策略中配置适用于所有用户、所有设备的设置。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: 2bc5493c906b0d21be2679f0d777cb4fd5fbe30c
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>如何为 Azure 信息保护配置策略设置

>*适用于：Azure 信息保护*

除了信息保护栏标题和工具提示，Azure 信息保护策略中有一些设置适用于所有用户、所有设备：

![Azure 信息保护策略全局设置](../media/info-protect-policy-default-settingsv2.png)


配置这些设置：

1. 如果尚未执行此操作，请在新浏览器窗口中，以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要配置的设置将应用于所有用户，请选择“Azure 信息保护 - 全局策略”边栏选项卡。
    
    如果要配置的设置位于[作用域内策略](configure-policy-scope.md)中，仅应用于所选用户，请从“策略”菜单选项中选择“作用域内策略”。 然后从“Azure 信息保护 - 作用域内策略”边栏选项卡选择作用域内策略。

3. 从“Azure 信息保护 - 全局策略”边栏选项卡或“策略: \<名称>”边栏选项卡中，配置以下设置：
    
    - **所有文档和电子邮件都必须有标签**：此选项设置为“**打开**”时，所有已保存的文档和发送的电子邮件都必须应用标签。 标记可能由用户手动分配，或因[条件](configure-policy-classification.md)自动分配，或（通过设置“**选择默认标签**”选项）默认分配。 
        
        如果在用户保存文档或发送电子邮件时未分配标签，系统会提示用户选择一个标签。 例如：
        
        ![Azure 信息保护提示（如果强制实施了标记）](../media/info-protect-enforce-labelv2.png)
        
    - **选择默认标签**：当设置此选项时，选择标签以分配给没有标签的文档和电子邮件。 如果具有子标签，不能将标签设置为默认标签。 
        
    - **用户必须提供理由以设置较低分类标签、删除标签或删除保护**：此选项设置为“开”时，如果用户执行下列任一操作（例如，将“公共”标签更改为“个人”），则系统会提示用户提供此操作的理由。 例如，用户可能会解释该文档不再包含敏感信息。 在其本地 Windows 事件日志中记录他们的操作和理由：**应用程序** > **Microsoft Azure 信息保护**。  
        
        ![Azure 信息保护提示新分类是否较低](../media/info-protect-lower-justification.png)
        
        此选项不适用于子标签。
        
    - **对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签**：将此选项设置为“推荐”时，系统会提示用户将标签应用到其电子邮件中。 将基于应用于附件的分类标签动态选择标签，并选择最高等级的标签。 附件必须是物理文件，并且不能是指向文件的链接（例如，指向 SharePoint 或 OneDrive for Business 文件的链接）。 用户可接受或忽略该建议。 将此选项设置为“开”时，将自动应用该标签，但用户可以在发送电子邮件之前删除该标签或选择另一个标签。  

    - **为 Azure 信息保护客户端“告诉我详细信息”网页提供自定义 URL**：当用户在其 Office 应用程序中从“开始”选项卡选择“保护” > “帮助和反馈”时，将在“帮助和反馈”部分的“Microsoft Azure 信息保护”对话框中看到此链接。 默认情况下，此链接将转到 [Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection)网站。 如果希望此链接转到备选网页，可输入 HTTP 或 HTTPS（推荐）URL。 不进行检查来验证输入的自定义 URL 是否可供访问或是否可在所有设备上正确显示。
        
        例如，对于支持人员，输入的 Microsoft 文档页可包含有关安装和使用客户端的信息 (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) 或者有关发布版本的信息 (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**)。 另外，可以发布自己的网页，提供供用户联系支持人员的信息，或提供指导用户如何使用已配置标签的视频。

3. 单击“**保存**”以保存更改。

4. 若要使所做的更改适用于用户，请在初始“Azure 信息保护”边栏选项卡，单击“发布”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
