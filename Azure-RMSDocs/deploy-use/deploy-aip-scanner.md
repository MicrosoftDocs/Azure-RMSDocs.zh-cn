---
title: "部署 Azure 信息保护扫描程序"
description: "说明如何安装、配置和运行 Azure 信息保护扫描程序以发现和保护数据存储中的文件并对其进行分类。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 924a9e0b19203f60827693adecc9b74fa62edef1
ms.sourcegitcommit: 92bbef77091c66300e0d2acce60c064ffe314752
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2017
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>部署 Azure 信息保护扫描程序以自动对文件进行分类和保护

>适用于：Azure 信息保护、Windows Server 2016、Windows Server 2012 R2

> [!NOTE]
> 此功能目前处于预览状态，随时可能更改。

利用此信息了解 Azure 信息保护扫描程序，并了解如何成功安装、配置和运行该扫描程序。 

此扫描程序在 Windows Server 上作为服务运行，使你能够发现和保护以下数据存储中的文件并对其进行分类：

- 运行扫描程序的 Windows Server 计算机上的本地文件夹。

- 网络共享（使用通用 Internet 文件系统 (CIFS) 协议）的 UNC 路径。

- SharePoint Server 2016 和 SharePoint Server 2013 的站点和库。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序概述

为应用自动分类的标签配置 [Azure 信息保护策略](configure-policy.md)后，可为此扫描程序发现的文件设置标签。 标签可应用分类，并且可以应用保护或移除保护：

![Azure 信息保护扫描程序概述](../media/infoprotect-scanner.png)

自动分类使用 Office 365 内置数据丢失防护 (DLP) 敏感信息类型和模式检测，或 Office 365 正则表达式模式。 因为扫描程序使用 Azure 信息保护客户端，所以它可以对相同[文件类型](../rms-client/client-admin-guide-file-types.md)进行分类和保护。

可仅在发现模式下运行扫描程序，利用报告确认对文件设置标签时会发生什么情况。 或者，可运行扫描程序自动应用标签。

注意，扫描程序不会实时发现和标记。 它会系统地浏览指定数据存储中的文件，可将此周期配置为运行一次或多次。

## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序的先决条件
安装 Azure 信息保护扫描程序之前，请确保已满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|运行扫描程序服务的 Windows Server 计算机：<br /><br />- 4 个进程<br /><br />- 4 GB 的 RAM|Windows Server 2016 或 Windows Server 2012 R2。<br /><br />此服务器可是物理或虚拟计算机，并且可以快速、可靠地通过网络连接到要进行扫描的数据存储。 <br /><br />确保此服务器具有 Azure 信息保护所需的 [Internet 连接](../get-started/requirements.md#firewalls-and-network-infrastructure)。 或者，必须将其配置为[断开连接的计算机](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)。|
|存储扫描程序配置的 SQL Server：<br /><br />- 本地或远程实例|SQL Server 2012 R2 是以下版本的最低版：<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express|
|运行扫描程序服务的服务帐户|此帐户必须是同步到 Azure AD 的 Active Directory 帐户，并满足以下额外要求：<br /><br />- “本地登录”权限。 此权限是安装和配置扫描程序所必需的，但不可用于操作。 必须将此权限授予服务帐户，但当确认扫描程序可发现、保护文件并对其进行分类后，可删除此权限。<br /><br />- “作为服务登录”权限。 扫描程序安装过程中会自动将此权限授予服务帐户，此权限是安装、配置和操作扫描程序所必需的。 <br /><br />- 数据存储库的权限：必须授予“读取”和“写入”权限才可扫描文件，然后将分类和保护应用到满足 Azure 信息保护策略中条件的文件。 若仅在发现模式下运行扫描程序，则只需“读取”权限即可。<br /><br />- 对于可重新保护或移除保护的标签：要确保扫描程序始终能够访问受保护的文件，请将此帐户设置为 Azure Rights Management 服务的[超级用户](configure-super-users.md)，并确保已启用超级用户功能。 要详细了解应用保护的帐户要求，请参阅[准备用户和组以便使用 Azure 信息保护](../plan-design/prepare.md)。|
|在 Windows Server 计算机上安装 Azure 信息保护客户端|当前，Azure 信息保护扫描程序需要 Azure 信息保护客户端预览版。<br /><br />如果愿意，可通过用于安装和配置扫描程序的 PowerShell 模块 (AzureInformationProtection) 来安装客户端。<br /><br />有关客户端安装说明，请参阅[管理员指南](../rms-client/client-admin-guide.md)。|
|已配置可应用自动分类和保护（可选）的标签|有关如何配置条件的详细信息，请参阅[如何配置 Azure 信息保护的自动和建议分类的条件](/deploy-use/configure-policy-classification.md)。<br /><br />要详细了解如何配置标签以将保护应用到文件，请参阅[如何配置标签以进行 Rights Management 保护](../deploy-use/configure-policy-protection.md)。 |


## <a name="install-the-azure-information-protection-scanner"></a>安装 Azure 信息保护扫描程序

1. 使用为运行扫描程序而创建的服务帐户，登录运行该扫描程序的 Windows Server 计算机。

2. 使用“以管理员身份运行”选项打开 Windows PowerShell 会话。

3. 运行 [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) cmdlet，指定要在其中为 Azure 信息保护扫描程序创建数据库的 SQL Server 实例。 系统提示时，请提供扫描程序服务帐户的凭据 (\<域\用户名>) 和密码： 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    例如：
        
    - 对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    - 对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    - 对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`

4. 使用“管理工具” > “服务”验证服务现在是否已安装。 
    
    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行。

现已安装扫描程序，需获取 Azure AD 令牌以便扫描程序服务帐户进行身份验证，从而实现以无人参与的方式运行。 

## <a name="get-an-azure-ad-token-for-the-scanner-service-account-to-authenticate-to-the-azure-information-protection-service"></a>获取 Azure AD 令牌以便扫描程序服务帐户向 Azure 信息保护服务进行身份验证

1. 通过同一台 Windows Server 计算机或通过桌面登录 Azure 门户，创建 2 个 Azure AD 应用程序 - 指定用于身份验证的访问令牌时需使用这两个应用程序。 首次以交互方式登录后，此令牌将允许扫描程序以非交互方式运行。
    
    要创建这些应用程序，请按照管理员指南中[如何以非交互方式为 Azure 信息保护标记文件](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)的说明执行操作。

2. 在 Windows Server 计算机中，仍使用扫描程序服务帐户登录，然后运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)（指定从上一步中复制的值）：
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```

3. 系统提示时，请为 Azure AD 的服务帐户凭据指定密码，然后单击“接受”。

扫描程序现已拥有一个令牌，可向 Azure AD 进行身份验证。该令牌的有效期为 1 年、2 年或永不过期，具体取决于 Azure AD 中“Web 应用/API”的配置。 如果令牌过期，则须重复步骤 1 到 3。

现可指定要扫描的数据存储。 

## <a name="specify-data-stores-for-the-azure-information-protection-scanner"></a>为 Azure 信息保护扫描程序指定数据存储

使用 [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository) cmdlet 指定将由 Azure 信息保护扫描程序进行扫描的数据存储。 可指定本地文件夹、UNC 路径以及 SharePoint 站点和库的 SharePoint Server URL。 

支持的 SharePoint 版本：SharePoint Server 2016 和 SharePoint Server 2013。

1. 在同一台 Windows Server 计算机中，通过在 PowerShell 会话中运行以下命令来添加第一个数据存储：
    
        Add-AIPScannerRepository -Path <path>
    
    例如：`Add-AIPScannerRepository -Path \\NAS\Documents`
    
    有关其他示例，请参阅此 cmdlet 的[联机帮助](/powershell/module/azureinformationprotection/Add-AIPScannerRepository#examples)。

2. 对想要扫描的所有数据存储重复此命令。 如果要删除已添加的数据存储，请使用 [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository) cmdlet。

3. 确认已正确指定所有数据存储，方法是运行 [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository) cmdlet：
    
        Get-AIPScannerRepository

利用扫描程序的默认配置，现在可在发现模式下运行首次扫描。

## <a name="run-a-discovery-cycle-and-view-reports-for-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序的发现周期运行和报告查看

1. 使用“管理工具” > “服务”，启动“Azure 信息保护扫描程序”服务。

2. 等待扫描程序完成其周期。 当扫描程序浏览完指定数据存储中所有文件时，服务停止。 可使用 Windows 应用程序事件日志、Azure 信息保护扫描程序来确认服务的停止时间。 请查看信息事件 ID 911。

3. 查看存储在 %localappdata%\Microsoft\MSIP\Scanner\Reports 中的报告，这些报告的文件格式为 .csv。 利用扫描程序默认配置，只有满足自动分类条件的文件才会被包括在这些报告中。
    
    如果结果与预期不符，建议对在 Azure 信息保护策略中指定的条件进行微调。 如果是这种情况，请重复步骤 1 到 3，直到可更改配置以应用分类和保护（可选）。 每当重复这些步骤时，请先在 Windows Server 计算机上运行以下 PowerShell 命令：
    
        Set-AIPScannerConfiguration -Schedule OneTime

如果已准备好对扫描程序发现的文件进行自动标记，请继续下一步。 

## <a name="configure-the-azure-information-protection-scanner-to-apply-classification-and-protection-to-discovered-files"></a>配置 Azure 信息保护扫描程序以对发现文件应用分类和保护

在其默认设置中，扫描程序在仅报告模式下运行一次。 要更改这些设置，请运行 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet。

1. 在 Windows Server 计算机上的 PowerShell 会话中，运行以下命令：
    
        Set-AIPScannerConfiguration -ScanMode Enforce -Schedule Continuous
    
    你可能还希望更改其他配置设置。 例如，是否更改文件属性，以及报告中应记录的内容。 此外，如果 Azure 信息保护策略包括需要理由信息以降低分类级别或移除保护的设置，请使用此 cmdlet 指定该信息。 有关每个配置设置的详细信息，请使用[联机帮助](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters)。 

2. 使用“管理工具” > “服务”，重启“Azure 信息保护扫描程序”服务。

3. 如前所述，监视事件日志和报告，了解标记了哪些文件、应用了什么分类以及是否应用了保护。

因为我们将计划配置为持续运行，所以当扫描程序扫描完所有文件时，它将开始新周期，以便可发现新文件和更改的文件。

## <a name="list-of-cmdlets-for-the-azure-information-protection-scanner"></a>适用于 Azure 信息保护扫描程序的 cmdlet 列表 

利用其他适用于扫描程序的 cmdle，可更改该扫描程序的服务帐户和数据库、获取扫描程序的当前设置，以及卸载扫描程序服务。 扫描程序使用以下 cmdlet：

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)


## <a name="event-log-ids-and-descriptions"></a>事件日志 ID 和说明

利用以下部分，确定扫描程序可能的事件 ID 和说明。

-----

信息 910

**扫描程序周期已开始。**

当扫描程序服务启动并开始扫描指定数据存储库中的文件时，会记录此事件。

----

信息 911

**扫描程序周期已结束。**

如果服务器启动后，扫描程序已完成其一次性扫描，或扫描程序已完成连续计划的一个周期，则会记录此事件。

----

信息 913

**扫描程序已停止，因为扫描程序被设置为“从不”。**

如果扫描程序被配置为运行一次（而不是连续运行），并且启动计算机后已手动重启 Azure 信息保护扫描程序服务，则会记录此事件。  

要再次扫描文件，必须手动启用服务。 要更改此行为以使扫描程序连续运行，请使用 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet 并将“Schedule”参数设置为“连续”。

----

错误 912

**出现未知错误。**

详细报告中记录了更多信息，该报告的存储位置为 %localappdata%\Microsoft\MSIP\Scanner\Reports\DetailedReport_YYYY_MM_DD_HH_MM.csv。

如果此事件继续被记录，请联系 [Microsoft 支持部门](../get-started/information-support.md#to-contact-microsoft-support)。 

----

错误 914

**由于配置出错，服务自动停止：策略文件丢失或损坏。**

如果 Azure 信息保护客户端未向要运行的扫描程序提供有效策略文件，则会记录此事件。

Azure 信息保护策略存储在 %localappdata%\Microsoft\MSIP 中，并且必须使用标签（具有应用自动分类的条件）进行配置。 或者，必须将策略配置为使用默认标签。

请确保防火墙不会阻止所需的 Internet 连接。 有关详细信息，请参阅 Azure 信息保护的[防火墙和网络基础结构](../get-started/requirements.md#firewalls-and-network-infrastructure)要求。 如果无法实现 Internet 连接，请按照说明进行操作，以支持使用[断开连接的计算机](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)。


## <a name="next-steps"></a>后续步骤

还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 要详细了解此方案及使用 PowerShell 的其他方案，请参阅[将 PowerShell 与 Azure 信息保护客户端配合使用](../rms-client/client-admin-guide-powershell.md)。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]