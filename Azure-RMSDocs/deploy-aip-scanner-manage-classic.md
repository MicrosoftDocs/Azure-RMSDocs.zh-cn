---
title: '运行 Azure 信息保护经典扫描器 (AIP) '
description: 有关运行 Azure 信息保护经典扫描程序以发现、分类和保护数据存储中的文件的说明。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c3292782a3a824db1166e255be3935978c8b8ce9
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316392"
---
# <a name="running-the-azure-information-protection-classic-scanner"></a>运行 Azure 信息保护经典扫描程序

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、windows server 2016、windows Server 2012 R2*

>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>
> 如果使用的是统一标签扫描程序，请参阅 [运行 Azure 信息保护扫描程序](deploy-aip-scanner-manage.md)。

确认 [系统要求](deploy-aip-scanner-prereqs-classic.md) 并 [配置并安装了扫描仪](deploy-aip-scanner-configure-install-classic.md)后， [运行发现扫描](#run-a-discovery-cycle-and-view-reports-for-the-scanner) 以开始使用。

使用下面详细介绍的其他步骤来管理你的扫描前进。

- [停止扫描](#stopping-a-scan)
- [重新扫描文件](#rescanning-files)
- [排查停止的扫描问题](#troubleshooting-a-stopped-scan)
- [使用扫描仪诊断工具进行故障排除](#troubleshooting-using-the-scanner-diagnostic-tool)
- [扫描器事件日志 Id 和说明](#event-log-ids-and-descriptions-for-the-scanner)

有关详细信息，请参阅 [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>运行发现周期并查看扫描程序报告

[配置并安装扫描程序](deploy-aip-scanner-configure-install.md)后，请使用以下过程初步了解内容。

当内容更改时，请根据需要再次执行这些步骤。

1. 在 Azure 门户的 " **Azure 信息保护-内容扫描作业** " 窗格上，选择你的内容扫描作业，然后选择 " **立即扫描** " 选项：

    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)

    或者，在 PowerShell 会话中，运行以下命令：
    
    ```ps
    Start-AIPScan
    ```

1. 等待扫描程序完成其周期。 扫描程序通过指定数据存储中的所有文件进行爬网时，扫描完成。

    执行以下任一操作来监视扫描程序进度：

    - **刷新扫描作业。**  在 " **Azure 信息保护-内容扫描作业** " 窗格上，选择 " **刷新**"。

        请等待，直到看到 " **最后一次扫描结果** " 列的值和 **最后一个 "扫描 (结束时间")** 列。

    - **使用 PowerShell 命令。** 运行 `Get-AIPScannerStatus` 监视状态更改。

    - **检查 Windows 事件日志。** 检查名为 " **Azure 信息保护**" 的本地 Windows **应用程序和服务** 事件日志。

        此日志还报告扫描程序完成扫描的时间，包括结果摘要。 请查看信息事件 ID 911。 有关详细信息，请参阅 [事件日志 id 和扫描程序的描述](#event-log-ids-and-descriptions-for-the-scanner)。

1. 扫描完成后，请查看存储在 **% *localappdata*% \ Microsoft\MSIP\Scanner\Reports** 目录中的报表。

    - .txt 摘要文件包括扫描所用的时间、扫描的文件数以及匹配信息类型的文件数量。

    - .csv 文件包含每个文件的更多详细信息。 此文件夹为每个扫描周期最多存储 60 个报表，并且压缩除最新报表之外的所有报表，以帮助最大程度地减少所需的磁盘空间。

[初始配置](deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal) 指导您将仅 **发现的信息类型** 设置为 " **策略**"。 此配置意味着仅在详细报告中包括满足你为自动分类配置的条件的文件。

如果看不到任何已应用的标签，请检查标签配置是否包括 "自动" 而不是推荐的分类，或 "启用 **建议标记为** 在 scanner 版本 2.7. x 和更高版本中提供的自动 () 。

如果结果仍不符合预期，则可能需要重新配置为标签指定的条件。 如果是这种情况，请根据需要重新配置条件，并重复此过程，直到对结果满意为止。 然后，自动更新配置，并可选择进行保护。

### <a name="viewing-updates-in-the-azure-portal"></a>查看 Azure 门户中的更新

扫描程序每隔五分钟就会将此信息发送到 Azure 信息保护，这样您就可以从 Azure 门户接近实时地查看结果。 有关详细信息，请参阅 [Azure 信息保护报表](reports-aip.md)。

Azure 门户仅显示有关上次扫描的信息。 如果需要查看先前扫描的结果，请返回到扫描程序计算机上存储的报表，它位于 %localappdata%\Microsoft\MSIP\Scanner\Reports 文件夹中。

### <a name="changing-log-levels-or-locations"></a>更改日志级别或位置

使用 [set-aipscannerconfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration)的 *eportlevel* 参数更改日志记录级别。

不能更改报表文件夹位置或名称。 如果要将报表存储在不同的位置，请考虑使用文件夹的目录连接。

例如，使用 [Mklink](/windows-server/administration/windows-commands/mklink) 命令： `mklink /j D:\Scanner_reports C:\Users\aipscannersvc\AppData\Local\Microsoft\MSIP\Scanner\Reports`

如果在初始配置和安装之后执行了这些步骤，请继续 [配置扫描仪以应用分类和保护](deploy-aip-scanner-configure-install.md#configure-the-scanner-to-apply-classification-and-protection)。

## <a name="stopping-a-scan"></a>停止扫描

若要停止当前正在运行的扫描，请使用下列方法之一：

- **Azure 门户。** 选择 " **停止扫描**"：

    ![停止扫描 Azure 信息保护扫描程序](./media/scanner-stop-scan.png)

- **运行 PowerShell 命令。** 运行下面的命令：
    
    ```ps
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>重新扫描文件

对于 [第一个扫描周期](#run-a-discovery-cycle-and-view-reports-for-the-scanner)，扫描程序会检查配置的数据存储中的所有文件。 对于后续扫描，仅检查新文件或已修改的文件。

如果希望报表包含所有文件，并且扫描程序在发现模式下运行，则再次检查所有文件通常非常有用。

使用以下方法之一对所有文件运行新扫描：

- [手动运行完全重新扫描](#manually-run-a-full-rescan)
- [通过刷新策略触发完全重新扫描](#trigger-a-full-rescan-by-refreshing-the-policy)

### <a name="manually-run-a-full-rescan"></a>手动运行完全重新扫描

根据需要，从 Azure 门户中的 " **Azure 信息保护-内容扫描作业** " 窗格强制扫描程序重新检查所有文件。

从列表中选择内容扫描作业，然后选择 " **重新扫描所有文件** " 选项：

![启动 Azure 信息保护扫描程序重新扫描](./media/scanner-rescan-files.png)

完全扫描完成后，扫描类型会自动更改为增量，以便进行后续扫描时，只会重新扫描新文件或已修改的文件。

### <a name="trigger-a-full-rescan-by-refreshing-the-policy"></a>通过刷新策略触发完全重新扫描

当扫描程序下载具有新的或更改的条件的 Azure 信息保护策略时，还会在以下情况下检查所有文件。

扫描程序每隔一小时自动刷新一次策略，并在服务每次启动时以及发现策略超过一小时。

若要在测试过程中尽快刷新策略，请从 **%LocalAppData%\Microsoft\MSIP** 目录中手动删除 **Policy.msip** 策略文件，然后重新启动 Azure 信息保护服务。

> [!NOTE]
> 如果你还更改了标签的保护设置，请在重新启动 Azure 信息保护服务之前，等待额外的15分钟，然后再保存更新的保护设置。
>

## <a name="troubleshooting-a-stopped-scan"></a>排查停止的扫描问题

如果扫描程序意外停止在中间，并且没有完成扫描存储库中的大量文件，则可能需要修改下列设置之一：

- **动态端口数**。 可能需要增加承载文件的操作系统的动态端口数。 SharePoint 的服务器强化可能是导致扫描程序超出允许的网络连接数并因此停止的一个原因。

    若要检查这是否是扫描仪停止的原因，请查看是否在 **% *localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog** 文件中为扫描程序记录了以下错误消息。

    **无法连接到---> 的远程服务器。 SocketException：每个套接字地址 (协议/网络地址/端口) 通常只允许使用 IP：端口**

    > [!NOTE]
    > 如果有多个日志，则压缩此文件。

    有关如何查看当前端口范围并增加范围的详细信息，请参阅 [可修改的设置以提高网络性能](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance)。

- **列表视图阈值。** 对于大型 SharePoint 场，可能需要增加列表视图阈值。 默认情况下，列表视图阈值设置为5000。

    有关详细信息，请参阅 [在 SharePoint 中管理大型列表和库](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server)。

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>使用扫描仪诊断工具进行故障排除

如果你在使用 Azure 信息扫描程序时遇到问题，请使用以下 PowerShell 命令验证部署是否正常：

```ps
Start-AIPScannerDiagnostics
```

诊断工具会检查以下详细信息，然后导出包含结果的日志文件：

- 数据库是否是最新的
- 网络 Url 是否可访问
- 是否存在有效的身份验证令牌和是否可以获取策略
- 配置文件是否在 Azure 门户中定义
- 脱机/联机配置是否存在并可获取
- 配置的规则是否有效

> [!TIP]
> 如果在不是扫描仪用户的用户下运行命令，请确保添加 **-OnBehalf** 参数。 
>

> [!NOTE]
> **AIPScannerDiagnostics** 工具不会运行完整的先决条件检查。 如果扫描程序出现问题，还请确保系统符合 [扫描器要求](deploy-aip-scanner-prereqs.md)，并确保 [扫描仪配置和安装](deploy-aip-scanner-configure-install.md) 已完成。
>

## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>扫描程序的事件日志 ID 和说明

以下 AIP 扫描器日志事件存储在名为 " **Azure 信息保护**" 的 Windows **应用程序和服务** 事件日志中。

|事件 ID  |活动  |说明  |
|---------|---------|---------|
|**910**     | 扫描仪循环已启动        | 当扫描程序服务启动并开始扫描指定的数据存储库中的文件时，记录。        |
|**911**     |   扫描程序周期已完成      | 当扫描程序完成手动扫描，或扫描程序已完成连续计划的周期时记录。       |
| | | |

> [!TIP]
> 如果扫描程序被配置为手动运行而不是连续运行，则要再次扫描文件，请将 " **计划** " 设置为 " **手动** " 或 " **始终** 在内容扫描作业中"，然后重新启动该服务。 有关详细信息，请参阅重新 [扫描文件](#rescanning-files)。
>

## <a name="next-steps"></a>后续步骤

- 想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

- 您可能想知道： [Windows SERVER FCI 和 Azure 信息保护扫描程序之间的区别是什么？](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- 还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 要详细了解此方案及使用 PowerShell 的其他方案，请参阅[将 PowerShell 与 Azure 信息保护客户端配合使用](./rms-client/client-admin-guide-powershell.md)。