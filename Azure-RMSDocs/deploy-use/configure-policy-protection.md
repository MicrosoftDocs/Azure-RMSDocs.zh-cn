---
title: "配置 Azure 信息保护标签以进行保护"
description: "通过配置标签来使用 Rights Management 保护，可保护最敏感的文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: fda1cf5bf39bcacb26bff528f4011d9fbb21f9e5
ms.sourcegitcommit: 869e42f35a851c412164a71b1f657621af07b2f5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2017
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>如何配置标签以进行 Rights Management 保护

>适用于：Azure 信息保护

可通过使用 Rights Management 服务保护最敏感的文档和电子邮件。 此服务使用加密、标识和身份验证策略，有助于防止数据丢失。 配置标签将 Rights Management 保护用于文档和电子邮件，或将“不要转发”选项用于 Outlook 电子邮件时，均会应用此保护。 

## <a name="how-the-protection-works"></a>保护的工作原理

当文档或电子邮件受权限管理保护时，它会在处于静态时和传输过程中进行加密，并且只能由授权用户进行解密。 文档或电子邮件的这种加密保持不变，即使将其重命名。 此外，你可以配置使用权限和限制，如下面的示例：

- 只有组织内的用户才能打开公司机密文档或电子邮件。

- 只有市场营销部门的用户才能编辑和打印促销通知文档或电子邮件，而组织中的所有其他用户只能阅读该文档或电子邮件。

- 用户不能转发包含内部重组相关新闻的电子邮件或从中复制信息。

- 不能在指定日期后打开发送给业务合作伙伴的当前价目表。

有关 Azure 权限管理模板的详细信息，请参阅[在 Azure 信息保护策略中配置和管理模板](../deploy-use/configure-policy-templates.md)。

