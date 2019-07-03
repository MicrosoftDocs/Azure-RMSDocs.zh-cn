---
title: 激活 Azure 信息保护中的保护服务
description: 你的组织可以开始使用应用程序和支持此信息保护解决方案的服务保护文档和电子邮件之前，必须激活保护服务，Azure Rights Management。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 16c3ded1ea8f5d7c2191b994ec63132bd5f9bf1e
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520319"
---
# <a name="activating-the-protection-service-from-azure-information-protection"></a>激活 Azure 信息保护中的保护服务

>适用对象：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

> [!NOTE]
> 此配置信息适用于负责应用于组织中所有用户的服务的管理员。 如果你要寻找针对特定应用程序使用 Rights Management 功能，或者如何打开受权限保护的文件或电子邮件的用户帮助和信息，请使用你的应用程序附带的帮助和指南。
>
> 例如，对于 Office 应用程序，请单击帮助图标并输入搜索词，例如 **Rights Management** 或 **IRM**。 有关适用于 Windows 的 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端用户指南](./rms-client/client-user-guide.md)。
>
> 有关技术支持和其他服务问题，请参阅[支持选项和社区资源](information-support.md#support-options-and-community-resources)信息。

为你的组织激活 Azure 信息保护的保护服务，则管理员和用户可以开始使用应用程序和支持此信息保护解决方案的服务保护重要数据。 管理员还可以管理和监视你的组织拥有的受保护文档和电子邮件。 


## <a name="do-you-need-to-activate-the-protection-service-azure-rights-management"></a>是否需要激活保护服务，Azure Rights Management？

如果你拥有包含 Azure Rights Management 的服务计划，则可能不需要激活此服务：

- **如果你包含 Azure Rights Management 或 Azure 信息保护的订阅是在 2018 年 2 月底或之后获取的：** 此服务会自动为你激活。 除非你或你组织的其他全局管理员停用了 Azure Rights Management，否则你无需激活此服务。

- **如果你包含 Azure Rights Management 或 Azure 信息保护的订阅是在 2018 年 2 月期间或之前获取的：** 如果租户使用的是 Exchange Online，Microsoft 将开始为这些订阅激活 Azure Rights Management 服务。 对于这些订阅，自动激活将于 2018 年 8 月 1 日开始推出，届时将为你激活此服务，除非在运行 [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps) 时看到 AutomaticServiceUpdateEnabled  设置为 false  。 

如果两种后续方案都不适用，必须手动激活保护服务。 

激活此服务后，组织中的所有用户都可以对文档和电子邮件应用信息保护，并且所有用户都能打开（使用）受 Azure Rights Management 服务保护的文档和电子邮件。 但是，如果你愿意，可以通过对分阶段部署使用加入控制来限制哪些人员可以应用信息保护。 有关详细信息，请参阅本文中的 [为分阶段部署配置加入控制](#configuring-onboarding-controls-for-a-phased-deployment) 部分。

## <a name="how-to-activate-or-confirm-the-status-of-the-protection-service"></a>如何激活或确认保护服务的状态 

> [!IMPORTANT]
> 如果有 Active Directory Rights Management Services (AD RMS) 部署为你的组织，则不要激活保护服务。 [详细信息](prepare-environment-adrms.md)

若要使用此数据保护解决方案，你的组织必须拥有包含 Azure 信息保护中的 Azure Rights Management 服务的服务计划。 如果没有，不能激活保护服务。 必须具有以下项之一：

- [Azure 信息保护计划](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- [包含 Rights Management 的 Office 365 计划](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。

保护服务已激活，你的组织中的所有用户可以对其文档和电子邮件、 都应用信息保护和所有用户均可以都打开时 （使用） 文档和电子邮件的受保护的此服务。 但是，如果你愿意，可以通过对分阶段部署使用加入控制来限制哪些人员可以应用信息保护。 有关详细信息，请参阅本文中的 [为分阶段部署配置加入控制](#configuring-onboarding-controls-for-a-phased-deployment) 部分。

## <a name="choosing-your-activation-method"></a>选择激活方法

有关说明如何激活保护服务从你的管理门户中，选择是否使用 Microsoft 365 管理中心或 Azure 门户：

- [Microsoft 365 管理中心](activate-office365.md) - 需要全局管理员帐户

- [Azure 门户](activate-azure.md) - 不需要全局管理员帐户

或者，你也可以使用以下 PowerShell 命令：

1. 安装 AIPService 模块，若要配置和管理保护服务。 有关说明，请参阅[安装 AIPService PowerShell 模块](install-powershell.md)。

2. 在 PowerShell 会话中，运行[Connect AipService](/powershell/module/aipservice/connect-aipservice)，并出现提示时，提供你的 Azure 信息保护租户全局管理员帐户详细信息。

3. 运行[Get AipService](/powershell/module/aipservice/get-aipservice)以确认是否已激活保护服务。 状态为“Enabled”则确认已激活；状态为“Disabled”则指示此服务已停用   。

4. 若要激活此服务，运行[启用 AipService](/powershell/module/aipservice/enable-aipservice)。

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>为分阶段部署配置加入控制
如果不希望所有用户都能够保护文档和电子邮件立即使用 Azure 信息保护，你可以使用配置用户加入控制[集 AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) PowerShell命令。 在激活 Azure Rights Management 服务之前或之后，你可以运行此命令。

例如，如果出于测试目的，你最初只想让“IT 部门”组（具有对象 ID fbb99ded-32a0-45f1-b038-38b519009503）中的管理员能够保护内容，请使用以下命令：

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

请注意：对于此配置选项，必须指定组，不能指定单个用户。 若要获取组的对象 ID，可使用 Azure AD PowerShell，例如，对于 1.0 版的模块，请使用 [Get-MsolGroup](/powershell/msonline/v1/get-msolgroup) 命令。 或者，可以从 Azure 门户复制组的**对象 ID** 值。

或者，如果要确保只有正确获得使用 Azure 信息保护的许可的用户可以保护内容，请使用以下命令：

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $True
```

不需要再使用载入控件时，无论使用了组还是授权选项，都运行：

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
```

有关此 cmdlet 和其他示例的详细信息，请参阅[集 AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)帮助。

使用这些加入控制时，组织中的所有用户始终可以使用由用户的子集保护的受保护内容，但他们自身将不能从客户端应用程序应用信息保护。 例如，他们在 Office 应用程序时保护服务已激活，自动发布的默认保护模板也看可能会配置的自定义模板。 服务器端应用程序，如 Exchange，可以实现自己的每个用户控件来实现相同的结果。 例如，若要阻止用户保护网页版 Outlook 中的电子邮件，请使用 [Set-OwaMailboxPolicy](/powershell/module/exchange/client-access/set-owamailboxpolicy?view=exchange-ps)，以将 IRMEnabled  参数设置为 $false  。


## <a name="next-steps"></a>后续步骤
当为你的组织激活保护服务，则使用[Azure 信息保护部署路线图](deployment-roadmap.md)以检查是否有可能需要推出 Azure 之前执行其他配置步骤向用户和管理员的信息保护。 

例如，你可能想要使用[模板](configure-policy-templates.md)若要使用户更轻松地对文件应用保护，连接的本地服务器以使用保护服务通过安装[Rights Management 连接器](deploy-rms-connector.md)，并将其部署[Azure 信息保护客户端](./rms-client/aip-client.md)以便在所有设备上的所有文件类型都进行保护。 

Exchange Online 和 SharePoint Online 等 Office 服务需要进行其他配置，然后才能使用其信息权限管理 (IRM) 功能。 了解你的应用程序如何使用保护服务，Azure Rights Management，请参阅[应用程序如何支持 Azure Rights Management 服务](applications-support.md)。

