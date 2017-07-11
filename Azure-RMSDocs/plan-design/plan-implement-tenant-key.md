---
title: "你的 Azure 信息保护租户密钥"
description: "此信息有助于规划和管理 Azure 信息保护租户密钥。 为了遵守适用于组织的特别规定，你可能想要自行管理租户密钥，而不是由 Microsoft 管理你的租户密钥（默认设置）。 自行管理租户密钥也称为自带密钥 (BYOK)。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e14a57a8bd8343113e2bfc3f71835f55f0ee2dee
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
<a id="planning-and-implementing-your-azure-information-protection-tenant-key" class="xliff"></a>

# 计划和实施 Azure 信息保护租户密钥

>*适用于：Azure 信息保护、Office 365*

使用此文章中的信息可帮助你规划和管理 Azure 信息保护租户密钥。 例如，为了遵守组织的具体规定，你不能让 Microsoft 管理你的租户密钥（默认设置），而想要自行管理租户密钥。 自行管理租户密钥也称为自带密钥 (BYOK)。

> [!NOTE]
> Azure 信息保护租户密钥的本地等价物被称为服务器许可方证书 (SLC) 密钥。 Azure 信息保护为每个具有 Azure 信息保护订阅的组织维护了一个或多个密钥。 只要将密钥用于组织内部的 Azure 信息保护（例如用户密钥、计算机密钥、文档加密密钥），它们将通过加密方式链接到你的 Azure 信息保护租户密钥。

**概览：** 参考下表来快速了解建议的租户密钥拓扑。 然后，阅读其他文档以获取详细信息。

|业务要求|建议的租户密钥拓扑|
|------------------------|-----------------------------------|
|快速部署 Azure 信息保护，而无需特殊硬件|由 Microsoft 管理|
|需要装有 Azure Rights Management 服务的 Exchange Online 中的完整 IRM 功能|由 Microsoft 管理|
|你的密钥由你自己创建，并在硬件安全模块 (HSM) 中受保护|BYOK<br /><br />目前，此配置将导致 Exchange Online 中的 IRM 功能降低。 有关详细信息，请参阅 [BYOK 定价和限制](byok-price-restrictions.md)。|

如有需要，可以在部署后通过使用 [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) cmdlet 来更改租户密钥拓扑。


<a id="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok" class="xliff"></a>

## 选择你的租户密钥拓扑：由 Microsoft 管理（默认设置）或由你管理 (BYOK)
确定哪种租户密钥拓扑最适合你的组织。 默认情况下，Azure 信息保护生成你的租户密钥，并管理租户密钥生命周期的大多数方面。 这是最简单的选项，管理开销最低。 大多数情况下，你甚至不需要知道自己有租户密钥。 你只需注册 Azure 信息保护，密钥管理过程的剩余部分将由 Microsoft 处理。

