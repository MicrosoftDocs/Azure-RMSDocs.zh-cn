---
# required metadata

title: 计划和实现你的 Azure Rights Management 租户密钥 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 计划和实现你的 Azure Rights Management 租户密钥

*适用于：Azure Rights Management、Office 365*

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

或者，你可能希望完全控制自己的租户密钥，这就需要创建你的租户密钥，并将主副本保存在本地。 这种方案通常称为自带密钥 (BYOK)。 使用这种选项的过程如下：

1.  你根据 IT 策略在本地生成租户密钥。

2.  你将租户密钥从自己掌握的硬件安全模块 (HSM) 安全传送到由 Microsoft 拥有和管理的 HSM。 整个过程中，你的租户密钥从未离开硬件保护范围。

3.  当你将租户密钥传送到 Microsoft 时，它始终处于 Thales HSM 保护下。 Microsoft 与 Thales 进行了合作，确保你的租户密钥无法从 Microsoft 的 HSM 提取。

虽然这是可选的，但你可能希望使用 Azure RMS 提供的接近实时的使用日志，以便准确了解你的租户密钥的使用时间和方式。

> [!NOTE]
> 作为一种附加保护措施，Azure RMS 在位于北美、EMEA 地区（欧洲、中东和非州）和亚洲的数据中心使用单独的安全体系。 当你管理自己的租户密钥时，它将关联到你的 RMS 租户注册所在地区的安全体系。 例如，欧洲客户的租户密钥无法在北美或亚洲的数据中心使用。

## 租户密钥生命周期
如果你决定由 Microsoft 管理你的租户密钥，Microsoft 将处理大多数密钥生命周期操作。 但是，如果你决定自行管理租户密钥，则要负责很多密钥生命周期操作，以及其他一些过程。

下图显示和比较了这两个选项。 第一张图显示在由 Microsoft 管理租户密钥的默认配置中，管理员开销非常低。

![Azure RMS 租户密钥生命周期 - 由 Microsoft 管理，默认设置](../media/RMS_BYOK_cloud.png)

第二张图显示当你自行管理租户密钥时需要的其他步骤。

![Azure RMS 租户密钥生命周期 - 由你管理，BYOK](../media/RMS_BYOK_onprem.png)

