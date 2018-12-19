---
title: 你的 Azure 信息保护租户密钥
description: 此信息有助于规划和管理 Azure 信息保护租户密钥。 为了遵守适用于组织的特别规定，你可能想要自行管理租户密钥，而不是由 Microsoft 管理你的租户密钥（默认设置）。 自行管理租户密钥也称为自带密钥 (BYOK)。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/10/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3efae21dfabdb347826b177d5c58a3498d3276c5
ms.sourcegitcommit: 5b4eb0e17fb831d338d8c25844e9e6f4ca72246d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53173955"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>计划和实施 Azure 信息保护租户密钥

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用此文章中的信息可帮助你规划和管理 Azure 信息保护租户密钥。 例如，为了遵守组织的具体规定，你不能让 Microsoft 管理你的租户密钥（默认设置），而想要自行管理租户密钥。 自行管理租户密钥也称为自带密钥 (BYOK)。

什么是 Azure 信息保护租户密钥？

- Azure 信息保护租户密钥是组织的根密钥。 可以此根密钥派生出其他密钥，例如用户密钥、计算机密钥和文档加密密钥。 每当 Azure 信息保护使用组织的这些密钥时，它们会以加密方式链接到你的 Azure 信息保护租户密钥。

- Azure 信息保护租户密钥是 Active Directory Rights Management Services (AD RMS) 中服务器许可方证书 (SLC) 密钥的联机等效项。 

**概览：** 参考下表来快速了解建议的租户密钥拓扑。 然后，阅读其他文档以获取详细信息。

|业务要求|建议的租户密钥拓扑|
|------------------------|-----------------------------------|
|无需特殊的硬件、额外的软件或 Azure 订阅即可快速部署 Azure 信息保护。<br /><br />例如：测试环境以及当组织没有针对密钥管理的法规要求时。|由 Microsoft 管理|
|合规性规定、额外的安全性以及对所有生命周期操作的控制。 <br /><br />例如：密钥必须由硬件安全模块 (HSM) 保护。|BYOK|


如有需要，可以在部署后通过使用 [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) cmdlet 来更改租户密钥拓扑。


## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>选择你的租户密钥拓扑：由 Microsoft 管理（默认设置）或由你管理 (BYOK)

确定哪种租户密钥拓扑最适合你的组织：

- **由 Microsoft 托管**：Microsoft 会为你的组织自动生成一个专用于 Azure 信息保护的租户密钥。 默认情况下，Microsoft 将此密钥用于租户并管理租户密钥生命周期的大多数方面。 
    
    这是最简单的选项，管理开销最低。 大多数情况下，你甚至不需要知道自己有租户密钥。 你只需注册 Azure 信息保护，密钥管理过程的剩余部分将由 Microsoft 处理。

- **自行管理 (BYOK)**：如果要完全控制租户密钥，请结合使用 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 和 Azure 信息保护。 对于此租户密钥拓扑，可以直接在 Key Vault 中创建密钥或本地创建密钥。 如果本地创建密钥，接着需要将此密钥传输或导入到 Key Vault 中。 然后将 Azure 信息保护配置为使用此密钥，并在 Azure Key Vault 中管理它。
    

### <a name="more-information-about-byok"></a>有关 BYOK 的详细信息
若要创建自己的密钥，有如下选项可供选择：

- **一个密钥，此密钥经本地创建，然后传输或导入到 Key Vault**：
    
    - 一个受 HSM 保护的密钥，此密钥经在本地创建，然后传输到 Key Vault 作为受 HSM 保护的密钥。
    
    - 一个受软件保护的密钥，此密钥经本地创建和转换，然后传输到 Key Vault 作为受 HSM 保护的密钥。 仅在[从 Active Directory Rights Management Services (AD RMS) 迁移](migrate-from-ad-rms-to-azure-rms.md)时才支持此选项。
    
    - 一个受软件保护的密钥，此密钥经本地创建，然后导入到 Key Vault 作为受软件保护的密钥。 此选项需要 .PFX 证书文件。
    
- **在 Key Vault 中创建的一个密钥**：
    
    - 在 Key Vault 中创建的一个受 HSM 保护的密钥。
    
    - 在 Key Vault 中创建的一个受软件保护的密钥。

