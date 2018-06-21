---
title: Rights Management 连接器的注册表设置 - AIP
description: 有关使用 RMS 连接器在服务器上进行注册表设置的信息。 配置这些设置的推荐方法是使用适用于 Microsoft RMS 连接器的服务器配置工具。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed3e9a3d-0f7c-4abc-9d0b-aa3b18403d39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9334a781378ffdbe76dd9fe9d78f5db5913766d1
ms.sourcegitcommit: 373e05ff0c411d29cc5b61c36edaf5a203becc14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
ms.locfileid: "34216828"
---
# <a name="registry-setting-for-the-rights-management-connector"></a>Rights Management 连接器的注册表设置

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2


只有当需要在运行 Exchange、SharePoint 或 Windows Server 的服务器上手动添加或检查注册表设置时，才使用以下部分的表格。 这些注册表设置将服务器配置为使用 [RMS 连接器](deploy-rms-connector.md)。 配置这些服务器的推荐方法是使用适用于 Microsoft RMS 连接器的服务器配置工具。

有关使用这些配置时的说明：

-   \<YourTenantURL> 是 Azure 信息保护租户的 Azure 权限管理服务 URL。 查找此值：

    1.  为 Azure 权限管理服务运行 [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet。 如果尚未安装适用于 Azure RMS 的 Windows PowerShell 模块，请参阅[安装 AADRM PowerShell 模块](install-powershell.md)。

    2.  在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

        例如：LicensingIntranetDistributionPointUrl：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

    3.  在该值中，将 **/_wmcs/licensing** 从此字符串删除。 剩余字符串为 Azure 权限管理服务 URL。 在本示例中，Azure 权限管理服务 URL 为以下值：

        **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**
        
        可以通过运行以下 PowerShell 命令验证是否具有正确的值：
        
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

-   \<ConnectorFQDN> 是你在 DNS 中为连接器定义的负载平衡名称。 例如 **rmsconnector.contoso.com**。

-   如果你已将连接器配置为使用 HTTPS 与本地服务器通信，请使用 HTTPS 前缀作为连接器 URL。 有关详细信息，请参阅主要说明的[《Configuring the RMS connector to use HTTPS》](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)（将 RMS 连接器配置为使用 HTTPS）部分。 Azure 权限管理服务 URL 通常使用 HTTPS。


## <a name="exchange-2016-or-exchange-2013-registry-settings"></a>Exchange 2016 或 Exchange 2013 注册表设置

**注册表路径：** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**类型：** Reg_SZ

**值：** 默认

数据：https://\<YourTenantURL>/_wmcs/certification

---

**注册表路径：** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**类型：** Reg_SZ

**值：** 默认

数据：https://\<YourTenantURL>/_wmcs/Licensing

---

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\CertificationServerRedirection

**类型：** Reg_SZ

值：https://\<YourTenantURL>


**数据：** 以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<\ConnectorFQDN>

- https://<\ConnectorFQDN>

---

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**类型：** Reg_SZ

值：https://<\YourTenantURL>


**数据：** 以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<\ConnectorFQDN>

- https://<\ConnectorFQDN>


## <a name="exchange-2010-registry-settings"></a>Exchange 2010 注册表设置

**注册表路径：** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\Activation

**类型：** Reg_SZ

**值：** 默认

数据：https://<\YourTenantURL>/_wmcs/certification

---

**注册表路径：** HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**类型：** Reg_SZ

**值：** 默认

数据：https://<\YourTenantURL>/_wmcs/Licensing

---

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\CertificationServerRedirection

**类型：** Reg_SZ

值：https://<\YourTenantURL>

**数据：** 以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<\ConnectorFQDN>

- https://<\ConnectorFQDN>

---

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**类型：** Reg_SZ

值：https://<\YourTenantURL>

**数据：** 以下前缀之一，具体取决于 Exchange 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<\ConnectorFQDN>

- https://<\ConnectorFQDN>


## <a name="sharepoint-2016-or-sharepoint-2013-registry-settings"></a>SharePoint 2016 或 SharePoint 2013 注册表设置

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\LicensingRedirection

**类型：** Reg_SZ

值：https://<\YourTenantURL>/_wmcs/licensing


**数据：** 以下前缀之一，具体取决于 SharePoint 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<\ConnectorFQDN>/_wmcs/licensing

- https://<\ConnectorFQDN>/_wmcs/licensing

---

**注册表路径:** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification

**类型：** Reg_SZ

**值：** 默认

**数据：** 以下前缀之一，具体取决于 SharePoint 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<\ConnectorFQDN>/_wmcs/certification

- https://<\ConnectorFQDN>/_wmcs/certification

---

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing

**类型：** Reg_SZ

**值：** 默认


**数据：** 以下前缀之一，具体取决于 SharePoint 服务器与 RMS 连接器之间的连接是使用 HTTP 还是 HTTPS：

- http://<\ConnectorFQDN>/_wmcs/licensing

- https://<\ConnectorFQDN>/_wmcs/licensing




## <a name="file-server-and-file-classification-infrastructure-registry-settings"></a>文件服务器和文件分类基础结构注册表设置

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

**类型：** Reg_SZ

**值：** 默认

数据：http://<\ConnectorFQDN>/_wmcs/licensing

---

**注册表路径：** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

**类型：** Reg_SZ

**值：** 默认

数据： http://<\ConnectorFQDN>/_wmcs/certification


返回到[部署 Azure Rights Management 连接器](deploy-rms-connector.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]