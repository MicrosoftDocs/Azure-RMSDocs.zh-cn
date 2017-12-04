---
title: "Azure 信息保护的要求"
description: "确定为组织部署 Azure 信息保护的必备条件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/29/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e6fa7c2912f2598f8eb2ad31d237caab80fd0273
ms.sourcegitcommit: 8d47080abab0be9b16672fee0d885ebe00f7f5f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="requirements-for-azure-information-protection"></a>Azure 信息保护的要求

>*适用于：Azure 信息保护、Office 365*

为组织部署 Azure 信息保护之前，请确保具备以下必备条件。 

## <a name="subscription-for-azure-information-protection"></a>Azure 信息保护订阅

对于分类、设置标签和保护，必须具有 [Azure 信息保护计划](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)。 

对于仅保护，必须具有[包括 Rights Management 的 Office 365计划](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。

若要确保组织的订阅具有想要使用的 Azure 信息保护功能，请查看 Azure 信息保护网站上的[订阅信息](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)和[功能列表](https://www.microsoft.com/cloud-platform/azure-information-protection-features)。

> [!NOTE]
> 如果对订阅或许可有任何疑问，请勿将问题发布在此页面上，而是联系你的 Microsoft 客户经理或 [Microsoft 支持部门](information-support.md#to-contact-microsoft-support)。

## <a name="azure-active-directory"></a>Azure Active Directory

你的组织必须具有 Azure Active Directory (Azure AD) 才能支持用户身份验证和 Azure 信息保护身份授权。 此外，如果你希望使用本地目录 (AD DS) 中的用户帐户，则还必须配置目录集成。

具有所需客户端软件并正确配置 MFA 支持基础结构后，Azure 信息保护将支持多重身份验证 (MFA)。

预览版支持按条件访问受 Azure 信息保护进行保护的文档。 有关详细信息，请参阅以下常见问题解答：[我看到 Azure 信息保护被列为可用于条件访问的云应用 - 工作原理是什么？](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

有关身份验证要求的详细信息，请参阅 [Azure 信息保护的 Azure Active Directory 要求](requirements-azure-ad.md)。 

有关对用户和组帐户进行授权的要求的详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](../plan-design/prepare.md)。

## <a name="client-devices"></a>客户端设备

用户必须拥有运行支持 Azure 信息保护的操作系统的客户端设备（计算机或移动设备）。

以下设备支持 Azure 信息保护客户端，它可使用户分类并标记其文档和电子邮件：

- Windows 10（x86、x64）

- Windows 8.1（x86、x64）

- Windows 8（x86、x64）

- Windows 7 Service Pack 1（x86、x64）

- Windows Server 2016 

- Windows Server 2012 R2 和 Windows Server 2012

- Windows Server 2008 R2 

对于列出的服务器版本，远程桌面服务支持用于 Azure 信息保护客户端。 将 Azure 信息保护客户端与远程桌面服务结合使用时，如果删除用户配置文件，请勿删除“%Appdata%\Microsoft\Protect”文件夹。

当 Azure 信息保护客户端通过使用 Azure 权限管理服务保护数据时，支持 Azure 权限管理服务的[同一设备](requirements-client-devices.md)可以使用此数据。

## <a name="applications"></a>应用程序

Azure 信息保护客户端可使用以下 Office 版本中的 Word、Excel、PowerPoint 和 Outlook 等 Office 应用程序对文档和电子邮件设置标签和进行保护：

- 含 2016 应用或 2013 应用的 Office 365 ProPlus（即点即用或基于 Windows Installer 的安装）

- Office Professional Plus 2016

- Office Professional Plus 2013 Service Pack 1

- Office Professional Plus 2010 Service Pack 2

Office 的其他版本无法通过使用 Rights Management 服务保护文档和电子邮件。 对于这些版本，仅支持 Azure 信息保护分类。 应用保护的标签不会显示在 Azure 信息保护栏上。 

有关支持数据保护服务的 Office 版本的信息，请参阅[支持 Azure Rights Management 数据保护的应用程序](requirements-applications.md)。

## <a name="firewalls-and-network-infrastructure"></a>防火墙和网络基础结构

如果你有配置为允许特定连接的防火墙或类似中介网络设备，请参阅以下 Office 文章的 [Office 365 门户和共享](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity)部分中有关 Azure 权限管理 (RMS) 的信息：[Office 365 URL 和 IP 地址范围](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。

使用此 Office 文章中的说明通过订阅 RSS 源来跟踪本信息的最新更改。

除了 Office 文章中特定于 Azure 信息保护的信息外：

- 允许 TCP 443 上的 HTTPS 流量流入 api.informationprotection.azure.com。

- 不要终止 TLS 客户端到服务连接（例如，为了执行数据包级别检查）。 这样做会中断 RMS 客户端用于 Microsoft 托管的 CA 以帮助确保其与 Azure RMS 的通信安全的证书锁定。

- 如果使用要求进行身份验证的 Web 代理，必须将其配置为将集成 Windows 身份验证与用户的 Active Directory 登录凭据配合使用。


### <a name="on-premises-servers"></a>本地服务器

如果想要将 Azure 信息保护中的 Azure Rights Management 服务与本地服务器配合使用，则支持以下产品：

- Exchange Server

- SharePoint Server

- 支持文件分类基础结构的 Windows Server 文件服务器

有关此方案的其他要求的信息，请参阅[支持 Azure Rights Management 数据保护的本地服务器](requirements-servers.md)。

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>AD RMS 和 Azure RMS 共存

不支持以下部署方案，除非将 AD RMS 保护与 Azure 信息保护配合使用（“自留密钥”或 HYOK 配置）：

- 在同一个组织中并行运行 AD RMS 和 Azure RMS，除非是在迁移过程中，如[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)所述。

支持[从 AD RMS 到 Azure 信息保护](http://technet.microsoft.com/library/Dn858447.aspx)和[从 Azure 信息保护到 AD RMS](/powershell/module/aadrm/Set-AadrmMigrationUrl) 的迁移路径。 如果你部署 Azure 信息保护，然后决定不再想要使用此云服务，请参阅[解除 Azure 信息保护授权和停用 Azure 信息保护](../deploy-use/decommission-deactivate.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


