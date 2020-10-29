---
title: Azure 信息保护要求 - AIP
description: 确定在组织中部署 Azure 信息保护所需满足的先决条件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: edf42dc9d41aebe8f4cb21bbca624bd671b5eba4
ms.sourcegitcommit: 22ac808221a66141406589a9d8d619bfee056cf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92429195"
---
# <a name="azure-information-protection-requirements"></a>Azure 信息保护要求

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

在部署 Azure 信息保护之前，请确保系统满足以下先决条件：

- [Azure 信息保护订阅](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [客户端设备](#client-devices)
- [应用程序](#applications)
- [防火墙和网络基础结构](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Azure 信息保护订阅

必须有以下计划之一，具体视你要使用的 Azure 信息保护功能而定：

- [Azure 信息保护计划](https://azure.microsoft.com/pricing/details/information-protection/)。 使用 Azure 信息保护扫描程序或客户端（经典或统一标记）进行分类、标记和保护所必需

- [包括 Azure 信息保护的 Office 365 计划](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。 仅进行保护所必需。

若要验证订阅是否包括要使用的 Azure 信息保护功能，请查看 [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)中的功能列表。

如果你对许可有疑问，请仔细阅读许可的[常见问答解答](https://azure.microsoft.com/pricing/details/information-protection#faq)。

> [!TIP]
> 要确定 Microsoft 365 计划或 Exchange Online 独立计划是否支持 [Office 365 邮件加密的新功能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)，以便向个人电子邮件地址发送受保护的电子邮件？ 例如 Gmail、Yahoo 和 Microsoft。 请参阅以下资源：
>
> - [Exchange Online 服务说明](/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description)
>
> - [Office 365 教育版](/office365/servicedescriptions/office-365-platform-service-description/office-365-education)
>
> - [Office 365 美国政府版](/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/office-365-us-government)

如果你对订阅或许可有任何疑问，请勿在此页发布它们。 相反，请查看许可的[常见问答解答](https://azure.microsoft.com/pricing/details/information-protection#faq)中是否有答案。 如果问题没有得到解答，请与 Microsoft 客户经理或 [Microsoft 支持部门](information-support.md#to-contact-microsoft-support)联系。

## <a name="azure-active-directory"></a>Azure Active Directory

为了支持 Azure 信息保护的身份验证和授权，必须有 Azure Active Directory (AD)。 若要使用本地目录 (AD DS) 中的用户帐户，还必须配置目录集成。

- Azure 信息保护支持单一登录 (SSO)，这样就不会反复提示用户输入凭据。 如果使用其他供应商解决方案进行联合身份验证，请与相应供应商确认如何为它配置 Azure AD。 WS-Trust 是这些解决方案支持单一登录所需满足的常见要求。 

- 多重身份验证 (MFA) 可以与 Azure 信息保护配合使用，前提是你拥有所需的客户端软件，并正确配置了支持 MFA 的基础结构。

预览版支持按条件访问受 Azure 信息保护进行保护的文档。 有关详情，请参阅：[我看到 Azure 信息保护被列为可用于条件访问的云应用 - 工作原理是什么？](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

对于特定方案（如当使用 Office 2010、基于证书的身份验证或多重身份验证时，或当 UPN 值与用户电子邮件地址不一致时），还需要满足额外的先决条件。 有关详细信息，请参阅 [Azure 信息保护的额外 Azure AD 要求](requirements-azure-ad.md)。

有关详细信息，请参阅：

- [什么是 Azure AD Directory？](/azure/active-directory/fundamentals/active-directory-whatis)
- [将本地 Active Directory 域与 Azure Active Directory 集成](/azure/architecture/reference-architectures/identity/azure-ad)。

## <a name="client-devices"></a>客户端设备

用户计算机或移动设备必须在支持 Azure 信息保护的操作系统上运行。

- [客户端设备支持的操作系统](#supported-operating-systems-for-client-devices)
- [虚拟机](#virtual-machines)
- [服务器支持](#server-support)
- [每个客户端的额外要求](#additional-requirements-per-client)

### <a name="supported-operating-systems-for-client-devices"></a>客户端设备支持的操作系统

以下操作系统既支持 Azure 信息保护统一标记客户端，也支持 Azure 信息保护客户端： 

- Windows 10（x86 和 x64）。 Windows 10 RS4 内部版本及更高版本中不支持手写。
 
- **Windows 8.1** (x86, x64)

- **Windows 8** (x86, x64)

- **Windows Server 2019**

- **Windows Server 2016**

- Windows Server 2012 R2 和 Windows Server 2012

[两个客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)都可便于用户对文档和电子邮件进行分类和标记。

若要详细了解旧版 Windows 中的支持，请联系 Microsoft 帐户或支持代表。

> [!NOTE]
> 如果 Azure 信息保护客户端使用 Azure Rights Management 服务来保护数据，那么数据可以被支持 Azure Rights Management 服务的[相同设备](#client-devices)使用。
>
### <a name="arm64"></a>ARM64 

暂不支持 ARM64。 

### <a name="virtual-machines"></a>虚拟机

如果使用的是虚拟机，请检查虚拟桌面解决方案的软件供应商是否作为运行 Azure 信息保护统一标记客户端或 Azure 信息保护客户端所需的额外配置。 

例如，对于 Citrix 解决方案，你可能需要对 Office、Azure 信息保护统一标记客户端或 Azure 信息保护客户端[禁用 Citrix 应用程序编程接口 (API) 挂钩](https://support.citrix.com/article/CTX107825)。 

这些应用程序分别使用以下文件：winword.exe、excel.exe、outlook.exe、powerpnt.exe、msip.app.exe、msip.viewer.exe

### <a name="server-support"></a>服务器支持

对于上面列出的每个服务器版本，Azure 信息保护客户端都可以与远程桌面服务配合使用。 

如果在将 Azure 信息保护客户端与远程桌面服务配合使用时删除了用户配置文件，请勿删除 %Appdata%\Microsoft\Protect 文件夹。

此外，不支持服务器核心和 Nano Server。

### <a name="additional-requirements-per-client"></a>每个客户端的额外要求

每个 Azure 信息保护客户端都有额外的先决条件。 有关详细信息，请参阅：

- [Azure 信息保护统一标记客户端先决条件](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- [Azure 信息保护客户端先决条件](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>应用程序

Azure 信息保护客户端可使用以下任意 Office 版本中的 Microsoft Word、Excel、PowerPoint 和 Outlook 对文档和电子邮件进行标记和保护：

- Microsoft 365 商业应用版或 Microsoft 365 商业高级版中的 Office 应用最低版本 1805（内部版本 9330.2078）。 

    仅当用户分配有 Azure Rights Management（亦称为“Microsoft 365 Azure 信息保护”）许可证时，才支持此版本。

- Microsoft 365 企业应用版

- Office 专业增强版 2019

- Office 专业增强版 2016

- Office 专业增强版 2013 Service Pack 1

- Office 专业增强版 2010 Service Pack 2

Office 的其他版本无法通过使用 Rights Management 服务保护文档和电子邮件。 对于这些版本，只支持使用 Azure 信息保护进行分类，不会向用户显示应用保护的标签。 

这些标签本来会显示在 Azure 信息保护栏或统一标记客户端中的 Office 功能区上（通过经典客户端中的“保护”按钮，或统一标记客户端中的“敏感度”按钮）。 

有关详细信息，请参阅[支持 Azure Rights Management 数据保护的应用程序](requirements-applications.md)。

### <a name="office-features-and-capabilities-not-supported"></a>不支持的 Office 特性和功能

- Azure 信息保护客户端（包括经典和统一标记）都不支持在同一台计算机上使用 Office 的多个版本，也不支持在 Office 中切换用户帐户。

- Office [邮件合并](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705)功能无法与 Azure 信息保护功能配合使用。

## <a name="firewalls-and-network-infrastructure"></a>防火墙和网络基础结构

如果你有防火墙或配置为允许特定连接的类似中间网络设备，请参阅下面这篇 Office 文章中列出的网络连接要求：[Microsoft 365 Common 和 Office Online ](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online)。

Azure 信息保护有以下额外要求：

- 统一标记客户端。 若要下载标签和标签策略，请允许通过 HTTPS 使用以下 URL：*.protection.outlook.com

- Web 代理。 如果使用要求进行身份验证的 Web 代理，必须将代理配置为将集成 Windows 身份验证与用户的 Active Directory 登录凭据配合使用。

    要在使用代理获取令牌时支持 Proxy.pac 文件，请添加以下新的注册表项：

    - 路径：`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIP\`
    - 密钥：`UseDefaultCredentialsInProxy`
    - 类型：`DWORD`
    - 值：`1`
    
- TLS 客户端到服务连接。 不要终止与 aadrm.com URL 的任何 TLS 客户端到服务连接（例如，为了执行数据包级别检查）。 那样做会打破 RMS 客户端用于 Microsoft 托管 CA 的证书固定，导致无法确保其与 Azure Rights Management 服务的通信安全。
     
    若要确定客户端连接是否在到达 Azure Rights Management 服务之前就终止，请使用以下 PowerShell 命令：

    ```PowerShell
    $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
    $request.GetResponse()
    $request.ServicePoint.Certificate.Issuer
    ```

    结果应显示发证 CA 来自 Microsoft CA（例如：`CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`）。 
    
    如果发现发证 CA 名称不是来自 Microsoft，那么很可能安全的客户端到服务连接要被终止，需要在防火墙上重新配置。

- TLS 版本 1.2 或更高版本（仅限统一标记客户端）。 统一标记客户端需要 1.2 或更高版本的 TLS，以确保使用加密安全协议并遵循 Microsoft 安全准则。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS 和 Azure RMS 共存

仅在用于 [HYOK（自留密钥）保护](configure-adrms-restrictions.md)（含 Azure 信息保护）的 AD RMS 中支持在同一组织中并行使用 AD RMS 和 Azure RMS，以保护同一组织中的同一用户的内容。

[迁移](migrate-from-ad-rms-to-azure-rms.md)期间不支持此方案。
支持的迁移路径包括：

* [从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)

* [从 Azure 信息保护迁移到 AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> 如果你部署 Azure 信息保护，然后决定不再想要使用此云服务，请参阅[解除 Azure 信息保护授权和停用 Azure 信息保护](decommission-deactivate.md)。

对于其他非迁移方案，即两个服务在同一组织中都是活动的，必须对两个服务进行配置，以便只有一个服务允许任何给定的用户保护内容。 按照以下方式配置此类方案：

* 对[从 AD RMS 迁移到 Azure RMS](migrate-from-ad-rms-to-azure-rms.md) 使用重定向

* 如果两个服务必须同时针对不同的用户处于活动状态，请使用服务端配置来强制实现排他性。  使用云服务中的 Azure RMS 加入控件和发布 URL 上的 ACL 为 AD RMS 设置只读模式。

### <a name="service-tags"></a>服务标记

请务必允许访问以下服务标记的所有端口：

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor.Frontend**

Azure 信息保护服务还依赖于两个特定的 IP 地址：
 - 13.107.6.181 
 - 13.107.9.181
 - 端口 443（对于 HTTPS 流量）

请务必创建规则来允许对这些特定 IP 地址进行出站访问，以及通过此端口进行访问。

## <a name="supported-on-premises-servers-for-azure-rights-management-data-protection"></a>支持 Azure Rights Management 数据保护的本地服务器

当你使用 Azure Rights Management 连接器时，以下本地服务器可以与 Azure 信息保护配合使用。

此连接器充当通信接口，并在本地服务器和 Azure Rights Management 服务之间中继，Azure 信息保护使用此服务来保护 Office 文档和电子邮件。 

若要使用该连接器，必须配置 Active Directory 林和 Azure Active Directory 之间的目录同步。

支持的服务器包括：

|服务器类型  |支持的版本  |
|---------|---------|
|**Exchange Server**     | - Exchange Server 2016 </br>- Exchange Server 2013 </br>- Exchange Server 2010       |
|**Office SharePoint Server**     |- Office SharePoint Server 2016 </br>- Office SharePoint Server 2013 </br>- Office SharePoint Server 2010         |
|**运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器**     |- Windows Server 2016 </br>- Windows Server 2012 R2 </br>- Windows Server 2012       |
| | |

有关详细信息，请参阅[部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

## <a name="supported-operating-systems-for-azure-rights-management"></a>支持 Azure Rights Management 的操作系统

以下操作系统支持为 AIP 提供数据保护的 Azure Rights Management 服务：

|OS  |支持的版本  |
|---------|---------|
|**Windows 计算机**     |- Windows 7（x86 和 x64） </br>- Windows 8（x86、x64） </br>- Windows 8.1（x86、x64） </br>- Windows 10（x86、x64）       | 
|**macOS**     |   最低版本为 macOS 10.8 (Mountain Lion)      |
|Android 手机和平板电脑     | 最低版本为 Android 6.0        |
|**iPhone 和 iPad**     | 最低版本为 iOS 11.0        |
|Windows 手机和平板电脑 | Windows 10 移动版|
| | |



## <a name="next-steps"></a>后续步骤

在审阅了所有的 AIP 要求并确认系统符合要求后，继续阅读[准备用户和组以供 Azure 信息保护使用](prepare.md)。