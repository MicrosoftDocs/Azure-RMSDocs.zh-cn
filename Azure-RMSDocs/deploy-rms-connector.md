---
title: 部署 Rights Management 连接器 - AIP
description: 有关部署 RMS 连接器的说明。该连接器提供数据保护服务，包括保护使用 Exchange Server、SharePoint Server 或 Windows Server 和文件分类基础结构 (FCI) 的现有本地部署。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/10/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a495ea2ca1cc08da081c10496c8e2b51f7718706
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382524"
---
# <a name="deploying-the-azure-rights-management-connector"></a>部署 Azure Rights Management 连接器

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、2016、windows Server 2012 R2、windows server 2012 *
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

利用此信息了解 Azure 权限管理连接器，并了解如何为组织成功部署该连接器。 此连接器为使用 Microsoft **Exchange Server**、 **SharePoint Server** 或文件服务器（运行 Windows Server 和 **文件分类基础结构** (FCI) ）的现有本地部署提供数据保护。


## <a name="overview-of-the-microsoft-rights-management-connector"></a>Microsoft 权限管理连接器概述

借助 Microsoft Rights Management (RMS) 连接器，你可以迅速让现有本地服务器将信息权限管理 (IRM) 功能用于基于云的 Microsoft Rights Management 服务 (Azure RMS)。 使用此功能，IT 部门和用户能够轻松地保护组织内部和外部的文档和图片，既无需安装其他基础结构，也无需建立与其他组织的信任关系。 

RMS 连接器是一项小型服务，可在运行 Windows Server 2016、Windows Server 2012 R2、Windows server 2012 的服务器上本地安装。 除了在物理计算机上运行连接器之外，你也可以在虚拟机（包括 Azure IaaS VM）上运行它。 部署连接器后，它将充当本地服务器和云服务之间的通信接口（一种中继），如下图所示。 箭头表示网络连接启动的方向。

![RMS 连接器体系结构概述](./media/RMS_connector.png)


### <a name="on-premises-servers-supported"></a>支持的本地服务器

RMS 连接器支持下列本地服务器：Exchange Server、SharePoint Server，以及运行 Windows Server 并使用文件分类基础结构来进行分类并将策略应用于文件夹内 Office 文档的文件服务器。 

> [!NOTE]
> 如果想要通过使用文件分类基础结构保护多个文件类型（不仅是 Office 文档），请勿使用 RMS 连接器，而是使用 [AzureInformationProtection cmdlet](/powershell/azureinformationprotection/vlatest/aip)。

