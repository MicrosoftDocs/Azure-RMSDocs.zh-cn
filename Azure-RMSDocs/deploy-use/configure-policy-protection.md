---
title: "配置 Azure 信息保护标签以进行保护"
description: "通过配置标签来使用 Rights Management 保护，可保护最敏感的文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: 696d744ae21d8957225a24d39547493515b63d76
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>如何配置标签以进行 Rights Management 保护

>*适用于：Azure 信息保护*

你可以使用权限管理服务的加密、标识和授权策略保护最敏感的文档和电子邮件，以帮助防止数据丢失。 配置标签将 Rights Management 模板用于文档和电子邮件，或将“不要转发”选项用于 Outlook 电子邮件时，均会应用此保护。 

此模板可以是激活 Azure Rights Management 时自动创建的默认模板之一，也可以是自定义模板。 支持 Azure 权限管理部门模板，但仅当文档或电子邮件作者属于模板配置的作用域时应用保护。 如果用户不在作用域内，则会看到 Azure 信息保护不能应用标签的消息。

## <a name="how-the-protection-works"></a>保护的工作原理

当文档或电子邮件受权限管理保护时，它会在处于静态时和传输过程中进行加密，并且只能由授权用户进行解密。 文档或电子邮件的这种加密保持不变，即使将其重命名。 此外，你可以配置使用权限和限制，如下面的示例：

- 只有组织内的用户才能打开公司机密文档或电子邮件。

- 只有市场营销部门的用户才能编辑和打印促销通知文档或电子邮件，而组织中的所有其他用户只能阅读该文档或电子邮件。

- 用户不能转发包含内部重组相关新闻的电子邮件。

- 不能在指定日期后打开发送给业务合作伙伴的当前价目表。

有关 Azure 权限管理模板以及如何配置这些使用权限和限制的详细信息，请参阅[为 Azure 权限管理服务配置自定义模板](../deploy-use/configure-custom-templates.md)。

有关 Azure 权限管理及其工作原理的详细信息，请参阅 [什么是 Azure 权限管理？](../understand-explore/what-is-azure-rms.md)(#什么是-azure-权限管理？)

> [!IMPORTANT]
> 若要配置标签以应用 Azure 权限管理保护，必须为组织激活 Azure 权限管理服务。 如果尚未这样做，请参阅 [激活 Azure 权限管理](../deploy-use/activate-service.md)(#激活-azure-权限管理)。

用户可以在 Outlook 中应用标签以保护其电子邮件之前，不必为信息权限管理 (IRM) 配置 Exchange。 但是，在为 IRM 配置 Exchange 之前，你无法获得将 Exchange 与Azure Rights Management 保护配合使用的完整功能。 例如，用户无法在移动电话上或通过 Outlook Web Access 查看受保护的电子邮件，无法将受保护的电子邮件编入索引用于搜索，并且你无法为权限管理保护配置 Exchange Online DLP。 若要将 Exchange 配置为支持这些其他的方案，请参阅以下资源：

- 对于 Exchange Online，请参阅 [Exchange Online：IRM 配置](../deploy-use/configure-office365.md#exchange-online-irm-configuration)简介。

- 对于 Exchange 内部部署，必须部署 [RMS 连接器并配置 Exchange 服务器](../deploy-use/deploy-rms-connector.md)。 


## <a name="to-configure-a-label-for-rights-management-protection"></a>配置权限管理保护标签的具体步骤

1. 如果尚未这样做，请打开一个新的浏览器窗口并以全局管理员的身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 

    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要配置的标签将应用于所有用户，请选择“**Azure 信息保护**”边栏选项卡中“**全局**”。 不过，如果要配置的标签包含在[限定范围的策略](configure-policy-scope.md)中，以便仅应用于选定用户，请改为选择限定范围的相应策略。

3. 在“**策略**”边栏选项卡上，选择要配置的标签。此时，系统会打开“**标签**”边栏选项卡。 

4. 在“**标签**”边栏选项卡上，找到“为包含此标签的文档和电子邮件设置权限”并选择以下选项之一。
    
    - **未配置**：如果标签当前配置为应用保护，而你不再需要所选的标签应用保护，请选择此选项。 然后转到步骤 10。
    
    - **保护**：选择此选项应用保护，然后转到步骤 5。
    
    - **删除保护**：如果已为文档或电子邮件配置保护，选择此选项可删除保护。 然后转到步骤 10。
        
        请注意，用户必须具有删除 Rights Management 保护的权限，才能应用具有此选项的标签。 此选项要求用户具有**导出**或**完全控制**[使用权限](../deploy-use/configure-usage-rights.md)，或者为 Rights Management 所有者（自动授予完全控制使用权限）或者为 [Azure Rights Management 的超级用户](../deploy-use/configure-super-users.md)。 默认 Azure Rights Management 模板不包括允许用户删除保护的使用权限。 
        
        如果用户不具有删除 Rights Management 保护的权限，并选择使用此“删除保护”选项配置的标签，他们将会看到以下消息：**Azure 信息保护无法应用此标签。如果此问题仍然存在，请与管理员联系。**

5. 如果已选择“保护”，现在请选择“保护”将“保护”边栏选项卡打开：
    
    ![为 Azure 信息保护标签配置保护权限](../media/info-protect-protection-bar.png)

6. 在“保护”边栏选项卡上，选择“Azure RMS”或“HYOK (AD RMS)”。 
    
    大多数情况下，你会为权限设置选择“**Azure RMS**”。 请勿选择“**HYOK (AD RMS)**”，除非你已阅读并了解此“*自留密钥*”(HYOK) 配置随附的先决条件和限制。 有关详细信息，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](configure-adrms-restrictions.md)。 若要继续配置 HYOK (AD RMS)，请转到步骤 9。
    
7. 选择“**不要转发**”（如果要为电子邮件设置此 Outlook 选项的话）或“**选择模板**”。 
    
8. 如果为“**Azure RMS**”选择了“**选择模板**”，请单击下拉框，然后选择要用于保护包含此标签的文档和电子邮件的[模板](../deploy-use/configure-custom-templates.md)。
    
    如果选择**部门模板**，或者如果已配置[载入控件](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)：
    
    - 配置的模板作用域外的用户或从应用 Azure 权限管理保护中排除的用户仍将看到该标签，但不能应用该标签。 如果他们选择该标签，则会看到以下消息：**Azure 信息保护无法应用此标签。如果此问题仍然存在，请与管理员联系。**
    
        请注意，将始终显示所有模板，即使正在配置作用域内策略。 例如，正在为市场营销组配置作用域内策略。 可选择的 Azure RMS 模板不限于作用域为“营销”组的模板，还可以选择所选用户不能使用的部门模板。 为了方便配置和尽量减少故障排除，请考虑命名部门模板以匹配作用域内策略中的标签。 
            
9. 如果为“**HYOK (AD RMS)**”选择了“**选择模板**”，请提供 AD RMS 群集的模板 GUID 和授权 URL。 [详细信息](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

10. 单击“确定”关闭“保护”边栏选项卡，然后“标签”边栏选项卡上的“保护”选项中会显示你选择的“不要转发”或模板。

10. 在“**标签**”边栏选项卡上，单击“**保存**”。

11. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]