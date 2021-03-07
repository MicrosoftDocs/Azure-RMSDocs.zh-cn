---
title: 'Azure 信息保护的常见问题解答 (AIP) '
description: 获取有关 Azure 信息保护的常见问题解答 (AIP) 及其保护服务，Azure Rights Management (Azure RMS) 。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 9f19b02045ea98fe7c7dc54299ea60abaa6d3312
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415001"
---
# <a name="frequently-asked-questions-for-azure-information-protection-aip"></a>Azure 信息保护的常见问题 (AIP) 

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>相关内容：*[AIP 统一标记客户端和经典客户端](#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

对于 Azure 信息保护有疑问 (AIP) ，或是 Azure Rights Management 服务 (Azure RMS) ？ 

请参阅下面的 [更具体的常见问题页面](#what-do-i-do-if-my-question-isnt-here)。

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Azure 信息保护和 Microsoft 信息保护之间有何不同？

与 Azure 信息保护不同， [Microsoft 信息保护](https://www.microsoft.com/security/business/information-protection) 不是可以购买的订阅或产品。 它是一个框架，适用于产品和集成功能，可帮助你保护组织的敏感信息。

**Microsoft 信息保护产品包括**：
- Azure 信息保护
- Microsoft 365 信息保护，如 Microsoft 365 DLP
- Windows 信息保护
- Microsoft Cloud App Security

**Microsoft 信息保护功能包括**：
- 统一标签管理
- Office 应用中内置的最终用户标签体验
- Windows 了解统一标签并对数据应用保护的能力
- Microsoft 信息保护 SDK
- Adobe Acrobat Reader 中的功能，用于查看标签和受保护的 Pdf

有关详细信息，请参阅 [信息保护功能，帮助保护敏感数据](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)。

## <a name="whats-the-difference-between-labels-in-microsoft-365-and-labels-in-azure-information-protection"></a>Azure 信息保护中 Microsoft 365 和标签之间的标签有何区别？

最初，Microsoft 365 仅具有 [保留标签](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30)，使你能够对文档和电子邮件进行分类，以便在将内容存储到 Microsoft 365 services 中时对其进行审核和保留。 

与此相反，Azure 信息保护标签是在 Azure 门户中使用 AIP 经典客户端配置的，因此，无论它们是存储在本地还是云中，都可以为文档和电子邮件应用一致的分类和保护策略。

除了保留标签外，Microsoft 365 现在还支持 [敏感标签](/microsoft-365/compliance/sensitivity-labels) 。 可以在以下管理中心创建和配置敏感度标签：

- Office 365 安全与合规中心
- Microsoft 365 安全中心
- Microsoft 365 合规中心

如果在 Azure 门户中配置了旧版 AIP 标签，则建议将其迁移到敏感度标签和统一的标签客户端。 有关详细信息，请参阅[教程：从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端](tutorial-migrating-to-ul.md)。

有关详细信息，请参阅[宣布推出信息保护功能以帮助保护你的敏感数据](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967)。

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>如何确定我的租户是否在统一的标签平台上？

如果你的租户位于统一的标签平台上，则它支持可由 [支持统一标签的客户端和服务](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)使用的敏感度标签。 如果在2019年6月版或更高版本中获取了 Azure 信息保护订阅，则租户会自动在统一的标签平台上，无需执行其他操作。 你的租户还可能在此平台上，因为有人迁移了你的 Azure 信息保护标签。

如果你的租户不在统一的标签平台上，你会在 " **Azure 信息保护** " 窗格上的 "Azure 门户中看到以下信息横幅：

![迁移信息横幅](media/migration-status-banner.png)

你还可以通过转到 **Azure 信息保护**  >  **管理**  >  **统一标签** 来进行检查，并查看 **统一标签** 状态：

|状态 |描述  |
|---------|---------|
|**停**     |  你的租户在统一的标签平台上。 <br />你可以从 "Microsoft 365 相容性中心" [创建、配置和发布标签](/microsoft-365/compliance/create-sensitivity-labels) 。       |
|**未激活**    |  你的租户不在统一的标签平台上。 <br />有关迁移说明和指南，请参阅 [如何将 Azure 信息保护标签迁移到统一的敏感度标签](configure-policy-migrate-labels.md)。       |
| | |

## <a name="whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients"></a>Azure 信息保护经典和统一标签客户端之间有何区别？

旧的 Azure 信息保护客户端（称为 *经典* 客户端）将从 Azure 下载标签和策略设置，并使你能够从 Azure 门户配置 [AIP 策略](overview-policy.md) 。

*统一标签客户端* 是最新的客户端，其中包含最新的更新，并且支持多个应用程序和服务使用的统一标签平台。 统一标签客户端从以下管理中心下载 [灵敏度标签](/microsoft-365/compliance/sensitivity-labels) 和策略设置：

- Office 365 安全与合规中心
- Microsoft 365 安全中心
- Microsoft 365 合规中心

如果你是管理员，请在 [选择 Windows 标签解决方案](rms-client/use-client.md#choose-your-windows-labeling-solution)中了解详细信息。

### <a name="classic-client-deprecation"></a>经典客户端弃用

为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月 31** 日被 **弃用**。 

弃用后，客户端将继续按预期方式工作。 但是，管理员将无法在门户上更新策略，也不会为经典客户端提供更多的修补程序或更改。

在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

如果你当前已部署了经典客户端，则建议升级到统一的标签客户端。 有关详细信息，请参阅。

- [教程：从经典客户端迁移到统一的标签客户端](tutorial-migrating-to-ul.md)
- [如何将 Azure 信息保护标签迁移到统一敏感度标签](configure-policy-migrate-labels.md)
### <a name="identify-the-client-you-have-installed"></a>识别已安装的客户端

如果用户想要了解是否安装了经典或统一标签客户端，则可以执行以下操作之一：

- 在 Office 应用中，检查 " **敏感度** " 或 " **保护** " 工具栏按钮。 统一标签客户端会显示 " **敏感度**" :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: 按钮，而经典客户端则会显示 " **保护** " 按钮。 

- 检查已安装的 Azure 信息保护应用程序的版本号。

    - 版本 **1.x** 表示你具有经典客户端。 示例： **1.54.59.0**
    - 版本 **2.x** 表明你具有统一的标签客户端。 示例： **2.8.85.0**

    例如，在 " **Windows 设置" > "应用和功能** " 区域中，向下滚动到 **Microsoft Azure 信息保护** 应用程序，并检查版本号。

    :::image type="content" source="media/client-about.png" alt-text="查看 Azure 信息保护客户端版本":::

## <a name="when-is-the-right-time-to-migrate-my-labels-to-unified-labeling"></a>将标签迁移到统一标签时的正确时间是什么？

建议将 Azure 信息保护标签迁移到统一的标签平台，以便可以将它们用作 [支持统一标签的其他客户端和服务的](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)敏感度标签。

有关详细信息和说明，请参阅 [如何将 Azure 信息保护标签迁移到统一的敏感度标签](configure-policy-migrate-labels.md)。

## <a name="after-ive-migrated-my-labels-to-unified-labeling-which-management-portal-do-i-use"></a>将标签迁移到统一标签后，使用哪种管理门户？

在 Azure 门户中迁移标签后，请根据你安装的客户端，继续将其管理到以下位置之一：

|客户端  |描述  |
|---------|---------|
|仅限[客户端和服务的统一标签](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)    |  如果只安装了统一的标记客户端，请在某个管理中心中管理标签： Office 365 Security & 相容性中心、Microsoft 365 安全中心或 Microsoft 365 合规中心。 统一标签客户端从这些管理中心下载标签和策略设置。 <br /><br />有关说明，请参阅 [创建和配置敏感度标签及其策略](/microsoft-365/compliance/create-sensitivity-labels)。     |
|仅[经典客户端](./rms-client/aip-client.md)  | 如果已迁移标签，但仍安装了经典客户端，请继续使用 Azure 门户编辑标签和策略设置。 经典客户端继续从 Azure 下载标签和策略设置。
|AIP [经典客户](./rms-client/aip-client.md) 端和 [统一标签](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) 客户端     | 如果同时安装了两个客户端，请使用管理中心或 Azure 门户来更改标签。 <br /><br />要使经典客户端选择管理中心所做的标签更改，请返回到 Azure 门户进行发布。 在 "Azure 门户 > **Azure 信息保护-统一标签** " 窗格中，选择 " **发布**"。  <br /><br /> 继续使用 Azure 门户进行[集中报告](reports-aip.md)和[扫描程序](deploy-aip-scanner.md)。     |
| | |

## <a name="do-i-need-to-re-encrypt-my-files-after-moving-to-sensitivity-labels-and-the-unified-labeling-platform"></a>移动到敏感度标签和统一标签平台后，是否需要重新加密文件？

不需要，在从 AIP 经典客户端迁移并在 Azure 门户中托管的标签后，在迁移到敏感度标签和统一标签平台后，不需要重新加密文件。

迁移后，请从标记管理中心管理标签和标签策略，包括 Microsoft 安全中心、Microsoft 相容性中心或 Microsoft Security & 相容性中心。 

有关详细信息，请参阅 Microsoft 365 文档中的 " [敏感标签](/microsoft-365/compliance/sensitivity-labels) " 和 " [了解统一标签迁移](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185) " 博客。


## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Azure 信息保护和 Azure Rights Management 之间有何不同？

Azure 信息保护 (AIP) 为组织的文档和电子邮件提供分类、标签和保护。

使用 Azure Rights Management 服务（现为 AIP 的组件）保护内容。 

有关详细信息，请参阅 [AIP 如何保护你的数据](aip-classification-and-protection.md#how-aip-protects-your-data) 以及 [什么是 Azure Rights Management？](what-is-azure-rms.md)。

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Azure 信息保护的身份管理的作用是什么？

标识管理是 AIP 的重要组成部分，因为用户必须具有有效的用户名和密码才能访问受保护的内容。

要详细了解 Azure 信息保护如何帮助保护数据，请参阅 [Azure 信息保护在保护数据方面的角色](/enterprise-mobility-security/solutions/azure-information-protection-securing-data)。 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>需要为 Azure 信息保护准备哪个订阅，以及它包括哪些功能？

若要了解有关 AIP 订阅的详细信息，请参阅 [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection) 页上的订阅信息和功能列表。

如果你拥有包含 Azure Rights Management 数据保护的 Microsoft 365 订阅，请下载 [Azure 信息保护许可数据表](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) ，详细了解如何与 AIP 集成。

还有关于许可的问题吗？ 查看[许可的常见问答解答](https://azure.microsoft.com/pricing/details/information-protection#faq)部分是否有答案。

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>是否必须是全局管理员才能配置 Azure 信息保护？我可以委派给其他管理员吗？

Microsoft 365 租户或 Azure AD 租户的全局管理员可以很明显地运行 Azure 信息保护的所有管理任务。 

但是，如果要将管理权限分配给其他用户，请使用以下角色：

- [Azure 信息保护管理员](#azure-information-protection-administrator)
- [合规性管理员或合规性数据管理员](#compliance-administrator-or-compliance-data-administrator)
- [安全读取器或全局读取器](#security-reader-or-global-reader)
- [安全管理员](#security-administrator)
- [Azure Rights Management 全局管理员和连接器管理员](#azure-rights-management-global-administrator-and-connector-administrator)

此外，在管理管理任务和角色时，请注意以下事项：

|问题  |详细信息  |
|---------|---------|
|**支持的帐户类型**     | Microsoft 帐户不支持 Azure 信息保护的委派管理，即使这些帐户分配给列出的某个管理角色。         |
|**载入控件**     |如果配置了[加入控制](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，此配置不会影响管理 Azure 信息保护的能力（RMS 连接器除外）。 <br /><br />例如，如果你配置了加入控制以便保护内容的能力限制为 *IT 部门* 组，则用于安装和配置 RMS 连接器的帐户必须是该组的成员。          |
|**删除保护**     |  管理员无法自动删除受 Azure 信息保护保护的文档或电子邮件的保护。 <br /><br />只有被分配为超级用户的用户才可以删除保护，并且仅当启用超级用户功能时。 <br /><br />具有 Azure 信息保护管理权限的任何用户都可以启用超级用户功能，并将用户分配为超级用户，包括其自己的帐户。<br /><br />这些操作记录在管理员日志中。 <br /><br />有关详细信息，请参阅 [为 Azure 信息保护和发现服务或数据恢复配置超级用户](configure-super-users.md)中的 "最佳安全做法" 部分。 <br><br>**提示**：如果你的内容存储在 SharePoint 或 OneDrive 中，则管理员可以运行 [SensitivityLabelEncryptedFile](/powershell/module/sharepoint-online/unlock-sposensitivitylabelencryptedfile) cmdlet 以删除灵敏度标签和加密。 有关详细信息，请参阅 [Microsoft 365 文档](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files#remove-encryption-for-a-labeled-document)。 |
|**迁移到统一的标签存储**      |  如果要将 Azure 信息保护标签迁移到统一的标签存储，请务必参阅标签迁移文档中的以下部分： <br />[支持统一标签平台的管理角色](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform)。 |
| | |
### <a name="azure-information-protection-administrator"></a>Azure 信息保护管理员

此 Azure Active Directory 管理员角色允许管理员配置 Azure 信息保护，但不能配置其他服务。 

具有此角色的管理员可以：

- 激活和停用 Azure Rights Management 保护服务
- 配置保护设置和标签
- 配置 Azure 信息保护策略
- 运行[Azure 信息保护客户端](./rms-client/clientv2-admin-guide-powershell.md)和[AIPService 模块](administer-powershell.md)的所有 PowerShell cmdlet
    
若要将用户分配到此管理角色，请参阅[将用户分配到 Azure Active Directory 中的管理员角色](/azure/active-directory/active-directory-users-assign-role-azure-portal)。

> [!NOTE]
> 此角色不支持跟踪和撤消用户的文档，如果你的租户在 [统一的标签平台](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)上，则不支持在 Azure 门户中。
    
### <a name="compliance-administrator-or-compliance-data-administrator"></a>合规性管理员或合规性数据管理员

这些 Azure Active Directory 管理员角色使管理员能够：

- 配置 Azure 信息保护，包括激活和停用 Azure Rights Management 保护服务
- 配置保护设置和标签
- 配置 Azure 信息保护策略
- 运行 [Azure 信息保护客户端](./rms-client/clientv2-admin-guide-powershell.md) 和 [AIPService 模块](administer-powershell.md)的所有 PowerShell cmdlet。 

若要将用户分配到此管理角色，请参阅[将用户分配到 Azure Active Directory 中的管理员角色](/azure/active-directory/active-directory-users-assign-role-azure-portal)。 

若要查看具有这些角色的用户具有哪些其他权限，请参阅 Azure Active Directory 文档中的 " [可用角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) " 部分。

> [!NOTE]
> 这些角色不支持跟踪和撤消用户的文档。
>     
    
### <a name="security-reader-or-global-reader"></a>安全读取器或全局读取器

这些角色仅用于 [Azure 信息保护分析](reports-aip.md) ，并使管理员能够：

- 查看标签的使用方式
- 监视用户对标记文档和电子邮件的访问权限
- 查看对分类所做的更改
- 确定包含必须受到保护的敏感信息的文档 

由于此功能使用 Azure Monitor，因此还必须具有支持的 [RBAC 角色](reports-aip.md#permissions-required-for-azure-information-protection-analytics)。

### <a name="security-administrator"></a>安全管理员

此 Azure Active Directory 管理员角色使管理员能够在 Azure 门户以及其他 Azure 服务的某些方面配置 Azure 信息保护。 

具有此角色的管理员不能 [从 AIPService 模块运行任何 PowerShell cmdlet](administer-powershell.md)，也不能为用户跟踪和撤销文档。
    
若要将用户分配到此管理角色，请参阅[将用户分配到 Azure Active Directory 中的管理员角色](/azure/active-directory/active-directory-users-assign-role-azure-portal)。 

若要查看具有此角色的用户还拥有哪些其他权限，请参阅 Azure Active Directory 文档的[可用角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles)部分。

### <a name="azure-rights-management-global-administrator-and-connector-administrator"></a>Azure Rights Management 全局管理员和连接器管理员

全局管理员角色使用户能够 [从 AIPService 模块运行所有 PowerShell cmdlet](administer-powershell.md) ，而无需使其成为其他云服务的全局管理员。

连接器管理员角色使用户能够仅运行 Rights Management (RMS) 连接器。 

这些管理角色不会授予对管理控制台的权限，也不支持跟踪和撤消用户的文档。
    
若要分配其中任一管理角色，请使用 AIPService PowerShell cmdlet [AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator)。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure 信息保护是否支持本地和混合方案？

是的。 尽管 Azure 信息保护是基于云的解决方案，但它可对存储在本地和云中的文档和电子邮件进行分类、标签设置和保护。

如果你有 Exchange Server、SharePoint Server 和 Windows 文件服务器，请使用以下方法中的一种或两种：

- 部署 [Rights Management 连接器](deploy-rms-connector.md) ，以便这些本地服务器可以使用 Azure Rights Management 服务来保护你的电子邮件和文档
- 使用 Azure AD 同步和联合 Active Directory 域控制器，以便为用户提供更无缝的身份验证体验。 例如，使用 [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect)。

Azure Rights Management 服务根据需要自动生成并管理 XrML 证书，因此它不使用本地 PKI。 

有关 Azure Rights Management 如何使用证书的详细信息，请参阅 [Azure RMS 工作原理的演练：首次使用、内容保护、内容使用](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)。

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Azure 信息保护可以分类和保护哪些类型的数据？

Azure 信息保护可以分类和保护电子邮件和文档，无论它们是位于本地还是云中。 这些文档包括 Word 文档、Excel 电子表格，PowerPoint 演示文稿、PDF 文档、基于文本的文件和图像文件。 

有关详细信息，请参阅支持的完整列表 [文件类型](./rms-client/clientv2-admin-guide-file-types.md)。

> [!NOTE]
> Azure 信息保护无法对结构化数据（例如数据库文件、日历项、Yammer 帖子、Sway 内容和 OneNote 笔记本）进行分类和保护。
> 

> [!TIP]
> Power BI 支持通过使用敏感度标签进行分类，并且可以将这些标签中的保护应用于导出为以下文件格式的数据： .pdf、.xls 和 .ppt。 有关详细信息，请参阅 [Power BI 中的数据保护](/power-bi/admin/service-security-data-protection-overview)。
> 
## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>我看到 Azure 信息保护被列为可用于条件访问的云应用 - 工作原理是什么？

是的，作为预览产品，你可以为 Azure 信息保护配置 Azure AD 条件性访问。

当用户打开受 Azure 信息保护保护的文档时，管理员现可基于标准条件访问控制，阻止其租户中用户的访问或授予他们访问权限。 最常见的请求条件之一是需要多重身份验证 (MFA)。 另一种是设备必须 [符合你的 Intune 策略](/intune/protect/conditional-access-intune-common-ways-use) ，以便例如，移动设备满足你的密码要求和最低操作系统版本，并且计算机必须已加入域。

有关详细信息和演练示例，请参阅以下博客文章：[Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/)（Azure 信息保护的条件访问策略）。

其他信息：

|主题  |详细信息  |
|---------|---------|
|**评估频率**    | 对于 Windows 计算机和当前预览版本，在 [初始化用户环境](./how-does-it-work.md#initializing-the-user-environment) 时会评估 Azure 信息保护的条件性访问策略 (此过程也称为 "引导) ，然后每30天一次。<br /><br />若要微调条件访问策略的计算频率，请 [配置令牌生存期](/azure/active-directory/active-directory-configurable-token-lifetimes)。       |
|**管理员帐户**     |建议你不要将管理员帐户添加到条件访问策略，因为这些帐户将无法访问 Azure 门户中的 "Azure 信息保护" 窗格。         |
|**MFA 和 B2B 协作**     | 如果在条件访问策略中使用 MFA 与其他组织展开协作 (B2B)，则必须使用 [Azure AD B2B 协作](/azure/active-directory/b2b/what-is-b2b)，并为要在其他组织中共享的用户创建来宾帐户。        |
|**使用条款提示**     |  使用 Azure AD 12 月2018预览版，你现在可以提示用户在首次打开受保护文档之前 [接受使用条款](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822) 。       |
|**云应用**     |  如果针对条件访问使用许多云应用，则列表中可能不会显示“Microsoft Azure 信息保护”选项，因此无法进行选择。 <br /><br />在这种情况下，可使用列表顶部的搜索框。 开始键入“Microsoft Azure 信息保护”，筛选可用应用。 如果已有受支持的订阅，则可以看到“Microsoft Azure 信息保护”选项，可进行选择。        |
| | |

> [!NOTE]
> 用于条件访问的 Azure 信息保护支持目前以预览版提供。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 
> 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>我看到 Azure 信息保护被列为 Microsoft Graph 安全提供商，它是如何工作的？我将收到哪些警报？

是，作为公共预览版产品/服务，现可收到有关 **Azure 信息保护异常数据访问** 的警报。 当尝试访问由 Azure 信息保护进行保护的数据存在异常时，将触发此警报。 例如，访问大量的数据，在某天的异常时间访问或者从未知位置访问。

此类警报可以帮助你检测环境中与数据相关的高级攻击和内部威胁。 这些警报使用机器学习来分析访问受保护数据的用户的行为。 

可以通过[使用 Microsoft Graph 安全 API](/graph/api/resources/security-api-overview) 来访问 Azure信息保护警报，也可以使用 Azure Monitor 将[警报流式传输](/graph/security-integration)到 SIEM 解决方案，例如 Splunk 和 IBM Qradar。

有关 Microsoft Graph 安全 API 的详细信息，请参阅 [Microsoft Graph 安全 API 概述](/graph/security-concept-overview)。

> [!NOTE]
> Azure 信息保护对 Microsoft Graph 安全性的支持目前以预览版提供。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 
> 

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>我听说过，Azure 信息保护即将推出新版本，何时发布？

本技术文档不包含即将发布的版本的相关信息。 对于这种类型的信息，请使用 [Microsoft 365 路线图](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent)查看 [企业移动性 + 安全性博客](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services)。

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure 信息保护是否适用于我所在的国家/地区？

不同国家/地区的要求和法规不同。 要帮助你的组织回答此问题，请参阅[针对不同国家/地区的适用性](./compliance.md#suitability-for-different-countries)。

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Azure 信息保护如何帮助你符合 GDPR？

[!INCLUDE [gdpr-hybrid-note](includes/gdpr-hybrid-note.md)]

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>在何处可以找到 Azure 信息保护的支持信息 — 例如法律、合规性和 SLA？
请参阅 [Azure 信息保护的合规性和支持信息](./compliance.md)。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>如何针对 Azure 信息保护报告问题或发送反馈？

若要获取技术支持，请使用标准支持渠道或[联系 Microsoft 支持](information-support.md#to-contact-microsoft-support)。

我们还邀请你加入我们的工程团队：[Azure 信息保护 Yammer 站点](https://www.yammer.com/askipteam/)。 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>如果我的问题不在这里，我该怎么办？

首先，查看下面列出的常见问题，这些问题特定于分类和标签，或特定于数据保护。 [Azure Rights Management 服务 (Azure RMS) ](what-is-azure-rms.md)为 Azure 信息保护提供数据保护技术。 Azure RMS 可与分类和标签结合使用，也可单独使用。 

- [分类和标签 FAQ](faqs-infoprotect.md)

- [数据保护 FAQ](faqs-rms.md)

- [仅经典客户端的常见问题解答](faqs-classic.md)

如果你的问题未得到解答，请参阅 [Azure 信息保护的信息和支持](information-support.md)中列出的链接和资源。
