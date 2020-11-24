---
title: 已知问题 - Azure 信息保护
description: 搜索并浏览 Azure 信息保护的已知问题和限制。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0a1ac4e5470df68076585d9f328b28c76377a26d
ms.sourcegitcommit: 5b7235f7bb77cc88716f15dda0aa0d832e0f7063
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/24/2020
ms.locfileid: "95735008"
---
# <a name="known-issues---azure-information-protection"></a>已知问题 - Azure 信息保护

使用下面的列表和表来查找有关 Azure 信息保护功能相关的已知问题和限制的详细信息。

> [!NOTE]
> 本文介绍经典和统一标签客户端中的已知问题。 不确定这些客户端之间有何区别？ 请参阅 [常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。

## <a name="client-support-for-container-files-such-as-zip-files"></a>容器文件的客户端支持，例如 .zip 文件

容器文件是包括其他文件的文件，典型示例是包括压缩文件的 .zip 文件。 其他示例包括 .rar、.7z、.msg 文件和包含附件的 PDF 文档。

可对这些容器文件进行分类和保护，但分类和保护不会应用到容器内每个文件。

如果容器文件包括已分类和受保护的文件，必须先提取这些文件，以更改其分类或保护设置。 但是，使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet，可删除受支持容器文件中所有文件的保护。

Azure 信息保护查看器无法打开受保护的 PDF 文档中的附件。 在这种情况下，在查看器中打开文档时，附件不可见。

有关详细信息，请参阅 [管理员指南： Azure 信息保护客户端支持的文件类型](rms-client/client-admin-guide-file-types.md)。

## <a name="known-issues-for-aip-and-exploit-protection"></a>AIP 和 Exploit Protection 的已知问题

在安装了 [Exploit Protection](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) 的 .net 2 或3计算机上，不支持 Azure 信息保护客户端。

如果你的 .NET 版本为2或3，但你的系统需要 .NET 4.x 版本，请确保在安装 AIP 之前禁用 Exploit protection。 

若要通过 PowerShell 禁用 Exploit protection，请运行以下内容：

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

有关详细信息，请参阅 [Azure 信息保护统一标签客户端的其他先决条件](rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)。

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的 PowerShell 支持

与 Azure 信息保护客户端一起安装的 **AzureInformationProtection** PowerShell 模块的当前版本具有以下已知问题：

- **Outlook 个人文件夹 (*.pst * 文件) * *。 使用 **AzureInformationProtection** 模块不支持本机保护 *的 .pst* 文件。

- **Outlook 保护的电子邮件消息 *( .rpmsg* 文件)**。 仅当取消保护 Outlook 受保护的电子邮件位于 Outlook 个人文件夹 *( .pst* 文件) 中时，才 **支持该模块**。

    不支持 *.pst* 文件之外的取消保护电子邮件。

有关详细信息，请参阅 [管理员指南：将 PowerShell 与 Azure 信息保护客户端配合使用](rms-client/client-admin-guide-powershell.md)。

## <a name="aip-known-issues-in-office-applications"></a>AIP Office 应用程序中的已知问题

|功能  |已知问题  |
|---------|---------|
|**多个版本的 Office**    | Azure 信息保护客户端（包括经典和统一标记）都不支持在同一台计算机上使用 Office 的多个版本，也不支持在 Office 中切换用户帐户。       |
|**多显示器** |如果使用多个显示器并打开 Office 应用程序： <br><br>-你可能会遇到 Office 应用中的性能问题。<br>-Azure 信息保护栏在办公室屏幕中间可能显示为浮动，其中一个或两个显示器 <br><br>若要确保性能一致，并使该条形保持在正确的位置，请打开 Office 应用程序的 " **选项** " 对话框，并在 " **常规"** 下选择 " **优化兼容性** ，而不是 **优化以获得最佳外观"。**    |
|**Office 2016 中的 IRM 支持**| Azure 信息保护标签不支持用于控制 Office 2016 中元数据加密的 [DRMEncryptProperty](/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) 注册表设置。|
|**Word 中的内容标记**    | 当相同的页眉或页脚也包含一个表时，Microsoft Word 页眉或页脚中的 AIP [内容标记](configure-policy-markings.md) 可能会偏移或放置不正确，或者可能完全隐藏。<br><br>有关详细信息，请参阅 [何时应用视觉标记](configure-policy-markings.md#when-visual-markings-are-applied)。 |
|**附加到电子邮件的文件** |由于最新的 Windows 更新中的限制， [Microsoft Outlook 受 Azure Rights Management 保护](office-apps-services-support.md)，因此在打开该文件后，附加到电子邮件的文件可能会被锁定。 |
|**邮件合并**    |  Office [邮件合并](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705)功能无法与 Azure 信息保护功能配合使用。       |
| **S/MIME 电子邮件** | 在 Outlook 的阅读窗格中打开 S/MIME 电子邮件可能会造成性能问题。 <br><br>若要防止 S/MIME 电子邮件出现性能问题，请启用 [**OutlookSkipSmimeOnReadingPaneEnabled**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) 高级属性。 <br><br>**注意：** 启用此属性可防止 AIP 栏或电子邮件分类显示在 Outlook 的阅读窗格中。 |
|**"发送到文件资源管理器" 选项** |如果你选择在文件资源管理器中右键单击任何文件，然后选择 " **发送到 > 邮件收件人**"，则在附加了文件的情况下打开的 Outlook 邮件可能不会显示 AIP 工具栏。 <br><br>如果发生这种情况，并且你需要使用 AIP 工具栏选项，请从 Outlook 内启动电子邮件，然后浏览到并附加要发送的文件。|
| | |

## <a name="known-issues-in-policies"></a>策略中的已知问题

发布策略可能需要长达24小时。

## <a name="known-issues-in-the-aip-client"></a>AIP 客户端中的已知问题

- **最大文件大小。** 支持大于 2 GB 的文件进行保护，但不支持解密。

- **AIP 查看器。** "AIP 查看器" 以纵向模式显示图像，某些宽、横向视图的图像可能显示为已拉伸。

    例如，原始图像显示在左侧下方，在右侧的 AIP 查看器中显示为横向扩展版本。 
    
    :::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="客户端查看器中的拉伸图像":::
    
    有关详细信息，请参阅：

    - [**统一标签客户端**：通过 Azure 信息保护查看器查看受保护的文件](rms-client/clientv2-view-use-files.md)
    - [**经典客户端**：通过 Azure 信息保护查看器查看受保护的文件](rms-client/client-view-use-files.md)


## <a name="aip-for-windows-and-office-versions-in-extended-support"></a>AIP for Windows 和 Office 版本（扩展支持）

- [**Windows 7 扩展支持于2020年1月14日结束**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。 

    强烈建议升级到较新版本的 Windows 10。 但是，如果你有 (ESU) 的扩展安全更新和支持协定，则可以使用 AIP 支持来继续保护 Windows 7 系统的安全。

    有关详细信息，请与支持人员联系。

- [**Office 2010 当前提供扩展支持**](https://support.microsoft.com/lifecycle/search?alpha=office%202010)。 

    此支持将于10月13日（2020）结束，将不会进行扩展。 此外，不会为 Office 2010 提供 ESU，强烈建议升级到较新版本的 Office 365。 
    
    对于当前在扩展支持中运行 Office 2010 的客户，AIP 支持在2020年10月13日之前可用。 

    有关详细信息，请与支持人员联系。

## <a name="aip-based-conditional-access-policies"></a>基于 AIP 的条件性访问策略

接收受 [条件访问策略](/azure/active-directory/conditional-access/concept-conditional-access-policy-common) 保护的内容的外部用户必须 Azure Active Directory (Azure AD) 企业到企业 (B2B) 协作来宾用户帐户才能查看内容。

虽然你可以邀请外部用户激活来宾用户帐户，以便他们能够进行身份验证和传递条件访问要求，但可能很难确保为所需的所有外部用户进行此操作。

建议仅为内部用户启用基于 AIP 的条件性访问策略。

**仅为内部用户启用 AIP 的条件性访问策略：**

1.  在 Azure 门户中，导航到 " **条件性访问** " 边栏选项卡，然后选择要修改的条件性访问策略。 
2.  在 " **分配**" 下，选择 " **用户和组**"，然后选择 " **所有用户**"。 请确保 *未* 选中 "**所有来宾和外部用户**" 选项。
3.  保存所做更改。 
 
如果你的组织不需要该功能，则还可以在 Azure 信息保护中完全禁用 CA，以避免此潜在问题。 

有关详细信息，请参阅 [条件访问文档](/azure/active-directory/conditional-access/concept-conditional-access-users-groups)。

## <a name="more-information"></a>详细信息

以下附加文章可能有助于回答有关 Azure 信息保护中已知问题的问题：

- [有关 Azure 信息保护的常见问题](faqs.md)
- [Azure 信息保护中的有关数据保护的常见问题](faqs-rms.md)
- [有关 Azure 信息保护中的分类和标签的常见问题](faqs-infoprotect.md)
- [适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题解答](rms-client/mobile-app-faq.md)