---
title: Azure 信息保护客户端-AIP
description: Microsoft Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的数据。 客户端（Azure 信息保护客户端或 Rights Management 客户端）与在计算机和移动设备上运行的应用程序集成。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/20/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: fd76ce1c8efa79050869a93a311f0ae80d59d0b4
ms.sourcegitcommit: d3548610fbfee6006e12acd5471e085edf2da483
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2021
ms.locfileid: "99473032"
---
# <a name="the-client-side-of-azure-information-protection"></a>Azure 信息保护的客户端

>***适用于**： Active Directory Rights Management Services， [azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，[azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows Server 2016，Windows server 2012 R2，windows server 2012 *
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP 和旧版 Windows 和 office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。*
>
>相关内容：*[AIP 统一标记客户端和经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。


Azure 信息保护统一标签客户端提供了一个客户端-服务器解决方案，可帮助保护组织的文档和电子邮件，并替代了 [用于 Microsoft Office 的内置标记解决方案](/microsoft-365/compliance/sensitivity-labels)。 

除了直接与 Office 应用程序集成外，统一的标签客户端还包括对文件资源管理器和 PowerShell 的支持，以便你可以在 Office 外部对文件进行分类和保护。 其他组件包括用于受保护的 Pdf 和图像的查看器以及用于本地数据存储的扫描仪。

统一标签客户端必须单独安装到 Office 应用。

服务位于云中或本地：

- 云服务是 **Azure 信息保护**，使用 Azure Rights 管理服务进行数据保护
- 本地服务 **Active Directory Rights Management Services** (AD RMS 中) 

## <a name="choose-your-windows-labeling-solution"></a>选择 Windows 标记解决方案

标签可让用户更轻松地应用保护，还可以提供分类，以便跟踪和管理数据。 

选择 Windows 标记解决方案时，请考虑以下基本差异：

- **从何处下载标签和标签策略** 

    内置标签解决方案和 AIP 统一标签客户端使用以下管理中心之一： 
    
    - Office 365 安全与合规中心 
    - Microsoft 365 安全中心 
    - Microsoft 365 合规中心
      
    如果你使用的是旧的 AIP 经典客户端，则会在 Azure 门户中下载和管理标签和标签策略。 

- **安装要求**

    内置标签解决方案无需单独安装。

    AIP 统一标签客户端和传统经典客户端均需要单独安装到 Office。 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载并安装统一的标签客户端。  

    如果需要下载并安装旧的经典客户端，请联系支持人员并打开票证以访问安装文件。 

使用下列部分来帮助你确定最适合你的组织的客户端：

- [内置 Office 标签解决方案](#built-in-office-labeling-solution)
- [Azure 信息保护统一标识客户端](#azure-information-protection-unified-labeling-client)
- [Azure 信息保护经典客户端](#azure-information-protection-classic-client)
- [在同一环境中使用多个客户端](#using-multiple-clients-in-the-same-environment)

有关详细信息，请参阅： AIP 客户端和功能的 [详细比较](#detailed-comparisons-for-the-azure-information-protection-clients) ， [不为统一标签客户端计划](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client)。

> [!NOTE]
> 最新版本的统一标签客户端使其能够与经典客户端在功能上关闭奇偶校验。 由于这种差距关闭，你会希望将新功能仅添加到统一的标签客户端。 
>
> 如果客户的当前功能集和功能满足你的业务要求，我们建议你部署统一的标签客户端。
> 

### <a name="built-in-office-labeling-solution"></a>内置 Office 标签解决方案

内置 Microsoft Office 的标记解决方案：

- 需要具有 Microsoft 365 应用程序的 Windows 计算机，最低版本1910
- 允许共享 macOS、iOS 和 Android 也可以使用的标签和策略设置
- 支持切换帐户
- 在 Office 应用程序中提供更好的性能
- 不需要单独安装和维护
- 无法禁用。

如果需要仅提供 Azure 信息保护客户端的功能（如功能区下的信息保护栏），**请勿使用** 内置的 Office 标签客户端。 此栏提供更轻松的标签选择和可见性。

### <a name="azure-information-protection-unified-labeling-client"></a>Azure 信息保护统一标识客户端

统一标签客户端需要 Windows 计算机，并使你能够共享 macOS、iOS 和 Android 也可以使用的标签和策略设置。

如果已在尚未 [迁移到统一标签存储](../configure-policy-migrate-labels.md)的 Azure 门户中配置了标签，**请不要使用** 统一标签客户端。

### <a name="azure-information-protection-classic-client"></a>Azure 信息保护经典客户端

经典客户端是 AIP 的旧客户端，支持与统一标签客户端类似的功能，并且还必须单独安装到 Office 应用。 

经典客户端 [在2021年3月被弃用](https://aka.ms/aipclassicsunset)。

仅当尚未迁移到统一标签时，才使用经典客户端。 有关详细信息，请参阅[教程：从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端](../tutorial-migrating-to-ul.md)。

对于 macOS、iOS 和 Android，经典客户端具有不同的策略设置。 因此，虽然你可能想要使用其他功能，但你必须使用单独的管理门户和用户体验来保护操作系统上的内容。

如果可能，我们建议使用统一标签客户端，而不是经典客户端。

### <a name="using-multiple-clients-in-the-same-environment"></a>在同一环境中使用多个客户端

可以在同一环境中使用不同的客户端以支持不同的业务要求，如下面的部署示例中所示。 在混合客户端环境中，建议使用统一标签，以便客户端共享相同的标签集以便于管理。 默认情况下，新客户具有统一标签，因为其租户位于统一的标签平台上。 有关详细信息，请参阅 [如何确定我的租户是否在统一标签平台上？](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

如果你的 Windows 计算机运行 Microsoft 365 最小版本1910的应用和安装其中一个 Azure 信息保护客户端，则默认情况下，在 Office 应用中禁用内置标记解决方案。 但是，可以更改此行为，以便仅对 Office 应用使用内置标记解决方案。 使用此配置时，Azure 信息保护客户端仍可用于在文件资源管理器、PowerShell 和扫描程序中进行标记。 有关在 Microsoft 365 应用中禁用 Azure 信息保护客户端的说明，请参阅 Microsoft 365 合规性文档中的 [Office 内置标签解决方案和 Azure 信息保护客户端](/microsoft-365/compliance/sensitivity-labels-office-apps#office-built-in-labeling-client-and-the-azure-information-protection-client) 部分。

##### <a name="sample-deployment-strategy"></a>示例部署策略

- 对于大多数用户，可以部署 Azure 信息保护统一标签客户端，因为此客户端满足这些用户的业务需求。 
    
    对于这些用户，他们在 Windows、Mac、iOS 和 Android 中的标记体验都是相似的，因为它们具有相同的发布到它们的标签和相同的策略设置。 作为管理员，你可以在同一管理中心管理这些标签和策略设置。

- 你还会自行安装统一标签客户端，以测试 Azure 信息保护扫描程序。

- 对于用户的子集，你可以部署经典客户端，因为这些用户需要应用 "保留你自己的密钥 ([HYOK](../configure-adrms-restrictions.md)) 保护的标签。
    
    对于这些用户，他们在使用此客户端时具有略微不同的标签体验。 例如，他们将在 Office 应用程序中看到 " **保护** " 按钮，而不是 " **敏感度** " 按钮。 作为管理员，你需要将不同管理中心的 HYOK 设置和策略设置的标签管理到其他客户端平台的标签和设置。

- 你有本地数据存储，其中包含需要扫描敏感信息或分类和保护的文档。 对于生产用途，请在服务器上部署统一的标记客户端，以运行 [Azure 信息保护扫描程序](../deploy-aip-scanner.md)。

#### <a name="rights-management-client"></a>Rights Management 客户端

RMS 客户端仅提供保护，并自动与某些应用程序（包括 Office 应用程序、AIP 统一标签和经典客户端）和其他软件供应商提供的 RMS 启用应用程序一起安装。 

你还可以 [自行安装 RMS 客户端](https://www.microsoft.com/download/details.aspx?id=38396)，以支持 [从受 IRM 保护的库和 OneDrive 同步文件](/onedrive/deploy-on-windows)，并为希望将 rights management 保护集成到业务线应用程序的开发人员提供支持。

## <a name="compare-the-labeling-solutions-for-windows-computers"></a>比较适用于 Windows 计算机的标记解决方案

使用下表来帮助比较 Windows 计算机的三个标记解决方案支持的功能。

若要在 Windows、macOS、iOS 和 Android) 的不同操作系统平台上比较 Office 内置敏感度标签功能，请参阅 Microsoft 365 符合性文档， [支持应用中的敏感度标签功能](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps) (。 本文档还包括 Office 生成号或受支持功能的 Office 更新通道信息。

有关更多详细信息，另请参阅：
- [Azure 信息保护客户端的详细比较](#detailed-comparisons-for-the-azure-information-protection-clients)
- [未计划在 Azure 信息保护统一标签客户端中的功能](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client)

|功能|经典客户端|统一标签客户端|Office 内置标签解决方案|
|:------|:------------:|:---------------------:|:-----------------------------:|
|**手动标记**| ![是](../media/yes-icon.png)   | ![是](../media/yes-icon.png)   |![是](../media/yes-icon.png) |
|**默认标签**| ![是](../media/yes-icon.png)| ![是](../media/yes-icon.png)| ![是](../media/yes-icon.png)|
|**建议或自动标记** <br />适用于 Word、Excel、PowerPoint、Outlook|![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |
|**强制标记**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |  ![是](../media/yes-icon.png)|
|**用户定义的标签权限**： <br />不转发电子邮件| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |
|**用户定义的标签权限**： <br />Word、Excel、PowerPoint 的自定义权限| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |
|**标签的多语言支持**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |![是](../media/yes-icon.png) |
|**从电子邮件附件中标记继承**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png)  | ![否](../media/no-icon.png)|
|**自定义项包括**：<br />- 电子邮件的默认标签<br />-在 Outlook 中弹出消息 <br />- S/MIME 支持<br />- 报告问题选项| ![是 ](../media/yes-icon.png) <sup>1</sup> | ![是 ](../media/yes-icon.png) <sup>2</sup> |  ![否](../media/no-icon.png)|
|**本地数据存储的扫描程序**| ![是](../media/yes-icon.png) |  ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|
|**集中报告 (分析)**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|
|**独立于标签的自定义权限集**| ![是](../media/yes-icon.png) | ![是 ](../media/yes-icon.png) <sup>3</sup>|  ![否](../media/no-icon.png)|
|**Office 应用中的信息保护栏**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png)|  ![否](../media/no-icon.png)|
|**作为标签操作的视觉标记**<br>  (页眉、页脚、水印) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png)|
|**每应用视觉标记**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是 ](../media/yes-icon.png) <sup>9</sup>|
|**带有变量的动态视觉标记**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是 ](../media/yes-icon.png) <sup>9</sup>|
|**删除应用中的外部内容标记**| ![是](../media/yes-icon.png)| ![是](../media/yes-icon.png)| ![否](../media/no-icon.png)|
|**带有文件资源管理器的标签**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|
|**受保护文件的查看器** <br>  (文本、图像、PDF、.pfile) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![否](../media/no-icon.png)|
|**PPDF 支持应用标签**| ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|  ![否](../media/no-icon.png)|
|**PowerShell 标记 cmdlet**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png)  |  ![否](../media/no-icon.png)|
|**脱机支持保护操作**| ![是](../media/yes-icon.png) | ![是 ](../media/yes-icon.png) <sup>4</sup> | ![是](../media/yes-icon.png) |
|**为断开连接的计算机手动执行策略文件管理**| ![是](../media/yes-icon.png) |![是](../media/yes-icon.png)|  ![否](../media/no-icon.png)|
|**HYOK 支持**| ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|  ![否](../media/no-icon.png)|
|**使用情况日志记录事件查看器**| ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)| ![否](../media/no-icon.png)|
|**在 Outlook 中显示“不可转发”按钮**| ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|  ![否](../media/no-icon.png)|
|**跟踪受保护的文档**| ![是 ](../media/yes-icon.png) <sup>5</sup> | ![是 ](../media/yes-icon.png) <sup>5</sup> |  ![否](../media/no-icon.png)|
|**吊销受保护的文档**| ![是 ](../media/yes-icon.png) <sup>5</sup> |  ![是 ](../media/yes-icon.png) <sup>5</sup>|  ![否](../media/no-icon.png)|
|**仅保护模式** (无标签) | ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|  ![否](../media/no-icon.png)|
|**支持帐户切换**|  ![否](../media/no-icon.png)|  ![否](../media/no-icon.png)| ![是](../media/yes-icon.png) |
|**支持远程桌面服务**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |
|**支持 AD RMS**| ![是](../media/yes-icon.png) |  ![无 ](../media/no-icon.png) <sup>6</sup> |  ![否](../media/no-icon.png)|
|**支持 Microsoft Office 97-2003 格式**| ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) |  ![无 ](../media/no-icon.png) <sup>8</sup>|
|**双重密钥加密**|  ![否](../media/no-icon.png)| ![是](../media/yes-icon.png) |  ![否](../media/no-icon.png)|
|**政府社区云** | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png) | ![是](../media/yes-icon.png)|
| | | | |

**脚注**：

<sup>1</sup> 这些设置以及 [在 Azure 门户中配置的高级客户端设置](client-admin-guide-customizations.md#how-to-configure-advanced-classic-client-configuration-settings-in-the-portal)支持许多其他设置。

<sup>2</sup> 这些设置以及其他许多设置都受支持，作为 [你用 PowerShell 配置的高级设置](clientv2-admin-guide-customizations.md#configuring-advanced-settings-for-the-client-via-powershell)。

<sup>3</sup> 由文件资源管理器和 PowerShell 支持。 在 Office 应用中，用户可以选择 "**文件信息**" "  >  **保护文档**" "  >  **限制访问**"。

<sup>4</sup> 对于文件资源管理器和 PowerShell 命令，用户必须连接到 internet 才能保护文件。

<sup>5</sup>有关详细信息，请参阅：**统一标记客户端**：[管理员指南 (公共预览版)](track-and-revoke-admin.md)  |   [用户指南 (公共预览版)](revoke-access-user.md)。 仅全局管理员支持跟踪。 **经典客户端**：[管理员指南](client-admin-guide-document-tracking.md)  |  [用户指南](client-track-revoke.md)。 管理员还可以使用 [集中报告](../reports-aip.md) 来确定是否从 Windows 计算机访问受保护的文档，以及访问是被授予还是被拒绝。

<sup>6</sup> 标签和保护操作不受支持。 但是，对于 AD RMS 部署，当你使用 [Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))时，查看器可以打开受保护的文档。

<sup>8</sup> 尽管 AIP 客户端同时支持 Microsoft Office 97-2003 文件格式，如 **.Doc** 和 Office Open xml 格式（如 **.docx**），但内置标签仅支持 Open xml 格式。

<sup>9</sup> 有关内置标签解决方案支持动态内容标记和每个应用内容标记的详细信息，请参阅 [Microsoft 365 文档](/microsoft-365/compliance/sensitivity-labels-office-apps#dynamic-markings-with-variables)。

### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Azure 信息保护客户端的详细比较

如果 Azure 信息保护经典客户端和 Azure 信息保护统一标签客户端都支持同一功能，请使用以下列表来帮助确定两个客户端之间的功能差异：


|功能 |经典客户端|统一标签客户端|
|--------------|-----------------------------------|-----------------------------------------------------------|
|**安装**| 安装本地演示策略的选项 | 没有本地演示策略|
|**在 Office 应用中应用标签时选择并显示标签**|通过功能区上的“保护”按钮 <br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|通过功能区上的“敏感度”按钮<br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|
|**管理 Office 应用中的信息保护栏**|**对于用户**：<br />用于显示或隐藏功能区上的 " **保护** " 按钮中的栏的选项<br /><br>用户选择隐藏栏时，默认情况下，此栏会在该应用中隐藏，但会继续自动显示在新打开的应用中 <br /><br /> **对于管理员**： <br />策略设置，用于在应用首次打开时自动显示或隐藏条形，并控制在用户选择隐藏栏后是否自动隐藏新打开的应用程序栏|**对于用户**： <br />用于显示或隐藏功能区上的 " **敏感度** " 按钮中的栏的选项。 <br><br />当用户选择隐藏此栏时，该应用程序和新打开的应用程序中将隐藏该条形 <br /><br />**对于管理员**： <br />用于管理栏的 PowerShell 设置 |
|**标签颜色**| 在 Azure 门户中配置 | 在迁移标签之后保留并可通过[PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)进行配置|
|**标签支持不同语言**| 在 Azure 门户中配置 | 使用[Office 365 Security & 相容性 PowerShell](/microsoft-365/compliance/create-sensitivity-labels#additional-label-settings-with-office-365-security--compliance-center-powershell)进行配置|
|**策略更新**| -Office 应用程序打开时 <br /> -右键单击以对文件或文件夹进行分类和保护 <br />-运行 PowerShell cmdlet 以进行标记和保护时<br />-每24小时 <br />-对于扫描程序：每小时和服务启动时间，策略超过1小时| -Office 应用程序打开时 <br />-右键单击以对文件或文件夹进行分类和保护 <br />-运行 PowerShell cmdlet 以进行标记和保护时<br />-每隔4小时 <br />-用于扫描程序：每4小时|
|**PDF 支持的格式**| **保护**： <br /> - PDF 加密的 ISO 标准（默认） <br /> - .ppdf <br /><br> **消耗**： <br /> - PDF 加密的 ISO 标准 <br />- .ppdf<br />- SharePoint IRM 保护| **保护**： <br /> - PDF 加密的 ISO 标准 <br /> <br /> **消耗**： <br /> - PDF 加密的 ISO 标准 <br />- .ppdf<br />- SharePoint IRM 保护|
|**在查看器中打开 () 常规受保护的文件**| 文件将在原始应用中打开，然后可在其中查看、修改和保存该文件而无需保护 | 文件将在原始应用中打开，然后可在其中进行查看和修改，但不能保存|
|**受支持的 cmdlet**| -用于标记的 cmdlet <br> -仅用于保护的 cmdlet | **用于标记的 cmdlet**：<br /> [Set-aipfileclassification](/powershell/module/azureinformationprotection/get-aipfileclassification) 和 [Set-aipfilelabel](/powershell/module/azureinformationprotection/get-aipfilelabel) 不支持 **Owner** 参数 <br /> 此外，对于未应用标签的所有场景，都有一条“无适用标签”的注释 <br /><br /> [Set-aipfileclassification](/powershell/module/azureinformationprotection/get-aipfileclassification) 支持 **WhatIf** 参数，因此它可以在发现模式下运行 <br /><br /> [Set-aipfilelabel](/powershell/module/azureinformationprotection/get-aipfilelabel) 不支持 *bre-walkthrough-enabletracking* 参数 <br /><br /> [Get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus) 不返回其他租户的标签信息，并且不显示 **RMSIssuedTime** 参数<br />此外， [get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus)的 **LabelingMethod** 参数显示 **特权** 或 **标准**，而不是 **手动** 或 **自动**。|
|**如果在 Office 中按操作配置) ，则 (对齐提示** | -Frequency：每个文件 <br /> -降低敏感度级别 <br /> -删除标签<br /> -正在删除保护 | -Frequency：每个会话 <br /> -降低敏感度级别<br />-删除标签|
|**删除应用的标签操作** | 系统提示用户确认 <br /><br />如果) 配置的默认标签或自动标签，则下次 Office 应用打开该文件时，不会自动应用 (  | 不提示用户进行确认<br /><br /> 默认标签或自动标签 (如果) 配置，则下次 Office 应用打开该文件时将自动应用该标签|
|**自动和推荐的标签** | 在 Azure 门户中配置为[标签条件](../configure-policy-classification.md)，其中包含使用短语或正则表达式的内置信息类型和自定义条件 <br /><br />配置选项包括： <br />- 唯一/非唯一计数 <br /> - 最小计数| 在管理中心中配置，包含内置敏感信息类型和[自定义信息类型](/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />配置选项包括：  <br />- 仅唯一计数 <br />- 最小和最大计数 <br />- 信息类型支持 AND 和 OR <br />- 关键字字典<br />- 可自定义的可信度和字符接近度|
|**对附件的子标签订购支持** | 使用[高级客户端设置](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)启用 | 默认情况下启用，无需配置|
|**更改文件类型的默认保护行为**| 使用 [注册表编辑](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) 替代本机保护和常规保护的默认值 | 使用 [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) 更改受保护的文件类型|
|**自动重新扫描** | 每次扫描程序检测到策略或标签设置发生更改时，都会自动运行完全重新扫描 | 从版本 [2.8.85.0](unifiedlabelingclient-version-release-history.md#version-28850)开始，管理员可以选择在更改策略或内容扫描作业设置后跳过完全重新扫描。 |
| (公开预览版的 **网络发现**)  |对于经典扫描程序，网络发现功能不可用 | 管理员可以通过扫描指定的 IP 地址或范围来发现其他危险的存储库。|
| | | |

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>未计划在 Azure 信息保护统一标签客户端中的功能

尽管 Azure 信息保护的统一标签客户端仍处于开发阶段，但当前未计划在未来版本中为统一标签客户端提供以下功能和行为差异： 

- 自定义权限是 [用户可在 Office 应用程序中选择的单独选项： Word、Excel 和 PowerPoint](client-classify-protect.md#set-custom-permissions-for-a-document)

- 敏感度工具栏不显示 **敏感度** 标题，也不显示标题工具提示。 栏本身显示在统一的标签客户端中。

- [仅保护模式](client-protection-only-mode.md) (不) 使用模板的标签

- 以 ppdf 格式保护 PDF 文档 [ (旧格式) ](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)

- 显示 Outlook 中的 " **不转发** " 按钮

- 演示策略

- 连接到 Rights Management 服务的单独 PowerShell cmdlet

- 显示应用了标签的用户标识


### <a name="parent-labels-and-their-sublabels"></a>父标签及其子标签 

Azure 信息保护经典客户端不支持指定具有子标签的父标签的配置。 这些配置包括指定默认标签和推荐分类或自动分类的标签。 如果某个标签具有子标签，可以指定其中一个子标签，但不能指定父标签。

对于奇偶校验，Azure 信息保护统一标签客户端也不支持应用具有子标签的父标签，即使可以在管理中心中选择这些标签，也无法应用。 在此方案中，Azure 信息保护统一标记客户端将不应用父标签。

## <a name="next-steps"></a>后续步骤

若要安装和配置 Azure 信息保护统一标签客户端，请参阅：

- [Azure 信息保护统一标记客户端管理员指南](clientv2-admin-guide.md)
- [Azure 信息保护统一标签用户指南](clientv2-user-guide.md)

有关使用 Microsoft 365 应用程序的内置标签解决方案的详细信息，请参阅 [Office 应用中的敏感度标签](/microsoft-365/compliance/sensitivity-labels-office-apps)。
