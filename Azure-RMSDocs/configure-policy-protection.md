---
title: 配置 Azure 信息保护标签以进行保护 - AIP
description: 通过配置标签来使用 Rights Management 保护，可保护最敏感的文档和电子邮件。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 141a8e6642745dc36dfd596d11b8153e20c09e69
ms.sourcegitcommit: 58e7d6e5c1cd3f21af03fe873076f282b684fd98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334158"
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>如何配置标签以进行 Rights Management 保护

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

> [!NOTE]
> 这些说明适用于 Azure 信息保护客户端（经典版），而不是 Azure 信息保护统一标记客户端。 不确定这些客户端之间有何区别？ 请参见[常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。
> 
> 如果你正在寻找信息来配置敏感度标签以应用 Rights Management 保护，请参阅 Microsoft 365 相容性文档。 例如，[通过在敏感度标签中使用加密来限制对内容的访问](/microsoft-365/compliance/encryption-sensitivity-labels)。

可通过使用 Rights Management 服务保护最敏感的文档和电子邮件。 此服务使用加密、标识和身份验证策略，有助于防止数据丢失。 保护应用于配置为使用 Rights Management 保护文档和电子邮件的标签，用户还可以在 Outlook 中选择“不可转发”按钮。****

当标签配置了“Azure (云密钥)”**** 保护设置，此操作会在后台创建并配置一个保护模板，集成了 Rights Management 模板的服务和应用程序都可以访问该模板。 例如，Exchange Online 和邮件流规则，以及 Outlook 网页版。 

## <a name="how-the-protection-works"></a>保护的工作原理

当文档或电子邮件受 Rights Management 服务保护时，它会在处于静态时和传输过程中进行加密， 而且只能由授权用户进行解密。 文档或电子邮件的这种加密保持不变，即使将其重命名。 此外，可以配置使用权限和限制，如下面的示例：

- 只有组织中的用户才能打开公司机密文档或电子邮件。

- 只有市场营销部门的用户才能编辑和打印促销通知文档或电子邮件，而组织中的所有其他用户只能阅读该文档或电子邮件。

- 用户不能转发包含内部重组相关新闻的电子邮件或从中复制信息。

- 不能在指定日期后打开发送给业务合作伙伴的当前价目表。

若要深入了解 Azure Rights Management 保护及其工作原理，请参阅[什么是 Azure Rights Management？](what-is-azure-rms.md)

> [!IMPORTANT]
> 若要配置标签来应用此保护，必须为组织激活 Azure Rights Management 服务。 有关详细信息，请参阅[激活 Azure 信息保护的保护服务](activate-service.md)。

标签应用保护时，受保护的文档不适合保存在 SharePoint 或 OneDrive 中。 对于受保护的文件，这些位置不支持以下功能：共同创作、Office 用于 web、搜索、文档预览、缩略图、电子数据展示和数据丢失防护（DLP）。

> [!TIP]
> [当你将标签迁移到](configure-policy-migrate-labels.md)统一的敏感性标签，并从标签管理中心（例如 Microsoft 365 合规中心）将其发布时，这些位置支持应用保护的标签。 有关详细信息，请参阅[在 SharePoint 和 OneDrive 中启用 Office 文件的敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)。

用户不必事先为 Azure 信息保护配置 Exchange 即可在 Outlook 中应用标签保护其电子邮件。 但是，在为 Azure 信息保护配置 Exchange 之前，你无法获得将 Exchange 与 Azure Rights Management 保护配合使用的完整功能。 例如，用户无法在移动电话上或通过 Outlook 网页版查看受保护的电子邮件，无法将受保护的电子邮件编入索引用于搜索，并且无法为 Rights Management 保护配置 Exchange Online DLP。 若要确保 Exchange 支持这些其他方案，请参阅以下资源：

- 对于 Exchange Online，请参阅 [Exchange Online：IRM 配置](configure-office365.md#exchangeonline-irm-configuration)说明。

- 对于本地 Exchange，必须部署 [RMS 连接器并配置 Exchange 服务器](deploy-rms-connector.md)。 

## <a name="to-configure-a-label-for-protection-settings"></a>若要配置保护设置标签

1. 如果尚未这样做，请打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)， 然后导航到“Azure 信息保护”窗格。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

2. 从 "**分类**  >  **标签**" 菜单选项：在 " **Azure 信息保护-标签**" 窗格中，选择要更改的标签。 

3. 在“标签”**** 窗格上，找到“为包含此标签的文档和电子邮件设置权限”**** 并选择以下选项之一：
    
    - **未配置**：如果标签当前配置为应用保护，而不再需要所选的标签应用保护，请选择此选项。 然后转到步骤 11。
        
        先前配置的保护设置将保留为存档的保护模板，如果将选项更改回“保护”，则会再次显示****。 Azure 门户中不会显示此模板，但如有需要，仍可通过 [PowerShell](configure-templates-with-powershell.md) 管理该模板。 这一行为表示，如果内容具有先前应用了保护设置的此标签，则仍可以访问该内容。
        
        当标签应用“未配置”保护设置时****：
        
         - 如果内容之前未使用标签进行保护，则将保留该保护。 
         
         - 如果内容之前使用标签进行保护，如果用户应用的标签有权删除权限管理保护，则将删除该保护。 此要求意味着用户必须具有 "**导出**" 或 "**完全控制**" 的[使用权限](configure-usage-rights.md)。 或者，成为权限管理所有者（自动授予完全控制使用权限）或者成为 [Azure 权限管理的超级用户](configure-super-users.md)。
             
             如果用户没有删除保护的权限，则无法应用该标签，并显示以下消息： **Azure 信息保护无法应用此标签。如果此问题仍然存在，请与您的管理员联系**。 
    
    - 保护****：选择此选项应用保护，然后转到步骤 4。
    
    - **删除保护**：如果文档或电子邮件受到保护，选择此选项可删除保护。 然后转到步骤 11。
        
        如果使用标签或保护模板应用保护，则保护设置将保留为存档的保护设置，且如果将选项更改回“保护”，则会再次显示****。 Azure 门户中不会显示此模板，但如有需要，仍可通过 [PowerShell](configure-templates-with-powershell.md) 管理该模板。 这一行为表示，如果内容具有先前应用了保护设置的此标签，则仍可以访问该内容。
        
        请注意，用户必须具有删除权限管理保护的权限，才能成功应用具有此选项的标签。 此要求意味着用户必须具有 "**导出**" 或 "**完全控制**" 的[使用权限](configure-usage-rights.md)。 或者，成为权限管理所有者（自动授予完全控制使用权限）或者成为 [Azure 权限管理的超级用户](configure-super-users.md)。 
        
        如果应用标签的用户不具有删除 Rights Management 保护的权限，则无法应用该标签，并显示以下消息： **Azure 信息保护无法应用此标签。如果此问题仍然存在，请与您的管理员联系。**

4. 如果提前选中了“保护”，则会在选择其他选项之一时自动打开“保护”窗格********。 如果新的窗格未自动打开，请选择“保护”****：
    
    ![为 Azure 信息保护标签配置保护](./media/info-protect-protection-bar-configured.png)

5. 在“保护”窗格上，选择“Azure (云密钥)”或“HYOK (AD RMS)”************。
    
    大多数情况下，为权限设置选择“Azure (云密钥)”。**** 请勿选择“HYOK (AD RMS)”，除非已阅读并了解此“自留密钥”(HYOK) 配置随附的先决条件和限制。****** 有关详细信息，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](configure-adrms-restrictions.md)。 若要继续配置 HYOK (AD RMS)，请转到步骤 9。
    