有关 Azure 权限管理及其工作原理的详细信息，请参阅 [什么是 Azure 权限管理？](../understand-explore/what-is-azure-rms.md)(#什么是-azure-权限管理？)

> [!IMPORTANT]
> 若要配置标签以应用 Azure 权限管理保护，必须为组织激活 Azure 权限管理服务。 如果尚未这样做，请参阅 [激活 Azure 权限管理](../deploy-use/activate-service.md)(#激活-azure-权限管理)。

标签应用保护时，受保护的文档不适合保存在 SharePoint 或 OneDrive 中。 对于受保护的文件，这些位置不支持以下内容：共同创作、Office Online、搜索、文档预览、缩略图和电子数据展示。 

用户可以在 Outlook 中应用标签以保护其电子邮件之前，不必为信息权限管理 (IRM) 配置 Exchange。 但是，在为 IRM 配置 Exchange 之前，你无法获得将 Exchange 与Azure Rights Management 保护配合使用的完整功能。 例如，用户无法在移动电话上或通过 Outlook 网页版查看受保护的电子邮件，无法将受保护的电子邮件编入索引用于搜索，并且你无法为权限管理保护配置 Exchange Online DLP。 若要将 Exchange 配置为支持这些其他的方案，请参阅以下资源：

- 对于 Exchange Online，请参阅 [Exchange Online：IRM 配置](../deploy-use/configure-office365.md#exchange-online-irm-configuration)简介。

- 对于 Exchange 内部部署，必须部署 [RMS 连接器并配置 Exchange 服务器](../deploy-use/deploy-rms-connector.md)。 

## <a name="to-configure-a-label-for-rights-management-protection"></a>配置权限管理保护标签的具体步骤

1. 如果尚未执行此操作，请打开新的浏览器窗口并以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 

    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要配置的标签将应用于所有用户，请选择初始“Azure 信息保护”边栏选项卡中的“全局策略”。 但是，如果要配置的标签位于[作用域内策略](configure-policy-scope.md)中，以便仅应用于所选用户，请改为选择“作用域内策略”，并从“Azure 信息保护 - 作用域内策略”边栏选项卡中选择作用域内策略。

3. 在“**策略**”边栏选项卡上，选择要配置的标签。此时，系统会打开“**标签**”边栏选项卡。 

4. 在“标签”边栏选项卡上，找到“为包含此标签的文档和电子邮件设置权限”并选择以下选项之一：
    
    - **未配置**：如果标签当前配置为应用保护，而你不再需要所选的标签应用保护，请选择此选项。 然后转到步骤 11。
    
    - **保护**：选择此选项应用保护，然后转到步骤 5。
    
    - **删除保护**：如果已为文档或电子邮件配置保护，选择此选项可删除保护。 然后转到步骤 11。
        
        请注意，用户必须具有删除 Rights Management 保护的权限，才能应用具有此选项的标签。 此选项要求用户具有“导出”或“完全控制”[使用权限](../deploy-use/configure-usage-rights.md)。 或者，他们必须为 Rights Management 所有者（自动授予完全控制使用权限）或者为 [Azure 权限管理的超级用户](../deploy-use/configure-super-users.md)。 默认 Azure 权限管理模板不包括允许用户删除保护的使用权限。 
        
        如果用户不具有删除 Rights Management 保护的权限，并选择使用此“删除保护”选项配置的标签，他们将会看到以下消息：**Azure 信息保护无法应用此标签。如果此问题仍然存在，请与管理员联系。**

5. 如果已选择“保护”，现在请选择“保护”将“保护”边栏选项卡打开：
    
    ![为 Azure 信息保护标签配置保护权限](../media/info-protect-protection-bar.png)

6. 在“保护”边栏选项卡上，选择“Azure RMS”或“HYOK (AD RMS)”。 
    
    大多数情况下，为权限设置选择“Azure RMS”。 请勿选择“**HYOK (AD RMS)**”，除非你已阅读并了解此“*自留密钥*”(HYOK) 配置随附的先决条件和限制。 有关详细信息，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](configure-adrms-restrictions.md)。 若要继续配置 HYOK (AD RMS)，请转到步骤 10。
    
7. 选择下列选项之一：
    
    - 不转发：为电子邮件设置此 Outlook 选项。
    
    - 选择预定义的模板：使用已配置的一个默认模板或自定义模板。 此模板必须为已发布（未存档），且必须未链接到另一个标签。
    
    - “设置权限”以在此门户中定义新的保护设置。

8. 如果为“Azure RMS”选择了“选择预配模板”，请单击下拉框，然后选择要用于保护包含此标签的文档和电子邮件的[模板](../deploy-use/configure-policy-templates.md)。 看不到已存档的模板或已为另一个标签选择的模板。
    
    如果选择“部门模板”，或者如果已配置[载入控件](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)：
    
    - 配置的模板作用域外的用户或从应用 Azure 权限管理保护中排除的用户仍将看到该标签，但不能应用该标签。 如果他们选择该标签，则会看到以下消息：**Azure 信息保护无法应用此标签。如果此问题仍然存在，请与管理员联系。**
    
        请注意，将始终显示所有已发布的模板，即使正在配置作用域内策略。 例如，正在为市场营销组配置作用域内策略。 可选择的 Azure RMS 模板不限于作用域为“营销”组的模板，还可以选择所选用户不能使用的部门模板。 为了方便配置和尽量减少故障排除，请考虑命名部门模板以匹配作用域内策略中的标签。 
            
9. 如果为“Azure RMS”选择“设置权限”，此选项将允许配置可在模板中配置的相同设置。 
    
    选择“添加权限”，在“添加权限”边栏选项卡上，选择有权使用所选标签保护的内容的第一组用户和组：
    
    - 选择“从列表中选择”以添加组织中的所有用户或浏览目录。
        
        用户或组必须有电子邮件地址。 在生产环境中，他们几乎都有电子邮件地址，但在简单的测试环境中，可能需要为用户帐户或组添加电子邮件地址。
        
    - 选择“输入详细信息”以手动为单个用户或组（内部或外部）指定电子邮件地址。 或者，通过输入另一个组织的域名来指定该组织中的所有用户。 
        
    >[!NOTE]
    >如果在选择用户或组后某个电子邮件地址发生更改，请参阅计划文档中的[电子邮件地址发生更改情况下的注意事项](../plan-design/prepare.md#considerations-for-azure-information-protection-if-email-addresses-change)部分。
    
    最佳做法是使用组，而不是使用用户。 此策略可简化配置，且可降低以后更新标签配置并重新保护内容的可能性。 但是，如果对组进行更改则请注意，出于性能原因，Azure 权限管理[将缓存组成员身份](../plan-design/prepare.md#group-membership-caching-by-azure-rights-management )。 
    
    指定第一组用户和组后，选择要授予这些用户和组的权限。 若要深入了解可选择的权限，请参阅 [为 Azure 权限管理配置使用权限](configure-usage-rights.md)。 但是，支持此保护的应用程序可能在实现这些权限的方式方面有所不同。 请查阅其文档，并在为用户部署模板之前，对用户使用的应用程序执行自己的测试以检查其行为。
    
    如有必要，现在可以添加另一组具有使用权限的用户和组。 重复此操作，直到指定所有用户和组及其各自的权限。

    >[!TIP]
    >请考虑添加“复制和提取内容”自定义权限，并向数据恢复管理员或其他拥有信息恢复职责的人员授予此权限。 如有必要，这些用户可删除要使用此标签或模板保护的文件和电子邮件中的保护。 这种可以在权限级别删除对文档或电子邮件的保护的功能可提供比[超级用户功能](configure-super-users.md)更精细的控制。
    
    对于指定的所有用户和组，在“保护”边栏选项卡上，立即检查是否想要对以下设置进行任何更改。 请注意，这些设置和权限一样，它们并不适用于 [Rights Management 颁发者或 Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)，也不适用于任何已分配的[超级用户](configure-super-users.md)。
    
    |Setting|更多信息|推荐设置
    |-----------|--------------------|--------------------|
    |**内容过期时间**|为此模板定义一个日期或天数，在此期间受模板保护的文档或电子邮件不应针对选中的用户打开。 你可以指定一个日期，也可以指定对内容应用保护后所经历的天数。<br /><br />如果你指定一个日期，它将在你当前时区的午夜生效。|除非内容具有特定的时间限制要求，否则**内容永不过期**。|
    |**允许脱机访问**|使用此设置在你的任何安全需求（包括吊销后的访问权限）与所选用户在没有 Internet 连接的情况下是否能够打开受保护的内容之间实现平衡。<br /><br />如果你指定内容在没有 Internet 连接的情况下不可用，或者指定内容仅在指定天数内可用，则在到达该阈值时，这些用户必须重新进行身份验证，他们的访问也将被记录。 发生这种情况时，如果用户的凭据不缓存，他们会收到提示，指示登录后才能打开文档或电子邮件。<br /><br />除了重新进行身份验证之外，还会重新评估策略和用户组成员身份。 这意味着，如果策略或组成员身份相比用户上一次访问文档或电子邮件时发生变化，则他们可能获得与上一次访问相同内容时不同的访问结果。 如果文档已被[撤销](../rms-client/client-track-revoke.md)，则可能不包含访问权限。|取决于内容的敏感程度：<br /><br />- **在没有 Internet 连接的情况下内容的可用天数** = **7**用于如果与未经授权的人员共享可能导致业务损失的敏感业务数据。 此建议提供灵活性和安全性之间的平衡折中。 例如合同、安全报告、预测摘要和销售客户数据。<br /><br />- **禁止访问**对于高度敏感的业务数据，如果与未经授权的人员共享将会导致业务损失。 此建议优先考虑安全性而不是灵活性，并确保一旦文档被撤销，那么所有授权用户都无法打开文档。 例如员工和客户信息、密码、源代码和预先公布的财务报表。|
    
    完成权限配置后，单击“确定” 。 
    
    此设置分组为 Azure 权限管理服务创建一个自定义模板。 这些模板可用于与 Azure 权限管理集成的应用程序和服务。 有关计算机和服务如何下载并刷新这些模板的信息，请参阅[为用户和服务刷新模板](refresh-templates.md)。

10. 如果为“HYOK (AD RMS)”选择了“选择预定义模板”：请提供 AD RMS 群集的模板 GUID 和授权 URL。 [详细信息](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

11. 单击“确定”关闭“保护”边栏选项卡，然后“标签”边栏选项卡上的“保护”选项中会显示你选择的“不要转发”或模板。

12. 在“**标签**”边栏选项卡上，单击“**保存**”。

13. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]