在这些 BYOK 选项中最典型的选项是一个受 HSM 保护的密钥，此密钥经本地创建，然后传输到 Key Vault 作为受 HSM 保护的密钥。 尽管此选项的管理开销最大，但是可能需要使用此选项以使你的组织符合特定法规。 Azure Key Vault 使用的 HSM 经过了 FIPS 140-2 级别 2 的验证。

使用这种选项的过程如下：

1. 根据 IT 策略和安全策略在本地生成租户密钥。 此密钥是主副本。 它保留在本地，而你负责备份它。

2. 创建此密钥的副本，然后将此副本从 HSM 安全传输到 Azure Key Vault。 整个过程中，此密钥的主副本从未离开过硬件保护范围。

3. 此密钥的副本受 Azure Key Vault 保护。

> [!NOTE]

> 作为一种附加保护措施，Azure 密钥保管库对位于北美、EMEA（欧洲、中东和非州）和亚洲等地区的数据中心使用独立安全域。 Azure Key Vault 还使用 Azure 的其他实例，如 Microsoft Azure 德国和 Azure 政府。 

虽然这是可选的，但你可能希望使用 Azure 信息保护提供的接近实时的使用日志，以便准确了解租户密钥的使用时间和方式。

### <a name="when-you-have-decided-your-tenant-key-topology"></a>在确定了你的租户密钥拓扑后

如果决定让 Microsoft 管理你的租户密钥： 