有关这些受 RMS 连接器支持的本地服务器的版本，请参阅[支持 Azure RMS 的本地服务器](requirements.md#supported-on-premises-servers-for-azure-rights-management-data-protection)。


### <a name="support-for-hybrid-scenarios"></a>支持混合方案

可以在混合方案中使用 RMS 连接器，即使一些用户连接到了在线服务。 例如，一些用户的邮箱使用 Exchange Online，一些用户的邮箱使用 Exchange Server。 安装 RMS 连接器后，所有用户都可以使用 Azure RMS 保护和使用电子邮件和附件，并且信息保护在两套部署配置中无缝合作。

### <a name="support-for-customer-managed-keys-byok"></a>支持由客户管理密钥 (BYOK)

如果你自行管理 Azure RMS 的租户密钥（自带密钥，即 BYOK 方案），RMS 连接器和使用该连接器的本地服务器不会访问包含你的租户密钥的硬件安全模块 (HSM)。 这是因为，使用租户密钥的所有加密操作都是在 Azure RMS 中执行的，而不是在在本地。

若要详细了解管理租户密钥的此方案，请参阅[计划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

## <a name="prerequisites-for-the-rms-connector"></a>RMS 连接器的必备组件

在安装 RMS 连接器之前，请确保符合以下要求。

|要求|更多信息|
|---------------|--------------------|
|保护服务已激活|[从 Azure 信息保护中激活保护服务](activate-service.md)|
|本地 Active Directory 林和 Azure Active Directory 之间的目录同步|RMS 激活之后，必须将 Azure Active Directory 配置为用于 Active Directory 数据库中的用户和组。<br /><br />**重要提示**：要使 RMS 连接器正常工作，你必须执行此目录同步步骤，即使对于测试网络，也是如此。 尽管可以使用在 Azure Active Directory 中手动创建的帐户来使用 Microsoft 365 和 Azure Active Directory，但此连接器要求 Azure Active Directory 中的帐户与 Active Directory 域服务同步;手动密码同步是不够的。<br /><br />有关详细信息，请参阅以下资源：<br /><br />- [将本地 Active Directory 域与 Azure Active Directory 集成](/azure/architecture/reference-architectures/identity/azure-ad)<br /><br />- [混合标识目录集成工具比较](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-tools-comparison)|
|在最少两台成员计算机上安装 RMS 连接器：<br /><br />-64 位物理或虚拟计算机，运行以下操作系统之一： Windows Server 2016，Windows Server 2012 R2，Windows Server 2012。<br /><br />- 至少 1 GB 的 RAM。<br /><br />- 至少 64 GB 的磁盘空间。<br /><br />- 至少一个网络接口。<br /><br />-通过防火墙访问 internet (或不需要身份验证的 web 代理) 。<br /><br />- 必须位于某个林或域中，而该林或域信任组织内的其他林（包含要用于 RMS 连接器的 Exchange 或 SharePoint 服务器安装）。|为了实现容错和高可用性，你必须在至少两台计算机上安装 RMS 连接器。<br /><br />**提示**：如果你正在使用 Outlook Web Access 或装有 Exchange ActiveSync IRM 的移动设备，并且你必须保持对 Azure RMS 保护的电子邮件和附件的访问权限，则我们建议你部署一组负载平衡的连接器服务器，以确保高可用性。<br /><br />你不需要专用服务器来运行连接器，但必须在将要使用连接器的服务器之外的独立计算机上安装连接器。<br /><br />**重要提示**：如果你希望在使用这些服务提供的功能时运行 Azure RMS，请不要将连接器安装在运行 Exchange Server、SharePoint Server 或文件服务器（已针对文件分类基础结构进行配置，前提是你希望将这些服务提供的功能用于 Azure RMS）的计算机上。 此外，请不要在域控制器上安装此连接器。<br /><br />如果有想要用于 RMS 连接器的服务器工作负载，但其服务器所在的域不被要在其中运行连接器的域所信任，则可以在这些不受信任的域或其林中的其他域中安装附加 RMS 连接器服务器。 <br /><br />可以为组织运行的连接器服务器的数量没有限制，并且在一个组织中安装的所有连接器服务器共享相同的配置。 但是，若要配置连接器来授权服务器，必须能够浏览想要授权的服务器或服务帐户，这意味着必须在可从其中浏览这些帐户的林中运行 RMS 管理工具。|


## <a name="steps-to-deploy-the-rms-connector"></a>部署 RMS 连接器的步骤

连接器不会自动检查成功部署所需的所有[必备组件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)，因此请务必准备好这些必备组件再开始。 部署要求安装连接器、配置连接器，然后配置要使用此连接器的服务器。 

-   **步骤 1**：  [安装 RMS 连接器](install-configure-rms-connector.md#installing-the-rms-connector)

-   **步骤 2**：  [输入凭据](install-configure-rms-connector.md#entering-credentials)

-   **步骤 3**：  [授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **步骤 4**：  [配置负载平衡和高可用性](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

    -   可选： [将 RMS 连接器配置为使用 HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

    -   可选：[为 Web 代理服务器配置 RMS 连接器](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

    -   可选： [在管理计算机上安装 RMS 连接器管理工具](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **步骤 5**：  [将服务器配置为使用 RMS 连接器](configure-servers-rms-connector.md)

    -   [将 Exchange 服务器配置为使用连接器](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [将 SharePoint 服务器配置为使用连接器](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [将文件分类基础结构的文件服务器配置为使用连接器](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## <a name="next-steps"></a>后续步骤

转到步骤 1：[安装并配置 Azure Rights Management 连接器](install-configure-rms-connector.md)。
