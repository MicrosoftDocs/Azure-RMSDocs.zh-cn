---
title: "从 AD RMS 迁移到 Azure Rights Management - 阶段 3 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: 75cce1d0e5a1cff0d4f6609d0f084fda1af62951


---

# 迁移阶段 3 - 支持服务配置

*适用于：Active Directory Rights Management Services、Azure Rights Management*


使用以下信息，完成从 AD RMS 迁移到 Azure Rights Management (Azure RMS) 的阶段 3。 这些过程涉及[从 AD RMS 迁移到 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 中的步骤 6-7。


## 步骤 6. 为 Exchange Online 配置 IRM 集成

如果以前已将 TDP 从 AD RMS 导入 Exchange Online，则必须删除此 TDP，以避免在迁移到 Azure RMS 后发生模板和策略冲突。 为此，请在 Exchange Online 中使用 [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) cmdlet。

如果你选择了 **Microsoft 管理**的 Azure RMS 租户密钥拓扑：

-   请参阅 [Office 365：客户端和联机服务的配置](../deploy-use/configure-office365.md)文章中的“Exchange Online：IRM 配置”[](../deploy-use/configure-office365.md#exchange-online-irm-configuration)部分。 此部分介绍了一些典型的命令，运行这些命令可以连接到 Exchange Online 服务、从 Azure RMS 导入租户密钥，以及为 Exchange Online 启用 IRM 功能。 完成这些步骤后，你将获得 Exchange Online 的完整 RMS 功能。

如果你选择了**客户管理 (BYOK)** 的 Azure RMS 租户密钥拓扑：

-   Exchange Online 的 RMS 功能将有所削减，如 [BYOK 定价和限制](byok-price-restrictions.md)文章中所述。

## 步骤 7. 部署 RMS 连接器
如果你已将 Exchange Server 或 SharePoint Server 的信息权限管理 (IRM) 功能与 AD RMS 一起使用，则必须先在这些服务器上禁用 IRM 并删除 AD RMS 配置。 然后，部署 Rights Management (RMS) 连接器，该连接器将充当本地服务器和 Azure RMS 之间的通信接口（中继）。

此步骤的最后一步，如果你已将多个用于保护电子邮件的 TPD 导入到 Azure RMS ，则必须手动编辑 Exchange Server 计算机上的注册表，将所有 TPD URL 重定向到 RMS 连接器。

> [!NOTE]
> 在开始之前，请从[支持 Azure RMS 的本地服务器](../get-started/requirements-servers.md)中核实 Azure RMS 所支持的本地服务器的版本。

### 在 Exchange 服务器上禁用 IRM 并删除 AD RMS 配置

1.  在每个 Exchange 服务器上，找到以下文件夹，并删除该文件夹中的所有条目：\ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  在任一 Exchange 服务器上，使用 Exchange [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) cmdlet，先对向内部收件人发送的消息禁用 IRM 功能：

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  然后使用同一 cmdlet 对向外部收件人发送的消息禁用 IRM 功能：

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  接下来，使用同一 cmdlet 在 Microsoft Office Outlook Web App 和 Microsoft Exchange ActiveSync 中禁用 IRM：

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  最后，使用同一 cmdlet 清除所有缓存的证书：

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  现在，在每个 Exchange Server 上重置 IIS，例如通过以管理员身份运行命令提示符并键入 **iisreset**。

### 在 SharePoint 服务器上禁用 IRM 并删除 AD RMS 配置

1.  请确保没有文档从 RMS 保护的库中签出。 如果有，这些文档将在此过程结束时变为不可访问。

2.  在 SharePoint 管理中心网站的“快速启动”部分中，单击“安全性”。

3.  在“安全性”页的“信息策略”部分中，单击“配置信息权限管理”。

4.  在“信息权限管理”页的“信息权限管理”部分中，选择“不在此服务器上使用 IRM”，然后单击“确定”。

5.  在每台 SharePoint Server 计算机上，删除文件夹 \ProgramData\Microsoft\MSIPC\Server\*&lt;运行 SharePoint Server 的帐户的 SID&gt;* 的内容。

#### 安装并配置 RMS 连接器

-   使用[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)文章中的说明。

#### 对于仅 Exchange 和多个 TPD：编辑注册表

-   在每个 Exchange 服务器上，手动为每个已导入的附加 TPD 添加以下注册表项，将 TPD URL 重定向到 RMS 连接器。 这些注册表项特定于迁移，并且不是通过 Microsoft RMS 连接器的服务器配置工具添加的。

    进行这些注册表编辑时，请使用以下说明：

    -   将 *ConnectorFQDN* 替换为你在 DNS 中为连接器定义的名称。 例如 **rmsconnector.contoso.com**。

    -   对连接器 URL 使用 HTTP 或 HTTPS 前缀，具体取决于你已将连接器配置为使用 HTTP 还是使用 HTTPS 与本地服务器通信。

对于 Exchange 2013 - 注册表编辑 1：


**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**键入：**

Reg_SZ

**Value：**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

对于 Exchange 2013 - 注册表编辑 2：

**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**键入：**

Reg_SZ

**Value：**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

对于 Exchange 2010 - 注册表编辑 1：



**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**键入：**

Reg_SZ

**Value：**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

对于 Exchange 2010 - 注册表编辑 2：


**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**键入：**

Reg_SZ

**Value：**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**数据：**

以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

完成这些过程之后，请务必阅读[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)文章中的“后续步骤”部分。

## 后续步骤
若要继续迁移，请转到[阶段 4 - 迁移后任务](migrate-from-ad-rms-phase4.md)。


<!--HONumber=Jul16_HO3-->


