---
title: "从 AD RMS 迁移到 Azure 信息保护 - 第 4 阶段"
description: "从 AD RMS 迁移到 Azure 信息保护的第 4 阶段包括从 AD RMS 迁移到 Azure 信息保护的步骤 8 至 9"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c6646b6e3df72105d0808e23b40fe01e444e164a
ms.sourcegitcommit: 384461f0e3fccd73cd7eda3229b02e51099538d4
translationtype: HT
---
# <a name="migration-phase-4---supporting-services-configuration"></a>迁移第 4 阶段 - 支持服务配置

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365*


使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的第 4 阶段。 这些过程包括[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 8-9。



## <a name="step-8-configure-irm-integration-for-exchange-online"></a>步骤 8. 为 Exchange Online 配置 IRM 集成

如果以前已将 TDP 从 AD RMS 导入 Exchange Online，则必须删除此 TDP，以避免在迁移到 Azure 信息保护后发生模板和策略冲突。 为此，请在 Exchange Online 中使用 [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) cmdlet。

如果你选择了 **Microsoft 管理**的 Azure 信息保护租户密钥拓扑：

1. 请使用 [Office 365：客户端和联机服务的配置](../deploy-use/configure-office365.md)一文中的[“Exchange Online：IRM 配置”](../deploy-use/configure-office365.md#exchange-online-irm-configuration)部分的说明。 此部分介绍了一些典型的命令，运行这些命令可以连接到 Exchange Online 服务、从 Azure 信息保护导入租户密钥，以及为 Exchange Online 启用 IRM 功能。 完成这些步骤后，你将获得 Exchange Online 的完整 Azure Rights Management 保护功能。

2. 除了为 Exchange Online 启用 IRM 的标准配置外，还可运行以下 PowerShell 命令以确保用户能够读取使用 AD RMS 保护发送的电子邮件。

    将自已的组织域名替换为 \<yourcompany.domain>。

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation
        $list += "https://adrms.<yourcompany.domain>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list
        Set-IRMConfiguration -internallicensingenabled $false
        Set-IRMConfiguration -internallicensingenabled $true


如果你选择了**客户管理 (BYOK)** 的 Azure 信息保护租户密钥拓扑：

-   Exchange Online 的 Rights Management 保护功能将有所削减，如 [BYOK 定价和限制](byok-price-restrictions.md)一文中所述。


## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>步骤 9. 为 Exchange Server 和 SharePoint Server 配置 IRM 集成

如果你已将 Exchange Server 或 SharePoint Server 的信息权限管理 (IRM) 与 AD RMS 集成，则需要部署 Rights Management (RMS) 连接器，以充当本地服务器与 Azure 信息保护的保护服务之间的通信接口（中继）。

这包括以下步骤：安装和配置连接器；对 Exchange 和 SharePoint 禁用 IRM；以及配置这些服务器以使用该连接器。 最后，如果你已将用于保护电子邮件的 AD RMS 数据配置文件 (.xml) 导入到 Azure 信息保护，则必须手动编辑 Exchange Server 计算机上的注册表，将所有受信任的发布域 URL 重定向到 RMS 连接器。

> [!NOTE]
> 在开始之前，请从[支持 Azure RMS 的本地服务器](../get-started/requirements-servers.md)中核实 Azure Rights Management 服务所支持的本地服务器的版本。

### <a name="install-and-configure-the-rms-connector"></a>安装并配置 RMS 连接器

请使用[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)一文中的说明，并执行步骤 1 至 4。 但不要执行连接器说明中的步骤 5。 

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>在 Exchange 服务器上禁用 IRM 并删除 AD RMS 配置

1.  在每个 Exchange Server 上，找到以下文件夹，并删除该文件夹中的所有条目：**\ProgramData\Microsoft\DRM\Server\S-1-5-18**

2. 在其中一台 Exchange Server 中，运行以下 PowerShell 命令，以确保用户能够读取使用 Azure Rights Management 保护的电子邮件。

    运行这些命令之前，请将 \<租户 URL>替换为你自己的 Azure Rights Management 服务 URL。

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation 
        $list + "<Your Tenant URL>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list

3.  现在对向外部收件人发送的消息禁用 IRM 功能：

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. 然后使用同一 cmdlet 在 Microsoft Office Outlook Web App 和 Microsoft Exchange ActiveSync 中禁用 IRM：

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最后，使用同一 cmdlet 清除所有缓存的证书：

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  现在，在每个 Exchange Server 上重置 IIS，例如通过以管理员身份运行命令提示符并键入 **iisreset**。

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>在 SharePoint 服务器上禁用 IRM 并删除 AD RMS 配置

1.  请确保没有文档从 RMS 保护的库中签出。 如果有，这些文档将在此过程结束时变为不可访问。

2.  在 SharePoint 管理中心网站的“快速启动”部分中，单击“安全性”。

3.  在“安全性”页的“信息策略”部分中，单击“配置信息权限管理”。

4.  在“信息权限管理”页的“信息权限管理”部分中，选择“不在此服务器上使用 IRM”，然后单击“确定”。

5.  在每台 SharePoint Server 计算机上，删除文件夹 \ProgramData\Microsoft\MSIPC\Server\\<运行 SharePoint Server 的帐户 SID> 的内容。

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>配置 Exchange 和 SharePoint 以使用连接器

1. 返回到部署 RMS 连接器的说明：[步骤 5：配置服务器以使用 RMS 连接器](../deploy-use/configure-servers-rms-connector.md)

    如果仅具有 SharePoint Server，请直接转到[后续步骤](#next-steps)继续该迁移。 

2. 在每台 Exchange Server 上，手动为下一节中的每个已导入的配置数据文件 (.xml) 添加注册表项，将受信任的发布域 URL 重定向到 RMS 连接器。 这些注册表项特定于迁移，并且不是通过 Microsoft RMS 连接器的服务器配置工具添加的。

    进行这些注册表编辑时，请使用以下说明：

    -   将 *连接器 FQDN* 替换为你在 DNS 中为该连接器定义的名称。 例如 **rmsconnector.contoso.com**。

    -   对连接器 URL 使用 HTTP 或 HTTPS 前缀，具体取决于你已将连接器配置为使用 HTTP 还是使用 HTTPS 与本地服务器通信。

#### <a name="registry-edits-for-exchange"></a>Exchange 的注册表编辑

对于所有 Exchange Server，请删除在准备阶段针对 LicenseServerRedirection 添加的注册表值。 这些值已被添加到以下路径：

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection


对于 Exchange 2013 和 Exchange 2016 - 注册表编辑 1：


**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**类型：** Reg_SZ

**值：**https://\<AD RMS Intranet 授权 URL\>/_wmcs/licensing

**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://\<连接器 FQDN\>/_wmcs/licensing

- https://\<连接器 FQDN\>/_wmcs/licensing


---

对于 Exchange 2013 - 注册表编辑 2：

**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 

**类型：** Reg_SZ

**值：**https://\<AD RMS Extranet 授权 URL\>/_wmcs/licensing

**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://\<连接器 FQDN\>/_wmcs/licensing

- https://\<连接器 FQDN\>/_wmcs/licensing

---

对于 Exchange 2010 - 注册表编辑 1：


**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**类型：** Reg_SZ

**值：**https://\<AD RMS Intranet 授权 URL\>/_wmcs/licensing

**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://\<连接器 FQDN\>/_wmcs/licensing

- https://\<连接器名称\>/_wmcs/licensing


---

对于 Exchange 2010 - 注册表编辑 2：


**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**类型：** Reg_SZ

**值：**https://\<AD RMS Extranet 授权 URL\>/_wmcs/licensing

**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://\<连接器 FQDN\>/_wmcs/licensing

- https://\<连接器 FQDN\>/_wmcs/licensing

---


## <a name="next-steps"></a>后续步骤
若要继续迁移，请转到[第 5 阶段 - 迁移后任务](migrate-from-ad-rms-phase5.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]