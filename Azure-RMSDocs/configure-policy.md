---
title: 配置 Azure 信息保护策略 - AIP
description: 若要为 Azure 信息保护经典客户端配置分类、设置标签和保护，必须配置 Azure 信息保护策略。
author: batamig
ms.author: bagol
ms.date: 08/17/2020
manager: rkarlin
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 722d5ec64fc93da5a7da8d5cad57c679345faf01
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382966"
---
# <a name="configuring-the-azure-information-protection-policy"></a>配置 Azure 信息保护策略

>***适用** 于 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标签客户端，请参阅 Microsoft 365 文档中的 " [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) "。 *

> [!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

若要为经典客户端配置分类、设置标签和保护，必须配置 Azure 信息保护策略。 然后将此策略下载到已安装 Azure 信息保护客户端的计算机。

该策略包含标签和设置：

- 标签将分类值应用于文档和电子邮件，并可以选择性地保护此内容。 用户从文件资源管理器中右键单击时，Azure 信息保护客户端在 Office 应用中为用户显示这些标签。 也可通过使用 PowerShell 和 Azure 信息保护扫描程序来应用这些标签。

- 这些设置可更改 Azure 信息保护客户端的默认行为。 例如，可选择默认标签、是否所有文档和电子邮件都必须具有标签，以及 Office 应用中是否显示 Azure 信息保护栏。

## <a name="subscription-support"></a>订阅支持

Azure 信息保护支持不同级别的订阅：

- Azure 信息保护 P2：支持所有分类、设置标签和保护功能。

- Azure 信息保护 P1：支持大多数分类、设置标签和保护功能，但不支持自动分类或 HYOK。

- 包含 Azure Rights Management 服务的 Microsoft 365：支持保护，但不支持分类和标记。

需要 Azure 信息保护 P2 订阅的选项在门户中进行标识。

如果贵组织拥有组合订阅，则你有责任确保用户不会使用其帐户未授权使用的功能。 Azure 信息保护客户端不会进行许可证检查以及强制执行。 在配置并非所有用户都具有相应许可证的选项时，请使用作用域内策略或注册表设置，以确保组织符合许可证：

- **当组织具备 Azure 信息保护 P1 和 Azure 信息保护 P2 的组合许可证时**：对于具有 P2 许可证的用户，请在配置需要 Azure 信息保护 P2 许可证的选项时创建并使用一个或多个 [作用域内策略](configure-policy-scope.md)。 请确保全局策略不包含需要 Azure 信息保护 P2 许可证的选项。

- **如果你的组织具有 Azure 信息保护订阅，但某些用户只有包含 azure Rights Management 服务的 Microsoft 365 许可证**：对于没有 Azure 信息保护许可证的用户，请在其计算机上编辑注册表，以使其不下载 Azure 信息保护策略。 有关说明，请参阅管理员指南了解以下自定义项：[当组织具备组合许可证时，强制执行仅保护模式](./rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses)。

有关订阅的详细信息，请参阅 [需要为 Azure 信息保护准备哪个订阅，它包括哪些功能？](faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

## <a name="signing-in-to-the-azure-portal"></a>登录到 Azure 门户

若要登录到 Azure 门户以配置和管理 Azure 信息保护：

- 使用以下链接：https://portal.azure.com

- 使用具有以下 [管理员角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)之一的 Azure AD 帐户：
    
    - **Azure 信息保护管理员**
    
  - **法规管理员**
    
  - **合规性数据管理员**
    
  - **安全管理员**
    
    **安全读者**  - 仅限 [Azure 信息保护分析](reports-aip.md)
    
    **全局读取器**  - 仅限 [Azure 信息保护分析](reports-aip.md)
    
  - **全局管理员**
    
    > [!NOTE] 
    > 如果你的租户位于 [统一的标签平台](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)上，则 Azure 信息保护管理员角色 (以前的 "信息保护管理员" ) 对于 Azure 门户不受支持。 [详细信息](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform)
    
    Microsoft 帐户无法管理 Azure 信息保护。

## <a name="to-access-the-azure-information-protection-pane-for-the-first-time"></a>首次访问 "Azure 信息保护" 窗格

1. 登录到 Azure 门户。

2. 选择“+ 创建资源”，然后在市场的搜索框中键入“Azure 信息保护”。 
    
3. 在结果列表中选择“Azure 信息保护”。 在 " **Azure 信息保护** " 窗格上，单击 " **创建**"。
    
    > [!TIP] 
    > （可选）选择“固定到仪表板”以便在仪表板上创建“Azure 信息保护”磁贴，这样，下次登录到门户时，就可以跳过浏览到该服务。
    
    再次单击“创建”。

4. 首次连接到该服务时，“快速入门”页会自动打开。 浏览建议的资源，或使用其他菜单选项。 要配置用户可选择的标签，请使用以下过程。

下次访问 " **Azure 信息保护** " 窗格时，它会自动选择 " **标签** " 选项，以便你可以查看和配置所有用户的标签。 从 "**常规**" 菜单中选择 "**快速启动**" 页即可返回到该页面。

## <a name="how-to-configure-the-azure-information-protection-policy"></a>如何配置 Azure 信息保护策略

1. 请确保使用以下管理角色之一登录到 Azure 门户： Azure 信息保护管理员、安全管理员或全局管理。 请参阅[前述部分](#signing-in-to-the-azure-portal)了解有关这些管理角色的详细信息。

2. 如有必要，请导航到 " **Azure 信息保护** " 窗格：例如，在 "中心" 菜单上，单击 " **所有服务** "，然后在 "筛选器" 框中开始键入 **信息保护** 。 在结果中选择“Azure 信息保护”。 
    
    此时会自动打开 " **Azure 信息保护-标签** " 窗格，以便查看和编辑可用标签。 可通过从策略中添加或删除标签，使标签可供所有用户和选定用户使用，或不供用户使用。

3. 若要查看和编辑策略，从菜单选项选择“策略”。 若要查看和编辑所有用户都可以获得的策略，请选择“全局”策略。 若要创建所选用户的自定义策略，请选择“添加新策略”。
    

### <a name="making-changes-to-the-policy"></a>对策略进行更改

可以创建任意数量的标签。 但是，如果因标签数量过多而导致用户难以看见并选择正确的标签，可以创建作用域内策略，使用户仅看见相关的标签。 应用保护的标签具有数量上限（500 个）。

当你在 "Azure 信息保护" 窗格中进行任何更改时，请单击 " **保存** " 以保存更改，或者单击 " **放弃** " 以还原到上次保存的设置。 保存策略中的更改或对添加到策略中的标签进行更改时，这些更改会自动发布。 不提供单独发布选项。

每当受支持的 Office 应用程序启动时，Azure 信息保护客户端都会检查是否有任何变化，并根据最新的 Azure 信息保护策略下载这些更改。 在客户端上刷新策略的其他触发器：

- 右键单击以分类和保护文件或文件夹。

- 运行 [PowerShell cmdlet](./rms-client/client-admin-guide-powershell.md) 以实现标签设置和保护（Get-AIPFileStatus、Set-AIPFileClassification 和 Set-AIPFileLabel）。

- 每 24 小时一次。

- 关于 [Azure 信息保护扫描程序](deploy-aip-scanner.md)：当服务启动时（如果策略超过一小时），以及操作期间每小时。


>[!NOTE]
>客户端下载策略时，需要等待几分钟，它才能完全正常运行。 实际时间会因多种因素而异，例如策略配置的大小和复杂性以及网络连接。 如果标签生成的操作与最新更改不匹配，请等待最多 15 分钟，然后重试。

### <a name="configuring-your-organizations-policy"></a>配置组织的策略

使用以下信息来帮助配置 Azure 信息保护策略：

- [默认信息保护策略](configure-policy-default.md)

- [如何配置策略设置](configure-policy-settings.md)

- [如何创建新标签](configure-policy-new-label.md)

- [如何添加或删除标签](configure-policy-add-remove-label.md)
 
- [如何删除或重排标签](configure-policy-delete-reorder.md)

- [如何更改或自定义现有标签](configure-policy-change-label.md)

- [如何配置标签以进行保护](configure-policy-protection.md)

- [如何配置标签以应用可视标记](configure-policy-markings.md)

- [如何为自动和建议分类配置条件](configure-policy-classification.md)

- [如何使用作用域内策略为特定用户配置策略](configure-policy-scope.md)

- [如何配置和管理模板](configure-policy-templates.md)

- [如何为不同语言配置标签](configure-policy-languages.md)

- [如何将 Azure 信息保护标签迁移到 Microsoft 365](configure-policy-migrate-labels.md)

## <a name="label-information-stored-in-emails-and-documents"></a>电子邮件和文档中存储的标签信息

如果标签应用于文档或电子邮件，标签实际上存储在元数据中，这样应用程序和服务就能读取标签了：

- 在电子邮件中，此信息存储在 x 标头中： **msip_labels： MSIP_Label_ \<GUID> _Enabled = True** 

- 对于 Word 文档 ( .doc 和 .docx) ，Excel 电子表格 ( .xls 和 .xlsx) ，PowerPoint 演示文稿 ( .ppt 和 .pptx) 和 PDF 文档中，此元数据存储在以下自定义属性中： **MSIP_Label_ \<GUID> _Enabled = True**

对于电子邮件，在发送电子邮件时，将存储标签信息。 对于文档，保存文件时将存储标签信息。 

若要标识标签的 GUID，请在查看或配置 Azure 信息保护策略时，在 "Azure 门户的" **标签** "窗格中找到" 标签 ID "值。 对于应用了标记的文件，还可运行 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell cmdlet 来标识 GUID（MainLabelId 或 SubLabelId）。 当标签包含子标签时，请始终指定子标签（而非父标签）的 GUID。

## <a name="next-steps"></a>后续步骤

有关如何自定义 Azure 信息保护策略以及查看所导致的用户行为的示例，请尝试学习以下教程：

- [编辑 Azure 信息保护策略并创建新标签](infoprotect-quick-start-tutorial.md)

- [配置协同工作的 Azure 信息保护策略设置](infoprotect-settings-tutorial.md)

若要查看策略的执行方式，请参阅 [Azure 信息保护的集中报告](reports-aip.md)。