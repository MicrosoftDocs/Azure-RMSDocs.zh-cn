---
title: Azure 信息保护的术语
description: 对 Microsoft Azure 信息保护相关的单词、短语或缩略词感到迷惑吗？ 在此处查找特定于 Azure 信息保护或具有特定含义（如果在此服务上下文中使用）的术语和缩写的定义。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 81595e38ed9dbaaf267ac86326ec0e2d8fd3e6b3
ms.sourcegitcommit: 1d2912b4f0f6e8d7596cbf31e2143a783158ab11
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2018
ms.locfileid: "53305533"
---
# <a name="terminology-for-azure-information-protection"></a>Azure 信息保护的术语

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

对 Microsoft Azure 信息保护相关的单词、短语或缩略词感到迷惑吗？ 在此处查找特定于 Azure 信息保护或具有特定含义（如果在此服务上下文中使用）的术语和缩写的定义。

|项|定义|
|--------|--------------|
|AADRM|Azure Rights Management 服务的 PowerShell 模块名称，派生自 Azure Rights Management 之前名为 (Windows) Azure Active Directory Rights Management 时的非正式缩写。|
|激活|启用 Azure 权限管理服务，使组织可以保护其文档和电子邮件。 此操作还会在 Exchange Online 和 SharePoint Online 中启用 IRM 功能。|
|Active Directory 权限管理服务|经常缩写为 AD RMS。<br /><br />一个 Windows Server 角色，它使用加密和策略来提供权限管理保护以帮助保护文档、文件和电子邮件。|
|AD RMS|请参阅 *Active Directory Rights Management 服务*。|
AzureInformationProtection|Azure 信息保护客户端的 PowerShell 模块名称。
|Azure 信息保护|一项基于云的服务，使用标签对文档和电子邮件进行分类和保护。 Azure 权限管理通过使用加密、标识和授权策略提供保护。|
Azure 信息保护客户端|Azure 信息保护客户端，便于用户、管理员和服务使用 Azure 信息保护策略中的标签和设置。|
|Azure 信息保护标签|此项将分类值应用于文档和电子邮件，并可以视需要保护这些内容。|
|Azure 信息保护策略|管理员定义的配置，便于客户端和服务使用 Azure 信息保护标签和策略设置。|
|Azure 信息保护扫描程序|在 Windows Server 上运行的一项服务，便于你发现、分类和保护本地文件夹、网络共享以及 SharePoint Server 网站和库中的文档。|
|Azure 信息保护查看器|在 Windows 计算机和移动设备上运行的应用，用于显示受保护文件。|
|Azure 权限管理|经常缩写为 Azure RMS。<br /><br />Azure 信息保护使用的一种 Azure 服务，它使用加密和策略来帮助保护文档、文件和电子邮件。  也称为 *Azure Rights Management 服务*。 之前的名称包括：<br /><br />- Windows Azure Active Directory Rights Management：常缩写为 Windows Azure AD Rights Management Service。<br /><br />- RMS Online：原始的建议名称，有时可能在错误消息和日志文件条目中看到。|
|Azure RMS|请参阅 *Azure Rights Management*。|
|默认模板|在你获取 Azure 信息保护订阅时自动为你创建的保护模板，便于你立即开始保护包含敏感信息的文档和电子邮件。|
|BYOK|请参阅 *自带密钥*。|
|自带密钥|经常缩写为 *BYOK*。<br /><br />想要为 Azure 信息保护生成和管理自己的租户密钥的组织选择的配置和拓扑选项。|
|内容密钥|启用 RMS 的应用程序为使用 Rights Management 保护的每个文档或电子邮件创建的唯一密钥，有助于遏制信息泄漏的风险。|
|使用|打开受 Rights Management 保护的文档或电子邮件，以读取或使用其中内容。 对于文档，使用内容包括编辑内容和向受保护文档添加新内容。 对于电子邮件，使用内容包括回复受保护邮件。|
|停用|禁用权限管理服务，使组织不再能够使用 Azure 信息保护。|
|部门模板|你创建的保护模板，配置为向选定用户（而不是组织中的所有用户）显示。 亦称为“范围内模板”。|
|启用的应用程序|原本就支持权限管理的应用程序，包括 Word 和 Excel 等 Office 应用程序。 独立软件供应商 (ISV) 和开发商也可以编写本身支持 Rights Management 的应用程序。|
|企业权限管理|一个符合行业标准的通用术语，通常用于描述可通过加密和策略授权工具组合来帮助组织保护敏感信息或重要信息的产品和解决方案。 Azure 信息保护就是企业权限管理 (ERM) 解决方案的例子。|
|ERM|请参阅 *企业权限管理*。|
|一般性保护|一种保护级别，它可以加密任何文件类型，并阻止未经授权的人员打开该文件。 该文件在打开后将处于未加密状态，并可以在本身不支持 Rights Management 的应用程序中使用。|
|HYOK|请参阅*自留密钥*。|
|自留密钥|经常缩写为 *HYOK*。<br /><br />一个配置和拓扑选项，面向通常出于法规或合规性方面的原因而想在本地生成并存储自己的密钥的组织。|
|密钥对象|在租户密钥的上下文中，包含 Azure 权限管理服务进行加密操作时所需的元数据的一个实体。|
|label|请参阅“Azure 信息保护标签”。|
|信息保护|有时缩写为 *IP*。<br /><br />一个符合行业标准的通用术语，表示保护数据和文件以防止未经授权的访问，即使在通过电子邮件或文档共享使这些数据和文件脱离组织边界后，也能提供这种保护。 Microsoft Azure 信息保护就是信息保护 (IP) 解决方案的一个例子。|
|信息权限管理|经常缩写为 *IRM*。<br /><br />一个用于 Exchange Server、Word 和 SharePoint Online 等 Office 服务的术语，说明是否支持 Microsoft Rights Management 服务。|
|IRM|请参阅 *信息权限管理*。|
|Office 消息加密|经常缩写为 OME。<br /><br />新的 Office 365 消息加密功能与 Azure Rights Management 服务本机集成，可为内部和外部用户提供相同的电子邮件保护、自动刷新模板，并支持“创建自己的密钥 (BYOK)”方案。 以前的 OME 实现仅面向外部收件人，需要邮件流规则，并且不支持 BYOK。|
|MSDRM|有时在 RMS 客户端 1.0（现已被新的客户端 MSIPC 取代）的参考信息中出现。 这个旧版客户端支持使用 RMS SDK 1.0 开发的应用程序，并支持 Office 2010 和 Office 2007、Exchange 2010 和 Exchange 2013 以及 SharePoint 2010 和 SharePoint 2007。|
|MSIPC|有时在 RMS 客户端 2.0（取代了旧版 RMS 客户端 MSDRM）的参考信息中出现。 这个较新版客户端支持使用 RMS SDK 2.0 开发的应用程序，并支持 Office 2016 和 Office 2013、SharePoint 2013 和 RMS 共享应用程序以及 Azure 信息保护客户端。|
|本机保护|所有启用的应用程序中提供的一种保护级别，可阻止未经授权的人员打开某个文件，并且还可以强制实施更严格的策略，例如只读、不允许打印。 此外，这种保护将一直伴随文件，即使将该文件转发给他人或将其保存在他人可以访问的公共位置。|
|。pfile|在受 Rights Management 服务的一般性保护的所有文件后面附加的文件扩展名。|
|权限级别|即对使用权限进行逻辑分组，使得最终用户和管理员更容易选择基于角色的配置选项。 例如，审阅者和合著者。|
|保护|使用加密、标识和访问控制策略，将 Rights Management 控件添加到文件或电子邮件，以帮助保护数据。|
|保护模板|亦称为“权限策略模板”、“Rights Management 模板”和“RMS 模板”。<br /><br />一组由管理员管理的保护设置，包含授权用户的已定义使用权限，以及有关到期和脱机访问的访问控制。 |
|publish|用于保护某个文件，以防他人在未经授权的情况下访问和使用该文件。 还用作与保护模板和 Azure 信息保护策略结合使用的术语，以便这些项可供客户端和服务使用。|
|权限管理连接器|可为 Exchange Server 和 SharePoint 等本地服务部署的出站代理中继，用于通过 Azure Rights Management 服务保护数据。|
|权限管理颁发者|保护文档或电子邮件的帐户。|
|权限管理所有者|此帐户通过自动授予“权限管理完全控制”使用权保留受保护文档或电子邮件的完全控制权，并且不受任何到期日期或离线设置限制。|
|权限管理服务|同时适用于 Rights Management (Azure Rights Management) 云版本和 Rights Management (AD RMS) 本地版本的通用术语。|
|权限管理共享应用程序|适用于 Windows 和移动设备的可选应用程序，用于支持安全共享本地文件以及通过电子邮件发送的文件，现被 Azure 信息保护客户端取代。|
|RMS|请参阅 *Rights Management 服务*。|
|RMS 连接器|请参阅 *Rights Management 连接器*。|
|个人 RMS|一个免费订阅，当用户的组织未订阅 Office 365 或 Azure Active Directory 时，用户可通过此订阅来使用 Rights Management。|
|RMS 共享应用程序|请参阅 *Rights Management 共享应用程序*。|
|RMS 模板|请参阅“保护模板”。|
|仅保护模式|不存在要应用标签的 Azure 信息保护策略时，Azure 信息保护客户端的一种操作模式。 在此模式下，不显示分类标签，但用户仍可以应用 Rights Management 保护。|
|扫描程序|请参阅“Azure 信息保护扫描程序”。|
|超级用户|高度受信任的管理员组，可以解密及访问组织使用 Rights Management 服务保护的文件。 通常，进行合法电子发现时需要此访问级别，并且审核团队也需要此访问级别。|
|租户密钥|也称为服务器许可方证书 (SLC) 密钥。<br /><br />组织独有的密钥，可为链接到此租户密钥的所有 Rights Management 加密功能提供终极保护。|
|取消保护|从文件或电子邮件中删除保护控件，这些控件使用加密、标识、使用权限和访问控制策略帮助保护数据。|
|使用许可证|向打开受 Rights Management 服务保护的文件或电子邮件的用户授予的每文档证书。 该证书包含此用户对文件或电子邮件消息所具有的权限、用于加密内容的加密密钥，以及文档策略中定义的其他访问限制。|
