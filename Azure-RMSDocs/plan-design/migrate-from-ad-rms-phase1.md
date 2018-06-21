---
title: 迁移 AD RMS-Azure 信息保护 - 第 1 阶段
description: 从 AD RMS 迁移到 Azure 信息保护的第 1 阶段涉及从 AD RMS 迁移到 Azure 信息保护中的步骤 1 至 3。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ea4c121d8945aabb4bb5a13a043a100e32e5924a
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
ms.locfileid: "30206717"
---
# <a name="migration-phase-1---preparation"></a>迁移第 1 阶段 - 准备

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的阶段 1。 这些过程涉及[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的步骤 1 至 3，以及准备好迁移环境但确保对用户无任何影响。


## <a name="step-1-install-the-aadrm-powershell-module-and-identify-your-tenant-url"></a>步骤 1：安装 AADRM PowerShell 模块，并识别你的租户 URL

安装 AADRM 模块，这样使你可以配置和管理针对 Azure 信息保护提供数据保护的服务。

有关说明，请参阅[安装 AADRM PowerShell 模块](../deploy-use/install-powershell.md)。

> [!NOTE]
> 如果之前已下载了此 Windows PowerShell 模块，请运行以下命令来检查版本号是否高于或等于 **2.9.0.0**：`(Get-Module aadrm -ListAvailable).Version`

若要完成某些迁移说明，需要了解租户的 Azure Rights Management 服务 URL，以便看到对\<租户 URL\> 的引用时将其替换。 Azure Rights Management 服务 URL 采用以下格式：**{GUID}.rms.[Region].aadrm.com**。

例如：**5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

### <a name="to-identify-your-azure-rights-management-service-url"></a>确定 Azure Rights Management 服务 URL

1. 连接到 Azure Rights Management 服务，并在出现提示时输入租户全局管理员的凭据：
    
        Connect-AadrmService
    
2. 获取租户的配置：
    
        Get-AadrmConfiguration
    
3. 复制针对 **LicensingIntranetDistributionPointUrl** 显示的值，并从此字符串删除 `/_wmcs\licensing`。 
    
    剩余的是 Azure 信息保护租户的 Azure 权限管理服务 URL。 此值在以下迁移说明中通常缩写为你的租户 URL。
    
    可以通过运行以下 PowerShell 命令验证是否具有正确的值：
    
            (Get-AadrmConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]

## <a name="step-2-prepare-for-client-migration"></a>步骤 2： 客户端迁移准备

对于大多数迁移，一次性迁移所有客户端并不现实，因此很可能分批迁移客户端。 这意味着，一段时间内，一些客户端将使用 Azure 信息保护，而一些客户端仍将使用 AD RMS。 若要同时支持预迁移和已迁移用户，请使用载入控件并部署预迁移脚本。 此步骤在迁移过程期间是必需的，以便尚未迁移的用户可以使用已受已迁移用户（当前使用的是 Azure Rights Management）保护的内容。

1. 例如，创建名为 **AIPMigrated** 的组。 可以在 Active Directory 中创建此组，并将其同步到云，也可以在 Office 365 或 Azure Active Directory 中创建它。 此时，不要将任何用户分配到此组。 在后面的某个步骤中，用户迁移后将被添加到该组。

    记下该组的对象 ID。 为此，可使用 Azure AD PowerShell，例如，对于 1.0 版的模块，请使用 [Get-MsolGroup](/powershell/msonline/v1/Get-MsolGroup) 命令。 或者，可以从 Azure 门户复制组的对象 ID。

2. 为载入控件配置此组，以仅允许此组中的人员使用 Azure Rights Management 保护内容。 为此，在 PowerShell 会话中，请连接到 Azure Rights Management 服务，并在出现提示时，指定全局管理员凭据：

        Connect-Aadrmservice

    然后为载入控件配置此组，将组对象 ID 替换为本例中的对象 ID，并在出现以下提示时输入 **Y** 进行确认：

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501" -Scope WindowsApp

3. [下载下列文件](https://go.microsoft.com/fwlink/?LinkId=524619)，其中包含客户端迁移脚本：
    
    Migration-Scripts.zip
    
4. 提取文件，然后按照 PrepareClient.cmd 中的说明操作，使其包含 AD RMS 群集 Extranet 授权 URL 的服务器名称。 
    
    若要找到此名称：在 Active Directory Rights Management Services 控制台中，请单击群集名称。 在**群集详情**信息中，复制 Extranet 群集 URL 部分**授权**值的服务器名称。 例如：**rmscluster.contoso.com**.

    > [!IMPORTANT]
    > 说明包括将示例地址 **adrms.contoso.com** 替换为你自己的 AD RMS 服务器地址。 执行此操作时，请注意地址前后不要有多余空格，否则将中断迁移脚本，并且很难将其认定为问题的根本原因。 某些编辑工具会在粘贴文本后自动添加一个空格。
    >

5. 将此脚本部署到所有 Windows 计算机，以确保开始迁移客户端时，尚未迁移的客户端能继续与 AD RMS 进行通信，即使它们使用的内容受到已迁移客户端（当前使用的是 Azure Rights Management 服务）保护。

    可以使用组策略或其他软件部署机制来部署此脚本。

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>步骤 3： 准备迁移 Exchange 部署

如果使用的是 Exchange 内部部署或 Exchange Online，可能之前已将 Exchange 与 AD RMS 部署集成过。 此步骤将对它们进行配置，以使用现有的 AD RMS 配置支持 Azure RMS 保护的内容。 

请确保你具有[租户的 Azure Rights Management 服务 URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)，以便在下列命令中将该值替换为 &lt;YourTenantURL&gt; 

**如果已将 Exchange Online 与 AD RMS 集成**：打开一个 Exchange Online PowerShell 会话，然后逐一或在脚本中运行以下 PowerShell 命令：

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 

**如果你已将 Exchange 本地环境与 AD RMS 集成**：对于每个 Exchange 组织，首先在每个 Exchange 服务器上添加注册表值，然后运行 PowerShell 命令： 

Exchange 2013 和 Exchange 2016 的注册表值：

**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**类型：** Reg_SZ

**值：** https://\<租户 URL\>/_wmcs/licensing

**数据：** https://\<AD RMS Extranet 授权 URL\>/_wmcs/licensing

---

Exchange 2010 的注册表值：

**注册表路径：**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**类型：** Reg_SZ

**值：** https://\<租户 URL\>/_wmcs/licensing

**数据：** https://\<AD RMS Extranet 授权 URL>/_wmcs/licensing

---

PowerShell 命令可以逐个运行，也可以在脚本中运行

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset


为 Exchange Online 或 Exchange 本地环境运行这些命令后，如果 Exchange 部署已配置为支持受 AD RMS 保护的内容，则在迁移后，它们还支持受 Azure RMS 保护的内容。 在执行迁移过程中的下一步骤之前，Exchange 部署将继续使用 AD RMS 支持受保护的内容。


## <a name="next-steps"></a>后续步骤
转到[第 2 阶段：服务器端配置](migrate-from-ad-rms-phase2.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
