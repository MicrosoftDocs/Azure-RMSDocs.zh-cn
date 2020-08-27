---
title: 创建自己的密钥 (BYOK) 详细信息-Azure 信息保护
description: 当你使用客户管理的密钥 (称为 "自带密钥"）或使用 Azure 信息保护) BYOK 时，请了解详细信息和限制。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3e25ff7d202b7cef964f6b83259b4ff2588c2616
ms.sourcegitcommit: 2cb5fa2a8758c916da8265ae53dfb35112c41861
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953161"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>自带密钥 (BYOK Azure 信息保护) 详细信息

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

使用 Azure 信息保护订阅的组织可以选择使用自己的密钥（而不是由 Microsoft 生成的默认密钥）来配置其租户。 此配置通常称为创建自己的密钥 (BYOK) 。

BYOK 和 [使用情况日志记录](log-analyze-usage.md) 与 Azure 信息保护使用的 azure Rights Management 服务集成的应用程序无缝协作。

支持的应用程序包括：

- **云服务，** 例如 Microsoft SharePoint 或 Office 365

- **本地服务** ，运行通过 RMS 连接器使用 Azure Rights Management 服务的 Exchange 和 SharePoint 应用程序

- **客户端应用程序，** 例如 office 2019、office 2016 和 office 2013

