---
title: The client for Azure Information Protection - AIP
description: Microsoft Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的数据。 客户端（Azure 信息保护客户端或 Rights Management 客户端）与在计算机和移动设备上运行的应用程序集成。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: a5139eed7bccb8a7a57fda0a3b346a1965f7ea50
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474324"
---
# <a name="the-client-side-of-azure-information-protection"></a>Azure 信息保护的客户端

>*Applies to: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的文档和电子邮件：

- The client can be the built-in labeling client for Office, the Azure Information Protection unified labeling client for Windows, the Azure Information Protection client (classic) for Windows, or the Rights Management client.
    
    These clients are often referred to as the **Office built-in labeling client**, the **unified labeling client**, the **classic client**, and the **RMS client**, respectively. Whichever client you use, it integrates with applications that you run on computers and mobile devices.

- The service resides in the cloud or on-premises. The cloud service is Azure Information Protection, which uses the Azure Rights Management service for the data protection. The on-premises service is Active Directory Rights Management Services, more commonly known as AD RMS. 

All these clients integrate with Office applications but the unified labeling client and the classic client must be installed separately and support additional features and components. For example, these clients include support for File Explorer, so you can classify and protect files outside Office. Additional components include a viewer for protected PDF documents and protected images, and a scanner for on-premises data stores.