如果你决定让 Microsoft 管理你的租户密钥，则除了生成密钥之外，再无需任何额外操作，你可以直接执行[后续步骤](plan-implement-tenant-key.md#next-steps)。

如果你决定自行管理租户密钥，请阅读以下部分以获取更多信息。

## 实现你的 Azure Rights Management 租户密钥

如果你决定自行生成和管理租户密钥，请使用本部分中的信息和过程；“自带密钥”(BYOK) 方案：


> [!IMPORTANT]
> 如果你已经开始使用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]（服务已激活），但有些用户在运行 Office 2010，则在运行这些过程之前，[请与 Microsoft 支持部门联系](../get-started/information-support#to-contact-microsoft-support)。 根据你的方案和要求，你仍然可以使用 BYOK，但会受到一些限制，或者需要执行一些额外步骤。
> 
> 如果你的组织制定了关于密钥处理的特定策略，也[请与 Microsoft 支持部门联系](../get-started/information-support#to-contact-microsoft-support)。

### BYOK 的先决条件
有关自带密钥 (BYOK) 的先决条件列表，请参阅以下表格。

|要求|更多信息|
|---------------|--------------------|
|支持 Azure RMS 的订阅。|有关可用订阅的详细信息，请参阅[支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md)。|
|请不要使用个人 RMS 或 Exchange Online。 或者，如果你使用 Exchange Online，应了解并接受对此配置使用 BYOK 的限制。|有关 BYOK 当前限制的详细信息，请参阅 [BYOK 定价和限制](byok-price-restrictions.md)。<br /><br />**重要事项**：目前，BYOK 不兼容 Exchange Online。|
|Thales HSM、智能卡和支持软件。<br /><br />**注意**：如果要使用软件密钥到硬件密钥从 AD RMS 迁移到 Azure RMS，必须拥有 Thales 驱动程序的最低版本 11.62。|你必须能够使用 Thales 硬件安全模块，并且掌握有关 Thales HSM 的基本操作知识。 有关兼容型号的列表，请参阅 [Thales 硬件安全模块](http://www.thales-esecurity.com/msrms/buy) ，如果你还没有 HSM，请及时购买。|
|如果你希望通过 Internet 传送租户密钥，而不是亲自前往美国 Redmond 传送租户密钥。 有 3 个要求：<br /><br />1：脱机 x64 工作站，Windows 操作系统版本最低为 Windows 7，Thales nShield 软件至少为版本 11.62。<br /><br />如果此工作站运行 Windows 7，则必须 [安装 Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702)。<br /><br />2：连接到 Internet 的工作站，Windows 操作系统版本最低为 Windows 7。<br /><br />3：USB 驱动器或其他便携式存储设备，至少拥有 16 MB 可用空间。|如果你亲自将租户密钥送到 Redmond，则不需要这些先决条件。<br /><br />出于安全原因，我们建议第一个工作站不要连接到网络。 但是，程序对此没有强制要求。<br /><br />注意：在接下来的说明中，此第一个工作站称为**未连接工作站**。<br /><br />此外，如果你的租户密钥用于生产网络，我们建议你使用第二个独立工作站来下载工具集和上载租户密钥。 但如果用于测试目的，你可以使用同一个工作站。<br /><br />注意：在接下来的说明中，此第二个工作站称为**连接 Internet 的工作站**。|

生成和使用自己的租户密钥的过程，具体取决于你是要通过 Internet 传送租户密钥还是亲自传送租户密钥：

-   **通过 Internet：** 这种方式需要一些额外配置步骤，例如下载并使用工具集和 Windows PowerShell cmdlet。 但是，你无需亲自前往 Microsoft 设施传送你的租户密钥。 通过以下方法维护安全性：

    -   你从脱机工作站生成租户密钥，这样可以减小攻击面。

    -   租户密钥使用“密钥交换密钥”(KEK) 进行了加密，这样在传送到 Azure RMS HSM 之前可以一直保持加密状态。 只有已加密版本的租户密钥才能离开原始工作站。

    -   你的租户密钥的一个工具集属性，该属性将你的租户密钥绑定到 Azure RMS 安全体系。 因此，在 Azure RMS HSM 收到和解密你的租户密钥之后，只有这些 HSM 能够使用该密钥。 你的租户密钥无法导出。 绑定由 Thales HSM 实施。

    -   用于加密你的租户密钥的“密钥交换密钥”(KEK) 在 Azure RMS HSM 内部生成，而且无法导出。 HSM 强制要求在 HSM 外部不能有 KEK 的明文版本。 此外，工具集包括来自 Thales 的证明，它证实 KEK 是无法导出的，在 Thales 制造的真品 HSM 内部生成。

    -   工具集还包括来自 Thales 的证明，它证实 Azure RMS 安全体系也在 Thales 制造的真品 HSM 上生成。 这样可向你证明 Microsoft 使用了真品硬件。

    -   Microsoft 使用单独的 KEK，而且在每个地理区域中使用独立的安全体系，这样可以确保你的租户密钥只能在对其进行加密的区域内的数据中心使用。 例如，欧洲客户的租户密钥无法在北美或亚洲的数据中心使用。

    > [!NOTE]
    > 你的租户密钥可在不受信任的计算机和网络之间安全传送，因为它进行了加密，并且通过访问控制级别权限得到保护，只能在你的 HSM 和 Microsoft 的用于 Azure RMS 的 HSM 内部使用。 你可以使用工具集中提供的脚本来验证安全措施，并且阅读 Thales 提供的此方面内容的详细信息： [RMS 云中的硬件密钥管理](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud)。

-   **亲自传送密钥：**这种方式要求你[与 Microsoft 支持部门联系](../get-started/information-support#to-contact-microsoft-support)来安排 Azure RMS 的密钥传送预约。 你必须亲自前往位于美国华盛顿州 Redmond 市的 Microsoft 办事处，将你的租户密钥传送到 Azure RMS 安全体系。

有关操作方法说明，请选择你将通过 Internet 生成和传送租户密钥，还是亲自传送租户密钥： 

- [通过 Internet](generate-tenant-key-internet.md)
- [亲自](generate-tenant-key-in-person.md)


## 后续步骤

现在，你已经规划并根据需要生成了租户密钥，请执行以下操作：

1.  开始使用你的租户密钥：

    -   如果尚未开始使用，你必须立即启用权限管理，以便你的组织能够开始使用 RMS。 用户立即开始使用你的租户密钥（由 Microsoft 管理或由你管理）。

        有关激活的详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。

    -   如果你已经激活了权限管理，然后决定自行管理租户密钥，用户将逐渐从旧租户密钥迁移到新租户密钥，这种交错式迁移可能需要花费几周才能完成。 受旧租户密钥保护的文档和文件仍然可供授权用户访问。

2.  请考虑启用使用日志记录，该功能可记录 RMS 执行的每一个事务。

    如果你决定自行管理租户密钥，则日志记录包括租户密钥的使用信息。 请参见在 Excel 中显示的以下日志文件示例，其中的 **Decrypt** 和 **SignDigest** 请求类型显示该租户密钥正在使用中。

    ![正在使用租户密钥的 Excel 格式日志文件](../media/RMS_Logging.gif)

    有关使用日志记录的详细信息，请参阅[记录和分析 Azure Rights Management 使用情况](../deploy-use/log-analyze-usage.md)。

3.  维护你的租户密钥。

    有关详细信息，请参阅[你的 Azure Rights Management 租户密钥的操作](../deploy-use/operations-tenant-key.md)。



<!--HONumber=Jun16_HO2-->


