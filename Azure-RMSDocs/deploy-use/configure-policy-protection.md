---
title: "配置 Azure 信息保护标签以进行保护"
description: "通过配置标签来使用 Rights Management 保护，可保护最敏感的文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: f5c4e2f7513832a884820ec0c57c7da2dec5f04e
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2017
---
<a id="how-to-configure-a-label-for-rights-management-protection" class="xliff"></a>

# 如何配置标签以进行 Rights Management 保护

>*适用于：Azure 信息保护*

你可以使用权限管理服务的加密、标识和授权策略保护最敏感的文档和电子邮件，以帮助防止数据丢失。 配置标签将 Rights Management 模板用于文档和电子邮件，或将“不要转发”选项用于 Outlook 电子邮件时，均会应用此保护。 

此模板可以是激活 Azure Rights Management 时自动创建的默认模板之一，也可以是自定义模板。 支持 Azure 权限管理部门模板，但仅当文档或电子邮件作者属于模板配置的作用域时应用保护。 如果用户不在作用域内，则会看到 Azure 信息保护不能应用标签的消息。

<a id="how-the-protection-works" class="xliff"></a>

## 保护的工作原理

当文档或电子邮件受权限管理保护时，它会在处于静态时和传输过程中进行加密，并且只能由授权用户进行解密。 文档或电子邮件的这种加密保持不变，即使将其重命名。 此外，你可以配置使用权限和限制，如下面的示例：

- 只有组织内的用户才能打开公司机密文档或电子邮件。

- 只有市场营销部门的用户才能编辑和打印促销通知文档或电子邮件，而组织中的所有其他用户只能阅读该文档或电子邮件。

- 用户不能转发包含内部重组相关新闻的电子邮件或从中复制信息。

- 不能在指定日期后打开发送给业务合作伙伴的当前价目表。

有关 Azure 权限管理模板以及如何在 Azure 经典门户中对其进行配置的详细信息，请参阅[为 Azure 权限管理服务配置自定义模板](../deploy-use/configure-custom-templates.md)。