6. 选择下列选项之一：
    
   - **设置权限**：在此门户中定义新的保护设置。
    
   - “设置用户定义的权限(预览)”****：允许用户指定应向其授予权限的人员并指定具体的权限。 然后，可优化此选项并选择仅 Outlook 或 Word、Excel、PowerPoint 和文件资源管理器。 如果为[自动分类](configure-policy-classification.md)配置标签，则此选项不受支持且无法使用。
        
       如果选择 Outlook 选项：标签显示在 Outlook 中，并且用户应用该标签时产生的行为与 "不[转发](configure-usage-rights.md#do-not-forward-option-for-emails)" 选项相同。
        
       如果为 Word、Excel、PowerPoint 和文件资源管理器选择此选项：设置此选项后，标签将显示在这些应用程序中。 用户应用标签时产生的行为是显示对话框，以便用户选择自定义权限。 在此对话框中，用户选择其中一个[预定义权限级别](configure-usage-rights.md#rights-included-in-permissions-levels)，浏览或指定用户或组，并可选择设置到期日期。 确保用户具有关于如何提供这些值的说明和指导。
    
   - **选择预定义的模板**：使用已配置的一个默认模板或自定义模板。 请注意，如果正在编辑的标签之前曾使用“设置权限”选项，则不会对新标签显示此选项****。
    
     若要选择预定义的模板，此模板必须为已发布（未存档），且必须未链接到另一个标签。 选中此选项后，可以使用“编辑模板”按钮[将模板转换为标签](configure-policy-templates.md#to-convert-templates-to-labels)。****
    
     如果习惯于创建和编辑自定义模板，请参考[曾使用 Azure 经典门户执行的任务](migrate-portal.md)获取帮助。

7. 如果为“Azure (云密钥)”选择了“设置权限”********，可以使用此选项选择用户和使用权限。 
    
    如果未选择任何用户并在此窗格中选择 "确定"，**然后在**"**标签**" 窗格中选择 **"确定"** ，则会将标签配置为应用保护，以便仅应用标签的人员可以打开文档或电子邮件，而不会受到任何限制。 有时，此配置称为“只为我执行此操作”，这可能是必需的结果，这样用户便可将文件保存到任何位置，并确保只有他们能够打开它。 如果此结果符合你的要求，并且其他人不需要协作处理受保护内容，请不要选择“添加权限”****。 保存标签后，下次打开此“保护”窗格时，会看到“用户”显示“IPC_USER_ID_OWNER”，“权限”显示“共同所有者”以反映此配置********************。
    
    要指定希望能够打开受保护文档和电子邮件的用户，请选择“添加权限”****。 然后，在“添加权限”**** 窗格上，选择有权使用所选标签保护的内容的第一组用户和组：
    
   - **从列表中选择 "选择"** ，然后选择 "全部**添加 \<organization name> 成员**"，然后从组织添加所有用户。 此设置不包括来宾帐户。 或者，也可以选择“添加任何身份已验证的用户”**** 或浏览目录。
        
       选择所有成员或浏览目录时，用户和组必须有电子邮件地址。 在生产环境中，他们几乎都有电子邮件地址，但在简单的测试环境中，可能需要为用户帐户或组添加电子邮件地址。
        
       ###### <a name="more-information-about-add-any-authenticated-users"></a>详细了解如何**添加任何身份已验证的用户** 
       此设置不限制谁能访问标签保护的内容，同时仍加密内容，并提供限制内容使用方式（权限）和访问方式（到期和脱机访问）的选项。 不过，打开受保护内容的应用程序必须能够支持所使用的身份验证。 鉴于此，Google 等联合社交提供程序以及一次性密码身份验证应仅在你使用 Exchange Online 和 Office 365 邮件加密的新功能时，才只用于电子邮件。 可以将 Microsoft 帐户与 Azure 信息保护查看器和 Office 365 应用（即点即用）结合使用。 
          
       任何经过身份验证的用户设置的一些典型方案：
       - 不介意谁查看内容，但希望限制内容的使用方式。 例如，不希望对内容执行编辑、复制或打印操作。
       - 无需限制谁有权访问内容，但要能够跟踪谁打开和可能撤销了内容。
       - 有要求必须加密内容（无论是静态还是传输中），但无需执行访问控制。
        
   - 选择“输入详细信息”以手动为单个用户或组（内部或外部）指定电子邮件地址。**** 或者，使用此选项，通过输入另一个组织的任何域名来指定该组织中的所有用户。 还可以通过输入社交提供程序程序的域名（例，如 gmail.com、hotmail.com 或 outlook.com），将此选项用于这些程序************。
        
     >[!NOTE]
     >如果在选择用户或组后某个电子邮件地址发生更改，请参阅计划文档中的[电子邮件地址发生更改情况下的注意事项](prepare.md#considerations-for-azure-information-protection-if-email-addresses-change)部分。
    
     最佳做法是使用组，而不是使用用户。 此策略可简化配置，且可降低以后更新标签配置并重新保护内容的可能性。 但是，如果对组进行更改则请注意，出于性能原因，Azure Rights Management 将[缓存组成员身份](prepare.md#group-membership-caching-by-azure-information-protection)。 
    
    指定第一组用户和组后，选择要授予这些用户和组的权限。 若要深入了解可选择的权限，请参阅[为 Azure 信息保护配置使用权限](configure-usage-rights.md)。 但是，支持此保护的应用程序可能在实现这些权限的方式方面有所不同。 请查阅其文档，并在为用户部署模板之前，对用户使用的应用程序执行自己的测试以检查其行为。
    
     如有必要，现在可以添加另一组具有使用权限的用户和组。 重复此操作，直到指定所有用户和组及其各自的权限。

     >[!TIP]
     >请考虑添加“另存为，导出 (EXPORT)”自定义权限，并向数据恢复管理员或其他拥有信息恢复职责的人员授予此权限****。 如有必要，这些用户可删除要使用此标签或模板保护的文件和电子邮件中的保护。 这种可以在权限级别删除对文档或电子邮件的保护的功能可提供比[超级用户功能](configure-super-users.md)更精细的控制。
    
     对于指定的所有用户和组，在“保护”**** 窗格上，立即检查是否想要对以下设置进行任何更改。 请注意，这些设置和权限一样，它们并不适用于 [Rights Management 颁发者或 Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)，也不适用于任何已分配的[超级用户](configure-super-users.md)。
    
     ###### <a name="information-about-the-protection-settings"></a>有关保护设置的信息
    
     |设置|详细信息|建议的设置
     |-----------|--------------------|--------------------|
     |**文件内容有效期限**|定义一个日期或天数，在此期间不应为选定的用户打开受模板保护的文档。 对于电子邮件，由于某些电子邮件客户端使用的缓存机制，并不总是强制执行过期。<br /><br />可以指定一个日期，也可以指定对内容应用保护后所经历的天数。<br /><br />如果指定日期，它将在当前时区的午夜生效。|除非内容具有特定的时间限制要求，否则**内容永不过期**。|
     |**允许脱机访问**|使用此设置在你的任何安全需求（包括吊销后的访问权限）与所选用户在没有 Internet 连接的情况下是否能够打开受保护的内容之间实现平衡。<br /><br />如果你指定内容在没有 Internet 连接的情况下不可用，或者指定内容仅在指定天数内可用，则在到达该阈值时，这些用户必须重新进行身份验证，他们的访问也将被记录。 发生这种情况时，如果用户的凭据不缓存，他们会收到提示，指示登录后才能打开文档或电子邮件。<br /><br />除了重新进行身份验证之外，还会重新评估策略和用户组成员身份。 这意味着，如果策略或组成员身份相比用户上一次访问文档或电子邮件时发生变化，则他们可能获得与上一次访问相同内容时不同的访问结果。 如果文档已被[撤销](./rms-client/client-track-revoke.md)，则可能不包含访问权限。|取决于内容的敏感程度：<br /><br />- **在没有 internet 连接**  =  的情况下内容可用的天数**7**对于可能导致业务损失的敏感业务数据，如果与未经授权的人员共享。 此建议提供灵活性和安全性之间的平衡折中。 例如合同、安全报告、预测摘要和销售帐户数据。<br /><br />- **禁止**访问对于高度敏感的业务数据，如果与未经授权的人员共享将会导致业务损失。 此建议优先考虑安全性而不是灵活性，并确保一旦文档被撤销，那么所有授权用户都无法打开文档。 例如员工和客户信息、密码、源代码和预先公布的财务报表。|
    
     完成权限和设置配置后，单击“确定”****。 
    
     此设置分组为 Azure Rights Management 服务创建一个自定义模板。 这些模板可用于与 Azure Rights Management 集成的应用程序和服务。 有关计算机和服务如何下载并刷新这些模板的信息，请参阅[为用户和服务刷新模板](refresh-templates.md)。

8. 如果为“Azure (云密钥)”选择了“选择预配模板”，请单击下拉框，然后选择要用于保护包含此标签的文档和电子邮件的[模板](configure-policy-templates.md)。******** 看不到已存档的模板或已为另一个标签选择的模板。
    
    如果选择“部门模板”，或者如果已配置[加入控制机制](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)：****
    
    - 配置的模板作用域外的用户或从应用 Azure Rights Management 保护中排除的用户仍将看到该标签，但不能应用该标签。 如果他们选择该标签，则会看到以下消息： **Azure 信息保护无法应用此标签。如果此问题仍然存在，请与您的管理员联系。**
        
        请注意，将始终显示所有已发布的模板，即使正在配置作用域内策略。 例如，正在为市场营销组配置作用域内策略。 可选择的模板不限于作用域为“营销”组的模板，还可以选择所选用户不能使用的部门模板。 为了方便配置和尽量减少故障排除，请考虑命名部门模板以匹配作用域内策略中的标签。 

9. 如果选择了“HYOK (AD RMS)”，请选择“设置 AD RMS 模板详细信息”或“设置用户定义的权限(预览)”。************ 然后指定 AD RMS 群集的授权 URL。
    
    有关指定模板 GUID 和授权 URL 的说明，请参阅[查找相关信息以使用 Azure 信息保护标签指定 AD RMS 保护](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)。
    
    “用户定义的权限”选项允许用户指定应向其授予权限的人员并指定具体的权限。 然后，可以优化此选项并选择仅 Outlook（默认）或 Word、Excel、PowerPoint 和文件资源管理器。 如果为[自动分类](configure-policy-classification.md)配置标签，则此选项不受支持且无法使用。
    
    如果选择 Outlook 选项：标签显示在 Outlook 中，并且用户应用该标签时产生的行为与 "不[转发](configure-usage-rights.md#do-not-forward-option-for-emails)" 选项相同。
    
    如果为 Word、Excel、PowerPoint 和文件资源管理器选择此选项：设置此选项后，标签将显示在这些应用程序中。 用户应用标签时产生的行为是显示对话框，以便用户选择自定义权限。 在此对话框中，用户选择其中一个[预定义权限级别](configure-usage-rights.md#rights-included-in-permissions-levels)，浏览或指定用户或组，并可选择设置到期日期。 确保用户具有关于如何提供这些值的说明和指导。

10. 单击“确定”关闭“保护”窗格，然后“标签”窗格上的“保护”选项中会显示你选择的“用户定义的模板”或模板********************。

11. 在“标签”窗格上，单击“保存”********。

12. 在“Azure 信息保护”窗格上，使用“保护”列确认标签现在显示你所需的保护设置********：
    
    - 一个复选标记（若已配置保护）。 
    
    - 一个表示取消的 x 标记（若已将标签配置为删除保护）。
    
    - 未设置保护时，为空白字段。 

单击“保存”**** 时，更改将会自动提供给用户和服务。 不再提供单独发布选项。


## <a name="example-configurations"></a>示例配置

[默认策略](configure-policy-default.md)的“机密”和“高度机密”标签中的“所有员工”和“仅收件人”子标签提供了一些示例，说明如何配置可应用保护的标签。**************** 也可使用以下示例，帮助配置适用于不同情况的保护。 

对于下面的每个示例，请在 \<*label name*> 窗格上选择 "**保护**"。 如果“保护”**** 窗格不会自动打开，请选择“保护”**** 打开此窗格，以便选择保护配置选项：

![配置 Azure 信息保护标签以进行保护](./media/info-protect-protection-bar-configured.png)

### <a name="example-1-label-that-applies-do-not-forward-to-send-a-protected-email-to-a-gmail-account"></a>示例 1：对发送到 Gmail 帐户的受保护电子邮件应用“不要转发”的标签

此标签仅可用于 Outlook，且适用于 Exchange Online 已配置 [Office 365 邮件加密新功能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)的情况。 当用户需要向使用 Gmail 帐户的人员（或组织外部任何其他电子邮件帐户）发送受保护电子邮件时，指示用户选择此标签。 

用户在“收件人”框中键入 Gmail 电子邮件地址。****  然后，用户选择此标签，“不要转发”选项自动添加到电子邮件。 结果是收件人无法转发电子邮件、打印邮件、从中复制电子邮件，或使用 "**另存为**" 选项将电子邮件保存到邮箱外。 

1. 在“保护”窗格上，确保选中“Azure (云密钥)” 。
    
2. 选择“设置用户定义的权限(预览)”****。

3. 确保选中以下选项：“在 Outlook 中应用‘不要转发’”。****

4. 如果已选中，请清除以下选项：“在 Word、Excel、PowerPoint 和文件资源管理器中提示用户获取自定义权限”。****

5. 单击“保护”**** 窗格上的“确定”****，再单击“标签”**** 窗格上的“保存”****。


### <a name="example-2-label-that-restricts-read-only-permission-to-all-users-in-another-organization-and-that-supports-immediate-revocation"></a>示例 2：将只读权限限制到其他组织中所有用户并且支持即时撤销的标签

此标签适用于共享（只读）非常敏感的文档，这类文档始终需要 Internet 连接才可进行查看。 如果被撤销权限，用户下次打开文档时将无法进行查看。

此标签不适用于电子邮件。

1. 在“保护”窗格上，确保选中“Azure (云密钥)” 。
    
2. 确保选中“设置权限”选项，然后选择“添加权限”。********

3. 在“添加权限”窗格，选择“输入详细信息”********。

4. 输入其他组织的域名，例如 **fabrikam.com**。 然后选择“添加”。

5. 在“从预设中选择权限”中，选择“查看器”，然后选择“确定”。************

6. 回到“保护”窗格，为“允许脱机访问设置”选择“从不”************。

7. 单击“保护”**** 窗格上的“确定”****，再单击“标签”**** 窗格上的“保存”****。


### <a name="example-3-add-external-users-to-an-existing-label-that-protects-content"></a>示例 3：将外部用户添加到用于保护内容的现有标签

新添加的用户可打开已使用此标签进行保护的文档和电子邮件。 授予这些用户的权限可能与现有用户具有的权限有所不同。

1. 在“保护”窗格，确保选中“Azure (云密钥)”********。
    
2. 确保选中“设置权限”，然后选择“添加权限”。********

3. 在“添加权限”窗格，选择“输入详细信息”********。

4. 输入要添加的第一个用户或组的电子邮件地址，然后选择“添加”。****

5. 为此用户（或组）选择权限。

6. 为每个要添加此标签的用户（或组）重复步骤 4 和 5。 。

7. 单击“保护”**** 窗格上的“确定”****，再单击“标签”**** 窗格上的“保存”****。

### <a name="example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward"></a>示例 4：针对受保护电子邮件并提供限制性低于“不要转发”的权限的标签

此标签不可限制到 Outlook，但可提供限制性低于“不要转发”的控制。 例如，希望收件人能够复制电子邮件或附件，或者保存和编辑附件。

如果指定 Azure AD 中没有帐户的外部用户：

- 当 Exchange Online 使用 [Office 365 邮件加密中的新功能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)时，此标签适用于电子邮件。 
 
- 对于自动受保护的 Office 附件，可以在浏览器中查看这些文档。 若要编辑这些文档，请使用 Office 365 应用（即点即用）和使用相同电子邮件地址的 Microsoft 帐户下载和编辑它们。 [详细信息](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)


> [!NOTE]
> Exchange Online 即将推出新选项 - [仅加密](configure-usage-rights.md#encrypt-only-option-for-emails)。 此选项不可用于标签配置。 不过，如果知道收件人是谁，可以使用此示例来配置拥有同一组使用权限的标签。 

用户在“收件人”框中指定电子邮件地址时，该地址必须与为此标签配置指定的用户地址相同。**** 因为用户可能属于组并且拥有多个电子邮件地址，所以他们指定的电子邮件地址不必与针对权限指定的电子邮件地址完全匹配， 虽然这是确保成功对收件人授权的最简单方法。 若要详细了解如何向用户授予权限，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。 

1. 在“保护”窗格上，确保选中“Azure (云密钥)” 。
    
2. 确保选中“设置权限”，然后选择“添加权限”。********

3. 在 "**添加权限**" 窗格中：要向组织中的用户授予权限，请选择 "**添加 \<organization name> -所有成员**" 以选择租户中的所有用户。 此设置不包括来宾帐户。 或者，选择“浏览目录”**** 以选择特定组。 若要向外部用户授予权限或者键入电子邮件地址，请选择“输入详细信息”，然后键入用户或 Azure AD 组的电子邮件地址或键入域名****。
    
    重复此步骤，指定其他应具有相同权限的用户。

4. 对于“从预设中选择权限”，可选择“共有者”、“合著者”、“审阅者”或“自定义”，以选择希望授予的权限。********************
    
    注意：请勿对电子邮件选择“查看器”，并且如果选择“自定义”，请确保包括“编辑和保存”。************
    
    要从 Exchange Online 中选择与新的“仅加密”选项匹配的相同权限，请选择“自定义”********。 然后选择“另存为，导出(导出)”和“完全控制(所有者)”之外的所有权限********。

5. 若要指定其他应具有不同权限的用户，请重复步骤 3 和 4。

6. 在“添加权限”窗格上单击“确定”********。

7. 单击“保护”**** 窗格上的“确定”****，再单击“标签”**** 窗格上的“保存”****。


### <a name="example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it"></a>示例 5：加密内容但不限制谁能访问内容的标签

此配置的优势在于，无需指定用户、组或域来保护电子邮件或文档。 仍可以加密内容，并指定使用权限、到期日期和脱机访问。 仅当无需限制谁能打开受保护文档或电子邮件时，才使用此配置。 [详细了解此设置](#more-information-about-add-any-authenticated-users)

1. 在“保护”窗格，确保选中“Azure (云密钥)”********。
    
2. 请务必依次选择“设置权限”**** 和“添加权限”****。

3. 在“添加权限”**** 窗格上的“从列表中选择”**** 选项卡中，选择“添加任何身份已验证的用户”****。

4. 选择相应权限，再单击“确定”****。

5. 如有需要，返回到“保护”窗格，配置“文件内容有效期限”和“允许脱机访问”设置，再单击“确定”****************。

6. 在“标签”**** 窗格上，选择“保存”****。


### <a name="example-6-label-that-applies-just-for-me-protection"></a>示例6：适用于 "仅限我" 保护的标签

此配置为文档提供与安全协作相对的方式：[超级用户](configure-super-users.md)除外，只有应用标签的人员才能打开受保护的内容，而不会受到任何限制。 此配置通常被称为“只为我执行”保护，适用于用户想要将文件保存到任何位置并确保只有他们可以打开它的情况。

标签配置看似简单：

1. 在“保护”窗格，确保选中“Azure (云密钥)”********。
    
2. 选择“确定”，而不选择任何用户，或在此窗格上配置任何设置****。
    
    虽然可以配置“文件内容过期”和“允许脱机访问”的设置，但如果未指定用户及其权限，则这些访问设置不适用********。 这是因为应用保护的人是内容的 [Rights Management 颁发方](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)，这个角色没有这些访问限制。

3. 在“标签”**** 窗格上，选择“保存”****。

## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用[配置组织的策略](configure-policy.md#configuring-your-organizations-policy)部分中的链接。 

Exchange 邮件流规则还能根据标签应用保护。 有关详细信息和示例，请参阅[配置 Azure 信息保护标签的 Exchange Online 邮件流规则](configure-exo-rules.md)。  
