---
title: "迁移 AD RMS-Azure 信息保护"
description: "用于将 Active Directory Rights Management Services (AD RMS) 部署迁移到 Azure 信息保护的说明。 迁移之后，用户将仍然可以访问你的组织使用 AD RMS 来保护的文档和电子邮件，新保护的内容将使用 Azure 信息保护。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/03/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b82132d45f1d671c11355c44104dacf521e18082
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>从 AD RMS 迁移到 Azure 信息保护

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*

使用下面的一组指令将 Active Directory Rights Management Services (AD RMS) 部署迁移到 Azure 信息保护。 迁移之后，用户将仍然可以访问你的组织使用 AD RMS 来保护的文档和电子邮件，新保护的内容将使用 Azure 信息保护中的 Azure Rights Management 服务。

不确定这种 AD RMS 迁移是否适合你的组织？

-   有关 Azure 信息保护的简介，请参阅[什么是 Azure 信息保护？](../understand-explore/what-is-information-protection.md)

-   有关 Azure 信息保护与 AD RMS 的比较，请参阅[比较 Azure 信息保护与 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>建议在迁移到 Azure 信息保护之前阅读的内容

虽然不是必需的，但在开始迁移之前阅读以下内容可能会有所帮助，这样可以更好地理解与迁移步骤相关的技术的工作原理：

- [规划和实现 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)：了解可用于 Azure 信息保护租户的密钥管理选项；其中，云中的 SLC 密钥等效项要么由 Microsoft（默认）管理，要么由自己管理（“自带密钥”或 BYOK 配置）。 

- [RMS 服务发现](../rms-client/client-deployment-notes.md#rms-service-discovery)：RMS 客户端部署备注的此部分说明了服务发现的顺序是**注册表** > **SCP** > **云**。 在迁移过程中，如果仍在安装 SCP，则可以使用 Azure 信息保护租户的注册表设置来配置客户端，以确保它们不会使用从 SCP 返回的 AD RMS 群集。

- [ 连接器概述](../deploy-use/deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector)：RMS 连接器文档的此部分说明了本地服务器如何连接到 Azure 权限管理服务以保护文档和电子邮件。

此外，如果熟悉 AD RMS 的工作方式，就会发现阅读[Azure RMS 的工作原理？揭秘](../understand-explore/how-does-it-work.md)非常有用，可帮助识别不同云版本的哪些技术过程是相同的或不同的。

## <a name="prerequisites-for-migrating-ad-rms-to-azure-information-protection"></a>将 AD RMS 迁移到 Azure 信息保护的先决条件
在开始迁移到 Azure 信息保护之前，请确保具备以下先决条件，并确保你了解所有限制。

- **支持的 RMS 部署：**
    
    - 以下版本的 AD RMS 支持到 Azure 信息保护的迁移：
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
        - Windows Server 2016 (x64)
        
    - 支持所有有效的 AD RMS 拓扑：
    
        - 单个林、单个 RMS 群集
        
        - 单个林、多个仅授权 RMS 群集
        
        - 多个林、多个 RMS 群集
        
    注意：默认情况下，多个 AD RMS 群集将迁移到单个 Azure 信息保护租户。 如果你想要迁移到单独的 Azure 信息保护租户，必须将它们视为不同的迁移。 不能将一个 RMS 群集的密钥导入到多个 Azure 信息保护租户。

- **运行 Azure 信息保护的所有要求，包括 Azure 信息保护租户（未激活）：**

    请参阅 [Azure 信息保护的要求](../get-started/requirements-azure-rms.md)。

    尽管在从 AD RMS 迁移之前你必须拥有 Azure 信息保护租户，但我们建议在迁移之前不要激活 Rights Management 服务。 迁移过程包括此步骤，在从 AD RMS 导出密钥和模板并将其导入到 Azure 信息保护之后执行此操作。 但是，如果 Rights Management 服务已激活，你仍可以从 AD RMS 迁移。


- **Azure 信息保护的准备工作：**

    - 在本地目录和 Azure Active Directory 之间进行目录同步

    - 在 Azure Active Directory 中已启用邮件的组

    请参阅[准备 Azure 信息保护](prepare.md)。


- **如果你已使用过 Exchange Server 的信息权限管理 (IRM) 功能**（例如，传输规则和 Outlook Web Access）或者带 AD RMS 的 SharePoint Server：

    - 为这些服务器上未提供 IRM 的较短期间拟定计划
 
    在迁移后，你可以继续将这些服务器上的 IRM 与 Azure Rights Management 服务一起使用。 但是，其中一个迁移步骤是暂时禁用 IRM 服务、安装并配置连接器、重新配置服务器，然后重新启用 IRM。

    在迁移过程中，只有这一步会出现服务中断。

- **如果想要通过使用 HSM 保护的密钥管理自己的 Azure 信息保护租户密钥**：

    - 此可选的配置需要 Azure 密钥保管库和一个支持含 HSM 保护密钥的密钥保管库的 Azure 订阅。 有关详细信息，请参阅 [Azure 密钥保管库定价页](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。 


### <a name="cryptographic-mode-considerations"></a>加密模式注意事项

虽然不是迁移的先决条件，但还是建议进行迁移前在加密模式 2 中运行 AD RMS 服务器和客户端。 

有关不同模式以及如何升级的详细信息，请参阅 [AD RMS Cryptographic Modes](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx)（AD RMS 加密模式）。

如果 AD RMS 群集处于加密模式 1 且无法升级，则必须在迁移完成时重新键入 Azure 信息保护租户密钥。 重新键入将创建一个新租户密钥，该密钥使用加密模式 2。 将 Azure Rights Management 服务与加密模式 1 配合使用仅在迁移过程中受支持。

确认 AD RMS 加密模式：
 
- 对于 Windows Server 2012 R2 和 Windows 2012：“AD RMS 群集属性”>“常规”选项卡。 

- 对于所有支持版本的 AD RMS：使用 [RMS 分析工具](https://www.microsoft.com/en-us/download/details.aspx?id=46437)和“AD RMS 管理员”选项可在“RMS 服务信息”中查看加密模式。


### <a name="migration-limitations"></a>迁移限制

-   虽然迁移过程支持将服务器授权证书 (SLC) 密钥迁移到 Azure 信息保护的硬件安全模块 (HSM)，但 Exchange Online 目前对于 Azure 信息保护使用的 Rights Management 服务不支持此配置。 如果你希望在迁移到 Azure 信息保护之后获得 Exchange Online 的完整 IRM 功能，必须[由 Microsoft 管理](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok)你的 Azure 信息保护租户密钥。 你也可以自行管理 Azure 信息保护租户 (BYOK)，在这种情况下，Exchange Online 的 IRM 功能将会受限。 有关将 Exchange Online 与 Azure Rights Management 服务配合使用的详细信息，请参阅这些迁移说明中的[步骤 6.为 Exchange Online 配置 IRM 集成](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online)。

-   如果 Azure 信息保护使用的 Rights Management 服务不支持你的软件和客户端，则它们无法保护或使用受 Azure Rights Management 保护的内容。 请务必查看 [Azure Rights Management 的要求](../get-started/requirements-azure-rms.md)文章中的“支持的应用程序和客户端”部分。

-   如果你将本地密钥作为存档导入 Azure 信息保护（在导入过程中未将 TPD 设置为活动）并在分阶段迁移过程中分批迁移用户，则 AD RMS 中保留的用户将无法访问已迁移用户最近保护的内容。 在这种情况下，请尽量缩短迁移持续时间，并以逻辑批的形式迁移用户，以便在用户相互协作的情况下会一起迁移。

    如果你在导入过程中将 TPD 设置为活动，则不存在这种限制，因为所有用户将使用同一密钥保护内容。 我们建议采用这种配置，因为这样你就可以根据自己的步调单独迁移所有用户。

-   如果你与外部合作伙伴协作（例如，通过使用受信任的用户域或联合），则在你迁移的同时或之后尽早的时间，这些合作伙伴也必须迁移到 Azure 信息保护。 若要继续访问你的组织以前使用 Azure 信息保护进行保护的内容，这些合作伙伴必须进行与你进行的更改（在本文档中提供了这些更改）类似的客户端配置更改。

    由于你的合作伙伴进行的配置可能有所变动，确切说明此重新配置已超出了本文档的范围。 若要获得帮助，[请与 Microsoft 支持部门联系](../get-started/information-support.md#support-options-and-community-resources)。

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>将 AD RMS 迁移到 Azure 信息保护的步骤概述


迁移步骤可分为 4 个阶段，在不同的时间由不同的管理员执行。

[**阶段 1：AD RMS 的服务器端配置**](migrate-from-ad-rms-phase1.md)

- **步骤 1：下载“Azure RMS 管理”管理工具**

    迁移过程要求你从随“Azure RMS 管理”管理工具一起安装的 Azure RMS 模块中运行一个或多个 Windows PowerShell cmdlet。

- **步骤 2：从 AD RMS 中导出配置数据并将其导入到 Azure 信息保护**

    将 AD RMS 中的配置数据（密钥、模板、URL）导出到 XML 文件，然后使用 Import-AadrmTpd Windows PowerShell cmdlet 将该文件上传到 Azure 信息保护中的 Azure Rights Management 服务。 可能需要其他步骤，具体取决于你的 AD RMS 密钥配置：

    - **软件保护密钥到软件保护密钥的迁移**：

        AD RMS 中集中管理的基于密码的密钥迁移到由 Microsoft 管理的 Azure 信息保护租户密钥。 这是最简单的迁移路径，并且无需执行任何附加步骤。

    - **HSM 保护密钥到 HSM 保护密钥的迁移**：

        将 HSM 存储的 AD RMS 密钥迁移到客户管理的 Azure 信息保护租户密钥（“自带密钥”方案，简称 BYOK）。 这需要执行附加步骤，以将密钥从本地 Thales HSM 传送到 Azure 密钥保管库并授权 Azure Rights Management 服务使用此密钥。 现有的 HSM 保护密钥必须受模块保护；Rights Management Services 不支持 OCS 保护密钥。

    - **软件保护密钥到 HSM 保护密钥的迁移**：

        AD RMS 中集中管理的基于密码的密钥迁移到由客户管理的 Azure 信息保护租户密钥（“携带你自己的密钥”或 BYOK 方案）。 这需要的配置最多，因为必须先提取软件密钥并将其导入到本地 HSM 中，然后再执行附加步骤以将该密钥从本地 Thales HSM 传送到 Azure 密钥保管库 HSM，并授权 Azure Rights Management 服务使用存储该密钥的密钥保管库。

- **步骤 3：激活 Azure 信息保护租户**

    如果可能，请在执行导入过程之后而不是之前执行此步骤。

- **步骤 4：配置导入的模板**

    当你导入权限策略模板时，系统会将其状态存档。 如果你希望用户能够查看并使用这些模板，则必须在 Azure 经典门户中将模板状态更改为“已发布”。


[**阶段 2：客户端配置**](migrate-from-ad-rms-phase2.md)


- **步骤 5：重新配置客户端以使用 Azure 信息保护**

    必须将现有 Windows 计算机重新配置为使用 Azure 信息保护服务而不是 AD RMS。 此步骤适用于你组织中的计算机以及合作伙伴组织(如果你在运行 AD RMS 时已与其协作)中的计算机。

    此外，如果你部署了[移动设备扩展](http://technet.microsoft.com/library/dn673574.aspx)以支持移动设备（如 iOS 手机和 iPad、Android 手机和平板电脑、Windows Phone 以及 Mac 计算机），则必须删除 DNS 中重定向这些客户端的 SRV 记录才能使用 AD RMS。


[**阶段 3：支持服务配置**](migrate-from-ad-rms-phase3.md)


- **步骤 6：配置 IRM 与 Exchange Online 的集成**

    如果你要将 Exchange Online 与 Azure 信息保护中的 Azure Rights Management 服务结合使用，则需要此步骤。


- **步骤 7：部署 RMS 连接器**

    如果你要将以下任何本地服务与 Azure Rights Management 服务结合使用来保护 Office 文档和电子邮件，则需要此步骤：

    - Exchange Server（例如，传输规则和 Outlook Web Access）

    - SharePoint Server

    - 运行文件分类基础结构 (FCI) 的 Windows Server


[**阶段 4：迁移后任务**](migrate-from-ad-rms-phase4.md )

- **步骤 8：解除 AD RMS 授权**

    当你已确认所有客户端均使用 Azure 信息保护而不再访问 AD RMS 服务器，你可以解除 AD RMS 部署的授权。


- **步骤 9：更新 Azure 信息保护租户密钥**

    如果在迁移前未运行加密模式 2，此步骤是必需的；对于所有迁移来说，此步骤是可选的但建议执行，以帮助保护 Azure 信息保护租户密钥的安全性。


## <a name="next-steps"></a>后续步骤
若要开始迁移，请转到[阶段 1 - 服务器端配置](migrate-from-ad-rms-phase1.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
