---
title: "部署 Azure Rights Management 连接器 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e31656e417a0861d33deb2436d2e4b596a7512a7
ms.openlocfilehash: 6b9b3b039ba2de0de174a134768afd763d26b5dd


---

# 部署 Azure Rights Management 连接器

*适用于：Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

使用以下信息可以了解 Azure Rights Management (RMS) 连接器，以及如何使用该连接器提供信息保护，包括保护使用 Microsoft Exchange Server、Microsoft SharePoint Server 或文件服务器（运行 Windows Server 并使用文件服务器资源管理器的文件分类基础结构 (FCI) 功能）的现有本地部署。

> [!TIP]
> 有关带屏幕截图的高级示例方案，请参阅[运行中的 Azure RMS ](../understand-explore/what-admins-users-see.md) 文章中的[自动保护运行 Windows Server 和文件分类基础结构的文件服务器上的文件](../understand-explore/what-admins-users-see.md#automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure)部分。

## Microsoft 权限管理连接器概述
借助 Microsoft Rights Management (RMS) 连接器，你可以迅速让现有本地服务器将信息权限管理 (IRM) 功能用于基于云的 Microsoft Rights Management 服务 (Azure RMS)。 使用此功能，IT 部门和用户能够轻松地保护组织内部和外部的文档和图片，既无需安装其他基础结构，也无需建立与其他组织的信任关系。 你可以在混合方案中使用此连接器，即使你的一些用户连接到了在线服务。 例如，一些用户的邮箱使用 Exchange Online，一些用户的邮箱使用 Exchange Server。 安装 RMS 连接器后，所有用户都可以使用 Azure RMS 保护和使用电子邮件和附件，并且信息保护在两套部署配置中无缝合作。

RMS 连接器是一种小型化服务，你可将其安装在本地，也可以安装在运行 Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2 的服务器上。 除了在物理计算机上运行连接器之外，你也可以在虚拟机（包括 Azure IaaS VM）上运行它。 在你安装和配置连接器之后，它将充当本地服务器和云服务之间的通信接口（一种中继）。

如果你自行管理 Azure RMS 的租户密钥（自带密钥，即 BYOK 方案），RMS 连接器和使用该连接器的本地服务器不会访问包含你的租户密钥的硬件安全模块 (HSM)。 这是因为，使用租户密钥的所有加密操作都是在 Azure RMS 中执行的，而不是在在本地。

![RMS 连接器体系结构概述](../media/RMS_connector.png)

RMS 连接器支持下列本地服务器：Exchange Server、SharePoint Server，以及运行 Windows Server 并使用文件分类基础结构来进行分类并将策略应用于文件夹内 Office 文档的文件服务器。 如果你想要通过文件分类保护所有文件类型，请勿使用 RMS 连接器，而是使用 [RMS 保护 cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx)。

> [!NOTE]
> 有关这些本地服务器的受支持版本，请参阅[支持 Azure RMS 的本地服务器](..\get-started\requirements-servers.md)。

使用以下信息可帮助你计划、安装和配置 RMS 连接器。 你必须随后进行一些安装后配置，使得你的服务器能够使用连接器。

-   [RMS 连接器的必备组件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)

-   **步骤 1：**[安装 RMS 连接器](install-configure-rms-connector.md#installing-the-rms-connector)

-   **步骤 2：**[输入凭据](install-configure-rms-connector.md#entering-credentials)

-   **步骤 3：**[授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **步骤 4：**[配置负载平衡和高可用性](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   可选：[将 RMS 连接器配置为使用 HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   可选：[为 Web 代理服务器配置 RMS 连接器](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   可选：[在管理计算机上安装 RMS 连接器管理工具](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **步骤 5：**[将服务器配置为使用 RMS 连接器](configure-servers-rms-connector.md)

    -   [将 Exchange 服务器配置为使用连接器](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [将 SharePoint 服务器配置为使用连接器](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [将文件分类基础结构的文件服务器配置为使用连接器](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## RMS 连接器的必备组件
在安装 RMS 连接器之前，请确保符合以下要求。

|要求|更多信息|
|---------------|--------------------|
|权限管理服务 (RMS) 已激活|[激活 Azure 权限管理](activate-service.md)|
|本地 Active Directory 林和 Azure Active Directory 之间的目录同步|RMS 激活之后，必须将 Azure Active Directory 配置为用于 Active Directory 数据库中的用户和组。<br /><br />**重要提示**：要使 RMS 连接器正常工作，你必须执行此目录同步步骤，即使对于测试网络，也是如此。 尽管你可以通过在 Azure Active Directory 中手动创建的帐户来使用 Office 365 和 Azure Active Directory，但此连接器要求 Azure Active Directory 中的帐户必须与 Active Directory 域服务同步；进行手动密码同步是不够的。<br /><br />有关详细信息，请参阅下列资源：<br /><br />[将本地标识与 Azure Active Directory 集成](/active-directory/active-directory-aadconnect)<br /><br />[混合身份目录集成工具比较](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|只是可选但也推荐的选项：<br /><br />启用本地 Active Directory 和 Azure Active Directory 之间的联合身份验证|你可以启用本地目录和 Azure Active Directory 之间的联合身份验证。 此配置使用 RMS 服务单一登录，实现更加无缝的用户体验。 而如果没有单一登录，用户在能够使用权限保护内容之前，会收到提供凭据的提示。<br /><br />有关使用 Active Directory 联合身份验证服务 (AD FS) 来配置 Active Directory 域服务和 Azure Active Directory 之间的联合身份验证的说明，请参阅 Windows Server 库中的 [清单：使用 AD FS 实现和管理单一登录](http://technet.microsoft.com/library/jj205462.aspx) 。|
|在最少两台成员计算机上安装 RMS 连接器：<br /><br />- 64 位物理或虚拟计算机，运行以下操作系统之一：Windows Server 2012 R2、Windows Server 2012 或 Windows Server 2008 R2。<br /><br />- 至少 1 GB 的 RAM。<br /><br />- 至少 64 GB 的磁盘空间。<br /><br />- 至少一个网络接口。<br /><br />- 通过防火墙（或 Web 代理）访问 Internet，无需进行身份验证。<br /><br />- 必须位于某个林或域中，而该林或域信任组织内的其他林（包含要用于 RMS 连接器的 Exchange 或 SharePoint 服务器安装）。|为了实现容错和高可用性，你必须在至少两台计算机上安装 RMS 连接器。<br /><br />**提示**：如果你正在使用 Outlook Web Access 或装有 Exchange ActiveSync IRM 的移动设备，并且你必须保持对 Azure RMS 保护的电子邮件和附件的访问权限，则我们建议你部署一组负载平衡的连接器服务器，以确保高可用性。<br /><br />你不需要专用服务器来运行连接器，但必须在将要使用连接器的服务器之外的一台独立计算机上安装连接器。<br /><br />**重要提示**：如果你希望在使用这些服务提供的功能时运行 Azure RMS，请不要将连接器安装在运行 Exchange Server、SharePoint Server 或文件服务器（已针对文件分类基础结构进行配置，前提是你希望将这些服务提供的功能用于 Azure RMS）的计算机上。 此外，请不要在域控制器上安装此连接器。|

## 后续步骤

转到[安装和配置 Azure Rights Management 连接器](install-configure-rms-connector.md)。


<!--HONumber=Jul16_HO3-->


