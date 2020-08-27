---
title: 已知问题-Azure 信息保护
description: 搜索并浏览 Azure 信息保护的已知问题和限制。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/10/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: af4a6989dca815d204fee72aafa6d839d2673fc4
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88952855"
---
# <a name="known-issues---azure-information-protection"></a>已知问题-Azure 信息保护

使用下面的列表和表来查找有关 Azure 信息保护功能相关的已知问题和限制的详细信息。

> [!NOTE]
> 本文介绍经典和统一标签客户端中的已知问题。 不确定这些客户端之间有何区别？ 请参阅 [常见问题解答](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。

## <a name="client-support-for-container-files-such-as-zip-files"></a>容器文件的客户端支持，例如 .zip 文件

容器文件是包括其他文件的文件，典型示例是包括压缩文件的 .zip 文件。 其他示例包括 .rar、.7z、.msg 文件和包含附件的 PDF 文档。

可对这些容器文件进行分类和保护，但分类和保护不会应用到容器内每个文件。

如果容器文件包括已分类和受保护的文件，必须先提取这些文件，以更改其分类或保护设置。 但是，使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet，可删除受支持容器文件中所有文件的保护。

Azure 信息保护查看器无法打开受保护的 PDF 文档中的附件。 在这种情况下，在查看器中打开文档时，附件不可见。

有关详细信息，请参阅 [管理员指南： Azure 信息保护客户端支持的文件类型](rms-client/client-admin-guide-file-types.md)。

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的 PowerShell 支持

与 Azure 信息保护客户端一起安装的 **AzureInformationProtection** PowerShell 模块的当前版本具有以下已知问题：

- **Outlook 个人文件夹 (*.pst * 文件) * *。 使用**AzureInformationProtection**模块不支持本机保护*的 .pst*文件。

- **Outlook 保护的电子邮件消息 * ( .rpmsg* 文件) **。 仅当取消保护 Outlook 受保护的电子邮件位于 Outlook 个人文件夹* ( .pst*文件) 中时，才**支持该模块**。

    不支持 *.pst* 文件之外的取消保护电子邮件。

有关详细信息，请参阅 [管理员指南：将 PowerShell 与 Azure 信息保护客户端配合使用](rms-client/client-admin-guide-powershell.md)。

## <a name="aip-known-issues-in-office-applications"></a>AIP Office 应用程序中的已知问题

|功能  |已知问题  |
|---------|---------|
|**多个版本的 Office**    | Azure 信息保护客户端（包括经典标签和统一标签）在同一台计算机上不支持多个 Office 版本，或在 Office 中切换用户帐户。       |
|**多显示器** |如果使用多个显示器并打开 Office 应用程序： </br></br>-你可能会遇到 Office 应用中的性能问题。</br>-Azure 信息保护栏在办公室屏幕中间可能显示为浮动，其中一个或两个显示器 </br></br>若要确保性能一致，并使该条形保持在正确的位置，请打开 Office 应用程序的 " **选项** " 对话框，并在 " **常规"** 下选择 " **优化兼容性** ，而不是 **优化以获得最佳外观"。**    |
|**Office 2016 中的 IRM 支持**| Azure 信息保护标签不支持用于控制 Office 2016 中元数据加密的 [DRMEncryptProperty](https://docs.microsoft.com/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) 注册表设置。|
|**Word 中的内容标记**    | 当页脚中还包含一个表时，Azure 信息保护内容 [标记](configure-policy-markings.md) 可能会隐藏在 Microsoft Word 页脚中。 有关详细信息，请参阅 [何时应用视觉标记](configure-policy-markings.md#when-visual-markings-are-applied)。 |
|**附加到电子邮件的文件** |由于最新的 Windows 更新中的限制， [Microsoft Outlook 受 Azure Rights Management 保护](office-apps-services-support.md)，因此在打开该文件后，附加到电子邮件的文件可能会被锁定。 |
|**邮件合并**    |  Azure 信息保护功能不支持 Office [邮件合并](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) 功能。       |
| | |

## <a name="known-issues-in-policies"></a>策略中的已知问题

发布策略可能需要长达24小时。

## <a name="known-issues-in-the-aip-client"></a>AIP 客户端中的已知问题

- **最大文件大小。** 支持大于 2 GB 的文件进行保护，但不支持解密。

- **AIP 查看器。** "AIP 查看器" 以纵向模式显示图像，某些宽、横向视图的图像可能显示为已拉伸。

    例如，原始图像显示在左侧下方，在右侧的 AIP 查看器中显示为横向扩展版本。 
    
    :::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="客户端查看器中的拉伸图像":::
    
    有关详细信息，请参阅：

    - [**经典客户端**：通过 Azure 信息保护查看器查看受保护的文件](rms-client/client-view-use-files.md)
    - [**统一标签客户端**：通过 Azure 信息保护查看器查看受保护的文件](rms-client/clientv2-view-use-files.md)


## <a name="more-information"></a>详细信息

以下附加文章可能有助于回答有关 Azure 信息保护中已知问题的问题：

- [有关 Azure 信息保护的常见问题](faqs.md)
- [Azure 信息保护中的有关数据保护的常见问题](faqs-rms.md)
- [有关 Azure 信息保护中的分类和标签的常见问题](faqs-infoprotect.md)
- [适用于 iOS 和 Android 的 Microsoft Azure 信息保护应用的常见问题解答](rms-client/mobile-app-faq.md)