有关 Azure 权限管理及其工作原理的详细信息，请参阅 [什么是 Azure 权限管理？](../understand-explore/what-is-azure-rms.md)(#什么是-azure-权限管理？)

> [!IMPORTANT]
> 若要配置标签以应用 Azure 权限管理保护，必须为组织激活 Azure 权限管理服务。 如果尚未这样做，请参阅 [激活 Azure 权限管理](../deploy-use/activate-service.md)(#激活-azure-权限管理)。

用户可以在 Outlook 中应用标签以保护其电子邮件之前，不必为信息权限管理 (IRM) 配置 Exchange。 但是，在为 IRM 配置 Exchange 之前，你无法获得将 Exchange 与Azure Rights Management 保护配合使用的完整功能。 例如，用户无法在移动电话上或通过 Outlook 网页版查看受保护的电子邮件，无法将受保护的电子邮件编入索引用于搜索，并且你无法为权限管理保护配置 Exchange Online DLP。 若要将 Exchange 配置为支持这些其他的方案，请参阅以下资源：

- 对于 Exchange Online，请参阅 [Exchange Online：IRM 配置](../deploy-use/configure-office365.md#exchange-online-irm-configuration)简介。

- 对于 Exchange 内部部署，必须部署 [RMS 连接器并配置 Exchange 服务器](../deploy-use/deploy-rms-connector.md)。 


<a id="to-configure-a-label-for-rights-management-protection" class="xliff"></a>

## 配置权限管理保护标签的具体步骤

1. 如果尚未执行此操作，请打开新的浏览器窗口并以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 

    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果要配置的标签将应用于所有用户，请选择“**Azure 信息保护**”边栏选项卡中“**全局**”。 不过，如果要配置的标签包含在[限定范围的策略](configure-policy-scope.md)中，以便仅应用于选定用户，请改为选择限定范围的相应策略。

3. 在“**策略**”边栏选项卡上，选择要配置的标签。此时，系统会打开“**标签**”边栏选项卡。 

4. 在“**标签**”边栏选项卡上，找到“为包含此标签的文档和电子邮件设置权限”并选择以下选项之一。
    
    - **未配置**：如果标签当前配置为应用保护，而你不再需要所选的标签应用保护，请选择此选项。 然后转到步骤 11。
    
    - **保护**：选择此选项应用保护，然后转到步骤 5。
    
    - **删除保护**：如果已为文档或电子邮件配置保护，选择此选项可删除保护。 然后转到步骤 11。
        
        请注意，用户必须具有删除 Rights Management 保护的权限，才能应用具有此选项的标签。 此选项要求用户具有**导出**或**完全控制**[使用权限](../deploy-use/configure-usage-rights.md)，或者为 Rights Management 所有者（自动授予完全控制使用权限）或者为 [Azure Rights Management 的超级用户](../deploy-use/configure-super-users.md)。 默认 Azure Rights Management 模板不包括允许用户删除保护的使用权限。 
        
        如果用户不具有删除 Rights Management 保护的权限，并选择使用此“删除保护”选项配置的标签，他们将会看到以下消息：**Azure 信息保护无法应用此标签。如果此问题仍然存在，请与管理员联系。**

5. 如果已选择“保护”，现在请选择“保护”将“保护”边栏选项卡打开：
    
    ![为 Azure 信息保护标签配置保护权限](../media/info-protect-protection-bar.png)

6. 在“保护”边栏选项卡上，选择“Azure RMS”或“HYOK (AD RMS)”。 
    
    大多数情况下，你会为权限设置选择“**Azure RMS**”。 请勿选择“**HYOK (AD RMS)**”，除非你已阅读并了解此“*自留密钥*”(HYOK) 配置随附的先决条件和限制。 有关详细信息，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](configure-adrms-restrictions.md)。 若要继续配置 HYOK (AD RMS)，请转到步骤 10。
    
7. 选择下列选项之一：
    
    - 不转发：为电子邮件设置此 Outlook 选项。
    
    - 选择预定义的模板：使用已配置的一个默认模板或自定义模板。
    
    - 设置权限（预览）以在此门户中定义新的保护设置。

8. 如果为 Azure RMS 选择了“选择预配模板”，请单击下拉框，然后选择要用于保护包含此标签的文档和电子邮件的[模板](../deploy-use/configure-custom-templates.md)。
    
    如果选择**部门模板**，或者如果已配置[载入控件](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)：
    
    - 配置的模板作用域外的用户或从应用 Azure 权限管理保护中排除的用户仍将看到该标签，但不能应用该标签。 如果他们选择该标签，则会看到以下消息：**Azure 信息保护无法应用此标签。如果此问题仍然存在，请与管理员联系。**
    
        请注意，将始终显示所有模板，即使正在配置作用域内策略。 例如，正在为市场营销组配置作用域内策略。 可选择的 Azure RMS 模板不限于作用域为“营销”组的模板，还可以选择所选用户不能使用的部门模板。 为了方便配置和尽量减少故障排除，请考虑命名部门模板以匹配作用域内策略中的标签。 
            
9. 如果为 Azure RMS 选择了“设置权限（预览）”，则此选项具有[自定义模板](configure-custom-templates.md)的大部分配置选项，你可以在 Azure 经典门户中对其进行配置。 此外，可轻松添加组织中的所有用户，并在指定域名时，为单个用户或组，或为其他组织中的所有用户指定外部电子邮件地址。 
    
    有关此预览配置的详细信息，请参阅博客文章 [Azure Information Protection unified administration now in Preview](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/)（当前预览中的 Azure 信息保护统一管理）。 
    
    若要深入了解可选择的权限，请参阅 [为 Azure 权限管理配置使用权限](configure-usage-rights.md)。
    
    包含在“设置权限（预览版）”选项中，确认你是否要对以下设置进行任何更改。 请注意，这些设置和权限一样，它们并不适用于 [Rights Management 颁发者或 Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)，也不适用于任何已分配的[超级用户](configure-super-users.md)。
    
    |Setting|更多信息|推荐设置
    |-----------|--------------------|--------------------|
    |**内容过期时间**|为此模板定义一个日期或天数，在此期间受模板保护的文档或电子邮件不应针对选中的用户打开。 你可以指定一个日期，也可以指定对内容应用保护后所经历的天数。<br /><br />如果你指定一个日期，它将在你当前时区的午夜生效。|除非内容具有特定的时间限制要求，否则**内容永不过期**。|
    |**允许脱机访问**|使用此设置在你的任何安全需求（包括吊销后的访问权限）与所选用户在没有 Internet 连接的情况下是否能够打开受保护的内容之间实现平衡。<br /><br />如果你指定内容在没有 Internet 连接的情况下不可用，或者指定内容仅在指定天数内可用，则在到达该阈值时，这些用户必须重新进行身份验证，他们的访问也将被记录。 发生这种情况时，如果用户的凭据不缓存，他们会收到提示，指示登录后才能打开文档或电子邮件。<br /><br />除了重新进行身份验证之外，还会重新评估策略和用户组成员身份。 这意味着，如果策略或组成员身份相比用户上一次访问文档或电子邮件时发生变化，则他们可能获得与上一次访问相同内容时不同的访问结果。 如果文档已被[撤销](../rms-client/client-track-revoke.md)，则可能不包含访问权限。|取决于内容的敏感程度：<br /><br />- **在没有 Internet 连接的情况下内容的可用天数** = **7**用于如果与未经授权的人员共享可能导致业务损失的敏感业务数据。 此建议提供灵活性和安全性之间的平衡折中。 例如合同、安全报告、预测摘要和销售客户数据。<br /><br />- **禁止访问**对于高度敏感的业务数据，如果与未经授权的人员共享将会导致业务损失。 此建议优先考虑安全性而不是灵活性，并确保一旦文档被撤销，那么所有授权用户都无法打开文档。 例如员工和客户信息、密码、源代码和预先公布的财务报表。|
    
    此设置分组为 Azure 权限管理服务创建一个自定义模板。 这些模板可用于与 Azure 权限管理集成的应用程序和服务。 有关计算机和服务如何下载并刷新这些模板的信息，请参阅[为用户和服务刷新模板](refresh-templates.md)。

10. 如果为“**HYOK (AD RMS)**”选择了“**选择模板**”，请提供 AD RMS 群集的模板 GUID 和授权 URL。 [详细信息](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

11. 单击“确定”关闭“保护”边栏选项卡，然后“标签”边栏选项卡上的“保护”选项中会显示你选择的“不要转发”或模板。

12. 在“**标签**”边栏选项卡上，单击“**保存**”。

13. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

<a id="next-steps" class="xliff"></a>

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]