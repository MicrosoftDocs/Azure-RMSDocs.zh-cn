---
title: 部署 Azure 信息保护扫描程序
description: 说明如何安装、配置和运行 Azure 信息保护扫描程序以发现和保护数据存储中的文件并对其进行分类。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 20d29079-2fc2-4376-b5dc-380597f65e8a
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 794a8649b803407eff0e651a0b9396d164355380
ms.sourcegitcommit: 61a4cda950706c823233b19e63951668fdcd5ef3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088626"
---
# <a name="deploying-the-azure-information-protection-scanner-to-automatically-classify-and-protect-files"></a>部署 Azure 信息保护扫描程序以自动对文件进行分类和保护

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012 R2

利用此信息了解 Azure 信息保护扫描程序，并了解如何成功安装、配置和运行该扫描程序。 

此扫描程序在 Windows Server 上作为服务运行，使你能够发现和保护以下数据存储中的文件并对其进行分类：

- 运行扫描程序的 Windows Server 计算机上的本地文件夹。

- 使用服务器消息块 (SMB) 协议的网络共享 UNC 路径。

- SharePoint Server 2016 和 SharePoint Server 2013 的站点和库。

若要扫描云存储库上的文件并为之设置标签，请使用 [Cloud App Security](https://docs.microsoft.com/cloud-app-security/)。

## <a name="overview-of-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序概述

为应用自动分类的标签配置 [Azure 信息保护策略](configure-policy.md)后，可为此扫描程序发现的文件设置标签。 标签可应用分类，并且可以应用保护或移除保护：

![Azure 信息保护扫描程序体系结构概述](../media/infoprotect-scanner.png)

通过使用计算机上安装的 iFilters，扫描程序可检查 Windows 能编制索引的任何文件。 然后，为了确定是否需要标记文件，扫描程序会使用 Office 365 内置数据丢失防护 (DLP) 敏感信息类型和模式检测，或 Office 365 正则表达式模式。 因为扫描程序使用 Azure 信息保护客户端，所以它可以对相同[文件类型](../rms-client/client-admin-guide-file-types.md)进行分类和保护。

可仅在发现模式下运行扫描程序，利用报告确认对文件设置标签时会发生什么情况。 或者，可运行扫描程序自动应用标签。 还可以运行扫描程序来发现包含敏感信息类型的文件，无需配置条件标签来应用自动分类。

注意，扫描程序不会实时发现和标记。 它会系统地浏览指定数据存储中的文件，可将此周期配置为运行一次或多次。

可以指定要扫描或排除不进行扫描的文件类型。 若要限制扫描程序检查的文件，可使用 [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes) 定义一个文件类型列表。


## <a name="prerequisites-for-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序的先决条件
安装 Azure 信息保护扫描程序之前，请确保已满足以下要求。

|要求|更多信息|
|---------------|--------------------|
|运行扫描程序服务的 Windows Server 计算机：<br /><br />- 4 核处理器<br /><br />- 4 GB 的 RAM<br /><br />- 临时文件 10GB 可用空间（平均）|Windows Server 2016 或 Windows Server 2012 R2。 <br /><br />注意：在非生产环境中出于测试或评估目的时，可以使用 [Azure 信息保护客户端支持的](../get-started/requirements.md#client-devices) Windows 客户端操作系统。<br /><br />此计算机可以是物理或虚拟计算机，需拥有快速可靠的网络，可连接到要进行扫描的数据存储。<br /><br /> 扫描程序需要足够的磁盘空间，才能为其扫描的每个文件（每个核心四个文件）创建临时文件。 借助建议的 10GB 磁盘空间，4 核处理器可以扫描 16 个文件，每个文件的大小为 625MB。 <br /><br />确保此计算机具有 Azure 信息保护所需的 [Internet 连接](../get-started/requirements.md#firewalls-and-network-infrastructure)。 如果由于组织策略而无法连接到 Internet，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。|
|存储扫描程序配置的 SQL Server：<br /><br />- 本地或远程实例<br /><br />- 安装扫描程序的 Sysadmin 角色|SQL Server 2012 是以下版本的最低版本：<br /><br />- SQL Server Enterprise<br /><br />- SQL Server Standard<br /><br />- SQL Server Express<br /><br />如果安装扫描程序且帐户拥有 Sysadmin 角色，那么在安装过程中会自动创建 AzInfoProtectionScanner 数据库，并向运行扫描程序的服务帐户授予相应 db_owner 角色。  如果无法获得 Sysadmin 角色或组织策略要求手动创建和配置数据库，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。|
|运行扫描程序服务的服务帐户|除了运行扫描程序服务，此帐户还对 Azure AD 进行身份验证，并下载 Azure 信息保护策略。 此帐户必须是同步到 Azure AD 的 Active Directory 帐户。 如果由于组织策略而无法同步此帐户，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />此服务帐户有以下要求：<br /><br />- “本地登录”权限。 此权限是安装和配置扫描程序所必需的，但不可用于操作。 必须将此权限授予服务帐户，但当确认扫描程序可发现、保护文件并对其进行分类后，可删除此权限。 如果由于组织策略的限制而甚至无法在短时间内授予此权限，请参阅[使用备用配置部署扫描程序](#deploying-the-scanner-with-alternative-configurations)部分。<br /><br />- “作为服务登录”权限。 扫描程序安装过程中会自动将此权限授予服务帐户，此权限是安装、配置和操作扫描程序所必需的。 <br /><br />- 数据存储库的权限：必须授予“读取”和“写入”权限才可扫描文件，然后将分类和保护应用到满足 Azure 信息保护策略中条件的文件。 若仅在发现模式下运行扫描程序，则只需“读取”权限即可。<br /><br />- 对于可重新保护或移除保护的标签：要确保扫描程序始终能够访问受保护的文件，请将此帐户设置为 Azure Rights Management 服务的[超级用户](configure-super-users.md)，并确保已启用超级用户功能。 要详细了解应用保护的帐户要求，请参阅[准备用户和组以便使用 Azure 信息保护](../plan-design/prepare.md)。 此外，如果对分阶段部署实现了[载入控件](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，还请确保已配置的载入控件中包含此帐户。|
|在 Windows Server 计算机上安装 Azure 信息保护客户端|必须安装扫描程序的完整客户端。 请勿安装只带有 PowerShell 模块的客户端。<br /><br />有关客户端安装说明，请参阅[管理员指南](../rms-client/client-admin-guide.md)。 如果现在需要将已安装的旧扫描程序升级到更高版本，请参阅[升级 Azure 信息保护扫描程序](../rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)。|
|已配置可应用自动分类和保护（可选）的标签|有关如何在 Azure 信息保护策略中配置条件的详细信息，请参阅[如何配置 Azure 信息保护的自动和建议分类的条件](configure-policy-classification.md)。<br /><br />要详细了解如何配置标签以将保护应用到文件，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)。<br /><br />这些标签可位于全局策略中，或位于一个或多个[作用域内策略](configure-policy-scope.md)中。<br /><br />注意：即使尚未配置标签来应用自动分类，也可以运行扫描程序。尽管如此，这些说明并未涵盖此方案。 [详细信息](#using-the-scanner-with-alternative-configurations)| 

如果由于组织策略禁止而无法满足表中的所有要求，请参阅下一部分中介绍的备用配置。

如果满足所有要求，请直接转到[安装部分](#install-the-azure-information-protection-scanner)。

### <a name="deploying-the-scanner-with-alternative-configurations"></a>使用备用配置部署扫描程序

表中列出的先决条件是扫描程序的默认要求，之所以建议是因为它们是用于扫描程序部署的最简单配置。 它们应适用于初始测试，以便能够检查扫描程序的功能。 不过，在产品环境中，组织策略可能会禁止这些默认要求，因为存在下列一个或多个限制：

- 禁止服务器连接到 Internet

- 无法获得 Sysadmin 角色，或必须手动创建和配置数据库

- 无法向服务帐户授予“本地登录”权限

- 服务帐户无法同步到 Azure Active Directory，但服务器可以连接到 Internet

虽然扫描程序可以适应这些限制，但需要其他配置。


#### <a name="restriction-the-scanner-server-cannot-have-internet-connectivity"></a>限制：扫描程序服务器无法连接到 Internet

请按照适用于[已断开连接的计算机](../rms-client/client-admin-guide-customizations.md#support-for-disconnected-computers)的说明操作。 

请注意，在此配置中，扫描程序无法使用组织的基于云的密钥来应用（或删除）保护配置。 相反，扫描程序只能使用应用分类或 [HYOK](configure-adrms-restrictions.md) 保护的标签。 

#### <a name="restriction-you-cannot-be-granted-sysadmin-or-databases-must-be-created-and-configured-manually"></a>限制：无法获得 Sysadmin 角色，或必须手动创建和配置数据库

如果可以获得 Sysadmin 角色来安装扫描程序，就能在扫描程序安装完成后删除此角色。 使用此配置时，数据库会自动创建，而且扫描程序的服务帐户也会自动获得相应权限。 不过，配置扫描程序的用户帐户需要拥有 AzInfoProtectionScanner 数据库的 db_owner 角色，你必须手动向用户帐户授予此角色。

如果无法临时获得 Sysadmin 角色，必须在安装扫描程序前手动创建 AzInfoProtectionScanner 数据库。 使用此配置时，请分配以下角色：
    
|帐户|数据库级角色|
|--------------------------------|---------------------|
|扫描程序的服务帐户|db_owner|
|用于安装扫描程序的用户帐户|db_owner|
|用于配置扫描程序的用户帐户 |db_owner|

用于安装和配置扫描程序的用户帐户通常是相同的。 不过，如果使用不同的帐户，它们都需要拥有 AzInfoProtectionScanner 数据库的 db_owner 角色。

#### <a name="restriction-the-service-account-for-the-scanner-cannot-be-granted-the-log-on-locally-right"></a>限制：无法向扫描程序的服务帐户授予“本地登录”权限

如果组织策略禁止向服务帐户授予“本地登录”权限，但允许授予“以批处理作业形式登录”权限，请按照管理员指南内[对 Set-AIPAuthentication 指定和使用 Token 参数](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一文中的说明操作。

#### <a name="restriction-the-scanner-service-account-cannot-be-synchronized-to-azure-active-directory-but-the-server-has-internet-connectivity"></a>限制：扫描程序服务帐户无法同步到 Azure Active Directory，但服务器可以连接到 Internet

可以使用一个帐户来运行扫描程序服务，并使用另一个帐户对 Azure Active Directory 进行身份验证：

- 对于扫描程序服务帐户，可以使用本地 Windows 帐户或 Active Directory 帐户。

- 如果使用 Azure Active Directory 帐户，请按照管理员指南内[对 Set-AIPAuthentication 指定和使用 Token 参数](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一文中的说明操作。


## <a name="install-the-scanner"></a>安装扫描程序

1. 登录到将要运行扫描程序的 Windows Server 计算机。 使用具有本地管理员权限并具有写入到 SQL Server master 数据库权限的帐户。

2. 使用“以管理员身份运行”选项打开 Windows PowerShell 会话。

3. 运行 [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) cmdlet，指定要在其中为 Azure 信息保护扫描程序创建数据库的 SQL Server 实例： 
    
    ```
    Install-AIPScanner -SqlServerInstance <database name>
    ```
    
    例如：
    
    对于默认实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1`
    
    对于命名实例：`Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER`
    
    对于 SQL Server Express：`Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS`
    
    如需更多[详细示例](/powershell/module/azureinformationprotection/install-aipscanner#examples)，请使用此 cmdlet 的在线帮助。
    
    系统提示时，请提供扫描程序服务帐户的凭据 (\<域\用户名>) 和密码。

4. 使用“管理工具” > “服务”验证服务现在是否已安装。 
    
    已安装的服务被命名为 Azure信息保护扫描程序，并被配置为使用你创建的扫描程序服务帐户运行。

现已安装扫描程序，需获取 Azure AD 令牌以便扫描程序服务帐户进行身份验证，从而实现以无人参与的方式运行。 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>获取扫描程序的 Azure AD 令牌

借助 Azure AD 令牌，Azure 信息保护服务可以验证扫描程序服务帐户。

1. 通过同一台 Windows Server 计算机或通过桌面登录 Azure 门户，创建 2 个 Azure AD 应用程序 - 指定用于身份验证的访问令牌时需使用这两个应用程序。 首次以交互方式登录后，此令牌将允许扫描程序以非交互方式运行。
    
    要创建这些应用程序，请按照管理员指南中[如何以非交互方式为 Azure 信息保护标记文件](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)的说明执行操作。

2. 在 Windows Server 计算机中，如果你的扫描程序服务帐户已就安装授予了“本地登录”权限：使用此帐户登录并启动 PowerShell 会话。 运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)，指定从上一步骤中复制的值：
    
    ```
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application>  -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application >
    ```
    
    系统提示时，请为 Azure AD 的服务帐户凭据指定密码，然后单击“接受”。
    
    如果你的扫描程序服务帐户无法就安装授予“本地登录”权限：请按照管理员指南中[指定和使用 Set-AIPAuthentication 的令牌参数](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)一节中的说明来操作。 

扫描程序现已拥有一个令牌，可向 Azure AD 进行身份验证。该令牌的有效期为 1 年、2 年或永不过期，具体取决于 Azure AD 中“Web 应用/API”的配置。 如果令牌过期，则须重复步骤 1 和步骤 2。

现可指定要扫描的数据存储。 

## <a name="specify-data-stores-for-the-scanner"></a>指定扫描程序的数据存储

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

## <a name="run-a-discovery-cycle-and-view-reports-for-the-scanner"></a>运行发现周期并查看扫描程序报告

1. 使用“管理工具” > “服务”，启动“Azure 信息保护扫描程序”服务。

2. 等待扫描程序完成其周期。 当扫描程序浏览完指定数据存储中所有文件时，服务停止。 可使用本机 Windows 应用程序和服务事件日志、Azure 信息保护来确认服务的停止时间。 请查看信息事件 ID 911。

3. 查看存储在 %localappdata%\Microsoft\MSIP\Scanner\Reports 中的报告，这些报告的文件格式为 .csv。 利用扫描程序默认配置，只有满足自动分类条件的文件才会被包括在这些报告中。
    
    如果结果与预期不符，建议对在 Azure 信息保护策略中指定的条件进行微调。 如果是这种情况，请重复步骤 1 到 3，直到可更改配置以应用分类和保护（可选）。 每当重复这些步骤时，请先在 Windows Server 计算机上运行以下 PowerShell 命令：
    
        Set-AIPScannerConfiguration -Schedule OneTime

如果已准备好对扫描程序发现的文件进行自动标记，请继续下一步。 

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>将扫描程序配置为应用分类和保护

在其默认设置中，扫描程序在仅报告模式下运行一次。 要更改这些设置，请运行 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet。

1. 在 Windows Server 计算机上的 PowerShell 会话中，运行以下命令：
       
        Set-AIPScannerConfiguration -Enforce On -Schedule Continuous
    
    你可能还希望更改其他配置设置。 例如，是否更改文件属性，以及报告中应记录的内容。 此外，如果 Azure 信息保护策略包括需要理由信息以降低分类级别或移除保护的设置，请使用此 cmdlet 指定该信息。 有关每个配置设置的详细信息，请使用[联机帮助](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration#parameters)。 

2. 使用“管理工具” > “服务”，重启“Azure 信息保护扫描程序”服务。

3. 如前所述，监视事件日志和报告，了解标记了哪些文件、应用了什么分类以及是否应用了保护。

因为我们将计划配置为持续运行，所以当扫描程序扫描完所有文件时，它将开始新周期，以便可发现新文件和更改的文件。


## <a name="how-files-are-scanned"></a>如何扫描文件

扫描程序会自动跳过[从分类和保护中排除](../rms-client/client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)的文件，如可执行文件和系统文件。

可以定义要扫描或不要扫描的文件类型列表，从而更改此行为。 在指定此列表并且不指定数据存储库时，该列表适用于未指定其自己列表的所有数据存储库。 若要指定此列表，请使用 [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes)。 指定文件类型列表后，可以使用 [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes) 向列表添加新文件类型，并能使用 [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes) 从列表中删除文件类型。

然后扫描程序使用 Windows iFilter 扫描以下文件类型。 对于以下文件类型，将使用为标签指定的条件标记文档。

|应用程序类型|文件类型|
|--------------------------------|-------------------------------------|
|Word|.docx; .docm; .dotm; .dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|Project|.mpp; .mpt|
|PDF|。pdf|
|文本|.txt; .xml; .csv|


最后，对于剩余的文件类型，扫描程序将应用 Azure 信息保护策略中的默认标签，或应用为扫描程序配置的默认标签。

|应用程序类型|文件类型|
|--------------------------------|-------------------------------------|
|Project|.mpp; .mpt|
|发布者|.pub|
|Visio|.vsd; .vdw; .vst; .vss; .vsdx; .vsdm; .vssx; .vssm; .vstx; .vstm|
|XPS|.xps; .oxps; .dwfx|
|Solidworks|.sldprt; .slddrw; .sldasm|
|Jpeg |.jpg; .jpeg; .jpe; .jif; .jfif; .jfi|
|Png |。png|
|Gif|.gif|
|位图|.bmp; .giff|
|Tiff|.tif; .tiff|
|Photoshop|.psdv|
|DigitalNegative|.dng|
|Pfile|。pfile|

如果扫描程序应用保护标签，默认只有 Office 文件类型受到保护。 可以更改此行为，让其他文件类型也受到保护。 不过，如果标签向文档应用常规保护，文件扩展名变成 .pfile。 此外，文件将变为只读，直到该文件被已授权用户打开并以本机格式保存。 文本和图像文件也可以更改其文件扩展名并变为只读。 

例如，若要将此默认扫描程序行为更改为以常规方式保护其他文件类型，必须手动编辑注册表，并指定要保护的其他文件类型。 有关说明，请参阅开发人员指南中的[文件 API 配置](../develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。 对于扫描程序，必须指定特定文件名扩展，且不可使用 `*` 通配符。

## <a name="when-files-are-rescanned"></a>重新扫描文件时的情况

在第一个扫描周期，扫描程序会检查所配置的数据存储中的所有文件，然后在后续扫描中仅检查新文件或修改后的文件。 

可通过运行 `-Type` 参数设为 Full 的 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)强制扫描程序重新检查所有文件。 在你希望报告包含所有文件时，此配置非常有用；且它通常在扫描程序于发现模式中运行时使用。 完成全部扫描后，扫描类型自动更改为“增量”，以便后续扫描仅扫描新文件或修改后的文件。

此外，在扫描程序下载具有新条件或更改后的条件时，会检查所有文件。 扫描程序每小时刷新一次策略，当服务启动时以及策略执行一小时之后，也会刷新。  

> [!TIP]
> 如需以低于一小时的间隔刷新策略（例如在测试期间）：请从 **%LocalAppData%\Microsoft\MSIP\Policy.msip** 和 **%LocalAppData%\Microsoft\MSIP\Scanner** 手动删除策略文件 **Policy.msip**。 然后重新启动 Azure 信息扫描程序服务。
> 
> 如果更改了此策略中的保护设置，请在保存保护设置后等待 15 分钟，再重新启动该服务。

如果扫描程序下载了未配置任何自动条件的策略，不会更新扫描程序文件夹中的策略文件副本。 在此方案中，必须从 **%LocalAppData%\Microsoft\MSIP\Policy.msip** 和 **%LocalAppData%\Microsoft\MSIP\Scanner** 中删除策略文件 **Policy.msip**，然后扫描程序才能够使用正确配置了自动条件标签的新下载的策略文件。

## <a name="using-the-scanner-with-alternative-configurations"></a>使用具有备选配置的扫描程序

Azure 信息保护扫描程序支持两种备选方案，在任何一种方案中都无需配置标签： 

- 将默认标签应用于数据存储库中的所有文件。
    
    对于此配置，使用 [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) cmdlet，并将“MatchPolicy” 参数设置为“关闭”。 
    
    根据为数据存储库指定的默认标签（通过 SetDefaultLabel参数），不会检查文件的内容并会标记数据存储库中的所有文件；如果未指定，则将该默认标签指定为扫描程序帐户的策略设置。
    

- 标识所有自定义条件和已知敏感信息类型。
    
    对于此配置，使用 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet，并将“DiscoverInformationTypes”参数设置为“全部”。
    
    扫描程序使用为 Azure 信息保护策略中的标签指定的任何自定义条件以及可指定用于 Azure 信息保护策略中的标签的信息类型列表。 

## <a name="optimizing-the-performance-of-the-scanner"></a>优化扫描程序性能

若要最大程度实现扫描程序的性能：

- **在扫描程序计算机和被扫描的数据存储之间建立高速可靠的网络连接**
    
    例如，将扫描程序计算机置于所扫描的数据存储所在的 LAN 或（首选）网络段中。
    
    网络连接的质量会影响扫描程序的性能，因为要检查文件，扫描程序需将文件内容传输到运行扫描程序服务的计算机中。 如果减少（或消除）此数据需传输的网络跃点数，网络上的负载随之减少。 

- **确保扫描程序计算机具有可用的处理器资源**
    
    检查文件内容是否与你配置的条件相匹配，以及进行文件加密和解密，这些操作都是处理器密集型操作。 请监视所指定的数据存储的典型扫描周期，以确定缺少处理器资源是否对扫描程序性能造成负面影响。
    
- **不扫描运行扫描程序服务的计算机上的本地文件夹**
    
    如果 Windows 服务器上具有要扫描的文件夹，请在其他计算机上安装扫描程序，并将这些文件夹配置为要扫描的网络共享。 将承载文件和扫描文件这两大功能分开，这意味着这些服务的计算资源不相互竞争。

影响扫描程序性能的其他因素：

- 包含要扫描的文件的数据存储的当前负载和响应时间

- 扫描程序是在发现模式还是强制模式下运行
    
    通常，发现模式的扫描速率比强制模式的高，因为发现操作需要单一文件读取操作，而强制模式需要读取和写入操作。

- 更改 Azure 信息保护中的条件
    
    在第一个扫描周期，扫描程序必须检查每个文件，而后续扫描周期默认仅扫描新文件和更改的文件，因此第一个周期明显比后续周期耗时长。 但是，如果更改 Azure 信息保护中的条件，则重新扫描所有文件，如[上一部分](#when-files-are-rescanned-by-the-azure-information-protection-scanner)所述。

- 所选的日志记录级别
    
    可对扫描程序报告选择“调试”、“信息”、“错误”或“关闭”。 “关闭”可使性能最佳；“调试”会明显减低扫描程序的速度，应仅用于故障排除。 有关详细信息，请参阅 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet 的 eportLevel 参数。

- 文件自身：
    
    - 扫描 Office 文件比扫描 PDF 文件耗时更短。
    
    - 扫描未受保护的文件比扫描受保护的文件耗时更短。
    
    - 扫描大型文件明显比扫描小文件耗时更多。

- 此外：
    
    - 确认运行扫描程序的服务帐户仅具有[扫描程序先决条件](#prerequisites-for-the-azure-information-protection-scanner)部分中记录的权限，然后再将[高级客户端属性](../rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner)配置为禁用扫描程序的低完整性级别。
    
    - 在使用[备选配置](#using-the-scanner-with-alternative-configurations)将默认标签应用于所有文件时，扫描程序可以更快地运行，因为扫描程序不检查文件内容。
    
    - 在使用[备选配置](#using-the-scanner-with-alternative-configurations)标识所有自定义条件和已知敏感信息类型时，扫描程序的运行速度更为缓慢。
    

## <a name="list-of-cmdlets-for-the-scanner"></a>适用于扫描程序的 cmdlet 列表 

利用其他适用于扫描程序的 cmdle，可更改该扫描程序的服务帐户和数据库、获取扫描程序的当前设置，以及卸载扫描程序服务。 扫描程序使用以下 cmdlet：

- [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes)

- [Add-AIPScannerRepository](/powershell/module/azureinformationprotection/Add-AIPScannerRepository)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerRepository](/powershell/module/azureinformationprotection/Get-AIPScannerRepository)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Remove-AIPScannerRepository](/powershell/module/azureinformationprotection/Remove-AIPScannerRepository)

- [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes)

- [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)


## <a name="event-log-ids-and-descriptions-for-the-scanner"></a>扫描程序的事件日志 ID 和说明

利用以下部分，确定扫描程序可能的事件 ID 和说明。 这些事件记录在扫描程序服务的服务器上、Windows 应用程序和服务事件日志和 Azure 信息保护中。

-----

信息 910

**扫描程序周期已开始。**

当扫描程序服务启动并开始扫描指定数据存储库中的文件时，会记录此事件。

----

信息 911

**扫描程序周期已结束。**

如果服务器启动后，扫描程序已完成其一次性扫描，或扫描程序已完成连续计划的一个周期，则会记录此事件。

如果扫描程序配置为运行一次（而不是连续运行），必须将计划设置为“一次”或“连续”，并手动重启服务，然后才能重新扫描文件。 若要更改计划，请使用 [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) cmdlet 和 Schedule 参数。

----

## <a name="next-steps"></a>后续步骤

你可能想知道：[Windows Server FCI 和 Azure 信息保护扫描程序有何区别？](../get-started/faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

还可在台式计算机中，利用 PowerShell 以交互方式对文件进行分类和保护。 要详细了解此方案及使用 PowerShell 的其他方案，请参阅[将 PowerShell 与 Azure 信息保护客户端配合使用](../rms-client/client-admin-guide-powershell.md)。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
