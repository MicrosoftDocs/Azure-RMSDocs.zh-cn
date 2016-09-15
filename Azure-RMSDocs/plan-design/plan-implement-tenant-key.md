---
title: "计划和实现你的 Azure Rights Management 租户密钥 | Azure RMS"
description: "此信息有助于规划和管理 Azure RMS 的 Rights Management (RMS) 租户密钥。 例如，为了遵守组织的具体规定，你不能让 Microsoft 管理你的租户密钥（默认设置），而想要自行管理租户密钥。 自行管理租户密钥也称为自带密钥 (BYOK)。"
author: cabailey
manager: mbaldwin
ms.date: 09/01/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: eec7cc8b20435df11d7b8f89c4b9e9d0f039dc55
ms.openlocfilehash: 25d47ab488474ed756b3139bb9d42d420cea25f7


---

# 计划和实现你的 Azure Rights Management 租户密钥

>*适用于：Azure Rights Management、Office 365*

使用本文章中的信息，帮助规划和管理 Azure RMS 的 Rights Management (RMS) 租户密钥。 例如，为了遵守组织的具体规定，你不能让 Microsoft 管理你的租户密钥（默认设置），而想要自行管理租户密钥。  自行管理租户密钥也称为自带密钥 (BYOK)。

> [!NOTE]
> RMS 租户密钥也称为服务器许可方证书 (SLC) 密钥。 Azure RMS 为订阅 Azure RMS 的每个组织维护一个或多个密钥。 只要将密钥用于组织内部的 RMS（例如用户密钥、计算机密钥、文档加密密钥），它们将通过加密方式链接到你的 RMS 租户密钥。

**概览：** 参考下表来快速了解建议的租户密钥拓扑。 然后，阅读其他文档以获取详细信息。

如果你使用 Microsoft 管理的租户密钥部署 Azure RMS，则你以后可以改为使用 BYOK。 但是，目前你无法将 Azure RMS 租户密钥从 BYOK 改为由 Microsoft 管理。

|业务要求|建议的租户密钥拓扑|
|------------------------|-----------------------------------|
|快速部署 Azure RMS，而无需特殊硬件|由 Microsoft 管理|
|需要装有 Azure RMS 的 Exchange Online 中的完整 IRM 功能|由 Microsoft 管理|
|你的密钥由你自己创建，并在硬件安全模块 (HSM) 中受保护|BYOK<br /><br />目前，此配置将导致 Exchange Online 中的 IRM 功能降低。 有关详细信息，请参阅 [BYOK 定价和限制](byok-price-restrictions.md)。|

## 选择你的租户密钥拓扑：由 Microsoft 管理（默认设置）或由你管理 (BYOK)
确定哪种租户密钥拓扑最适合你的组织。 默认情况下，Azure RMS 生成你的租户密钥，并管理租户密钥生命周期的大多数方面。 这是最简单的选项，管理开销最低。 大多数情况下，你甚至不需要知道自己有租户密钥。 你只需注册 Azure RMS，密钥管理过程的剩余部分将由 Microsoft 处理。

