---
title: "如何配置全局策略设置 | Azure 信息保护"
description: "Azure 信息保护策略中有 3 个设置适用于所有用户、所有设备。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 8fa2ed9ff9ebe5c850ab5681e4dcc1f3d3c676b3
ms.openlocfilehash: de5f5fbddb84e4444751e9fefbfe6ec3fe3e45e4


---

# <a name="how-to-configure-the-global-policy-settings-for-azure-information-protection"></a>如何配置 Azure 信息保护的全局策略设置

>*适用于：Azure 信息保护*

Azure 信息保护策略中有 4 个设置适用于所有用户、所有设备：

![Azure 信息保护策略全局设置](../media/info-protect-policy-settings.png)


配置这些设置：

1. 如果尚未这样做，请在新的浏览器窗口中以全局管理员的身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在“**Azure 信息保护**”边栏选项卡上，配置这些全局设置：

    - **所有文档和电子邮件都必须有标签**：此选项设置为“**打开**”时，所有已保存的文档和发送的电子邮件都必须应用标签。 标记可能由用户手动分配，或因[条件](configure-policy-classification.md)自动分配，或（通过设置“**选择默认标签**”选项）默认分配。 

    如果在用户保存文档或发送电子邮件时未分配标签，系统会提示你选择一个标签：

    ![Azure 信息保护提示新分类是否较低](../media/info-protect-enforce-label.png)

    - **选择默认标签**：当设置此选项时，选择标签以分配给没有标签的文档和电子邮件。 如果具有子标签，不能将标签设置为默认标签。 

    - **用户必须提供理由以设置较低分类标签、删除标签或删除保护**：此选项设置为“开”时，如果用户执行下列任一操作（例如，将“秘密”更改为“个人”，则系统会提示用户提供此操作的理由。 例如，用户可能会解释该文档不再包含敏感信息。 在其本地 Windows 事件日志中记录他们的操作和理由：**应用程序** > **Microsoft Azure 信息保护**。  

    ![Azure 信息保护提示新分类是否较低](../media/info-protect-lower-justification.png)

    此选项不适用于子标签。

    - **为 Azure 信息保护客户端“告诉我详细信息”网页提供自定义 URL**：当用户在其 Office 应用程序中从“开始”选项卡选择“保护” > “帮助和反馈”时，将在“帮助和反馈”部分的“Microsoft Azure 信息保护”对话框中看到此链接。 默认情况下，此链接将转到 [Azure 信息保护](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection)网站。 如果希望此链接转到备选网页，可输入 HTTP 或 HTTPS（推荐）URL。 不进行检查来验证输入的自定义 URL 是否可供访问或是否可在所有设备上正确显示。
    
    例如，对于支持人员，输入的 Microsoft 文档页可包含有关安装和使用客户端的信息 (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) 或者有关发布版本的信息 (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**)。 另外，可以发布自己的网页，提供供用户联系支持人员的信息，或提供指导用户如何使用已配置标签的视频。

3. 单击“**保存**”以保存更改。

4. 若要使所做的更改应用于用户，请单击“**发布**”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  












<!--HONumber=Nov16_HO3-->


