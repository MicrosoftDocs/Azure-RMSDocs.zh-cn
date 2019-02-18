---
title: 迁移 AD RMS-Azure 信息保护
description: 用于将 Active Directory Rights Management Services (AD RMS) 部署迁移到 Azure 信息保护的说明。 迁移之后，用户将仍然可以访问你的组织使用 AD RMS 来保护的文档和电子邮件，新保护的内容将使用 Azure 信息保护。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 85bbf60e2d17c623572671b745c22d1ffdcfe871
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258039"
---
# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>从 AD RMS 迁移到 Azure 信息保护

>适用范围：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

使用下面的一组指令将 Active Directory Rights Management Services (AD RMS) 部署迁移到 Azure 信息保护。 

迁移之后，AD RMS 服务器将不再可用，但用户将仍然可以访问你的组织使用 AD RMS 来保护的文档和电子邮件。 新保护的内容将使用 Azure 信息保护中的 Azure Rights Management 服务 (Azure RMS)。

不确定这种 AD RMS 迁移是否适合你的组织？

- 有关 Azure 信息保护的简介，请参阅[什么是 Azure 信息保护？](./what-is-information-protection.md)

- 有关 Azure 信息保护与 AD RMS 的比较，请参阅[比较 Azure 信息保护与 AD RMS](./compare-on-premise.md)。

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>建议在迁移到 Azure 信息保护之前阅读的内容

虽然不是必需的，但在开始迁移之前，阅读以下文档可能会很有用。 这一知识可以让你更好地了解与迁移步骤相关的技术的工作原理。

- [计划和实施 Azure 信息保护租户密钥](./plan-implement-tenant-key.md)：了解可用于 Azure 信息保护租户的密钥管理选项；在其中，云中的 SLC 密钥等效项要么由 Microsoft 管理（默认），要么由自己管理（即“自带密钥”或 BYOK 配置）。 

