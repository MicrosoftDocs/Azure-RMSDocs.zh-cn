---
title: 从 AD RMS 迁移到 Azure 信息保护 - 第 4 阶段
description: 从 AD RMS 迁移到 Azure 信息保护的第 4 阶段包括从 AD RMS 迁移到 Azure 信息保护的步骤 8 至 9
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e7431ebdf016b89e1750b833dc4fca2d9646b195
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316715"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>迁移第 4 阶段 - 支持服务配置

>*适用于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的第 4 阶段。 这些过程包括[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 8-9。

## <a name="step-8-configure-irm-integration-for-exchange-online"></a>步骤 8。 为 Exchange Online 配置 IRM 集成

> [!IMPORTANT]
> 你无法控制迁移的用户可能会选择哪些收件人来查看受保护的电子邮件。
>
> 因此，请确保组织中的所有用户和启用邮件的组都在 Azure AD 中有一个可与 Azure 信息保护一起使用的帐户。
>
> 有关详细信息，请参阅[准备用户和组以便使用 Azure 信息保护](prepare.md)。

无论选择哪种 Azure 信息保护租户密钥拓扑，请执行以下操作：

1. **先决条件**：为了使 Exchange Online 能够解密受 AD RMS 保护的电子邮件，需要知道群集的 AD RMS URL 对应于租户中可用的密钥。 

    这是通过 AD RMS 群集的 DNS SRV 记录完成，此记录还用于将 Office 客户端重新配置为使用 Azure 信息保护。 

    如果未在 [步骤 7](migrate-from-ad-rms-phase3.md#step-7-reconfigure-windows-computers-to-use-azure-information-protection)中创建用于客户端重新配置的 DNS SRV 记录，请立即创建此记录以支持 Exchange Online。 [说明](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    此 DNS 记录就位后，使用 Outlook 网页版和移动电子邮件客户端的用户便能在这些应用中查看受 AD RMS 保护的电子邮件，并且 Exchange 可以使用你从 AD RMS 导入的密钥，对已受 AD RMS 保护的内容执行解密、编制索引、日志记录和保护操作。  

1. **运行 Exchange Online [set-irmconfiguration](/powershell/module/exchange/get-irmconfiguration) 命令。** 

    如需运行此命令的帮助，请参阅 [Exchange Online：IRM 配置](configure-office365.md#exchangeonline-irm-configuration)中的分步说明。
    
    在输出中，检查“AzureRMSLicensingEnabled”是否设置为“True”：
    
    - 如果将 **AzureRMSLicensingEnabled** 设置为 **True**，则此步骤不需要进一步的配置。 
    
    - 如果 **AzureRMSLicensingEnabled** 设置为 **False**，请运行， `Set-IRMConfiguration -AzureRMSLicensingEnabled $true` 然后确认 Exchange Online 现在已准备好使用 Azure Rights Management 服务。 
    
        有关详细信息，请参阅 [基于 Azure 信息保护构建的新 Microsoft 365 消息加密功能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)中的验证步骤。

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>步骤 9. 为 Exchange Server 和 SharePoint Server 配置 IRM 集成

如果已使用 AD RMS 的 Exchange Server 或 SharePoint Server (IRM) 功能 Rights Management 的信息，则需要部署 Rights Management (RMS) 连接器。

连接器充当通信接口， (本地服务器和 Azure 信息保护的保护服务之间的中继) 。

此步骤包括安装和配置连接器、对 Exchange 和 SharePoint 禁用 IRM，以及配置这些服务器以使用该连接器。 

最后，如果已导入用于保护中的电子邮件的 AD RMS .xml 数据文件，则必须手动编辑 Exchange Server 计算机上的注册表，将所有受信任的发布域 Url 重定向到 RMS 连接器。

> [!NOTE]
> 在开始之前，请从[支持 Azure RMS 的本地服务器](requirements.md#supported-on-premises-servers-for-azure-rights-management-data-protection)中核实 Azure Rights Management 服务所支持的本地服务器的版本。

### <a name="install-and-configure-the-rms-connector"></a>安装并配置 RMS 连接器

按照 [部署 Azure Rights Management 连接器](./deploy-rms-connector.md) 一文中的说明进行操作，并执行步骤1到4。 

但不要执行连接器说明中的步骤 5。

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>在 Exchange 服务器上禁用 IRM 并删除 AD RMS 配置

> [!IMPORTANT]
> 如果你尚未在任何 Exchange 服务器上配置 IRM，只需执行步骤2和6。
> 
> 当你运行 [set-irmconfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration)时，如果 *LicensingLocation* 参数中没有显示所有 AD RMS 群集的所有授权 url，请执行所有这些步骤。

1. 在每个 Exchange 服务器上，找到以下文件夹，并删除该文件夹中的所有条目： **\programdata\microsoft\drm\server\s-1-5-18**

2. 在其中一台 Exchange Server 中，运行以下 PowerShell 命令，以确保用户能够读取使用 Azure Rights Management 保护的电子邮件。

    在运行这些命令之前，请将你自己的 Azure Rights Management 服务 URL 替换为 *\<Your Tenant URL>* 。

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation 
    $list += "<Your Tenant URL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    ```

    现在，当你运行 [set-irmconfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration)时，你应该会看到所有 AD RMS 群集授权 url 和为 *LicensingLocation* 参数显示的 Azure Rights Management 服务 URL。

3.  现在对向外部收件人发送的消息禁用 IRM 功能：

    ```PowerShell
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. 然后使用同一 cmdlet 在 Microsoft Office Outlook Web App 和 Microsoft Exchange ActiveSync 中禁用 IRM：

    ```PowerShell
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最后，使用同一 cmdlet 清除所有缓存的证书：

    ```PowerShell
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  现在，在每个 Exchange 服务器上重置 IIS，例如，通过以管理员身份运行命令提示符并键入 **iisreset**。

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>在 SharePoint 服务器上禁用 IRM 并删除 AD RMS 配置

1.  请确保没有文档从 RMS 保护的库中签出。 如果有，这些文档将在此过程结束时变为不可访问。

2.  在 SharePoint 管理中心网站的“快速启动”部分中，单击“安全性”。

3.  在“安全性”页的“信息策略”部分中，单击“配置信息权限管理”。

4.  在“信息权限管理”页的“信息权限管理”部分中，选择“不在此服务器上使用 IRM”，然后单击“确定”。

5.  在每台 SharePoint server 计算机上，删除 \\ < *运行 SharePoint server>帐户* 的文件夹 \ProgramData\Microsoft\MSIPC\Server SID 的内容。

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>配置 Exchange 和 SharePoint 以使用连接器

1. 返回到部署 RMS 连接器的说明：[步骤 5：配置服务器以使用 RMS 连接器](./configure-servers-rms-connector.md)

    如果仅具有 SharePoint Server，请直接转到[后续步骤](#next-steps)继续该迁移。 

2. 在每台 Exchange Server 上，手动为下一节中的每个已导入的配置数据文件 (.xml) 添加注册表项，将受信任的发布域 URL 重定向到 RMS 连接器。 这些注册表项特定于迁移，并且不是通过 Microsoft RMS 连接器的服务器配置工具添加的。

    进行这些注册表编辑时，请使用以下说明：

    -   将 *连接器 FQDN* 替换为你在 DNS 中为该连接器定义的名称。 例如 **rmsconnector.contoso.com**。

    -   对连接器 URL 使用 HTTP 或 HTTPS 前缀，具体取决于你已将连接器配置为使用 HTTP 还是使用 HTTPS 与本地服务器通信。

#### <a name="registry-edits-for-exchange"></a>Exchange 的注册表编辑

对于所有 Exchange 服务器，将以下注册表值添加到 LicenseServerRedirection，具体视 Exchange 版本而定：

1. 对于 **exchange 2013 和 exchange 2016，请** 添加以下注册表值：

    - **注册表路径：**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection`

    - **键入：** Reg_SZ

    - 值：`https://\<AD RMS Intranet Licensing URL\>/_wmcs/licensing`

    - **数据：** 以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

        - `http://\<connector FQDN\>/_wmcs/licensing`
        
        - `https://\<connector FQDN\>/_wmcs/licensing`

1. 对于 Exchange 2013，请添加以下附加注册表值：

    - **注册表路径：**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection` 

    - **键入：** Reg_SZ

    - **值：** https:// \<AD RMS Extranet Licensing URL\> /_wmcs/licensing

    - **数据：** 以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

        - `http://\<connector FQDN\>/_wmcs/licensing`

        - `https://\<connector FQDN\>/_wmcs/licensing`

## <a name="next-steps"></a>后续步骤
若要继续迁移，请转到[第 5 阶段 - 迁移后任务](migrate-from-ad-rms-phase5.md)。