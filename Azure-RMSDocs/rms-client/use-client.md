---
title: Azure 信息保护客户端-AIP
description: Microsoft Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的数据。 客户端（Azure 信息保护客户端或 Rights Management 客户端）与在计算机和移动设备上运行的应用程序集成。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 51d5ea830335e86007a3caabbbf724d16c33f97b
ms.sourcegitcommit: 47a6def47b8a121eb5aa8071863a765bfc31fc9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2020
ms.locfileid: "83825450"
---
# <a name="the-client-side-of-azure-information-protection"></a>Azure 信息保护的客户端

>*适用于： Active Directory Rights Management Services， [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）**** 和标签管理**** 将于 2021 年 3 月 31 日**** 弃用****。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。


Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的文档和电子邮件：

- 客户端可以是适用于 Office 的内置标签客户端、适用于 Windows 的 Azure 信息保护统一标签客户端、适用于 Windows 的 Azure 信息保护客户端（经典）或 Rights Management 的客户端。
    
    这些客户端通常称为**Office 内置标签客户端**、**统一标签客户端**、**经典客户**端和**RMS 客户**端。 无论使用哪种客户端，它都将与你在计算机和移动设备上运行的应用程序相集成。

- 此服务驻留在云中或本地。 云服务是 Azure 信息保护，它使用 Azure Rights Management 服务进行数据保护。 本地服务 Active Directory Rights Management Services，更常见的称为 AD RMS。 

所有这些客户端与 Office 应用程序集成，但必须单独安装统一标签客户端和经典客户端，并支持其他功能和组件。 例如，这些客户端包括对文件资源管理器的支持，因此你可以在 Office 外部对文件进行分类和保护。 其他组件包括用于受保护的 PDF 文档和受保护的图像的查看器，以及用于本地数据存储的扫描仪。

RMS 客户端仅提供保护。 此客户端与某些应用程序（如 Office 应用程序、Azure 信息保护客户端和软件供应商提供的启用应用程序）自动安装。 不过，它也可以[自行安装](https://www.microsoft.com/en-us/download/details.aspx?id=38396)，以支持[从受 IRM 保护的库和 OneDrive 同步文件](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)，并为希望将 rights management 保护集成到业务线应用程序的开发人员提供支持。

## <a name="choose-which-labeling-client-to-use-for-windows-computers"></a>选择要用于 Windows 计算机的标记客户端

如果可能，请使用其中一个标签客户端，因为标签抽象地为用户应用保护的复杂性，并且标签还提供分类，以便您可以跟踪和管理数据。

你为 Windows 计算机选择的标记客户端可能会受到你使用的管理门户的影响：

- Office 内置标签客户端和 Azure 信息保护统一标签客户端从以下管理中心下载标签和策略设置： 
    - Office 365 安全与合规中心
    - Microsoft 365 安全中心
    - Microsoft 365 合规中心

- Azure 信息保护客户端（经典）从 Azure 门户下载标签和策略设置。

由于统一的标签客户端和经典客户端需要单独安装到 Office，因此你必须从[Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载并安装这些客户端。 

应使用哪种客户端？

- 如果你的 Office 365 应用程序的最低版本为1910，并且你想要使用 MacOS、iOS 和 Android 也可以使用的相同标签和策略设置，则在 Windows 计算机上使用**为 office 内置的标签客户端**，你将需要使用可由、IOS 和 Android 使用的相同标签和策略设置。 这些功能包括功能区下的信息保护栏，便于选择和查看标签。 
    
    此客户端支持切换帐户，因为它不使用 Office 加载项，所以它比使用任何一个 Azure 信息保护客户端在 Office 应用中提供的性能更好。 由于在 Office 中内置了标记，因此此标签客户端无单独安装和维护。 此外，与 Office 外接程序不同的是，不能禁用。

- 使用 Windows 计算机上的**Azure 信息保护统一的标签客户端**，可以使用 MacOS、IOS 和 Android 等标签和策略设置，而无需将文件独立于 Office 365 应用，也不需要经典客户端支持的功能。 这些功能目前包括使用本地密钥（HYOK）保护内容和本地数据存储的扫描程序的通用版本。

- 如果需要的客户端版本的客户端尚不支持统一标签客户端，请在 Windows 计算机上安装**Azure 信息保护客户端（经典）** 。 尽管此客户端可以使用 MacOS、iOS 和 Android 使用的相同标签，但它具有不同的策略设置。 因此，你的折衷是使用另一个管理门户和用户的不同用户体验进行管理。

最新版本的统一标签客户端使其能够与经典客户端在功能上关闭奇偶校验。 由于这种差距关闭，你会希望将新功能仅添加到统一的标签客户端。 出于此原因，我们建议你在其当前功能集和功能满足你的业务需求的情况下部署统一的标签客户端。 否则，或者如果已在尚未[迁移到统一标签存储](../configure-policy-migrate-labels.md)的 Azure 门户中配置了标签，请使用经典客户端。

可以在同一环境中使用不同的客户端以支持不同的业务要求，如下面的部署示例中所示。 在混合客户端环境中，建议使用统一标签，以便客户端共享相同的标签集以便于管理。 默认情况下，新客户具有统一标签，因为其租户位于统一的标签平台上。 有关详细信息，请参阅[如何确定我的租户是否在统一标签平台上？](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

如果 Windows 计算机运行的 Office 365 应用程序的最低版本为1910，并且安装了一个 Azure 信息保护客户端，则默认情况下，Office 应用程序中会禁用内置的标记客户端。 但是，可以更改此行为，以便仅将内置标签客户端用于 Office 应用。 使用此配置时，Azure 信息保护客户端（经典或统一标签）仍可用于在文件资源管理器、PowerShell 和扫描程序中进行标记。 有关禁用 Office 365 应用中的 Azure 信息保护客户端的说明，请参阅 Microsoft 365 合规性文档中的[Office 内置标签客户端和 Azure 信息保护客户](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#office-built-in-labeling-client-and-the-azure-information-protection-client)端部分。

##### <a name="example-deployment-strategy"></a>示例部署策略：

- 对于大多数用户，可以部署 Azure 信息保护统一标签客户端，因为此客户端满足这些用户的业务需求。 
    
    对于这些用户，他们在 Windows、Mac、iOS 和 Android 中的标记体验非常相似，因为它们具有相同的发布到它们的标签和相同的策略设置。 作为管理员，你可以在同一管理中心管理这些标签和策略设置。

- 你还会自行安装统一标签客户端，以测试 Azure 信息保护扫描程序。

- 对于用户的子集，可以部署经典客户端，因为这些用户需要应用 "保留自己的密钥" （HYOK）保护的标签。
    
    对于这些用户，他们在使用此客户端时具有略微不同的标签体验。 例如，他们将在 Office 应用程序中看到 "**保护**" 按钮，而不是 "**敏感度**" 按钮。 作为管理员，你需要将不同管理中心的 HYOK 设置和策略设置的标签管理到其他客户端平台的标签和设置。

- 你有本地数据存储，其中包含需要扫描敏感信息或分类和保护的文档。 对于生产用途，请在服务器上部署经典客户端，以运行 Azure 信息保护扫描程序。

## <a name="compare-the-labeling-clients-for-windows-computers"></a>比较 Windows 计算机的标签客户端

使用下表来帮助比较 Windows 计算机的三个标记客户端支持的功能。

若要在不同的操作系统平台（Windows、MacOS、iOS 和 Android）和 web 上比较 Office 内置敏感度标签功能，请参阅 Microsoft 365 符合性文档，了解如何[在应用中提供敏感度标签功能](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)。 本文档还包括 Office 生成号或受支持功能的 Office 更新通道信息。

|功能|经典客户端|统一标签客户端|Office 内置标签客户端|
|:------|:------------:|:---------------------:|:-----------------------------:|
|手动标记：| **是** | **是** |**是** |
|默认标签：| **是** | **是** | **是** |
|建议或自动添加标签： <br />-适用于 Word、Excel、PowerPoint| **是** | **是** | **是** |
|建议或自动添加标签：<br />-适用于 Outlook| **是** | **是** | 否 |
|必需标签：| **是** | **是** | 否 |
|用户定义的标签权限： <br />-不转发电子邮件| **是** | **是** | **是** |
|用户定义的标签权限： <br />-Word、Excel、PowerPoint、文件资源管理器的自定义权限| **是** | **是** | **是** |
|标签的多语言支持：| **是** | **是** |**是** |
|来自电子邮件附件的标签继承：| **是** | **是**  |否 |
|包括以下内容的自定义项：<br />- 电子邮件的默认标签<br />-Outlook 中的弹出消息 <br />- S/MIME 支持<br />- 报告问题选项| 是  <sup>1</sup> | 是  <sup>2</sup> | 否 |
|本地数据存储的扫描程序：| **是** | **是的<br />** | 否 |
|中心报告（分析）：| **是** | **是** | 否 |
|独立于标签的自定义权限集：| **是** | 是  <sup>3</sup>| 否 |
|Office 应用中的“信息保护”栏：| **是** | **是**| 否 |
|作为标签操作（页眉、页脚、水印）的可视标记：| **是** | **是** | **是**|
|每应用视觉标记：| **是** | **是** | 否 |
|带有变量的动态视觉标记：| **是** | **是** | 否 |
|带有文件资源管理器的标签：| **是** | **是** | 否 |
|受保护文件的查看器（文本、图像、PDF、.pfile）：| **是** | **是** | 否|
|应用标签的 PPDF 支持：| **是** | 否 | 否 |
|PowerShell 标记 cmdlet：| **是** | 是  <sup>4</sup> | 否 |
|离线支持保护操作：| **是** | 是  <sup>5</sup> | **是** |
|为断开连接的计算机手动执行策略文件管理：| **是** |**是**| 否 |
|HYOK 支持：| **是** | 否 | 否 |
|事件查看器中的使用日志记录：| **是** | 否 |否 |
|显示 Outlook 中的 "不要转发" 按钮：| **是** | 否 | 否 |
|跟踪受保护文档：| **是** | 是  <sup>6</sup> | 否 |
|吊销受保护的文档：| **是** | 否 | 否 |
|仅保护模式（无标签）：| **是** | 否 | 否 |
|支持帐户切换：| 否 | 否 | **是** |
|支持远程桌面服务：| **是** | **是** | **是** |
|对 AD RMS 的支持：| **是** | No <sup>7</sup> | 否 |
|删除应用中的外部内容标记| **是**| 否| **是**|


脚注：

<sup>1</sup>这些设置以及[在 Azure 门户中配置的高级客户端设置](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal)支持许多其他设置。

<sup>2</sup>这些设置以及其他许多设置都受支持，作为[你用 PowerShell 配置的高级设置](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)。

<sup>3</sup>由文件资源管理器和 PowerShell 支持。 在 Office 应用中，用户可以选择 "**文件信息**" "  >  **保护文档**" "  >  **限制访问**"。

<sup>4</sup>不支持删除容器文件（zip）的保护。

<sup>5</sup>对于文件资源管理器和 PowerShell 命令，用户必须连接到 internet 才能保护文件。

<sup>6</sup>统一标签客户端不支持经典客户端支持的文档跟踪站点。 但是，如果不需要首先注册要跟踪的文档，管理员就可以使用[集中报告](../reports-aip.md)来确定是否从 Windows 计算机访问受保护的文档，以及访问是被授予还是被拒绝。 

<sup>7</sup>不支持标签和保护操作。 但是，对于 AD RMS 部署，当你使用[Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))时，查看器可以打开受保护的文档。


### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Azure 信息保护客户端的详细比较

当 Azure 信息保护客户端（经典）和 Azure 信息保护统一标签客户端都支持相同的功能时，请使用下表来帮助确定两个客户端之间的功能差异。

|功能 |经典客户端|统一标签客户端|
|--------------|-----------------------------------|-----------------------------------------------------------|
|设置：| 安装本地演示策略的选项 | 没有本地演示策略|
|在 Office 应用程序中应用时的标签选择和显示：|通过功能区上的“保护”按钮**** <br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|通过功能区上的“敏感度”**** 按钮<br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|
|在 Office 应用程序中管理“信息保护”栏：|面向用户： <br /><br />- 从功能区上的“保护”按钮选择显示或隐藏栏****<br /><br />- 如果用户选择隐藏栏，默认情况下，该栏在应用程序中隐藏，但会继续自动显示在新打开的应用程序中 <br /><br /> 面向管理员： <br /><br />- 在应用程序首次打开时，通过策略设置自动显示或隐藏栏，并控制在用户选择隐藏栏后，该栏是否对新打开的应用程序自动保持隐藏状态|面向用户： <br /><br />- 从功能区上的“敏感度”按钮选择显示或隐藏栏****<br /><br />- 当用户选择隐藏栏时，该栏在该应用程序中以及新打开的应用程序中均处于隐藏状态 <br /><br />面向管理员： <br /><br />-用于管理栏的 PowerShell 设置 |
|标签颜色： | 在 Azure 门户中配置 | 在迁移标签之后保留并可通过[PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)进行配置|
|标签支持不同语言：| 在 Azure 门户中配置 | 使用[Office 365 Security & 相容性 PowerShell](/microsoft-365/compliance/create-sensitivity-labels#additional-label-settings-with-office-365-security--compliance-center-powershell)进行配置|
|策略更新： | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 24 小时一次 <br /><br />对于扫描程序：每小时和服务启动时间，策略超过1小时| 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 4 小时一次 <br /><br />对于扫描仪：每隔4小时|
|PDF 支持的格式：| 保护: <br /><br /> - PDF 加密的 ISO 标准（默认） <br /><br /> - .ppdf <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护| 保护: <br /><br /> - PDF 加密的 ISO 标准 <br /><br /> <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护|
|用查看器打开的通用受保护文件（.pfile）：| 文件将在原始应用中打开，然后可在其中查看、修改和保存该文件而无需保护 | 文件将在原始应用中打开，然后可在其中进行查看和修改，但不能保存|
|支持的 cmdlet：| 用于标记的 cmdlet 和用于保护的 cmdlet | 用于标记的 cmdlet：<br /><br /> Set-aipfileclassification 和 Set-aipfilelabel 不支持*Owner*参数 <br /><br /> 此外，对于未应用标签的所有场景，都有一条“无适用标签”的注释 <br /><br /> Set-aipfileclassification 支持*WhatIf*参数，因此它可以在发现模式下运行 <br /><br /> Set-AIPFileLabel 不支持 EnableTracking** 参数 <br /><br /> Get-AIPFileStatus 不从其他租户返回标签信息，也不显示 RMSIssuedTime** 参数<br /><br />此外，Get-aipfilestatus 的*LabelingMethod*参数显示**特权**或**标准**，而不是**手动**或**自动**。 有关详细信息，请参阅[联机文档](/powershell/module/azureinformationprotection/get-aipfilestatus)。|
|Office 中每个操作的对齐方式提示（如果已配置）： | 频率：每个文件 <br /><br /> 降低敏感度级别 <br /><br /> 删除标签<br /><br /> 删除保护 | 频率：每个会话 <br /><br /> 降低敏感度级别<br /><br /> 删除标签|
|删除已应用的标签操作： | 系统提示用户确认 <br /><br />下次 Office 应用程序打开文件时，不会自动应用默认标签或自动标签（如果已配置）  <br /><br />| 不提示用户确认<br /><br /> 下次 Office 应用程序打开文件时，自动应用默认标签或自动标签（如果已配置）|
|自动和推荐的标签： | 在 Azure 门户中配置为[标签条件](../configure-policy-classification.md)，其中包含使用短语或正则表达式的内置信息类型和自定义条件 <br /><br />配置选项包括： <br /><br />- 唯一/非唯一计数 <br /><br /> - 最小计数| 在管理中心中配置，包含内置敏感信息类型和[自定义信息类型](https://docs.microsoft.com/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />配置选项包括：  <br /><br />- 仅唯一计数 <br /><br />- 最小和最大计数 <br /><br />- 信息类型支持 AND 和 OR <br /><br />- 关键字字典<br /><br />- 可自定义的可信度和字符接近度|
|对附件的子标签订购支持： | 使用[高级客户端设置](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)启用 | 默认情况下启用，无需配置|
|更改文件类型的默认保护行为： | 你可以使用[注册表编辑](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)来替代本机保护和常规保护的默认值 | 你可以使用[PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)来更改受保护的文件类型|

有关特定保护设置的行为差异的详细比较，请参阅[比较标签的保护设置的行为](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label)。

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>未计划在 Azure 信息保护统一标签客户端中的功能

尽管 Azure 信息保护的统一标签客户端仍处于开发阶段，但当前未计划在未来版本中为统一标签客户端提供以下功能和行为差异： 

- 自定义权限是[用户可在 Office 应用程序中选择的单独选项： Word、Excel 和 PowerPoint](client-classify-protect.md#set-custom-permissions-for-a-document)

- 从 Office 应用和文件资源管理器[跟踪和撤消](client-track-revoke.md)选项

- Azure 信息保护栏标题和工具提示

- 使用模板[的仅保护模式](client-protection-only-mode.md)（无标签）

- 保护 PDF 文档为[ppdf （较旧格式）](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)

- 在 Outlook 中显示“不可转发”按钮

- 演示策略

- 确认提示**是否要删除此标签？** 对于用户，如果未使用策略设置进行理由，

- 连接到 Rights Management 服务的单独 PowerShell cmdlet

- 显示应用了标签的用户标识


### <a name="parent-labels-and-their-sublabels"></a>父标签及其子标签 

Azure 信息保护客户端（经典）不支持指定具有子标签的父标签的配置。 这些配置包括指定默认标签和推荐分类或自动分类的标签。 如果某个标签具有子标签，可以指定其中一个子标签，但不能指定父标签。

对于奇偶校验，Azure 信息保护统一标签客户端也不支持应用具有子标签的父标签，即使可以在管理中心中选择这些标签，也无法应用。 在此方案中，Azure 信息保护统一标记客户端将不应用父标签。

## <a name="next-steps"></a>后续步骤

若要安装和配置 Azure 信息保护客户端，请使用以下文档：

- [Azure 信息保护客户端](AIP-client.md)

- [Azure 信息保护统一标识客户端](unifiedlabelingclient-version-release-history.md)

若要详细了解如何使用 Office 365 应用的内置标签客户端，请参阅[office 应用中的敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)。