- [RMS 服务发现](./rms-client/client-deployment-notes.md#rms-service-discovery)：RMS 客户端部署备注的此部分说明了服务发现的顺序依次是注册表、SCP 和云。 在迁移过程中，如果仍在安装 SCP，则可以使用 Azure 信息保护租户的注册表设置来配置客户端，以确保它们不会使用从 SCP 返回的 AD RMS 群集。

- [Microsoft Rights Management 连接器概述](./deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector)：RMS 连接器文档的此部分说明了本地服务器如何连接到 Azure Rights Management 服务以保护文档和电子邮件。

此外，如果熟悉 AD RMS 的工作方式，就会发现阅读[Azure RMS 的工作原理？揭秘](./how-does-it-work.md)非常有用，可帮助识别不同云版本的哪些技术过程是相同的或不同的。

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
        
    注意：默认情况下，多个 AD RMS 群集将迁移到单个 Azure 信息保护的租户。 如果想要迁移到单独的 Azure 信息保护租户，必须将它们视为不同的迁移。 不能将一个 RMS 群集的密钥导入到多个租户中。

- **运行 Azure 信息保护的所有要求，包括 Azure 信息保护租户（Azure Rights Management 服务未激活）订阅：**

    请参阅 [Azure 信息保护的要求](./requirements.md)。

    请注意，如果拥有运行 Office 2010 的计算机，必须安装 Azure 信息保护客户端，因为此客户端可提供对云服务用户进行身份验证的功能。 对于更高版本的 Office，Azure 信息保护客户端是分类和标记所必需的，但如果只想保护数据，该客户端是可选的，但建议你使用它。 有关详细信息，请参阅 [Azure 信息保护客户端管理员指南](./rms-client/client-admin-guide.md)。

    尽管要求必须拥有 Azure 信息保护订阅才能迁移 AD RMS，但我们建议在开始迁移之前不要激活 Rights Management 服务。 迁移过程包括此激活步骤，在从 AD RMS 导出密钥和模板并将其导入到 Azure 信息保护租户之后执行此操作。 但是，如果 Rights Management 服务已激活，你仍可以凭借额外的步骤从 AD RMS 迁移。


- **Azure 信息保护的准备工作：**

  - 在本地目录和 Azure Active Directory 之间进行目录同步

  - 在 Azure Active Directory 中已启用邮件的组

    请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

- 如果你已使用过 Exchange Server 的信息权限管理 (IRM) 功能（例如，传输规则和 Outlook Web Access）或者带 AD RMS 的 SharePoint Server：

  - 为这些服务器上未提供 IRM 的较短期间拟定计划
 
    在迁移后，你可以继续在这些服务器上使用 IRM。 但是，其中一个迁移步骤是暂时禁用 IRM 服务、安装并配置连接器、重新配置服务器，然后重新启用 IRM。

    在迁移过程中，只有这一步会出现服务中断。

- **如果想要通过使用 HSM 保护的密钥管理自己的 Azure 信息保护租户密钥**：

    - 此可选的配置需要 Azure 密钥保管库和一个支持含 HSM 保护密钥的密钥保管库的 Azure 订阅。 有关详细信息，请参阅 [Azure 密钥保管库定价页](https://azure.microsoft.com/pricing/details/key-vault/)。 


### <a name="cryptographic-mode-considerations"></a>加密模式注意事项

如果 AD RMS 群集当前处于加密模式 1，则在开始迁移前，请勿将此群集升级到加密模式 2。 请改为使用加密模式 1 进行迁移，并在迁移结束时重新生成租户密钥，将其作为迁移后的任务之一。

确认 AD RMS 加密模式：
 
- 对于 Windows Server 2012 R2 和 Windows 2012：AD RMS 群集属性 > “常规”选项卡。 

- 对于 Windows Server 2008 R2：检查是否已安装了[在 Windows Server 2008 R2 和 Windows Server 2008 中，AD RMS 的 RSA 密钥长度增加到 2048 位](https://support.microsoft.com/help/2627272/rsa-key-length-is-increased-to-2048-bits-for-ad-rms-in-windows-server )修补程序。 如果不是，AD RMS 群集正以加密模式 1 运行。

### <a name="migration-limitations"></a>迁移限制

- 如果 Azure 信息保护使用的 Rights Management 服务不支持你的软件和客户端，则它们无法保护或使用受 Azure Rights Management 保护的内容。 请务必查看 [Azure Rights Management 的要求](./requirements.md)中的“支持的应用程序和客户端”部分。

- 如果将你的 AD RMS 部署配置为与外部合作伙伴协作（例如，通过使用受信任的用户域或联合），则在你迁移的同时或之后尽早的时间，这些合作伙伴也必须迁移到 Azure 信息保护。 若要继续访问你的组织以前使用 Azure 信息保护进行保护的内容，这些合作伙伴必须进行与你进行的更改（在本文档中提供了这些更改）类似的客户端配置更改。
    
    由于你的合作伙伴进行的配置可能有所变动，确切说明此重新配置已超出了本文档的范围。 但是，有关规划指导及其他帮助，请参阅下一节，[联系 Microsoft 支持部门](./information-support.md#support-options-and-community-resources)。

## <a name="migration-planning-if-you-collaborate-with-external-partners"></a>与外部伙伴协作时的迁移规划

包括迁移规划阶段的 AD RMS 合作伙伴，因为他们也必须迁移到 Azure 信息保护。 执行以下迁移步骤之前，请确保下列各项已就位：

- 他们拥有支持 Azure Rights Management 服务的 Azure Active Directory 租户。  
    
    例如，他们拥有 Office 365 E3 或 E5 订阅，或企业移动性 + 安全性订阅或 Azure 信息保护独立订阅。

- 他们的 Azure Rights Management 服务尚未激活，但他们知道其 Azure Rights Management 服务 URL。

    他们可以通过安装 Azure Rights Management 工具，连接到服务获取此信息 ([Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice))，然后查看其 Azure Rights Management 服务的租户信息 ([Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration))。

- 他们向你提供其 AD RMS 群集的 URL 及其 Azure Rights Management 服务 URL，以便你可以配置已迁移客户端，将其受 AD RMS 保护的内容的请求重定向到其租户的 Azure Rights Management 服务中。 步骤 7 说明了如何配置客户端重定向。

- 他们需先将其 AD RMS 群集根项 (SLC) 导入到其租户中，然后你才能开始迁移你的用户。 同样，你也需要先导入你的 AD RMS 群集根项，然后他们才能开始迁移其用户。 有关此迁移过程中导入密钥的说明，请参阅[步骤 4：从 AD RMS 中导出配置数据并将其导入到 Azure 信息保护](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection)。 

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>将 AD RMS 迁移到 Azure 信息保护的步骤概述

迁移步骤可分为五个阶段，在不同的时间由不同的管理员执行。

[**第 1 阶段：迁移准备**](migrate-from-ad-rms-phase1.md)

- **步骤 1：安装 AADRM PowerShell 模块，并标识你的租户 URL**

    迁移过程要求你从 AADRM 模块运行一个或多个 PowerShell cmdlet。 你还需要知道你的租户的 Azure Rights Management 服务 URL 才能完成多个迁移步骤，并且可使用 PowerShell 来确定此值。

- **步骤 2：客户端迁移准备**

    如果无法一次迁移所有客户端，并且将其分批次进行迁移，请使用载入控件并部署预迁移脚本。 但是，如果要同时迁移所有内容，而不是分步迁移，可跳过此步骤。

- **步骤 3：准备 Exchange 部署以进行迁移**

    如果当前正在使用 Exchange Online 的 IRM 功能或 Exchange 本地部署保护电子邮件，则需要此步骤。 但是，如果要同时迁移所有内容，而不是分步迁移，可跳过此步骤。

[**第 2 阶段：AD RMS 的服务器端配置**](migrate-from-ad-rms-phase2.md)

- **步骤 4：从 AD RMS 中导出配置数据并将其导入到 Azure 信息保护**

    将 AD RMS 中的配置数据（密钥、模板、URL）导出到 XML 文件，然后使用 Import-AadrmTpd PowerShell cmdlet 将该文件上传到 Azure 信息保护中的 Azure Rights Management 服务。 然后，确定要使用哪个导入的服务器许可方证书 (SLC) 密钥作为 Azure 权限管理服务的租户密钥。 可能需要其他步骤，具体取决于你的 AD RMS 密钥配置：

    - **软件保护密钥到软件保护密钥的迁移**：

        AD RMS 中集中管理的基于密码的密钥迁移到由 Microsoft 管理的 Azure 信息保护租户密钥。 这是最简单的迁移路径，并且无需执行任何附加步骤。

    - **HSM 保护密钥到 HSM 保护密钥的迁移**：

        将 HSM 存储的 AD RMS 密钥迁移到客户管理的 Azure 信息保护租户密钥（“自带密钥”方案，简称 BYOK）。 这需要执行附加步骤，以将密钥从本地 Thales HSM 传送到 Azure 密钥保管库并授权 Azure Rights Management 服务使用此密钥。 现有的 HSM 保护密钥必须受模块保护；Rights Management Services 不支持 OCS 保护密钥。

    - **软件保护密钥到 HSM 保护密钥的迁移**：

        AD RMS 中集中管理的基于密码的密钥迁移到由客户管理的 Azure 信息保护租户密钥（“携带你自己的密钥”或 BYOK 方案）。 这需要的配置最多，因为必须先提取软件密钥并将其导入到本地 HSM 中，然后再执行附加步骤以将该密钥从本地 Thales HSM 传送到 Azure 密钥保管库 HSM，并授权 Azure Rights Management 服务使用存储该密钥的密钥保管库。

- **步骤 5.激活 Azure Rights Management 服务**

    如果可能，请在执行导入过程之后而不是之前执行此步骤。 如果在导入前已激活服务，则需要执行额外的步骤。

- **步骤 6.配置导入的模板**

    当你导入权限策略模板时，系统会将其状态存档。 如果希望用户能够查看并使用这些模板，则必须在 Azure 经典门户中将模板状态更改为“已发布”。


[**第 3 阶段：客户端配置**](migrate-from-ad-rms-phase3.md)

- **步骤 7：重新配置 Windows 计算机以使用 Azure 信息保护**

    必须将现有 Windows 计算机重新配置为使用 Azure Rights Management 服务而不是 AD RMS。 此步骤适用于你组织中的计算机以及合作伙伴组织(如果你在运行 AD RMS 时已与其协作)中的计算机。

[**第 4 阶段：支持服务配置**](migrate-from-ad-rms-phase4.md)

- **步骤 8：为 Exchange Online 配置 IRM 集成**

    此步骤将为 Exchange Online 完成 AD RMS 迁移，以便现在使用 Azure Rights Management 服务。

- **步骤 9：为 Exchange Server 和 SharePoint Server 配置 IRM 集成**

    此步骤将为本地 Exchange 或本地 SharePoint 完成 AD RMS 迁移，以便现在使用 Azure Rights Management 服务，这需要部署 Rights Management 连接器。


[**第 5 阶段：迁移后任务**](migrate-from-ad-rms-phase5.md )

- **步骤 10：取消预配 AD RMS**

    如果已确认所有 Windows 计算机均使用 Azure Rights Management 服务而不再访问 AD RMS 服务器，则可以取消预配 AD RMS 部署。

- **步骤 11：完成客户端迁移任务**

    如果部署了[移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)以支持移动设备（如 iOS 手机和 iPad、Android 手机和平板电脑、Windows Phone 和平板电脑以及 Mac 计算机），则必须删除 DNS 中重定向这些客户端的 SRV 记录才能使用 AD RMS。 
    
    不再需要准备阶段配置的载入控件。 但是，如果因选择同时迁移所有内容（而非分步迁移）而未使用载入控件，可跳过有关删除载入控件的说明。
    
    如果 Windows 计算机运行的是 Office 2010，请检查是否需要禁用“AD RMS 权限策略模板管理（自动）”任务。

- **步骤 12：重新生成 Azure 信息保护租户密钥**

    如果迁移前未在加密模式 2 中运行，建议执行此步骤。


## <a name="next-steps"></a>后续步骤
若要开始迁移，请转到[第 1 阶段：准备](migrate-from-ad-rms-phase1.md)。

