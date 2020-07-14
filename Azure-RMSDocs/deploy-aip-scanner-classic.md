---
title: 了解 Azure 信息保护经典扫描器-AIP
description: 说明如何安装、配置和运行 Azure 信息保护经典扫描器，以发现、分类和保护数据存储中的文件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d6814e3a7b34ab25d8b38f2813440a717ad4bd1a
ms.sourcegitcommit: a606376373961dd4ce103f3cb465594831093820
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281947"
---
# <a name="what-is-the-azure-information-protection-classic-scanner"></a>什么是 Azure 信息保护经典扫描程序？

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>
> 如果你使用的是统一标签客户端，请参阅[什么是 Azure 信息保护统一标记扫描器？](deploy-aip-scanner.md)。

使用此部分中的信息来了解 Azure 信息保护扫描程序，然后了解如何成功地安装、配置、运行，并在必要时对其进行故障排除。

AIP 扫描程序在 Windows Server 上以服务的形式运行，并允许你发现、分类和保护以下数据存储中的文件：

- 使用服务器消息块（SMB）协议的网络共享的**UNC 路径**。

- Sharepoint**文档库和**sharepoint server 2019 通过 sharepoint server 2013 的文件夹。 如果客户[扩展了针对此版 SharePoint 的支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)，则 SharePoint 2010 也会受到支持。

> [!NOTE]
> 若要在云存储库上扫描并标记文件，请使用 [Cloud App Security](https://docs.microsoft.com/cloud-app-security/)，而不是扫描程序。
>
## <a name="azure-information-protection-classic-scanner-overview"></a>Azure 信息保护经典扫描器概述

AIP 扫描程序可以检查 Windows 可以为其编制索引的任何文件。 如果已配置了应用自动分类的标签，则扫描程序可以标记发现的文件以应用该分类，还可以选择 "应用" 或 "删除保护"。

下图显示了 AIP 扫描程序体系结构，扫描程序在该体系结构中发现本地和 SharePoint 服务器上的文件。

:::image type="content" source="media/classic-scanner-arch.png" alt-text="Azure 信息保护经典扫描程序体系结构":::

若要检查文件，扫描程序使用计算机上安装的 Ifilter。 若要确定是否需要标记文件，扫描程序将使用 Office 365 内置数据丢失防护（DLP）敏感信息类型和模式检测，或 Office 365 regex 模式。

扫描程序使用 Azure 信息保护客户端，并可以对与客户端相同的文件类型进行分类和保护。 有关详细信息，请参阅[Azure 信息保护客户端支持的文件类型](./rms-client/client-admin-guide-file-types.md)。

执行以下任一操作以根据需要配置扫描：

- **仅在发现模式下运行扫描程序**，以创建查看文件标记时所发生的情况的报表。
- **运行扫描程序以发现包含敏感信息的文件，** 而不配置应用自动分类的标签。
- **自动运行扫描程序**以按配置应用标签。
- **定义 "文件类型" 列表**以指定要扫描或排除的特定文件。

> [!NOTE]
> 扫描程序不会实时发现和标记。 它会在你指定的数据存储中通过文件系统地进行爬网。 将此循环配置为运行一次或重复运行。

## <a name="aip-scanning-process"></a>AIP 扫描过程

扫描文件时，AIP 扫描程序会执行以下步骤：

[1. 确定是包括还是排除文件以进行扫描](#1-determine-whether-files-are-included-or-excluded-for-scanning)

[2. 检查并标记文件](#2-inspect-and-label-files)

[3. 无法检查的标签文件](#3-label-files-that-cant-be-inspected)

> [!NOTE]
> 有关详细信息，请参阅[扫描仪未标记的文件](#files-not-labeled-by-the-scanner)。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. 确定是包括还是排除文件以进行扫描

扫描程序自动跳过从分类和保护中排除的文件，如可执行文件和系统文件。 有关详细信息，请参阅[从分类和保护中排除的文件类型](./rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)。

扫描器还会将显式定义的任何文件列表视为扫描，或从扫描中排除。 默认情况下，文件列表适用于所有数据存储库，并且只能为特定的存储库定义。

若要定义用于扫描或排除的文件列表，请使用内容扫描作业中的 "**文件类型" 来扫描**设置。 例如：

![配置 Azure 信息保护扫描程序要扫描的文件类型](./media/scanner-file-types.png)

有关详细信息，请参阅[部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-configure-install.md)。

### <a name="2-inspect-and-label-files"></a>2. 检查并标记文件

标识排除的文件后，扫描程序会再次筛选以识别检查支持的文件。

这些附加筛选器与操作系统用于 Windows 搜索和索引的筛选器相同，无需其他配置。 Windows IFilter 还用于扫描 Word、Excel 和 PowerPoint 使用的文件类型以及 PDF 文档和文本文件。

有关检查支持的文件类型的完整列表，以及用于将筛选器配置为包含 .zip 和 tiff 文件的其他说明，请参阅[检查支持的文件类型](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-inspection)。

检查后，支持的文件类型使用为标签指定的条件进行标记。 如果你使用的是发现模式，则可以将这些文件报告为包含为你的标签指定的条件，或者报告为包含任何已知的敏感信息类型。

### <a name="3-label-files-that-cant-be-inspected"></a>3. 无法检查的标签文件

对于无法检查的任何文件类型，AIP 扫描器会应用 Azure 信息保护策略中的默认标签，或为扫描程序配置的默认标签。

### <a name="files-not-labeled-by-the-scanner"></a>扫描仪未标记的文件

AIP 扫描程序在以下情况下无法标记文件：

- 如果标签应用分类，但不支持保护，而文件类型不支持客户端分类。 有关详细信息，请参阅[经典客户端文件类型](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-classification-only)。

- 标签应用分类和保护时，但扫描程序不支持文件类型。
  
    默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。

    [更改要保护的文件类型](deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect)时，可以添加其他类型的文件以进行保护。

**示例：** 检查 .txt 文件后，扫描程序无法应用配置为仅用于分类的标签，因为 .txt 文件类型不支持分类。

但是，如果将标签配置为分类和保护，并包含该文件类型以保护扫描程序，则扫描程序可以对文件进行标记。

## <a name="next-steps"></a>后续步骤

有关部署扫描器的详细信息，请参阅以下文章：

- [AIP 扫描程序部署先决条件](deploy-aip-scanner-prereqs.md)
- [配置和安装 AIP 扫描程序](deploy-aip-scanner-configure-install.md)
- [使用 AIP scanner 扫描运行扫描](deploy-aip-scanner-manage.md)

**详细信息：**

- 想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

- 您可能想知道： [Windows SERVER FCI 和 Azure 信息保护扫描程序之间的区别是什么？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- 还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 要详细了解此方案及使用 PowerShell 的其他方案，请参阅[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。