- 除非从 AD RMS 迁移，否则对于为租户生成密钥你无需进行任何额外的操作，可以直接转至[后续步骤](plan-implement-tenant-key.md#next-steps)。

- 如果当前已具有 AD RMS，且想迁移到 Azure 信息保护，请使用迁移说明：[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)。 

如果你决定自行管理租户密钥，请阅读以下部分以获取更多信息。

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>为 Azure 信息保护租户密钥实现 BYOK

如果你决定自行生成和管理租户密钥，请使用本部分中的信息和过程；“自带密钥”(BYOK) 方案：

> [!NOTE]
> 如果已开始结合使用 Azure 信息保护和由 Microsoft 管理的租户密钥，并且现在想要管理租户密钥（移动到 BYOK），则仍可以使用已存档密钥访问以前受保护的文档和电子邮件。 

### <a name="prerequisites-for-byok"></a>BYOK 的先决条件
有关自带密钥 (BYOK) 的先决条件列表，请参阅以下表格。

|要求|更多信息|
|---------------|--------------------|
|你的 Azure 信息保护租户必须具有 Azure 订阅。 如果没有订阅，可以注册[免费帐户](https://azure.microsoft.com/pricing/free-trial/)。 <br /><br /> 若要使用受 HSM 保护的密钥，必须拥有 Azure Key Vault 高级服务层。|免费的 Azure 订阅提供相应的访问权限，可配置 Azure Active Directory 以及 Azure 权限管理自定义模板（**可访问 Azure Active Directory**），但不足以使用 Azure 密钥保管库。 若要确认拥有可用于 BYOK 的 Azure 订阅，请使用 [Azure 资源管理器](https://msdn.microsoft.com/library/azure/mt786812\(v=azure.300\).aspx) PowerShell cmdlet： <br /><br /> 1.若要启动 Azure PowerShell 会话，请选择“以管理员身份运行”选项，并使用以下命令以 Azure 信息保护租户的全局管理员身份登录：`Login-AzureRmAccount`<br /><br />2.键入以下命令，并确认可以看到显示了订阅名称和 ID 以及 Azure 信息保护租户 ID 的值，并且状态为“已启用”：`Get-AzureRmSubscription`<br /><br />如果没有显示任何值，并且返回到提示，则表示没有可用于 BYOK 的 Azure 订阅。 <br /><br />**注意**：若要使用软件密钥到硬件密钥从 AD RMS 迁移到 Azure 信息保护，除了满足 BYOK 先决条件以外，还必须拥有最低版本为 11.62 的 Thales 固件。|
|若要使用本地创建的受 HSM 保护密钥，请执行以下操作： <br /><br />- 针对 Key Vault BYOK 列出的所有先决条件。 |请参阅 Azure 密钥保管库文档中的 [Prerequisites for BYOK](/azure/key-vault/key-vault-hsm-protected-keys#prerequisites-for-byok)（BYOK 的先决条件）。 <br /><br /> **注意**：若要使用软件密钥到硬件密钥从 AD RMS 迁移到 Azure 信息保护，除了满足 BYOK 先决条件以外，还必须拥有最低版本为 11.62 的 Thales 固件。|
|如果包含租户密钥的密钥保管库使用 Azure Key Vault 虚拟网络服务终结点： <br /><br />- 允许受信任 Microsoft 服务绕过此防火墙。|有关详细信息，请参阅 [Azure Key Vault 虚拟网络服务终结点](/azure/key-vault/key-vault-overview-vnet-service-endpoints)。|
|适用于 Windows PowerShell 的 Azure Rights Management 管理模块。|有关安装说明，请参阅[安装 AADRM PowerShell 模块](./install-powershell.md)。 <br /><br />如果之前已安装了此 Windows PowerShell 模块，请运行以下命令检查版本号是否高于或等于 **2.9.0.0**：`(Get-Module aadrm -ListAvailable).Version`|

有关 Thales HSM 及其如何与 Azure 密钥保管库一起使用的详细信息，请参阅 [Thales website](https://www.thales-esecurity.com/msrms/cloud)（Thales 网站）。

### <a name="choosing-your-key-vault-location"></a>选择密钥保管库位置

创建密钥保管库以包含要用作 Azure 信息的租户密钥的密钥时，必须指定一个位置。 此位置为 Azure 区域或 Azure 实例。

首先使选择满足合规性，然后在最大程度上降低网络延迟：

- 如果出于合规性原因而选择了 BYOK 密钥拓扑，这些合规性要求可能授权存储 Azure 信息保护租户密钥的 Azure 区域或 Azure 实例。

- 由于针对保护的所有加密调用都链接到 Azure 信息保护租户密钥，因此你可能希望这些调用发生时在最大程度上降低网络延迟。 若要实现这一点，请在与 Azure 信息保护租户相同的 Azure 区域或实例中创建密钥保管库。

若要标识 Azure 信息保护租户的位置，请使用 [Get-AadrmConfiguration](/powershell/module/aadrm/get-aadrmconfiguration) PowerShell cmdlet 并从 URL 中标识区域。 例如：

    LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

可以从 rms.na.aadrm.com 中标识区域，在此示例中，它位于北美。

通过下表确定推荐用于在最大程度上降低网络延迟的 Azure 区域或实例。

|Azure 区域或实例|建议的密钥保管库位置|
|---------------|--------------------|
|rms.**na**.aadrm.com|美国中北部或美国东部|
|rms.**eu**.aadrm.com|北欧或西欧|
|rms.**ap**.aadrm.com|东亚或东南亚|
|rms.**sa**.aadrm.com|美国西部或美国东部|
|rms.**govus**.aadrm.com|美国中部或美国东部 2|


### <a name="instructions-for-byok"></a>BYOK 的说明

使用 Azure Key Vault 文档创建密钥保管库以及要用于 Azure 信息保护的密钥。 请参阅[Azure Key Vault 入门](/azure/key-vault/key-vault-get-started)查看相关示例。

确保密钥长度为 2048 位（推荐）或 1024 位。 Azure 信息保护不支持其他的密钥长度。

若要本地创建受 HSM 保护的密钥并将它传输到密钥保管库作为受 HSM 保护的密钥，请按照[如何为 Azure 密钥保管库生成和传输受 HSM 保护的密钥](/azure/key-vault/key-vault-hsm-protected-keys)中的过程进行操作。

为使 Azure 信息保护使用密钥，所有密钥保管库操作必须允许使用密钥。 这是默认配置，且操作将被加密、解密、包装、解包、签名和验证。 可以通过使用 [Get-AzureKeyVauktKey](/powershell/module/azurerm.keyvault/get-azurekeyvaultkey) 并验证“密钥”详细信息中返回的 key_ops 值来检查密钥所允许的操作。 如有必要，使用 [Update-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/update-azurekeyvaultkey) 和 KeyOps 参数添加允许的操作。

Key Vault 中存储的密钥具有密钥 ID。 此密钥 ID 是包含密钥保管库名称、密钥容器、密钥名称和密钥版本的一个 URL。 例如：**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**。 若要使用此密钥，必须通过指定其 Key Vault URL 来配置 Azure 信息保护。

在 Azure 信息保护可以使用此密钥之前，必须授权 Azure Rights Management 服务在你组织的密钥保管库中使用该密钥。 要执行此操作，Azure Key Vault 管理员可以使用 Azure 门户或 Azure PowerShell：

使用 Azure 门户进行配置：

1. 依次导航至“密钥保管库” > \< 你的密钥保管库名称 > > “访问政策” > “添加新项”。

2. 在“添加访问策略”边栏选项卡中，在“根据模板配置(可选)”列表框中选择“Azure 信息保护 BYOK”，然后单击“OK”。
    
    所选模板具有以下配置：
    
    - 自动为“选择主体”分配“Microsoft Rights Management Services”。
    - 自动选择“获取”、“解密”和“签名”作为关键权限。 

使用 PowerShell 进行配置：

- 运行密钥保管库 PowerShell cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy)，并通过使用 GUID 00000012-0000-0000-c000-000000000000 向 Azure Rights Management 服务主体授予权限。 例如：
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get

现在可开始配置 Azure 信息保护以将此密钥用作你的组织的 Azure 信息保护租户密钥。 使用 Azure RMS cmdlet，首先连接到 Azure Rights Management 服务，并登录：

    Connect-AadrmService

然后运行 [Use-AadrmKeyVaultKey cmdlet](/powershell/module/aadrm/use-aadrmkeyvaultkey)，指定密钥 URL。 例如：

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> 在此示例中，“aaaabbbbcccc111122223333”是要使用的密钥版本。 如果不指定版本，则将使用当前版本的密钥而不发出警告，并且显示命令以进行工作。 但是，如果后来对密钥保管库中的密钥进行了更新（已续订），则即使你再次运行 Use-AadrmKeyVaultKey 命令，Azure Rights Management 服务也将停止为你的租户工作。
>
>在运行此命令时，除了密钥名称外，请确保还指定了密钥版本。 可以使用 Azure 密钥保管库 cmd [Get-AzureKeyVaultKey](/powershell/module/azurerm.keyvault\get-azurekeyvaultkey) 来获取当前密钥的版本号。 例如：`Get-AzureKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

如果需要确认已为 Azure 信息保护正确设置了密钥 URL：在 Azure Key Vault 中，运行 [Get-AzureKeyVaultKey](/powershell/module/azurerm.keyvault\get-azurekeyvaultkey) 以查看密钥 URL。

最后，如果 Azure Rights Management 服务已激活，请运行 [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) 以告诉 Azure 信息保护将此密钥用作 Azure Rights Management 服务的活动租户密钥。 如果不执行此步骤，Azure 信息保护将继续使用为租户自动创建的默认 Microsoft 托管密钥。


## <a name="next-steps"></a>后续步骤

在已经规划并根据需要创建和配置了租户密钥后，请执行以下操作：

1.  开始使用你的租户密钥：
    
    - 如果尚未激活保护服务，则必须立即激活 Rights Management 服务，以便组织能够开始使用 Azure 信息保护。 用户立即开始使用你的租户密钥（在 Azure Key Vault 中由 Microsoft 管理或由你管理）。
    
        有关激活的详细信息，请参阅[激活 Azure Rights Management](./activate-service.md)。
        
    - 如果已经激活了 Rights Management 服务，然后决定管理自己的租户密钥，用户将逐渐从旧租户密钥迁移到新租户密钥。 这种交错式转换可能需要花费几周才能完成。 受旧租户密钥保护的文档和文件仍然可供授权用户访问。
        
2. 请考虑启用使用日志记录，该功能记录了 Azure Rights Management 服务执行的每一个事务。
    
    如果你决定自行管理租户密钥，则日志记录包括租户密钥的使用信息。 请参阅显示在 Excel 中的日志文件的以下代码段，其中 **KeyVaultDecryptRequest** 和 **KeyVaultSignRequest** 请求类型显示该租户密钥正在使用中。
    
    ![正在使用租户密钥的 Excel 格式日志文件](./media/RMS_Logging.png)
    
    有关使用情况日志记录的详细信息，请参阅[记录和分析 Azure 权限管理服务的使用情况](./log-analyze-usage.md)。
    
3.  管理你的租户密钥。
    
    有关针对租户密钥的生命周期操作的详细信息，请参阅[针对 Azure 信息保护租户密钥的操作](./operations-tenant-key.md)。
