---
title: Azure 信息保护经典客户端的常见问题解答
description: 一些有关 Azure 信息保护及其保护服务、Azure Rights Management (Azure RMS) 的常见问题。 此处列出的 Faq 仅适用于 AIP 经典客户端。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 9f53544a201d3500f63c472b5cdd58e01c69dc1f
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446892"
---
# <a name="frequently-asked-questions-for-the-azure-information-protection-classic-client"></a>Azure 信息保护经典客户端常见问题

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>***相关** 内容： [仅限经典客户端 AIP 统一标签](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关详细信息，请参阅 [Azure 信息保护的常见问题](faqs.md)。 *

本文列出了仅与 Azure 信息保护经典客户端相关的常见问题。

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure 信息保护客户端是否只适用于包含分类和标记的订阅？

不是。 经典 AIP 客户端还可用于仅包含 Azure Rights Management 服务的订阅，以实现数据保护。

如果在未安装 Azure 信息保护策略的情况下安装经典客户端，客户端将自动在 [仅保护模式下](./rms-client/client-protection-only-mode.md)运行，这使用户可以应用 Rights Management 模板和自定义权限。 

如果以后购买确实包含分类和标记的订阅，客户端会在下载 Azure 信息保护策略后自动切换到标准模式。


## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI 和 Azure 信息保护扫描程序之间的区别是什么？

Windows Server 文件分类基础结构在过去一直都有一个选项：对文档进行分类，然后使用 [Rights Management 连接器](deploy-rms-connector.md)（仅 Office 文档）或 [PowerShell 脚本](./rms-client/configure-fci.md)（所有文件类型）保护文档。 

我们现在建议你使用 [Azure 信息保护扫描程序](deploy-aip-scanner.md)。 扫描程序使用 Azure 信息保护客户端和 Azure 信息保护策略来为文档（所有文件类型）添加标签，然后可以对这些文档进行分类并且还可根据需要保护文档。

这两种解决方案的主要差异是：

|  |Windows Server FCI  |Azure 信息保护扫描程序  |
|---------|---------|---------|
|**支持的数据存储**    | Windows Server 上的本地文件夹        | - Windows 文件共享和网络连接存储<br /><br />- SharePoint Server 2016 和 SharePoint Server 2013。 对于具有[对此版本 SharePoint 的延长支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)的客户，还支持 SharePoint Server 2010。        |
|**操作模式**     |真实数据         |系统地对数据存储进行一次或重复爬网         |
|**支持的文件类型**     | - 默认保护所有文件类型 <br /><br />- 通过编辑注册表，可以从保护配置中排除特定文件类型|对文件类型的支持： <br /><br />- 默认保护 Office 文件类型和 PDF 文档 <br /><br />- 通过编辑注册表，可以将其他文件类型纳入保护|

### <a name="setting-rights-management-owners"></a>设置 Rights Management 所有者

默认情况下，对于 Windows Server FCI 和 Azure 信息保护扫描程序， [Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) 设置为保护文件的帐户。

覆盖默认设置，如下所示：

- **Windows SERVER FCI**：将 Rights Management 所有者设置为所有文件的单个帐户，或者为每个文件动态设置 Rights Management 所有者。 

    若要动态设置 Rights Management 所有者，请使用 -OwnerMail [源文件所有者电子邮件] 参数和值。 此配置使用文件“所有者”属性中的用户帐户名从 Active Directory 检索用户的电子邮件地址。

- **Azure 信息保护扫描程序**：对于新保护的文件，请通过在扫描程序配置文件中指定 **默认所有者** 设置，将 Rights Management 所有者设置为指定数据存储中所有文件的单个帐户。 

    不支持为每个文件动态设置 Rights Management 所有者，也不会更改以前受保护文件的 Rights Management 所有者。 

    > [!NOTE]
    > 扫描程序保护 SharePoint 网站和库上的文件时，通过使用 SharePoint 编辑者值来动态地设置每个文件的 Rights Management 所有者。

## <a name="can-a-file-have-more-than-one-classification"></a>文件是否可以有多个分类？

用户一次仅可为每个文档或电子邮件选择一个标签，这通常只会产生一个分类。 但如果用户选择子标签，这实际上会同时应用两个标签；主标签和次要标签。 通过使用子标签，文件可以有两个分类，表示附加控制级别的父\子关系。

例如，标签“机密”可能包含子标签，如“法律”和“财务”。 可对这些子标签应用不同的分类视觉标记和不同的权限管理模板。 用户不能自行选择“机密”标签；只能选择其中一个子标签，如“法律”。 因此，会看到设置的标签是“机密\法律”。 该文件的元数据包括“Confidential”的一个自定义文本属性和“Legal”的一个自定义文本属性，以及另一个同时包含这两个值（“Confidential Legal”）的自定义文本属性。 

使用子标签时，请不要在主标签处配置视觉标记、保护和条件。 使用子级别时，请仅在子标签上配置这些设置。 如果在主标签及其子标签上配置这些设置，那么子标签上的设置具有更高优先级。
## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>如何防止他人删除或更改标签？

尽管有一个 [策略设置](configure-policy-settings.md) 要求用户指出为什么要降低分类标签、删除标签或删除保护的原因，但此设置不会阻止这些操作。 若要防止用户删除或更改标签，内容必须已受保护，并且保护权限不向用户授予 "导出" 或 "完全控制" [使用权限](configure-usage-rights.md)

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP 解决方案和其他应用如何与 Azure 信息保护相集成？

因为 Azure 信息保护将永久性元数据用于分类（包括明文标签），所以此信息可供 DLP 解决方案和其他应用程序读取。 

有关此元数据的详细信息，请参阅[电子邮件和文档中存储的标签信息](configure-policy.md#label-information-stored-in-emails-and-documents)。

有关将此元数据与 Exchange Online 邮件流规则配合使用的示例，请参阅[配置 Azure 信息保护标签的 Exchange Online 邮件流规则](configure-exo-rules.md)。

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>我能否创建自动包含分类的文档模板？

是的。 可以将标签配置为，[应用包含标签名称的页眉或页脚](configure-policy-markings.md)。 但如果不满足你的要求，则仅针对 Azure 信息保护经典客户端，你可以创建具有所需格式的文档模板，并将分类添加为字段代码。 

例如，文档的页眉中可能有一个显示分类的表。 或者，对引用文档分类的简介使用具体的字词。

若要在文档中添加此域代码，请执行以下操作：

1. 标记并保存文档。 此操作新建可立即用于域代码的元数据字段。

2. 在文档中，将光标置于要添加标签分类的位置，再在“插入”选项卡中依次选择“文本” > “文档部件” > “字段”。

3. 在“字段”对话框中，选择“类别”下拉列表中的“文档信息”。 然后，选择“字段名称”下拉列表中的“DocProperty”。

4. 在“属性”下拉列表中，依次选择“敏感度”和“确定”。

此时，当前标签的分类显示在文档中，并且这个值会在你每次打开文档或使用模板时自动刷新。 因此，如果标签发生更改，那么对此域代码显示的分类也会在文档中自动更新。

## <a name="how-is-classification-for-emails-using-azure-information-protection-different-from-exchange-message-classification"></a>使用 Azure 信息保护的电子邮件分类与 Exchange 邮件分类有何不同？

交换消息分类是一项较旧的功能，可对电子邮件进行分类，并且独立于 Azure 信息保护标签或应用分类的敏感度标签。

但是，你可以将此较旧的功能与标签集成，以便当用户使用 Outlook web 上的 Outlook 以及使用某些移动邮件应用程序对电子邮件进行分类时，会自动添加标签分类和相应的标签标记。

可以使用同一技术将标签用于 Outlook 网页版和这些移动邮件应用程序。

请注意，如果在使用 Exchange Online 的 web 上使用 Outlook，则无需执行此操作，因为这种组合在从 Office 365 Security & 相容性中心、Microsoft 365 安全中心或 Microsoft 合规中心发布敏感度标签时支持内置标签。

如果无法在 web 上使用 Outlook 内置标签，请参阅此解决方法的配置步骤： [与旧 Exchange 消息分类的集成](rms-client/client-admin-guide-customizations.md#integration-with-the-legacy-exchange-message-classification)

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>如何配置 Mac 计算机以保护和跟踪文档？

首先，请确保已使用 https://admin.microsoft.com 上的软件安装链接安装了 Office for Mac。 有关完整说明，请参阅 [在电脑或 Mac 上下载并安装或重新安装 Microsoft 365 或 Office 2019](https://support.office.com/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658)。

打开 Outlook 并使用您 Microsoft 365 的工作或学校帐户创建配置文件。 然后，创建新邮件，并执行以下操作来配置 Office，使其可以使用 Azure Rights Management 服务来保护文档和电子邮件：

1. 在新邮件的“选项”选项卡上，单击“权限”，然后单击“验证凭据”。

2. 出现提示时，再次指定 Microsoft 365 的工作或学校帐户详细信息，然后选择 " **登录**"。

    这将下载 Azure Rights Management 模板，“验证凭据”选项将替换为包括“无限制”、“不要转发”以及为租户发布任何 Azure Rights Management 模板的选项。 现在可以取消此新邮件。

保护电子邮件或文档：在“选项”选项卡上，单击“权限”，然后选择用于保护电子邮件或文档的选项或模板。

在保护文档之后跟踪文档：在安装了 Azure 信息保护经典客户端的 Windows 计算机上，使用 Office 应用程序或文件资源管理器将文档注册到文档跟踪站点。 有关说明，请参阅[跟踪和撤销文档](./rms-client/client-track-revoke.md)。 现在可以从 Mac 计算机使用 Web 浏览器访问文档跟踪站点 (https://track.azurerms.com) 来跟踪和撤销此文档。

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>在文档跟踪站点中测试吊销时，显式的消息提示人们仍可在 30 天内访问此文档—该时间段是否可配置？

是的。 该消息反映了此特定文件的[使用许可证](configure-usage-rights.md#rights-management-use-license)。

如果撤销文件，仅在用户对 Azure Rights Management 服务进行身份验证时才会强制执行此操作。 因此，如果文件的使用许可证有效期为 30 天，且用户已经打开过文档，则该用户在使用许可证期间仍继续拥有该文档的访问权限。 使用许可证过期时，用户必须重新进行身份验证，此时由于文件被撤销，因此会拒绝用户访问。

保护文档的用户，即 [Rights Management 颁发者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)不受此撤销的限制，始终能够访问其文档。

租户使用许可证有效期的默认值为 30 天，此设置可通过标签或模板中限制性更强的设置进行替代。 若要详细了解使用许可证以及如何对其进行配置，请参阅 [Rights Management 使用许可证](configure-usage-rights.md#rights-management-use-license)文档。

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>BYOK 和 HYOK 之间的区别是什么，应何时使用它们？

Azure 信息保护上下文中出现 **自带密钥** (BYOK) 时，则表示应为 Azure Rights Management 保护创建自己的本地密钥。 然后将该密钥传输到 Azure Key Vault 中的硬件安全模块 (HSM)，可在其中继续拥有并管理密钥。 若不执行此操作，Azure Rights Management 保护会使用 Azure 中自动创建并进行管理的密钥。 这种默认配置称为“Microsoft 管理”而不是“客户管理”（BYOK 选项）。

有关 BYOK 以及是否应为组织选择此密钥拓扑的详细信息，请参阅[规划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

在 Azure 信息保护的上下文中出现 **自留密钥** (HYOK)，则表示少量组织的文档或电子邮件自己无法通过存储在云中的密钥进行保护。 对于这些组织来说，即使使用 BYOK 创建和管理密钥，此限制仍然适用。 此限制通常是由于法规或符合性问题引起的，并且 HYOK 配置应仅应用于“顶级机密”信息，此信息永远不会在组织外部共享、仅会在内部网络中使用，并且无需通过移动设备访问。

对于这些异常（通常需要保护的内容少于所有内容的 10%），组织可使用本地解决方案 Active Directory Rights Management Services 创建保留在本地的密钥。 通过此解决方案，计算机可从云中获取其 Azure 信息保护策略，但可使用本地密钥来保护此标识的内容。

若要深入了解 HYOK 并确保了解其局限性和限制及使用指南，请参阅 [AD RMS 保护的自留密钥 (HYOK) 要求和限制](configure-adrms-restrictions.md)。

## <a name="what-do-i-do-if-my-question-isnt-here"></a>如果我的问题不在这里，我该怎么办？

首先，查看下面列出的常见问题，这些问题特定于分类和标签，或特定于数据保护。 [Azure Rights Management 服务 (Azure RMS) ](what-is-azure-rms.md)为 Azure 信息保护提供数据保护技术。 Azure RMS 可与分类和标签结合使用，也可单独使用。 

- [有关 Azure 信息保护的常见问题](faqs.md)

- [分类和标签 FAQ](faqs-infoprotect.md)

- [数据保护 FAQ](faqs-rms.md)

如果你的问题未得到解答，请参阅 [Azure 信息保护的信息和支持](information-support.md)中列出的链接和资源。

此外，我们还为最终用户制作了常见问题解答：

- [适用于 iOS 和 Android 的 Azure 信息保护应用的常见问题解答](./rms-client/mobile-app-faq.md)

- [适用于 Mac 计算机的 RMS 共享应用的常见问题解答](/previous-versions/msdn10/dn451248(v=msdn.10))