The RMS client provides protection only. This client is automatically installed with some applications, such as Office applications, the Azure Information Protection clients, and RMS-enlightened applications from software vendors. 但是，它也可以[单独安装](https://www.microsoft.com/en-us/download/details.aspx?id=38396)，以支持[从受 IRM 保护的库和 OneDrive for Business 同步文件](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)，并供希望将权限管理保护集成到业务线应用程序中的开发人员使用。

## <a name="choose-which-labeling-client-to-use-for-windows-computers"></a>Choose which labeling client to use for Windows computers

Where possible, use one of the labeling clients because labels abstract the complexity of applying protection for users, and labels also provide classification so you can track and manage your data.

Your choice of labeling client for your Windows computers might be influenced by which management portal you use:

- The Office built-in labeling client and the Azure Information Protection unified labeling client download labels and policy settings from the following admin centers: 
    - Office 365 Security & Compliance Center
    - Microsoft 365 security center
    - Microsoft 365 compliance center

- The Azure Information Protection client (classic) downloads label and policy settings from the Azure portal.

Because the unified labeling client and the classic client require a separate installation to Office, you must download and install these clients from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Which client should you use?

- Use the **labeling client built in to Office** for your Windows computers when you have Office 365 apps that are a minimum version 1910, you want to use the same labels and policy settings that can also be used by MacOS, iOS, and Android, and you don't need features in your Office apps that require the unified labeling client or classic client. These features include the Information Protection bar under the ribbon for easier label selection and visibility. This client supports switching accounts, and because it doesn't use an Office add-in, it has better performance in Office apps than using either of the Azure Information Protection clients.

- Use the **Azure Information Protection unified labeling client** on Windows computers for labels and policy settings that can also be used by MacOS, iOS, and Android, you want to label files independently from Office 365 apps, and you don’t need features that are only supported by the classic client. These features currently include protecting content with an on-premises key (HYOK) and a general availability version of the scanner for on-premises data stores.

- Install the **Azure Information Protection client (classic)** on Windows computers if you need a version of the client that has features that are not yet available with the unified labeling client. Although this client can use the same labels as those used by MacOS, iOS, and Android, it has different policy settings. So your tradeoff is administration using another management portal and a different user experience for users.

The latest version of the unified labeling client brings it to close parity in features with the classic client. As this gap closes, you can expect new features to be added only to the unified labeling client. For this reason, we recommend you deploy the unified labeling client if its current feature set and functionality meet your business requirements. If not, or if you have configured labels in the Azure portal that you haven't yet [migrated to the unified labeling store](../configure-policy-migrate-labels.md), use the classic client.

You can use different clients in the same environment to support different business requirements, as demonstrated in the following deployment example. In a mixed client environment, we recommend you use unified labels so that clients share the same set of labels for ease of administration. New customers have unified labels by default because their tenants are on the unified labeling platform. For more information, see [How can I determine if my tenant is on the unified labeling platform?](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

When you have a Windows computer that runs Office 365 apps that are a minimum version 1910 and one of the Azure Information Protection clients is installed, by default the built-in labeling client is disabled in Office apps. However, you can change this behavior to use the built-in labeling client for just your Office apps. With this configuration, the Azure Information Protection client (classic or unified labeling) remains available for labeling in File Explorer, PowerShell, and the scanner. For instructions to disable the Azure Information Protection client in Office 365 apps, see the section [Can sensitivity labels run alongside the Azure Information Protection client in Office for Windows?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#can-sensitivity-labels-run-alongside-the-azure-information-protection-client-in-office-for-windows) from the Office documentation.

##### <a name="example-deployment-strategy"></a>Example deployment strategy:

- For the majority of users, you deploy the Azure Information Protection unified labeling client because this client meets the business needs for these users. 
    
    For these users, their labeling experience is very similar across Windows, Mac, iOS, and Android because they have the same labels published to them and the same policy settings. As an admin, you manage these labels and policy settings in the same management center.

- You also install the unified labeling client for yourself, to test the preview version of the Azure Information Protection scanner.

- For a subset of users, you deploy the classic client because these users require labels that apply hold your own key (HYOK) protection.
    
    For these users, they have a slightly different labeling experience when they use this client. For example, they see a **Protect** button rather than a **Sensitivity** button in Office apps. As an admin, you need to manage their labels for HYOK settings and policy settings in a different management center to the labels and settings for the other client platforms.

- You have on-premises data stores with documents that need to be scanned for sensitive information, or classified and protected. For production use, you deploy the classic client on servers to run the Azure Information Protection scanner.

## <a name="compare-the-labeling-clients-for-windows-computers"></a>Compare the labeling clients for Windows computers

Use the following table to help compare which features are supported by the three labeling clients for Windows computers.

To compare the Office built-in sensitivity labeling features across different operating system platforms (Windows, MacOS, iOS, and Android) and for the web, see the Office documentation, [What sensitivity label capabilities are supported in Office today?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#what-sensitivity-label-capabilities-are-supported-in-office-today)

|功能|Classic client|Unified labeling client|Office built-in labeling client|
|:------|:------------:|:---------------------:|:-----------------------------:|
|Manual labeling:| **是** | **是** |**是** |
|Default label:| **是** | **是** | **是** |
|Recommended or automatic labeling:| **是** | **是** | 否 |
|Mandatory labeling:| **是** | **是** | 否 |
|User-defined permissions for a label:<br />- Do Not Forward for emails<br />- Custom permissions for Word, Excel, PowerPoint, File Explorer| **是** | **是** | 否 |
|Multilanguage support for labels:| **是** | **是** |**是** |
|来自电子邮件附件的标签继承：| **是** | **是**  |否 |
|Customizations that include:<br />- 电子邮件的默认标签<br />- Pop-up messages in Outlook <br />- S/MIME 支持<br />- 报告问题选项| **Yes** <sup>1</sup> | **Yes** <sup>2</sup> | 否 |
|本地数据存储的扫描程序：| **是** | **Yes <br />(preview)** | 否 |
|中心报告（分析）：| **是** | **是** | 否 |
|Custom permissions set independently from a label:| **是** | **Yes** <sup>3</sup>| 否 |
|Office 应用中的“信息保护”栏：| **是** | **是**| 否 |
|Visual markings as a label action (header, footer, watermark):| **是** | **是** | **是**|
|Per app visual markings:| **是** | 否 | 否 |
|Dynamic visual markings with variables:| **是** | 否 | 否 |
|Label with File Explorer:| **是** | **是** | 否 |
|A viewer for protected files (text, images, PDF, .pfile):| **是** | **是** | 否|
|PPDF support for applying labels:| **是** | 否 | 否 |
|PowerShell labeling cmdlets:| **是** | **Yes** <sup>4</sup> | 否 |
|离线支持保护操作：| **是** | **Yes** <sup>5</sup> | **是** |
|Manual policy file management for disconnected computers:| **是** |**Yes** <sup>6</sup>| 否 |
|HYOK 支持：| **是** | 否 | 否 |
|Usage logging in Event Viewer:| **是** | 否 |否 |
|Display the Do Not Forward button in Outlook:| **是** | 否 | 否 |
|Track protected documented:| **是** | **Yes** <sup>7</sup> | 否 |
|Revoke protected documents:| **是** | 否 | 否 |
|仅保护模式（无标签）：| **是** | 否 | 否 |
|Support for account switching:| 否 | 否 | **是** |
|对 AD RMS 的支持：| **是** | No <sup>8</sup> | 否 |

脚注：

<sup>1</sup> These settings, and many more are supported as [advanced client settings that you configure in the Azure portal](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal).

<sup>2</sup> These settings, and many more are supported as [advanced settings that you configure with PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).

<sup>3</sup> Supported by File Explorer and PowerShell. In Office apps, users can select **File Info** > **Protect Document** > **Restrict Access**.

<sup>4</sup> No support to remove protection from container files (zip, .rar, .7z, .msg, and .pst).

<sup>5</sup> For File Explorer and PowerShell commands, the user must be connected to the internet to protect files.

<sup>6</sup> Supported for labeling with File Explorer, PowerShell, and the scanner. Not supported for labeling in Office apps.

<sup>7</sup> The document tracking site that's supported by the classic client isn't supported by the unified labeling client. However, without the need to first register the document for tracking, administrators can use [central reporting](../reports-aip.md) to identify whether protected documented are accessed from Windows computers, and whether access was granted or denied. 

<sup>8</sup> Labeling and protection actions aren't supported. However, for an AD RMS deployment, the viewer can open protected documents when you use the [Active Directory Rights Management Services Mobile Device Extension](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).


### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Detailed comparisons for the Azure Information Protection clients

When the Azure Information Protection client (classic) and the Azure Information Protection unified labeling client both support the same feature, use the following table to help identify some functional differences between the two clients.

|功能 |Classic client|Unified labeling client|
|--------------|-----------------------------------|-----------------------------------------------------------|
|安装：| 安装本地演示策略的选项 | 没有本地演示策略|
|在 Office 应用程序中应用时的标签选择和显示：|通过功能区上的“保护”按钮 <br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|通过功能区上的“敏感度”按钮<br /><br /> 通过“信息保护”栏（功能区下方的水平栏）|
|在 Office 应用程序中管理“信息保护”栏：|面向用户： <br /><br />- 从功能区上的“保护”按钮选择显示或隐藏栏<br /><br />- 如果用户选择隐藏栏，默认情况下，该栏在应用程序中隐藏，但会继续自动显示在新打开的应用程序中 <br /><br /> 面向管理员： <br /><br />- 在应用程序首次打开时，通过策略设置自动显示或隐藏栏，并控制在用户选择隐藏栏后，该栏是否对新打开的应用程序自动保持隐藏状态|面向用户： <br /><br />- 从功能区上的“敏感度”按钮选择显示或隐藏栏<br /><br />- 当用户选择隐藏栏时，该栏在该应用程序中以及新打开的应用程序中均处于隐藏状态 <br /><br />面向管理员： <br /><br />- PowerShell setting to manage the bar |
|标签颜色： | 在 Azure 门户中配置 | Retained after label migration and configurable with [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Labels support different languages:| 在 Azure 门户中配置 | Configure by using Office 365 Security & Compliance PowerShell and the *LocaleSettings* parameter for [New-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) and [Set-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)|
|策略更新： | 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 24 小时一次 <br /><br />For the scanner: Every hour and when the service starts and the policy is older than one hour| 在 Office 应用程序打开时 <br /><br /> 在右键单击以分类和保护文件或文件夹时 <br /><br />在运行 PowerShell cmdlet 以实现标记和保护时<br /><br />每 4 小时一次 <br /><br />For the scanner: Every 4 hours|
|PDF 支持的格式：| 保护: <br /><br /> - PDF 加密的 ISO 标准（默认） <br /><br /> - .ppdf <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护| 保护: <br /><br /> - PDF 加密的 ISO 标准 <br /><br /> <br /><br /> 使用： <br /><br /> - PDF 加密的 ISO 标准 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保护|
|Generically protected files (.pfile) opened with the viewer:| File opens in the original app where it can then be viewed, modified, and saved without protection | File opens in the original app where it can then be viewed and modified, but not saved|
|支持的 cmdlet：| Cmdlets for labeling and cmdlets for protection-only | Cmdlets for labeling:<br /><br /> Set-AIPFileClassification and Set-AIPFileLabel don't support the *Owner* parameter <br /><br /> 此外，对于未应用标签的所有场景，都有一条“无适用标签”的注释 <br /><br /> Set-AIPFileClassification supports the *WhatIf* parameter, so it can be run in discovery mode <br /><br /> Set-AIPFileLabel 不支持 EnableTracking 参数 <br /><br /> Get-AIPFileStatus 不从其他租户返回标签信息，也不显示 RMSIssuedTime 参数<br /><br />In addition, the *LabelingMethod* parameter for Get-AIPFileStatus displays **Privileged** or **Standard** instead of **Manual** or **Automatic**. 有关详细信息，请参阅[联机文档](/powershell/module/azureinformationprotection/get-aipfilestatus)。|
|Office 中每个操作的对齐方式提示（如果已配置）： | Frequency: Per file <br /><br /> 降低敏感度级别 <br /><br /> 删除标签<br /><br /> 删除保护 | Frequency: Per session <br /><br /> 降低敏感度级别<br /><br /> 删除标签|
|删除已应用的标签操作： | 系统提示用户确认 <br /><br />下次 Office 应用程序打开文件时，不会自动应用默认标签或自动标签（如果已配置）  <br /><br />| 不提示用户确认<br /><br /> 下次 Office 应用程序打开文件时，自动应用默认标签或自动标签（如果已配置）|
|Automatic and recommended labels: | 在 Azure 门户中配置为[标签条件](../configure-policy-classification.md)，其中包含使用短语或正则表达式的内置信息类型和自定义条件 <br /><br />配置选项包括： <br /><br />- 唯一/非唯一计数 <br /><br /> - 最小计数| 在管理中心中配置，包含内置敏感信息类型和[自定义信息类型](https://docs.microsoft.com/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />配置选项包括：  <br /><br />- 仅唯一计数 <br /><br />- 最小和最大计数 <br /><br />- 信息类型支持 AND 和 OR <br /><br />- 关键字字典<br /><br />- 可自定义的可信度和字符接近度|
|Customizable policy tip for automatic and recommended labels: | “是” <br /><br />Use the Azure portal to replace the default message to users | 否 <br /><br /> Although the admin centers have an option to supply a customized policy tip, this option is not currently supported by the unified labeling client|
|Change the default protection behavior for file types: | You can use [registry edits](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) to override the defaults of native and generic protection | You can use [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) to change which file types get protected|

For a detailed comparison of behavior differences for specific protection settings, see [Comparing the behavior of protection settings for a label](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Features not planned to be in the Azure Information Protection unified labeling client

Although the Azure Information Protection unified labeling client is still under development, the following features and behavior differences from the classic client are not currently planned to be available in future releases for the unified labeling client: 

- Support Office apps for disconnected computers with manual policy file management

- Custom permissions as a separate option that users can select in Office apps: Word, Excel, and PowerPoint

- 从 Office 应用和文件资源浏览器中跟踪和撤销

- Azure 信息保护栏标题和工具提示

- Protection-only mode (no labels) using templates

- 将 PDF 文档作为 .ppdf 格式进行保护

- 在 Outlook 中显示“不可转发”按钮

- 演示策略

- 对删除保护的验证

- Confirmation prompt **Do you want to delete this label?** for users when you don't use the policy setting for justification

- 连接到 Rights Management 服务的单独 PowerShell cmdlet


### <a name="parent-labels-and-their-sublabels"></a>父标签及其子标签 

The Azure Information Protection client (classic) doesn't support configurations that specify a parent label that has sublabels. 这些配置包括指定默认标签和推荐分类或自动分类的标签。 如果某个标签具有子标签，可以指定其中一个子标签，但不能指定父标签。

对于奇偶校验，Azure 信息保护统一标签客户端也不支持应用具有子标签的父标签，即使可以在管理中心中选择这些标签，也无法应用。 在此方案中，Azure 信息保护统一标记客户端将不应用父标签。

## <a name="next-steps"></a>后续步骤

To install and configure the Azure Information Protection clients, use the following documentation:

- [Azure 信息保护客户端](AIP-client.md)

- [Azure 信息保护统一标记客户端](unifiedlabelingclient-version-release-history.md)

For more information about using the built-in labeling client for Office 365 apps, see [Sensitivity labels in Office apps](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps).
