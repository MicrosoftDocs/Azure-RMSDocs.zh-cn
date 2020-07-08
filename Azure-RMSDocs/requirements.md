---
title: Azure 信息保护要求 - AIP
description: 确定在组织中部署 Azure 信息保护所需的先决条件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/25/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bcb3006bdd7575385d37be066b627ef49f770c70
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047705"
---
# <a name="azure-information-protection-requirements"></a>Azure 信息保护要求

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

在部署 Azure 信息保护之前，请确保你的系统满足以下先决条件：

- [Azure 信息保护订阅](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [客户端设备](#client-devices)
- [应用程序](#applications)
- [防火墙和网络基础结构](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Azure 信息保护订阅

根据要使用的 Azure 信息保护功能，必须执行以下操作之一：

- ** [Azure 信息保护计划](https://azure.microsoft.com/pricing/details/information-protection/)**。 需要使用 Azure 信息保护扫描程序或客户端进行分类、标记和保护（经典或统一标签）

- **[包含 Azure 信息保护的 Office 365 计划](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)**。 仅用于保护。

若要验证你的订阅是否包含你要使用的 Azure 信息保护功能，请查看[Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)中的功能列表。

如果你对许可有疑问，请仔细阅读许可的[常见问答解答](https://azure.microsoft.com/pricing/details/information-protection#faq)。

> [!TIP]
> 希望查看 Office 365 计划或 Exchange Online 独立计划是否支持 [Office 365 邮件加密的新增功能](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801)，以向个人电子邮件地址发送受保护的电子邮件？ 例如 Gmail、Yahoo 和 Microsoft。 请参阅以下资源：
>
> - [Exchange Online 服务说明](https://technet.microsoft.com/library/exchange-online-service-description.aspx)
>
> - [Office 365 教育版](https://technet.microsoft.com/library/mt844095.aspx)
>
> - [Office 365 美国政府版](https://technet.microsoft.com/library/mt774581.aspx)

如果你对订阅或许可有任何疑问，请勿在此页发布它们。 相反，请查看许可的[常见问答解答](https://azure.microsoft.com/pricing/details/information-protection#faq)中是否有答案。 如果问题没有得到解答，请与 Microsoft 客户经理或 [Microsoft 支持部门](information-support.md#to-contact-microsoft-support)联系。

## <a name="azure-active-directory"></a>Azure Active Directory

若要支持 Azure 信息保护的身份验证和授权，必须有 Azure Active Directory （AD）。 若要使用本地控制器（AD DS）中的用户帐户，还必须配置目录集成。

- Azure 信息保护支持**单一登录（SSO）** ，以便不会重复提示用户输入其凭据。 如果使用其他供应商解决方案进行联合身份验证，请咨询该供应商，了解如何配置它以进行 Azure AD。 WS-Trust 是这些解决方案支持单一登录所需满足的常见要求。 

- 如果你具有所需的客户端软件并正确配置了 MFA 支持的基础结构，则 Azure 信息保护支持**多重身份验证（MFA）** 。

预览版支持按条件访问受 Azure 信息保护进行保护的文档。 有关更多详细信息，请参阅： [Azure 信息保护被列为可用于条件访问的云应用—这是如何工作的？](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

有关详细信息，请参阅：

- [Azure 信息保护的 Azure Active Directory 要求](requirements-azure-ad.md)

- [为 Azure 信息保护准备用户和组](prepare.md)

## <a name="client-devices"></a>客户端设备

用户计算机或移动设备必须在支持 Azure 信息保护的操作系统上运行。

### <a name="supported-operating-systems-for-client-devices"></a>客户端设备支持的操作系统

以下操作系统支持 Azure 信息保护统一标签和 Azure 信息保护客户端： 

- **Windows 10** （x86、x64）。 Windows 10 RS4 build 和更高版本不支持手写。
 
- **Windows 8.1** （x86、x64）

- **Windows 8** (x86, x64)

- **Windows Server 2019**

- **Windows Server 2016**

- **Windows server 2012 R2**和**windows server 2012**

[这两个客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)允许用户对其文档和电子邮件进行分类和标记。

有关更早版本的 Windows 中的支持的详细信息，请联系 Microsoft 帐户或支持代表。

> [!NOTE]
> 当 Azure 信息保护客户端使用 Azure Rights Management 服务保护数据时，数据可以由支持 Azure Rights Management 服务的[同一设备](requirements-client-devices.md)使用。
>

### <a name="virtual-machines"></a>虚拟机
如果使用的是虚拟机，请检查虚拟桌面解决方案的软件供应商是否为运行 Azure 信息保护统一标签或 Azure 信息保护客户端所需的其他配置。 

例如，对于 Citrix 解决方案，你可能需要禁用适用于 Office、Azure 信息保护统一标签客户端或 Azure 信息保护客户端的[Citrix 应用程序编程接口（API）挂钩](https://support.citrix.com/article/CTX107825)。 

这些应用程序分别使用以下文件： **winword.exe**、 **excel.exe**、 **outlook.exe**、 **powerpnt.exe**、 **msip.app.exe**、 **msip.viewer.exe**

### <a name="server-support"></a>服务器支持

对于上面列出的每个服务器版本，远程桌面服务支持 Azure 信息保护客户端。 

如果在远程桌面服务使用 Azure 信息保护客户端时删除用户配置文件，请勿删除 **%Appdata%\Microsoft\Protect**文件夹。

此外，不支持服务器核心和 Nano Server。

### <a name="additional-requirements-per-client"></a>每个客户端的其他要求

每个 Azure 信息保护客户端都具有额外的先决条件。 有关详细信息，请参阅：

- [Azure 信息保护统一标签客户端先决条件](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- [Azure 信息保护客户端先决条件](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>应用程序

Azure 信息保护客户端可以使用 Microsoft **Word**、 **Excel**、 **PowerPoint**和**Outlook**的任何以下 Office 版本来标记并保护文档和电子邮件：

- **Office 应用最小版本 1805**，从 Office 365 Business 或 Microsoft 365 商业版生成9330.2078。 

    仅当为用户分配了 Azure Rights Management 许可证（也称为 Azure 信息保护 for Office 365）时，才支持此版本。

- **Office 365 ProPlus**

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **带有 Service Pack 1 的 Office Professional Plus 2013**

- **带有 Service Pack 2 的 Office Professional Plus 2010**

Office 的其他版本无法通过使用 Rights Management 服务保护文档和电子邮件。 对于这些版本，仅支持 Azure 信息保护，而不会为用户显示应用保护的标签。 

这些标签会在 Azure 信息保护栏上或在 Office 功能区的统一标签客户端中显示（通过经典客户端中的 "**保护**" 按钮或统一标签客户端中的 "**敏感度**" 按钮）。 

有关更多详细信息，请参阅[支持 Azure Rights Management 数据保护的应用程序](requirements-applications.md)。

### <a name="office-features-and-capabilities-not-supported"></a>不支持的 Office 功能

- Azure 信息保护客户端（包括经典标签和统一标签）在同一台计算机上不支持多个 Office 版本，或在 Office 中切换用户帐户。

- Azure 信息保护功能不支持 Office[邮件合并](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705)功能。

## <a name="firewalls-and-network-infrastructure"></a>防火墙和网络基础结构

如果你具有配置为允许特定连接的防火墙或类似介入的网络设备，则此 Office 文章中列出了网络连接要求： [office 365 url 和 IP 地址范围 > Microsoft 365 Common And Office Online](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online)。

Azure 信息保护具有以下附加要求：

- **统一标签客户端**。 若要下载标签和标签策略，允许通过 HTTPS 上的以下 URL： ***. protection.outlook.com**

- **Web 代理**。 如果你使用需要身份验证的 web 代理，则必须将代理配置为将集成 Windows 身份验证与用户的 Active Directory 登录凭据一起使用。

    
- **TLS 客户端到服务连接**。 请勿终止任何 TLS 客户端到服务连接（例如，为了执行数据包级别检查）到**Aadrm.com** URL。 那样做会打破 RMS 客户端用于 Microsoft 托管 CA 的证书固定，导致无法确保其与 Azure Rights Management 服务的通信安全。
     
    若要确定客户端连接在到达 Azure Rights Management 服务之前是否终止，请使用以下 PowerShell 命令：

    ```ps
    $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
    $request.GetResponse()
    $request.ServicePoint.Certificate.Issuer
    ```

    结果应显示发证 CA 来自 Microsoft CA，例如： `CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US` 。 
    
    如果你看到的颁发 CA 名称不是 Microsoft，则很可能是你安全的客户端到服务连接被终止，需要在防火墙上重新配置。

- **TLS 版本1.2 或更高版本**（仅限统一标签客户端）。 统一标签客户端需要1.2 或更高版本的 TLS 版本，以确保使用加密的安全协议，并与 Microsoft 安全指南保持一致。
    
### <a name="on-premises-servers"></a>本地服务器

Azure 信息保护中的 Azure Rights Management 服务支持以下本地服务器：

- **Exchange Server**

- **SharePoint Server**

- 支持文件分类基础结构的**Windows Server 文件服务器**

有关此方案的其他要求的信息，请参阅[支持 Azure Rights Management 数据保护的本地服务器](requirements-servers.md)。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS 和 Azure RMS 共存

在同一个组织中并行使用 AD RMS 和 Azure RMS，以保护同一组织中的同一用户的内容，**仅**支持通过 Azure 信息保护进行[HYOK （拥有自己的密钥）保护](configure-adrms-restrictions.md)的 AD RMS。

[迁移](migrate-from-ad-rms-to-azure-rms.md)期间*不*支持此方案。
支持的迁移路径包括：

* [从 AD RMS 到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)

* [从 Azure 信息保护到 AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> 如果你部署 Azure 信息保护，然后决定不再想要使用此云服务，请参阅[解除 Azure 信息保护授权和停用 Azure 信息保护](decommission-deactivate.md)。

对于其他非迁移方案，如果这两个服务在同一组织中处于活动状态，则必须对这两个服务进行配置，使任何给定用户仅允许任何给定用户保护内容。 可以将其配置如下：

* 使用重定向来[Azure RMS 迁移 AD RMS](migrate-from-ad-rms-to-azure-rms.md)

* 如果两个服务必须同时针对不同用户处于活动状态，请使用服务端配置来强制实施独占性。  使用云服务中的 Azure RMS 载入控件，并使用发布 URL 上的 ACL 为 AD RMS 设置**只读**模式。

### <a name="service-tags"></a>服务标记

请确保允许访问以下服务标记的所有端口：

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor**

Azure 信息保护服务还依赖于两个特定的 IP 地址：
 - **13.107.6.181** 
 - **13.107.9.181**

请确保创建规则以允许对这些特定 IP 地址进行出站访问。 
