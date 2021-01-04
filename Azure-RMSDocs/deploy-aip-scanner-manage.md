---
title: '运行 Azure 信息保护统一标记扫描器 (AIP) '
description: 有关运行 Azure 信息保护统一标签扫描程序以发现、分类和保护数据存储中的文件的说明。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 344a2c8ed5f4912a96af2031accb9476358a2930
ms.sourcegitcommit: c6aa8f8ecec8950ac6104fc6f47a102e54804a95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2020
ms.locfileid: "97706097"
---
# <a name="running-the-azure-information-protection-scanner"></a>运行 Azure 信息保护扫描程序

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2019、Windows Server 2016、windows server 2012 R2 *
>
>***相关的**： [仅限 AIP 统一标签客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关经典扫描程序，请参阅 [运行 Azure 信息保护经典扫描器](deploy-aip-scanner-manage-classic.md)。 *

确认 [系统要求](deploy-aip-scanner-prereqs.md) 并 [配置并安装了扫描仪](deploy-aip-scanner-configure-install.md)后， [运行发现扫描](#run-a-discovery-cycle-and-view-reports-for-the-scanner) 以开始使用。

使用下面详细介绍的其他步骤来管理你的扫描前进。

- [停止扫描](#stopping-a-scan)
- [重新扫描文件](#rescanning-files)

有关详细信息，请参阅 [部署 Azure 信息保护扫描程序以自动对文件进行分类和保护](deploy-aip-scanner.md)。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>运行发现周期并查看扫描程序报告

[配置并安装扫描程序](deploy-aip-scanner-configure-install.md)后，请使用以下过程初步了解内容。

当内容更改时，请根据需要再次执行这些步骤。

1. 在 Azure 门户的 " **Azure 信息保护-内容扫描作业** " 窗格上，选择你的内容扫描作业，然后选择 " **立即扫描** " 选项：

    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)

    或者，在 PowerShell 会话中，运行以下命令：

    ```PowerShell
    Start-AIPScan
    ```

1. 等待扫描程序完成其周期。 扫描程序通过指定数据存储中的所有文件进行爬网时，扫描完成。

    执行以下任一操作来监视扫描程序进度：

    - **刷新扫描作业。**  在 " **Azure 信息保护-内容扫描作业** " 窗格上，选择 " **刷新**"。

        请等待，直到看到 " **最后一次扫描结果** " 列的值和 **最后一个 "扫描 (结束时间")** 列。

    - **使用 PowerShell 命令。** 运行 `Get-AIPScannerStatus` 监视状态更改。

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

- **运行 PowerShell 命令。** 运行以下命令：

    ```PowerShell
    Stop-AIPScan 
    ```

## <a name="rescanning-files"></a>重新扫描文件

对于 [第一个扫描周期](#run-a-discovery-cycle-and-view-reports-for-the-scanner)，扫描程序会检查配置的数据存储中的所有文件。 对于后续扫描，仅检查新文件或已修改的文件。

当你希望报表包含所有文件时，如果你想要在所有文件中应用更改，以及当扫描程序在发现模式下运行，则再次检查所有文件通常非常有用。

**手动运行完全重新扫描**：

1. 在 Azure 门户中导航到 " **Azure 信息保护-内容扫描作业** " 窗格。

1. 从列表中选择内容扫描作业，然后选择 " **重新扫描所有文件** " 选项：

    ![启动 Azure 信息保护扫描程序重新扫描](./media/scanner-rescan-files.png)

完全扫描完成后，扫描类型会自动更改为增量，以便进行后续扫描时，只会重新扫描新文件或已修改的文件。

> [!TIP]
> 如果已更改 AIP [内容扫描作业](deploy-aip-scanner-configure-install.md#create-a-content-scan-job)，Azure 门户会提示你跳过完全重新扫描。 若要确保重新扫描发生，请确保在出现的提示中选择 " **否** "。
> 
### <a name="trigger-a-full-rescan-by-modifying-your-settings-versions-271010-and-lower"></a>通过修改 (版本2.7.101.0 和更低版本的设置来触发完全重新扫描) 

在扫描程序版本 [2.7.101.0](rms-client/unifiedlabelingclient-version-release-history.md#version-271010) 和更低版本中，只要扫描程序检测到新的或更改的设置以自动和建议的标签，就会扫描所有文件。 扫描程序每四小时自动刷新一次策略。

若要更快地刷新策略（如测试时），请手动删除 **%LocalAppData%\Microsoft\MSIP\mip \<processname> \mip** 目录的内容，然后重新启动 Azure 信息保护服务。

如果你还更改了标签的保护设置，请在重新启动 Azure 信息保护服务之前，等待额外的15分钟，然后再保存更新的保护设置。

> [!IMPORTANT]
> 如果已升级到版本 [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) 或更高版本，则 AIP 会跳过完整的重新扫描以获取更新的设置，以确保性能一致。 如果已升级，请确保根据需要 [手动运行完全重新扫描](#rescanning-files) 。 
>
> 例如，如果你已将 "**强制 = 关闭**"**策略强制** 设置更改为 **"强制 = 启用**"，请确保运行完整的 "重新扫描" 以在内容中应用标签。
> 

## <a name="next-steps"></a>后续步骤

- 想了解 Microsoft 的 Core Services 工程和运行团队是如何实现此扫描程序的？  请阅读以下技术案例研究：[使用 Azure 信息保护扫描程序自动执行数据保护](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner)。

- 还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 有关此方案以及使用 PowerShell 的其他方案的详细信息，请参阅 [将 PowerShell 与 Azure 信息保护统一标签客户端配合使用](./rms-client/clientv2-admin-guide-powershell.md)。