> [!TIP]
> 如果需要，使用其他本地密钥向特定文档应用附加安全性。 有关详细信息，请参阅 [保存你自己的密钥 (HYOK) 保护](configure-adrms-restrictions.md) (经典客户端) 或 [双重密钥加密 (DKE) protection](plan-implement-tenant-key.md#double-key-encryption-dke-aip-unified-labeling-client-only)。
> 

## <a name="azure-key-vault-key-storage"></a>Azure Key Vault 密钥存储

客户生成的密钥必须存储在 Azure Key Vault 中，BYOK 保护。

> [!NOTE]
> 在 Azure Key Vault 中使用受 HSM 保护的密钥需要 [Azure Key Vault 高级服务层](https://azure.microsoft.com/pricing/details/key-vault/)，这会产生额外的月度订阅费用。

### <a name="sharing-key-vaults-and-subscriptions"></a>共享密钥保管库和订阅

建议为租户密钥使用 **专用密钥保管库** 。 专用密钥保管库有助于确保其他服务的调用不会导致超出 [服务限制](https://docs.microsoft.com/azure/key-vault/general/service-limits) 。 超过存储你的租户密钥的密钥保管库的服务限制可能会导致 Azure Rights Management 服务的响应时间限制。

随着不同服务具有不同的密钥管理要求，Microsoft 还建议对密钥保管库使用 **专用的 Azure 订阅** 。 专用 Azure 订阅：

- 帮助防范配置错误

- 如果不同的服务具有不同的管理员，则更安全

若要与使用 Azure Key Vault 的其他服务共享 Azure 订阅，请确保订阅共享一组公共管理员。 确认使用该订阅的所有管理员对他们可以访问的每个密钥都有一定的了解，这意味着它们不太可能 misconfigure 你的密钥。

**示例：** 在 Azure 信息保护租户密钥的管理员与管理 Office 365 客户密钥和 CRM online 的密钥的人员相同时使用共享 Azure 订阅。 如果这些服务的关键管理员不同，则建议使用专用订阅。

### <a name="benefits-of-using-azure-key-vault"></a>使用 Azure 密钥保管库的好处

Azure Key Vault 为许多使用加密的基于云的服务和本地服务提供了一个集中且一致的密钥管理解决方案。

除管理密钥外，Azure 密钥保管库还为安全管理员提供其他使用加密的服务和应用程序的存储、访问、管理证书和机密（如密码）的相同管理体验。

在 Azure Key Vault 中存储你的租户密钥具有以下优势：

|优点  |描述  |
|---------|---------|
|**内置接口**| Azure 密钥保管库为密钥管理提供了大量内置接口，包括 PowerShell、CLI、REST API 和 Azure 门户。 </br></br>其他服务和工具已与 Key Vault 集成，以实现特定任务（例如监视）的优化功能。 </br></br>例如，使用 Operations Management Suite Log analytics 分析密钥使用情况日志，在满足指定条件时设置警报，等等。        |
|**角色分隔**| Azure Key Vault 提供角色分隔作为公认的安全最佳做法。 </br></br>角色分隔确保 Azure 信息保护管理员可以重点关注其最高优先级，包括管理数据分类和保护，以及针对特定安全性或符合性要求的加密密钥和策略。 |
|**主密钥位置**| Azure Key Vault 在各种不同的位置提供，并支持具有主密钥可以使用的限制的组织。 </br></br>有关详细信息，请参阅 Azure 网站上的[可用产品（按区域）](https://azure.microsoft.com/regions/services/)页。|
|**分隔的安全域**|Azure Key Vault 对其数据中心使用单独的安全域，如北美、EMEA (欧洲、中东和非洲) 以及亚洲等区域。 </br></br>Azure Key Vault 还使用 Azure 的其他实例，如 Microsoft Azure 德国和 Azure 政府。 |
|**统一体验**| Azure Key Vault 还允许安全管理员存储、访问和管理证书和机密（如密码），以便使用加密的其他服务。 <br></br>使用租户密钥的 Azure Key Vault 为管理这些元素的管理员提供无缝的用户体验。|

若要了解最新更新并了解其他服务如何使用  [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/basic-concepts)，请访问 [Azure Key Vault 团队博客](https://blogs.technet.microsoft.com/kv/)。

## <a name="usage-logging-for-byok"></a>BYOK 的使用情况日志记录

使用情况日志由向 Azure Rights Management 服务发出请求的每个应用程序生成。

尽管使用日志记录是可选的，但我们建议使用 Azure 信息保护中的近乎实时的使用日志，以便准确了解你的租户密钥的使用方式和时间。

有关 BYOK 的密钥使用日志记录的详细信息，请参阅 [记录和分析 Azure 信息保护中的保护使用情况](log-analyze-usage.md)。

> [!TIP]
> 为了进一步保证，可以通过 [Azure Key Vault 日志记录](https://docs.microsoft.com/azure/key-vault/general/logging)交叉引用 Azure 信息保护使用情况日志记录。 Key Vault 日志提供一种可靠的方法，用于独立监视密钥仅由 Azure Rights Management 服务使用。
>
> 如有必要，请通过删除对密钥保管库的权限立即撤销对密钥的访问权限。

## <a name="options-for-creating-and-storing-your-key"></a>用于创建和存储密钥的选项

BYOK 支持在 Azure Key Vault 或本地创建的密钥。

如果在本地创建密钥，则必须将其传输到 Key Vault，并将 Azure 信息保护配置为使用该密钥。 在 Azure Key Vault 中执行任何其他密钥管理。

用于创建和存储自己的密钥的选项：

- **在 Azure Key Vault 中创建的。** 在 Azure Key Vault 中创建密钥并将其存储为 HSM 保护的密钥或软件保护的密钥。

- **在本地创建。** 使用以下选项之一在本地创建密钥，并将其传输到 Azure Key Vault：

    - **受 HSM 保护的密钥，作为 HSM 保护的密钥传输。** 最典型的选择方法。

        尽管此方法的管理开销最大，你的组织可能需要遵守特定的法规。 Azure Key Vault 使用的 Hsm 是验证了 FIPS 140-2 级别2的 Hsm。

    - **受软件保护的密钥，转换和传输为 Azure Key Vault 为 HSM 保护的密钥。** 仅当 [从 Active Directory Rights Management Services (AD RMS) 进行迁移 ](migrate-from-ad-rms-to-azure-rms.md)时，才支持此方法。

    - **作为受软件保护的密钥在本地创建，并作为受软件保护的密钥传输到 Azure Key Vault。** 此方法需要。PFX 证书文件。

例如，执行以下操作以使用在本地创建的密钥：

1. 根据组织的 IT 和安全策略，在本地生成租户密钥。 此密钥是主副本。 它保留在本地，并且你需要进行备份。

1. 创建主密钥的副本，并将其从 HSM 安全传输到 Azure Key Vault。 在此过程中，密钥的主副本永远不会保留硬件保护边界。

传输完成后，密钥副本将受到 Azure Key Vault 保护。

## <a name="exporting-your-trusted-publishing-domain"></a>导出受信任的发布域

如果你决定停止使用 Azure 信息保护，则需要 (TPD) 的可信发布域来解密受 Azure 信息保护保护的内容。

但是，如果你对 Azure 信息保护密钥使用 BYOK，则不支持导出你的 TPD。

若要为此方案做好准备，请确保预先创建适当的 TPD。 有关详细信息，请参阅 [如何准备 Azure 信息保护 "云退出" 计划](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631)。

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>为 Azure 信息保护租户密钥实现 BYOK

使用以下步骤实现 BYOK：

1. [查看 BYOK 先决条件](#prerequisites-for-byok)
1. [选择 Key Vault 位置](#choosing-your-key-vault-location)
1. [创建和配置密钥](#create-and-configure-your-key)

### <a name="prerequisites-for-byok"></a>BYOK 的先决条件

根据系统配置的不同，BYOK 必备组件会有所不同。 根据需要验证系统是否满足以下先决条件：

|要求  |说明  |
|---------|---------|
|**Azure 订阅**     |所有配置都需要。 </br>有关详细信息，请参阅 [验证是否有与 BYOK 兼容的 Azure 订阅](#verifying-that-you-have-a-byok-compatible-azure-subscription)。         |
|**适用于 Azure 信息保护的 AIPService PowerShell 模块**|所有配置都需要。 </br>有关详细信息，请参阅 [安装 AIPService PowerShell 模块](./install-powershell.md)。|
|**Azure Key Vault BYOK 的先决条件** | 如果使用的是在本地创建的、受 HSM 保护的密钥，请确保还符合 Azure Key Vault 文档中列出的 [BYOK 的先决条件](https://docs.microsoft.com/azure/key-vault/keys/hsm-protected-keys-byok#prerequisites) 。         |
|**Thales 固件版本11.62**    |如果要使用软件密钥到硬件密钥从 AD RMS 迁移到 Azure 信息保护，则必须具有 Thales 固件版本11.62，并将 Thales 固件用于 HSM。
|**受信任的 Microsoft 服务的防火墙旁路** |如果包含你的租户密钥的密钥保管库使用 Azure Key Vault 的虚拟网络服务终结点，则必须允许受信任的 Microsoft 服务跳过此防火墙。 </br>有关详细信息，请参阅 [Azure Key Vault 虚拟网络服务终结点](https://docs.microsoft.com/azure/key-vault/general/overview-vnet-service-endpoints)。       |

#### <a name="verifying-that-you-have-a-byok-compatible-azure-subscription"></a>验证你是否有与 BYOK 兼容的 Azure 订阅

你的 Azure 信息保护租户必须具有 Azure 订阅。 如果还没有帐户，可以注册一个 [免费帐户](https://azure.microsoft.com/pricing/free-trial/)。 但是，若要使用受 HSM 保护的密钥，必须具有 Azure Key Vault 高级服务层。

免费 Azure 订阅提供对 Azure Active Directory 配置和 Azure Rights Management 自定义模板配置的访问权限 *不足以* 使用 Azure Key Vault。

若要确认是否有与 BYOK 兼容的 Azure 订阅，请执行以下操作以使用 [Azure PowerShell](https://docs.microsoft.com/powershell/azure/) cmdlet 进行验证：

1. 以管理员身份启动 Azure PowerShell 会话。

1. 使用作为 Azure 信息保护租户的全局管理员登录 `Connect-AzAccount` 。

1. 将显示的令牌复制到剪贴板。 然后，在浏览器中转到， https://microsoft.com/devicelogin 然后输入复制的令牌。

    有关详细信息，请参阅 [登录 Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps)。

1. 在 PowerShell 会话中，输入 `Get-AzSubscription` 并确认显示以下值：

    - 订阅名称和 ID
    - 你的 Azure 信息保护租户 ID
    - 确认状态已启用

    如果未显示任何值并且返回到提示，则没有可用于 BYOK 的 Azure 订阅。

### <a name="choosing-your-key-vault-location"></a>选择密钥保管库位置

创建密钥保管库以包含要用作 Azure 信息的租户密钥的密钥时，必须指定一个位置。 此位置为 Azure 区域或 Azure 实例。

首先使选择满足合规性，然后在最大程度上降低网络延迟：

- 如果出于合规性原因选择了 BYOK 密钥方法，则这些符合性要求还可能会规定哪些 Azure 区域或实例可用于存储 Azure 信息保护租户密钥。

- 保护链对 Azure 信息保护密钥的所有加密调用。 因此，你可能需要在 Azure 信息保护租户所在的同一 Azure 区域或实例中创建密钥保管库，以最大程度地减少所需的网络延迟。

若要确定 Azure 信息保护租户的位置，请使用 [AipServiceConfiguration](https://docs.microsoft.com/powershell/module/aipservice/get-aipserviceconfiguration) PowerShell cmdlet 并标识 url 中的区域。 例如：

```ps
LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing
```
    
可以从 rms.na.aadrm.com 中标识区域，在此示例中，它位于北美****。

下表列出了建议用于将网络延迟降到最低的 Azure 区域和实例：

|Azure 区域或实例|建议的密钥保管库位置|
|---------------|--------------------|
|rms.**na**.aadrm.com|美国中北部或美国东部********|
|rms.**eu**.aadrm.com|**北欧** 或 **西欧**|
|rms.**ap**.aadrm.com|**东亚** 或 **东南亚**|
|rms.**sa**.aadrm.com|美国西部或美国东部********|
|rms.**govus**.aadrm.com|美国中部或美国东部 2********|
|**aadrm.us**|**US Gov 弗吉尼亚州** 或 **US Gov 亚利桑那州**|
|**aadrm.cn**|“中国东部 2”或“中国北部 2” |

### <a name="create-and-configure-your-key"></a>创建和配置密钥

创建一个 Azure Key Vault 和要用于 Azure 信息保护的密钥。 有关详细信息，请参阅 [Azure Key Vault 文档](https://docs.microsoft.com/azure/key-vault/)。

请注意以下事项：配置 BYOK 的 Azure Key Vault 和密钥：

- [密钥长度要求](#key-length-requirements)
- [在本地创建受 HSM 保护的密钥并将其传输到密钥保管库](#creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault)
- [配置具有密钥 ID 的 Azure 信息保护](#configuring-azure-information-protection-with-your-key-id)
- [授权 Azure Rights Management 服务使用你的密钥](#authorizing-the-azure-rights-management-service-to-use-your-key)

#### <a name="key-length-requirements"></a>密钥长度要求

创建密钥时，请确保密钥长度为2048位 (建议) 或1024位。 Azure 信息保护不支持其他的密钥长度。

> [!NOTE]
> 1024位密钥不被视为为活动租户密钥提供足够的保护级别。
>
>Microsoft 不允许使用较小的密钥长度，例如1024位的 RSA 密钥，以及用于提供不充分保护级别的协议的关联用途，如 SHA-1。
>

#### <a name="creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault"></a>在本地创建受 HSM 保护的密钥并将其传输到密钥保管库

若要在本地创建 HSM 保护的密钥并将其作为 HSM 保护的密钥传输到密钥保管库，请按照 Azure Key Vault 文档中的过程进行操作： [如何为 Azure Key Vault 生成和传输受 hsm 保护的密钥](https://docs.microsoft.com/azure/key-vault/keys/hsm-protected-keys-byok)。

要使 Azure 信息保护使用传输密钥，必须允许对密钥执行所有 Key Vault 操作，包括：

- encrypt
- 解密
- wrapKey
- unwrapKey
- 签名
- 验证

默认情况下，所有 Key Vault 操作都是允许的。

若要检查特定密钥的允许操作，请运行以下 PowerShell 命令：

```ps
(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps
```

如有必要，请使用 [AzKeyVaultKey](https://docs.microsoft.com/powershell/module/az.keyvault/update-azkeyvaultkey) 和 *KeyOps* 参数添加允许的操作。

#### <a name="configuring-azure-information-protection-with-your-key-id"></a>配置具有密钥 ID 的 Azure 信息保护

存储在 Azure Key Vault 中的密钥具有密钥 ID。

密钥 ID 是包含密钥保管库名称、密钥容器、密钥名称和密钥版本的 URL。 例如：

**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**.

通过指定密钥保管库 URL，将 Azure 信息保护配置为使用你的密钥。

#### <a name="authorizing-the-azure-rights-management-service-to-use-your-key"></a>授权 Azure Rights Management 服务使用你的密钥

必须授权 Azure Rights Management 服务使用你的密钥。 Azure Key Vault 管理员可以使用 Azure 门户或 Azure PowerShell 启用此授权。

##### <a name="enabling-key-authorization-using-the-azure-portal"></a>使用 Azure 门户启用密钥授权

1. 登录到 Azure 门户，然后访问**Key**vault  >  **\<*your key vault name*>**  >  **访问策略**"  >  **添加新**项"。

1. 在 " **添加访问策略** " 窗格中，从 " **配置自模板 (可选) ** 列表框中，选择" **AZURE 信息保护**"" BYOK "，然后单击 **" 确定 "**。

    所选模板具有以下配置：

    - **选择主体**值设置为**Microsoft Rights Management Services。**
    - 所选的 **密钥权限** 包括 **获取、** **解密** 和 **签名。**

##### <a name="enabling-key-authorization-using-powershell"></a>使用 PowerShell 启用密钥授权

使用 GUID **00000012-0000-0000-c000-000000000000**运行 Key Vault PowerShell cmdlet [AzKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)，并向 Azure Rights Management 服务主体授予权限。

例如：

```ps
Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get
```

### <a name="configure-azure-information-protection-to-use-your-key"></a>配置 Azure 信息保护以使用密钥

完成上述所有步骤后，即可将 Azure 信息保护配置为使用此密钥作为你的组织的租户密钥。

使用 Azure RMS cmdlet 运行以下命令：

1. 连接到 Azure Rights Management 服务并登录：
    ```ps
    Connect-AipService
    ```

1. 运行 [AipServiceKeyVaultKey cmdlet](https://docs.microsoft.com/powershell/module/aipservice/use-aipservicekeyvaultkey)，并指定密钥 URL。 例如：

    ```ps
    Use-AipServiceKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/<key-version>"
    ```

    > [!IMPORTANT]
    > 在此示例中， `<key-version>` 是要使用的密钥的版本。 如果未指定版本，则默认情况下将使用该密钥的当前版本，该命令可能会显示为 "正在运行"。 但是，如果以后更新或续订了密钥，则即使再次运行 **AipServiceKeyVaultKey** 命令，Azure Rights Management 服务也会停止适用于你的租户。
    >
    > 根据需要使用 [AzKeyVaultKey](https://docs.microsoft.com/powershell/module/az.keyvault/get-azkeyvaultkey) 命令来获取当前密钥的版本号。
    >
    > 例如：`Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

    若要确认正确设置了 Azure 信息保护的密钥 URL，请在 Azure Key Vault 中运行 [AzKeyVaultKey](https://docs.microsoft.com/powershell/module/az.keyvault/get-azkeyvaultkey) 命令以显示密钥 url。

1. 如果已激活 Azure Rights Management 服务，请运行 [AipServiceKeyProperties](https://docs.microsoft.com/powershell/module/aipservice/set-aipservicekeyproperties) ，告知 Azure 信息保护将此密钥用作 azure Rights Management 服务的活动租户密钥。

Azure 信息保护现在已配置为使用你的密钥，而不是为你的租户自动创建的默认 Microsoft 创建的密钥。

## <a name="next-steps"></a>后续步骤
配置 BYOK protection 后，请继续 [使用租户根密钥入门](get-started-tenant-root-keys.md) ，了解有关使用和管理密钥的详细信息。
