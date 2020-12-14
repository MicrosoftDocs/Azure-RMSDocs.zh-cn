---
title: 了解 Azure 信息保护统一标记扫描器-AIP
description: 说明如何安装、配置和运行当前版本的 Azure 信息保护统一标记扫描器，以发现、分类和保护数据存储中的文件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a8c0d8ae4989a31029979c819ac6c59c390a8f3c
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382541"
---
# <a name="what-is-the-azure-information-protection-unified-labeling-scanner"></a>什么是 Azure 信息保护统一标记扫描程序？

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***相关的**： [仅限 AIP 统一标签客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [什么是 Azure 信息保护经典扫描程序？](deploy-aip-scanner-classic.md)*

>[!NOTE] 
> 若要在云存储库上扫描并标记文件，请使用 [Cloud App Security](/cloud-app-security/)，而不是扫描程序。

使用此部分中的信息来了解 Azure 信息保护统一标签扫描程序，然后了解如何成功进行安装、配置、运行，并在必要时对其进行故障排除。

AIP 扫描程序在 Windows Server 上以服务的形式运行，并允许你发现、分类和保护以下数据存储中的文件：

- 使用 SMB 或 NFS (预览) 协议的网络共享的 **UNC 路径**。

- Sharepoint **文档库和** sharepoint server 2019 通过 sharepoint server 2013 的文件夹。 如果客户[扩展了针对此版 SharePoint 的支持](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)，则 SharePoint 2010 也会受到支持。

为了对文件进行分类和保护，扫描程序使用在 Microsoft 365 标签 "管理中心" 中配置的 [敏感度标签](/microsoft-365/compliance/sensitivity-labels) ，包括 "Microsoft 365 安全中心"、"Microsoft 365 符合性中心" 和 "Microsoft 365 安全性和符合性中心"。 

## <a name="azure-information-protection-unified-labeling-scanner-overview"></a>Azure 信息保护统一标记扫描器概述

AIP 扫描程序可以检查 Windows 可以为其编制索引的任何文件。 如果已将敏感度标签配置为应用自动分类，则扫描程序可以标记发现的文件以应用该分类，还可以选择应用或删除保护。 

下图显示了 AIP 扫描程序体系结构，扫描程序在该体系结构中发现本地和 SharePoint 服务器上的文件。

:::image type="content" source="media/ul-scanner-arch.png" alt-text="Azure 信息保护统一标签扫描程序体系结构":::

若要检查文件，扫描程序使用计算机上安装的 Ifilter。 若要确定是否需要标记文件，扫描程序会使用 Microsoft 365 内置数据丢失防护 (DLP) 敏感度信息类型和模式检测，或 Microsoft 365 regex 模式。

扫描程序使用 Azure 信息保护客户端，并可以对与客户端相同的文件类型进行分类和保护。 有关详细信息，请参阅 [Azure 信息保护统一标签客户端支持的文件类型](./rms-client/clientv2-admin-guide-file-types.md)。

执行以下任一操作以根据需要配置扫描：

- **仅在发现模式下运行扫描程序** ，以创建查看文件标记时所发生的情况的报表。
- **运行扫描程序以发现包含敏感信息的文件**，而不配置应用自动分类的标签。
- **自动运行扫描程序** 以按配置应用标签。 
- **定义 "文件类型" 列表** 以指定要扫描或排除的特定文件。

> [!NOTE]
> 扫描程序不会实时发现和标记。 它会在你指定的数据存储中通过文件系统地进行爬网。 将此循环配置为运行一次或重复运行。

> [!TIP]
> 统一的标记扫描器支持具有多个节点的扫描程序群集，使你的组织能够横向扩展，实现更快的扫描时间和更广泛的作用域。 
> 
> 从一开始就部署多个节点，或者从单节点群集开始，并在以后增长时添加更多节点。 使用 **install-aipscanner** cmdlet 的相同群集名称和数据库部署多个节点。
> 

## <a name="aip-scanning-process"></a>AIP 扫描过程

扫描文件时，AIP 扫描程序会执行以下步骤：

[1. 确定是包括还是排除文件以进行扫描](#1-determine-whether-files-are-included-or-excluded-for-scanning)

[2. 检查并标记文件](#2-inspect-and-label-files)

[3. 无法检查的标签文件](#3-label-files-that-cant-be-inspected) 

有关详细信息，请参阅 [扫描仪未标记的文件](#files-not-labeled-by-the-scanner)。

### <a name="1-determine-whether-files-are-included-or-excluded-for-scanning"></a>1. 确定是包括还是排除文件以进行扫描 

扫描程序自动跳过从分类和保护中排除的文件，如可执行文件和系统文件。 有关详细信息，请参阅 [从分类和保护中排除的文件类型](./rms-client/clientv2-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)。

扫描器还会将显式定义的任何文件列表视为扫描，或从扫描中排除。 默认情况下，文件列表适用于所有数据存储库，并且只能为特定的存储库定义。

若要定义用于扫描或排除的文件列表，请使用内容扫描作业中的 " **文件类型" 来扫描** 设置。 例如：

![配置 Azure 信息保护扫描程序要扫描的文件类型](./media/scanner-file-types.png)

有关详细信息，请参阅 [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner-configure-install.md)。

### <a name="2-inspect-and-label-files"></a>2. 检查并标记文件

标识排除的文件后，扫描程序会再次筛选以识别检查支持的文件。

这些附加筛选器与操作系统用于 Windows 搜索和索引的筛选器相同，无需其他配置。 Windows IFilter 还用于扫描 Word、Excel 和 PowerPoint 使用的文件类型以及 PDF 文档和文本文件。

有关检查支持的文件类型的完整列表，以及用于将筛选器配置为包含 .zip 和 tiff 文件的其他说明，请参阅 [检查支持的文件类型](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-inspection)。

检查后，支持的文件类型使用为标签指定的条件进行标记。 如果你使用的是发现模式，则可以将这些文件报告为包含为你的标签指定的条件，或者报告为包含任何已知的敏感信息类型。

#### <a name="stopped-scanner-processes"></a>已停止扫描进程

如果扫描程序停止且未完成对存储库中大量文件的扫描，可能需要增加承载文件的操作系统的动态端口数。

例如，针对 SharePoint 的服务器强化是指扫描程序会超出允许的网络连接数，因此停止的原因之一。

若要检查这是否是扫描仪停止的原因，请检查 **%localappdata%\Microsoft\MSIP\Logs\MSIPScanner.iplog** 中的扫描程序日志中是否存在以下错误消息 (多个日志已压缩为 zip 文件) ：

`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`

有关如何查看当前端口范围并在需要时对其进行增加的详细信息，请参阅 [可以修改以提高网络性能的设置](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)。

> [!TIP]
> 对于大型 SharePoint 场，可能需要增加列表视图阈值，默认值为 **5000**。
>
> 有关详细信息，请参阅在 [SharePoint 中管理大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。
>

### <a name="3-label-files-that-cant-be-inspected"></a>3. 无法检查的标签文件

对于无法检查的任何文件类型，AIP 扫描器会应用 Azure 信息保护策略中的默认标签，或为扫描程序配置的默认标签。

### <a name="files-not-labeled-by-the-scanner"></a>扫描仪未标记的文件
AIP 扫描程序在以下情况下无法标记文件：

- 如果标签应用分类，但不支持保护，而文件类型不支持客户端分类。 有关详细信息，请参阅 [统一标签客户端文件类型](./rms-client/clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only)。

- 标签应用分类和保护时，但扫描程序不支持文件类型。
  
    默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 

    [更改要保护的文件类型](deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect)时，可以添加其他类型的文件以进行保护。

**示例**：检查 .Txt 文件后，扫描程序不能应用为分类配置的标签，因为 .txt 文件类型不支持分类。 

但是，如果将标签配置为分类和保护，并包含该文件类型以保护扫描程序，则扫描程序可以对文件进行标记。

## <a name="next-steps"></a>后续步骤

有关部署扫描器的详细信息，请参阅以下文章：

- [AIP 扫描程序部署先决条件](deploy-aip-scanner-prereqs.md)
- [配置和安装 AIP 扫描程序](deploy-aip-scanner-configure-install.md)
- [使用 AIP scanner 扫描运行扫描](deploy-aip-scanner-manage.md)

**详细信息**：

- 查看有关统一标记扫描器的最佳实践的博客： [部署和使用 AIP UL 扫描器的最佳实践](https://aka.ms/AIPScannerBestPractices)

- 想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

- 还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 有关此方案以及使用 PowerShell 的其他方案的详细信息，请参阅 [将 PowerShell 与 Azure 信息保护统一标签客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)。