或者，你可能希望通过使用 [Azure 密钥保管库](https://azure.microsoft.com/services/key-vault/)完全控制你的租户密钥。 此方案涉及到创建你的租户密钥并将主控副本保存在本地。 这种方案通常称为自带密钥 (BYOK)。 使用这种选项的过程如下：

1.  根据 IT 策略和安全策略在本地生成租户密钥。

2.  使用 Azure 密钥保管库将租户密钥从自己掌握的硬件安全模块 (HSM) 安全传送到由 Microsoft 拥有和管理的 HSM。 整个过程中，你的租户密钥从未离开硬件保护范围。

3.  当你将租户密钥传送到 Microsoft 时，它始终处于 Azure 密钥保管库保护下。

虽然这是可选的，但你可能希望使用 Azure RMS 提供的接近实时的使用日志，以便准确了解你的租户密钥的使用时间和方式。

> [!NOTE]
> 作为一种附加保护措施，Azure 密钥保管库在位于北美、EMEA（欧洲、中东和非州）和亚洲等地区的数据中心使用单独的安全域。 对于 Azure 的其他实例，如 Microsoft Azure 德国和 Azure 政府。 当你管理自己的租户密钥时，它将关联到你的 RMS 租户注册所在地区或实例的安全域。 例如，欧洲客户的租户密钥无法在北美或亚洲的数据中心使用。

## 租户密钥生命周期
如果你决定由 Microsoft 管理你的租户密钥，Microsoft 将处理大多数密钥生命周期操作。 但是，如果你决定自行管理租户密钥，则要负责 Azure 密钥保管库中的很多密钥生命周期操作，以及其他一些过程。

下图显示和比较了这两个选项。 第一张图显示在由 Microsoft 管理租户密钥的默认配置中，管理员开销非常低。

![Azure RMS 租户密钥生命周期 - 由 Microsoft 管理，默认设置](../media/RMS_BYOK_cloud.png)

第二张图显示当你自行管理租户密钥时需要的其他步骤。

![Azure RMS 租户密钥生命周期 - 由你管理，BYOK](../media/RMS_BYOK_onprem4.png)

如果你决定让 Microsoft 管理你的租户密钥，则除了生成密钥之外，再无需任何额外操作，你可以直接执行[后续步骤](plan-implement-tenant-key.md#next-steps)。  

如果你决定自行管理租户密钥，请阅读以下部分以获取更多信息。

## 实现你的 Azure Rights Management 租户密钥

如果你决定自行生成和管理租户密钥，请使用本部分中的信息和过程；“自带密钥”(BYOK) 方案：


> [!IMPORTANT]
> 如果已开始结合使用 Azure RMS 和由 Microsoft 管理的租户密钥，并且现在想要管理租户密钥（移动到 BYOK），则仍可以使用已存档密钥访问以前受保护的文档和电子邮件。 但是，如果有运行 Office 2010 的用户，请在运行这些过程之前先[联系 Microsoft 支持](../get-started/information-support.md#to-contact-microsoft-support)。 这些计算机将需要一些其他配置步骤。
> 
> 如果你的组织制定了关于密钥处理的特定策略，也[请与 Microsoft 支持部门联系](../get-started/information-support.md#to-contact-microsoft-support)。

### BYOK 的先决条件
有关自带密钥 (BYOK) 的先决条件列表，请参阅以下表格。

|要求|更多信息|
|---------------|--------------------|
|支持 Azure RMS 的订阅。|有关可用订阅的详细信息，请参阅[支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md)。|
|请不要使用个人 RMS 或 Exchange Online。 或者，如果你使用 Exchange Online，应了解并接受对此配置使用 BYOK 的限制。|有关 BYOK 当前限制的详细信息，请参阅 [BYOK 定价和限制](byok-price-restrictions.md)。<br /><br />**重要事项**：目前，BYOK 不兼容 Exchange Online。|
|为密钥保管库 BYOK 列出的所有先决条件。|请参阅 Azure 密钥保管库文档的 [Prequisites for BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok)（BYOK 的先决条件）。 <br /><br />**注意**：如果要使用软件密钥到硬件密钥从 AD RMS 迁移到 Azure RMS，必须拥有 Thales 固件的最低版本 11.62。|
|用于 Windows PowerShell 的 Azure RMS 管理模块。|有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。 <br /><br />如果你之前已安装了此 Windows PowerShell 模块，请运行以下命令来检查你的版本号是否至少为 **2.5.0.0**： `(Get-Module aadrm -ListAvailable).Version`|

有关 Thales HSM 及其如何与 Azure 密钥保管库一起使用的详细信息，请参阅 [Thales website](https://www.thales-esecurity.com/msrms/cloud)（Thales 网站）。

若要生成你自己的租户密钥并将其传送到 Azure 密钥保管库，请按照 Azure 密钥保管库文档 [How to generate and transfer HSM-protected keys for Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/)（如何为 Azure 密钥保管库生成和传输受 HSM 保护的密钥）中的过程。

将该密钥传送到密钥保管库时，将在密钥保管库中为其给定一个密钥 ID，这是一个包含保管库名称、密钥容器、密钥名称和密钥版本的 URL。 例如：**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**。 将需要通过指定此 URL 告知 Azure RMS 使用此密钥。

但是，在 Azure RMS 可以使用该密钥前，必须授权 Azure RMS 可以在你的组织的密钥保管库中使用该密钥。 若要执行此操作，Azure 密钥保管库管理员将使用密钥保管库 PowerShell cmdlet，[Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx) 并向 Azure RMS 服务主体 **Microsoft.Azure.RMS** 授予权限。 例如：

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign 

现在可开始配置 Azure RMS 以将此密钥用作你的组织的 Azure RMS 租户密钥。 使用 Azure RMS cmdlet，需首先连接到 Azure RMS，并登录：

    Connect-AadrmService

然后运行 [Use-AadrmKeyVaultKey cmdlet](https://msdn.microsoft.com/library/azure/mt759829.aspx)，指定密钥 URL。 例如：

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

如果需要确认在 Azure RMS 中正确设置了密钥 URL，可在 Azure 密钥保管库中运行 [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) 查看密钥 URL。


## 后续步骤

现在，你已经规划并根据需要生成了租户密钥，请执行以下操作：

1.  开始使用你的租户密钥：

    -   如果尚未开始使用，你必须立即启用权限管理，以便你的组织能够开始使用 RMS。 用户立即开始使用你的租户密钥（在 Azure 密钥保管库中由 Microsoft 管理或由你管理）。

        有关激活的详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。

    -   如果你已经激活了权限管理，然后决定自行管理租户密钥，用户将逐渐从旧租户密钥迁移到新租户密钥，这种交错式迁移可能需要花费几周才能完成。 受旧租户密钥保护的文档和文件仍然可供授权用户访问。

2.  请考虑启用使用日志记录，该功能记录了 Azure 权限管理执行的每一个事务。

    如果你决定自行管理租户密钥，则日志记录包括租户密钥的使用信息。 请参阅显示在 Excel 中的日志文件的以下代码段，其中 **KeyVaultDecryptRequest** 和 **KeyVaultSignRequest** 请求类型显示该租户密钥正在使用中。

    ![正在使用租户密钥的 Excel 格式日志文件](../media/RMS_Logging.png)

    有关使用日志记录的详细信息，请参阅[记录和分析 Azure Rights Management 使用情况](../deploy-use/log-analyze-usage.md)。

3.  维护你的租户密钥。

    有关详细信息，请参阅[你的 Azure Rights Management 租户密钥的操作](../deploy-use/operations-tenant-key.md)。




<!--HONumber=Sep16_HO1-->