或者，你可能希望通过使用 [Azure 密钥保管库](https://azure.microsoft.com/services/key-vault/)完全控制你的租户密钥。 此方案涉及到创建你的租户密钥并将主控副本保存在本地。 这种方案通常称为自带密钥 (BYOK)。 使用这种选项的过程如下：

1.  根据 IT 策略和安全策略在本地生成租户密钥。

2.  使用 Azure 密钥保管库将租户密钥从自己掌握的硬件安全模块 (HSM) 安全传送到由 Microsoft 拥有和管理的 HSM。 整个过程中，你的租户密钥从未离开硬件保护范围。

3.  当你将租户密钥传送到 Microsoft 时，它始终处于 Azure 密钥保管库保护下。

虽然这是可选的，但你可能希望使用 Azure 信息保护提供的接近实时的使用日志，以便准确了解租户密钥的使用时间和方式。

> [!NOTE]
> 作为一种附加保护措施，Azure 密钥保管库在位于北美、EMEA（欧洲、中东和非州）和亚洲等地区的数据中心使用单独的安全域。 对于 Azure 的其他实例，如 Microsoft Azure 德国和 Azure 政府。 管理自己的租户密钥时，它将关联到你的 Azure 信息保护租户注册所在地区或实例的安全域。 例如，欧洲客户的租户密钥无法在北美或亚洲的数据中心使用。

<a id="the-tenant-key-lifecycle" class="xliff"></a>

## 租户密钥生命周期
如果你决定由 Microsoft 管理你的租户密钥，Microsoft 将处理大多数密钥生命周期操作。 但是，如果你决定自行管理租户密钥，则要负责 Azure 密钥保管库中的很多密钥生命周期操作，以及其他一些过程。

下图显示和比较了这两个选项。 第一张图显示在由 Microsoft 管理租户密钥的默认配置中，管理员开销非常低。

![Azure 信息保护租户密钥生命周期 - 由 Microsoft 管理，默认设置](../media/RMS_BYOK_cloud.png)

第二张图显示当你自行管理租户密钥时需要的其他步骤。

![Azure 信息保护租户密钥生命周期 - 由你管理，BYOK](../media/RMS_BYOK_onprem4.png)

如果你决定让 Microsoft 管理你的租户密钥，则除了生成密钥之外，再无需任何额外操作，你可以直接执行[后续步骤](plan-implement-tenant-key.md#next-steps)。  

如果你决定自行管理租户密钥，请阅读以下部分以获取更多信息。

<a id="implementing-your-azure-information-protection-tenant-key" class="xliff"></a>

## 实施 Azure 信息保护租户密钥

如果你决定自行生成和管理租户密钥，请使用本部分中的信息和过程；“自带密钥”(BYOK) 方案：


> [!IMPORTANT]
> 如果已开始结合使用 Azure 信息保护和由 Microsoft 管理的租户密钥，并且现在想要管理租户密钥（移动到 BYOK），则仍可以使用已存档密钥访问以前受保护的文档和电子邮件。 但是，如果有运行 Office 2010 的用户，请在运行这些过程之前先[联系 Microsoft 支持](../get-started/information-support.md#to-contact-microsoft-support)。 这些计算机将需要一些其他配置步骤。
> 
> 如果你的组织制定了关于密钥处理的特定策略，也[请与 Microsoft 支持部门联系](../get-started/information-support.md#to-contact-microsoft-support)。

<a id="prerequisites-for-byok" class="xliff"></a>

### BYOK 的先决条件
有关自带密钥 (BYOK) 的先决条件列表，请参阅以下表格。

|要求|更多信息|
|---------------|--------------------|
|支持 Azure 信息保护的订阅。|有关可用订阅的详细信息，请参阅 Azure 信息保护[定价页](https://go.microsoft.com/fwlink/?LinkId=827589)。|
|不使用 Exchange Online。<br /><br /> 或者，如果你使用 Exchange Online，应了解并接受对此配置使用 BYOK 的限制。|有关 BYOK 当前限制的详细信息，请参阅 [BYOK 定价和限制](byok-price-restrictions.md)。<br /><br />**重要事项**：目前，BYOK 不兼容 Exchange Online。|
|为 Key Vault BYOK 列出的所有先决条件，其中包括现有 Azure 信息保护租户的付费或试用版 Azure 订阅。 |请参阅 Azure 密钥保管库文档中的 [Prerequisites for BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok)（BYOK 的先决条件）。 <br /><br /> 免费的 Azure 订阅提供相应的访问权限，可配置 Azure Active Directory 以及 Azure 权限管理自定义模板（**可访问 Azure Active Directory**），但不足以使用 Azure 密钥保管库。 若要确认拥有可用于 BYOK 的 Azure 订阅，请使用 [Azure Resource Manager](https://msdn.microsoft.com/library/azure/mt786812\(v=azure.300\).aspx) PowerShell cmdlet： <br /><br /> 1.若要启动 Azure PowerShell 会话，请选择“以管理员身份运行”选项，并使用以下命令以 Azure 信息保护租户的全局管理员身份登录：`Login-AzureRmAccount`<br /><br />2.键入以下命令，并确认可以看到显示了订阅名称和 ID 以及 Azure 信息保护租户 ID 的值，并且状态为“已启用”：`Get-AzureRmSubscription`<br /><br />如果没有显示任何值，并且返回到提示，则表示没有可用于 BYOK 的 Azure 订阅。 <br /><br />**注意**：如果要使用软件密钥到硬件密钥从 AD RMS 迁移到 Azure 信息保护，则除 BYOK 先决条件以外，必须拥有最低版本为 11.62 的 Thales 固件。|
|适用于 Windows PowerShell 的 Azure Rights Management 管理模块。|有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。 <br /><br />如果之前已安装了此 Windows PowerShell 模块，请运行以下命令检查版本号是否高于或等于 **2.9.0.0**：`(Get-Module aadrm -ListAvailable).Version`|

有关 Thales HSM 及其如何与 Azure 密钥保管库一起使用的详细信息，请参阅 [Thales website](https://www.thales-esecurity.com/msrms/cloud)（Thales 网站）。

<a id="instructions-for-byok" class="xliff"></a>

### BYOK 的说明

若要生成你自己的租户密钥并将其传送到 Azure 密钥保管库，请按照 Azure 密钥保管库文档 [How to generate and transfer HSM-protected keys for Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/)（如何为 Azure 密钥保管库生成和传输受 HSM 保护的密钥）中的过程。

将该密钥传送到密钥保管库时，将在密钥保管库中为其给定一个密钥 ID，这是一个包含密钥保管库名称、密钥容器、密钥名称和密钥版本的 URL。 例如：**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**。 你将需要通过指定此 URL 命令 Azure 信息保护中的 Azure Rights Management 服务使用此密钥。

但在 Azure 信息保护可以使用此密钥之前，必须授权 Azure Rights Management 服务在你组织的密钥保管库中使用该密钥。 为此，Azure Key Vault 管理员将使用 Key Vault PowerShell cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy)，并通过使用 GUID 00000012-0000-0000-c000-000000000000 向 Azure 权限管理服务主体授予权限。 例如：

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

现在可开始配置 Azure 信息保护以将此密钥用作你的组织的 Azure 信息保护租户密钥。 使用 Azure RMS cmdlet，首先连接到 Azure Rights Management 服务，并登录：

    Connect-AadrmService

然后运行 [Use-AadrmKeyVaultKey cmdlet](/powershell/module/aadrm/use-aadrmkeyvaultkey)，指定密钥 URL。 例如：

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> 在此示例中，“aaaabbbbcccc111122223333”是要使用的密钥版本。 如果不指定版本，则将使用当前版本的密钥而不发出警告，并且显示命令以进行工作。 但是，如果后来对密钥保管库中的密钥进行了更新（已续订），则即使你再次运行 Use-AadrmKeyVaultKey 命令，Azure Rights Management 服务也将停止为你的租户工作。
>
>在运行此命令时，除了密钥名称外，请确保还指定了密钥版本。 可以使用 Azure 密钥保管库 cmd [Get-AzureKeyVaultKey](/powershell/resourcemanager/azurerm.keyvault\get-azurekeyvaultkey) 来获取当前密钥的版本号。 例如： `Get-AzureKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

如果需要确认在 Azure RMS 服务中是否正确设置了密钥 URL，可在 Azure 密钥保管库中运行 [Get-AzureKeyVaultKey](/powershell/resourcemanager/azurerm.keyvault\get-azurekeyvaultkey) 查看密钥 URL。

最后，如果已激活 Azure 权限管理服务，请运行 [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) 以告诉 Azure 权限管理将此密钥用作 Azure 权限管理服务的活动租户密钥。 如果不执行此步骤，Azure 权限管理则将继续使用激活服务时自动创建的默认的 Microsoft 托管密钥。


<a id="next-steps" class="xliff"></a>

## 后续步骤

现在，你已经规划并根据需要生成了租户密钥，请执行以下操作：

1.  开始使用你的租户密钥：
    
    - 如果尚未开始使用，则必须立即激活 Rights Management 服务，以便你的组织能够开始使用 Azure 信息保护。 用户立即开始使用你的租户密钥（在 Azure 密钥保管库中由 Microsoft 管理或由你管理）。
    
        有关激活的详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。
        
    - 如果你已经激活了 Rights Management 服务，然后决定自行管理租户密钥，用户将逐渐从旧租户密钥迁移到新租户密钥，这种交错式迁移可能需要花费几周才能完成。 受旧租户密钥保护的文档和文件仍然可供授权用户访问。
        
2. 请考虑启用使用日志记录，该功能记录了 Azure Rights Management 服务执行的每一个事务。
    
    如果你决定自行管理租户密钥，则日志记录包括租户密钥的使用信息。 请参阅显示在 Excel 中的日志文件的以下代码段，其中 **KeyVaultDecryptRequest** 和 **KeyVaultSignRequest** 请求类型显示该租户密钥正在使用中。
    
    ![正在使用租户密钥的 Excel 格式日志文件](../media/RMS_Logging.png)
    
    有关使用情况日志记录的详细信息，请参阅[记录和分析 Azure 权限管理服务的使用情况](../deploy-use/log-analyze-usage.md)。
    
3.  维护你的租户密钥。
    
    有关详细信息，请参阅[你的 Azure Rights Management 租户密钥的操作](../deploy-use/operations-tenant-key.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
