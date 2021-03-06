---
title: 已知问题 - Azure 信息保护
description: 搜索并浏览 Azure 信息保护的已知问题和限制。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/01/2021
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 77016efd46f045f324c9dea540d3b7ce75415d1d
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446960"
---
# <a name="known-issues---azure-information-protection"></a>已知问题 - Azure 信息保护

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>相关内容：*[AIP 统一标记客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

使用下面的列表和表来查找有关 Azure 信息保护功能相关的已知问题和限制的详细信息。

## <a name="client-support-for-container-files-such-as-zip-files"></a>容器文件的客户端支持，例如 .zip 文件

容器文件是包括其他文件的文件，典型示例是包括压缩文件的 .zip 文件。 其他示例包括 .rar、.7z、.msg 文件和包含附件的 PDF 文档。

可对这些容器文件进行分类和保护，但分类和保护不会应用到容器内每个文件。

如果容器文件包括已分类和受保护的文件，必须先提取这些文件，以更改其分类或保护设置。 但是，使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet，可删除受支持容器文件中所有文件的保护。

Azure 信息保护查看器无法打开受保护的 PDF 文档中的附件。 在这种情况下，在查看器中打开文档时，附件不可见。

有关详细信息，请参阅 [管理员指南： Azure 信息保护客户端支持的文件类型](rms-client/client-admin-guide-file-types.md)。

## <a name="known-issues-for-aip-and-exploit-protection"></a>AIP 和 Exploit Protection 的已知问题

Azure 信息保护客户端在具有 .NET 2 或3的计算机上不受支持，其中启用了 [Exploit Protection](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) ，并将导致 Office 应用程序意外运行。

在这种情况下，我们建议升级 .NET 版本。 有关详细信息，请参阅 [Microsoft .NET 框架要求](rms-client/reqs-ul-client.md#microsoft-net-framework-requirements)。

如果必须保留 .NET 版本2或3，请确保在安装 AIP 之前禁用 Exploit protection。 

若要通过 PowerShell 禁用 Exploit protection，请运行以下内容：

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的 PowerShell 支持

与 Azure 信息保护客户端一起安装的 **AzureInformationProtection** PowerShell 模块的当前版本具有以下已知问题：

- **Outlook 个人文件夹 (*.pst * 文件) * *。 使用 **AzureInformationProtection** 模块不支持本机保护 *的 .pst* 文件。

- **Outlook 保护的电子邮件消息 *( .rpmsg* 文件)**。 仅当取消保护 Outlook 受保护的电子邮件位于 Outlook 个人文件夹 *( .pst* 文件) 中时，才 **支持该模块**。

    不支持 *.pst* 文件之外的取消保护电子邮件。

有关详细信息，请参阅 [管理员指南：将 PowerShell 与 Azure 信息保护客户端配合使用](rms-client/client-admin-guide-powershell.md)。

## <a name="aip-known-issues-in-office-applications"></a>AIP Office 应用程序中的已知问题

|功能  |已知问题  |
|---------|---------|
|**多个版本的 Office <br> <br> 多个 office 帐户**    | Azure 信息保护客户端（包括经典标签和统一标签）不支持：  <br><br>-同一台计算机上有多个版本的 Office <br>-多个 Office 帐户，或在 Office 中切换用户帐户 <br>-共享邮箱     |
|**多显示器** |如果使用多个显示器并打开 Office 应用程序： <br><br>-你可能会遇到 Office 应用中的性能问题。<br>-Azure 信息保护栏在办公室屏幕中间可能显示为浮动，其中一个或两个显示器 <br><br>若要确保性能一致，并使该条形保持在正确的位置，请打开 Office 应用程序的 " **选项** " 对话框，并在 " **常规**" 下选择 " **优化兼容性** ，而不是 **优化以获得最佳外观**"。    |
|**Office 2016 中的 IRM 支持**| Azure 信息保护标签不支持用于控制 Office 2016 中元数据加密的 [DRMEncryptProperty](/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) 注册表设置。|
|**Outlook 对象模型访问** | -在 Azure 信息保护标签中不支持通过 Outlook 对象模型访问通讯簿时显示的提示的 [PromptOOMAddressBookAccess](/outlook/troubleshoot/security/information-about-email-security-settings#configure-a-prompt-when-a-program-accesses-an-address-book-by-using-the-outlook-object-model) 注册表设置。 <br><br>-" [PromptOOMAddressInformationAccess](/outlook/troubleshoot/security/information-about-email-security-settings#configure-a-prompt-when-a-program-reads-address-information-by-using-the-outlook-object-model) " 注册表设置，它控制在程序读取地址信息时显示的提示，不支持 Azure 信息保护标签。|
|**Word 中的内容标记**    | 当相同的页眉或页脚也包含一个表时，Microsoft Word 页眉或页脚中的 AIP [内容标记](configure-policy-markings.md) 可能会偏移或放置不正确，或者可能完全隐藏。<br><br>有关详细信息，请参阅 [何时应用视觉标记](configure-policy-markings.md#when-visual-markings-are-applied)。 |
|**附加到电子邮件的文件** |由于最新的 Windows 更新中的限制， [Microsoft Outlook 受 Azure Rights Management 保护](office-apps-services-support.md)，因此在打开该文件后，附加到电子邮件的文件可能会被锁定。 |
|**邮件合并**    |  Office [邮件合并](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705)功能无法与 Azure 信息保护功能配合使用。       |
| **S/MIME 电子邮件** | 在 Outlook 的阅读窗格中打开 S/MIME 电子邮件可能会造成性能问题。 <br><br>若要防止 S/MIME 电子邮件出现性能问题，请启用 [**OutlookSkipSmimeOnReadingPaneEnabled**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) 高级属性。 <br><br>**注意**：启用此属性可防止 AIP 栏或电子邮件分类显示在 Outlook 的阅读窗格中。 |
|**"发送到文件资源管理器" 选项** |如果你选择在文件资源管理器中右键单击任何文件，然后选择 " **发送到 > 邮件收件人**"，则在附加了文件的情况下打开的 Outlook 邮件可能不会显示 AIP 工具栏。 <br><br>如果发生这种情况，并且你需要使用 AIP 工具栏选项，请从 Outlook 内启动电子邮件，然后浏览到并附加要发送的文件。|
|**共同创作** |共同创作支持由 Azure 信息保护客户端的 [专用安装](rms-client/unifiedlabelingclient-version-release-history.md#version-210460-for-co-authoring-public-preview) 提供，目前以公共预览版提供。 <br><br>有关详细信息，请参阅 [共同创作 (公开预览版) 的已知问题 ](#known-issues-for-co-authoring-public-preview)。 |
| | |

### <a name="known-issues-for-co-authoring-public-preview"></a>共同创作 (公开预览版的已知问题) 

- [仅在测试环境中使用](#use-in-testing-environments-only)
- [共同创作和敏感度标签支持的版本](#supported-versions-for-co-authoring-and-sensitivity-labels)
- [策略更新](#policy-updates)
- [AIP 分析和审核日志](#aip-analytics-and-audit-logs)
- [具有用户定义的权限的标签](#labels-with-user-defined-permissions)
- [共同创作的不支持的功能](#unsupported-features-for-co-authoring)

> [!IMPORTANT]
> 不能将共同创作和敏感度标签部署到某些用户，因为使用较早版本的 Office 客户端的用户将看不到任何新标签。
> 
有关共同创作支持的详细信息，包括公共预览版的限制和已知问题，请参阅 [Microsoft 365 文档](/microsoft-365/compliance/sensitivity-labels-coauthoring)。

#### <a name="use-in-testing-environments-only"></a>仅在测试环境中使用

若要避免标记文件之间的冲突，在公共预览期间，不能通过客户支持来帮助共同创作共同创作。

出于此原因，我们建议您仅在测试环境中对系统启用共同创作。

#### <a name="supported-versions-for-co-authoring-and-sensitivity-labels"></a>共同创作和敏感度标签支持的版本

租户中的所有应用、服务和操作工具都必须支持共同创作。

在开始之前，请确保你的系统符合 [共同创作 Microsoft 365 先决条件](/microsoft-365/compliance/sensitivity-labels-coauthoring#prerequisites)中列出的版本要求。

> [!NOTE]
> 尽管可以对 Office 97-2003 格式的文件应用敏感度标签（例如  **.doc**、 **.ppt** 和 **.xls**），但不支持对这些文件类型进行共同创作。 将标签应用于新创建的文件或高级文件格式的文件（如 **.docx**、 **.pptx** 和 **.Xlsx**）后，以 Office 97-2003 格式保存该文件将导致删除该标签。
> 

#### <a name="policy-updates"></a>策略更新

如果在使用 Azure 信息保护打开 Office 应用程序时更新了标签策略，则会显示任何新标签，但应用它们会导致错误。 

如果出现这种情况，请关闭并重新打开 Office 应用程序，以便能够应用标签。

#### <a name="aip-analytics-and-audit-logs"></a>AIP 分析和审核日志

启用共同创作后，Azure 信息保护客户端不会发送任何 [审核日志](audit-logs.md)。

#### <a name="labels-with-user-defined-permissions"></a>具有用户定义的权限的标签

在 Microsoft Word、Excel 和 PowerPoint 中，具有用户定义的权限的标签仍可用，可以应用于文档，但共同创作功能不支持。 

这意味着，应用具有用户定义的权限的标签将会阻止您同时处理文档。

#### <a name="unsupported-features-for-co-authoring"></a>共同创作的不支持的功能

使用共同创作和敏感度标签时，不支持以下功能：

- **DKE 模板和 DKE 用户定义的属性**。 有关详细信息，请参阅 [双重密钥加密 (DKE) ](plan-implement-tenant-key.md#double-key-encryption-dke)。

- **删除应用中的外部内容标记**。 有关详细信息，请参阅 [Azure 信息保护的客户端](rms-client/use-client.md)。

- 以下高级设置：

    - **customPropertiesByLabel**。 有关详细信息，请参阅 [应用标签时应用自定义属性](rms-client/clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)。

    - **labelByCustomProperties** 和 **EnableLabelBySharePointProperties**。 有关详细信息，请参阅 [从安全孤岛迁移标签和其他标记解决方案](rms-client/clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)。

## <a name="known-issues-in-policies"></a>策略中的已知问题

发布策略可能需要长达24小时。

## <a name="maximum-file-sizes"></a>最大文件大小

支持大于 2 GB 的文件进行保护，但不支持解密。

## <a name="known-issues-for-the-aip-viewer"></a>AIP 查看器的已知问题

- [横向视图](#landscape-views-in-the-aip-viewer)
- [外部用户](#external-users-and-the-aip-viewer)

有关详细信息，请参阅 [**统一标签客户端**：通过 Azure 信息保护查看器查看受保护的文件](rms-client/clientv2-view-use-files.md)。
### <a name="landscape-views-in-the-aip-viewer"></a>AIP 查看器中的横向视图

"AIP 查看器" 以纵向模式显示图像，某些宽、横向视图的图像可能显示为已拉伸。

例如，原始图像显示在左侧下方，在右侧的 AIP 查看器中显示为横向扩展版本。 

:::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="客户端查看器中的拉伸图像":::

### <a name="external-users-and-the-aip-viewer"></a>外部用户和 AIP 查看器 

如果外部用户在 Azure AD 中已经有了 guest 帐户，则当用户打开受保护的文档时，AIP 查看器可能会显示错误，告知他们无法使用个人帐户登录。

如果出现此类错误，用户必须安装 [具有 MIP 扩展的 Adobe ACROBAT DC](https://helpx.adobe.com/il_en/acrobat/kb/mip-plugin-download.html) 才能打开受保护的文档。

使用 MIP 扩展安装 Adobe Acrobat DC 后打开受保护的文档时，用户可能仍会看到一个错误，指出租户中不存在所选用户帐户，并提示他们选择帐户。 

这是预期的错误。 在提示窗口中，选择 " **返回** " 以继续打开受保护的文档。

## <a name="known-issues-for-track-and-revoke-features-public-preview"></a> (公开预览版跟踪和撤消功能的已知问题) 

使用统一标签客户端跟踪和撤消文档访问具有以下已知问题：

- [受密码保护的文档](#password-protected-documents)
- [受保护的电子邮件中的多个附件](#multiple-attachments-in-a-protected-email)
- [通过 SharePoint 或 OneDrive 访问的文档](#documents-accessed-via-sharepoint-or-onedrive)

有关详细信息，请参阅 [管理员指南](rms-client/track-and-revoke-admin.md) 和 [用户指南](rms-client/revoke-access-user.md) 过程。

#### <a name="password-protected-documents"></a>受密码保护的文档

跟踪和撤消功能不支持受密码保护的文档。
#### <a name="multiple-attachments-in-a-protected-email"></a>受保护的电子邮件中的多个附件

如果将多个文档附加到电子邮件，然后保护并发送该电子邮件，则每个附件会获得相同的 Id 为值。

此 Id 为值将仅与已打开的第一个文件一起返回。 搜索其他附件不会返回获取跟踪数据所需的 Id 为值。

此外，撤消其中一个附件的访问权限还会撤消同一受保护电子邮件中其他附件的访问权限。

#### <a name="documents-accessed-via-sharepoint-or-onedrive"></a>通过 SharePoint 或 OneDrive 访问的文档

- 上载到 SharePoint 或 OneDrive 的受保护文档将丢失其 **id 为** 值，并且无法跟踪或撤销访问权限。

- 如果用户从 SharePoint 或 OneDrive 下载文件，并从本地计算机访问该文件，则在本地打开该文档时，新的 **id 为** 将应用到该文档。

    使用原始 **id 为** 值跟踪数据时，不会包括为用户下载的文件执行的任何访问权限。 此外，根据原始 **id 为** 值撤消访问权限将不会撤销对任何已下载文件的访问权限。

    在这种情况下，管理员可能能够使用 PowerShell 查找已下载的文件，以查找要跟踪或撤销访问权限的新 **id 为** 值。

### <a name="known-issues-for-the-aip-client-and-onedrive"></a>AIP 客户端和 OneDrive 的已知问题

如果你的文档存储在 OneDrive 中并且应用了敏感度标签，并且管理员更改了标记策略中的标签以添加保护，则新应用的保护不会自动应用于标记的文档。 

在这种情况下，请手动重新标记文档以根据需要应用保护。
## <a name="aip-and-legacy-windows-and-office-versions"></a>AIP 和旧版 Windows 和 Office 版本

- [**Windows 7 扩展支持于2020年1月14日结束**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

    强烈建议升级到较新版本的 Windows 10。

    但是，如果你有 (ESU) 的扩展安全更新和支持协定，则可以使用 AIP 支持来继续保护 Windows 7 系统的安全。

    有关详细信息，请与支持人员联系。

- [**Office 2010 扩展支持于2020年10月13日结束**](https://support.microsoft.com/lifecycle/search?alpha=office%202010)。

    此支持将不会扩展，并且不会为 Office 2010 提供 ESU。

    强烈建议升级到较新版本的 Office 365。

    有关详细信息，请与支持人员联系。

## <a name="aip-based-conditional-access-policies"></a>基于 AIP 的条件性访问策略

接收受 [条件访问策略](/azure/active-directory/conditional-access/concept-conditional-access-policy-common) 保护的内容的外部用户必须 Azure Active Directory (Azure AD) 企业到企业 (B2B) 协作来宾用户帐户才能查看内容。

虽然你可以邀请外部用户激活来宾用户帐户，以便他们能够进行身份验证和传递条件访问要求，但可能很难确保为所需的所有外部用户进行此操作。

建议仅为内部用户启用基于 AIP 的条件性访问策略。

**仅为内部用户启用 AIP 的条件性访问策略**：

1.  在 Azure 门户中，导航到 " **条件性访问** " 边栏选项卡，然后选择要修改的条件性访问策略。
2.  在 " **分配**" 下，选择 " **用户和组**"，然后选择 " **所有用户**"。 请确保 *未* 选中 "**所有来宾和外部用户**" 选项。
3.  保存所做更改。

如果你的组织不需要该功能，则还可以在 Azure 信息保护中完全禁用 CA，以避免此潜在问题。

有关详细信息，请参阅 [条件访问文档](/azure/active-directory/conditional-access/concept-conditional-access-users-groups)。

## <a name="more-information"></a>更多信息

以下附加文章可能有助于回答有关 Azure 信息保护中已知问题的问题：

- [有关 Azure 信息保护的常见问题](faqs.md)
- [Azure 信息保护中的有关数据保护的常见问题](faqs-rms.md)
- [有关 Azure 信息保护中的分类和标签的常见问题](faqs-infoprotect.md)
- [适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题解答](rms-client/mobile-app-faq.md)