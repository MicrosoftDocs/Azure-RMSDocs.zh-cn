---
title: "激活 Azure Rights Management - AIP"
description: "必须先激活 Azure Rights Management 服务，然后组织才可以开始使用支持此信息保护解决方案的应用程序和服务来保护文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e8fede85cddc44318ce93497a9ac454c689673d3
ms.sourcegitcommit: c3d57b175a4e7b5e136f7183c837fa08e7ac982e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2018
---
# <a name="activating-azure-rights-management"></a>激活 Azure Rights Management

>*适用于：Azure 信息保护、Office 365*

> [!NOTE]
> 此配置信息适用于负责应用于组织中所有用户的服务的管理员。 如果你要寻找针对特定应用程序使用 Rights Management 功能，或者如何打开受权限保护的文件或电子邮件的用户帮助和信息，请使用你的应用程序附带的帮助和指南。
>
> 例如，对于 Office 应用程序，请单击帮助图标并输入搜索词，例如 **Rights Management** 或 **IRM**。 有关适用于 Windows 的 Azure 信息保护客户端，请参阅 [Azure 信息保护客户端用户指南](../rms-client/client-user-guide.md)。
>
> 有关技术支持和其他服务问题，请参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)信息。

为租户激活 Azure 信息保护的 Azure 权限管理服务后，你的组织便可以开始使用支持此信息保护解决方案的应用程序和服务保护重要数据了。 管理员还可以管理和监视你的组织拥有的受保护文件和电子邮件。 能够开始在 Office、SharePoint 和 Exchange 中使用信息权限管理 (IRM) 功能保护任何敏感或机密文件之前，必须启用此服务。

如果要在激活该服务之前了解有关 Azure Rights Management 服务的详细信息（例如，它解决哪些业务问题、一些典型用例以及工作原理），请参阅[什么是 Azure Rights Management？](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> 如果为组织部署了 Active Directory Rights Management Services (AD RMS)，则不要激活 Azure 权限管理服务。 [详细信息](prepare-environment-adrms.md)

在激活 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 之前，请确保你的组织具有包含 Azure Rights Management 数据保护的服务计划。 如果没有，你将不能激活 Azure Rights Management。 必须具有以下项之一：

- [Azure 信息保护计划](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- [包含 Rights Management 的 Office 365 计划](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。

激活 Azure Rights Management 服务时，你的组织中的所有用户将可以对其文件应用信息保护，并且所有用户均可打开（使用）受 Azure Rights Management 服务保护的文件。 但是，如果你愿意，可以通过对分阶段部署使用加入控制来限制哪些人员可以应用信息保护。 有关详细信息，请参阅本文中的 [为分阶段部署配置加入控制](#configuring-onboarding-controls-for-a-phased-deployment) 部分。

有关如何从管理门户激活 Rights Management 服务的说明，请选择是使用 Office 365 管理中心还是 Azure 门户：

- [Office 365 管理中心](activate-office365.md) - 需要全局管理员帐户

- [Azure 门户](activate-azure.md) - 需要全局管理员帐户或[安全管理员帐户](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles)

也可以使用 PowerShell 激活 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]：

1. 安装 Azure Rights Management 管理工具，将安装 Azure Rights Management 管理模块。 相关说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。

2. 在 PowerShell 会话中，运行 [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice)，并在出现提示时提供 Azure 信息保护租户的全局管理员帐户详细信息。

3. 运行 [Enable-Aadrm](/powershell/module/aadrm/enable-aadrm)，该命令将激活 Azure Rights Management 服务。

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>为分阶段部署配置加入控制
如果不希望所有用户都能立即使用 Azure Rights Management 保护文件，则可以使用 [Set-AadrmOnboardingControlPolicy](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy) PowerShell 命令来配置用户加入控制。 在激活 Azure Rights Management 服务之前或之后，你可以运行此命令。

> [!IMPORTANT]
> 若要使用此命令，必须安装至少 **2.1.0.0** 版的 [Azure Rights Management PowerShell 模块](https://go.microsoft.com/fwlink/?LinkId=257721)。
>
> 若要检查已安装的版本，请运行：**(Get-Module aadrm –ListAvailable).Version**

例如，如果出于测试目的，你最初只想让“IT 部门”组（具有对象 ID fbb99ded-32a0-45f1-b038-38b519009503）中的管理员能够保护内容，请使用以下命令：

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

请注意：对于此配置选项，必须指定组，不能指定单个用户。 若要获取组的对象 ID，可使用 Azure AD PowerShell，例如，对于 1.0 版的模块，请使用 [Get-MsolGroup](/powershell/msonline/v1/get-msolgroup) 命令。 或者，可以从 Azure 门户复制组的**对象 ID** 值。

或者，如果要确保只有正确获得使用 Azure 信息保护的许可的用户可以保护内容，请使用以下命令：

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $True
```

不需要再使用载入控件时，无论使用了组还是授权选项，都运行：

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False
```


有关此 cmdlet 的详细信息和其他示例，请参阅 [Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy) 帮助。

使用这些加入控制时，组织中的所有用户始终可以使用由用户的子集保护的受保护内容，但他们自身将不能从客户端应用程序应用信息保护。 例如，他们将在其 Office 客户端中看不到激活 Azure Rights Management 时自动发布的默认模板，也看不到你可能会配置的自定义模板。  服务器端应用程序（如 Exchange）可以为 Rights Management 集成实现自己的每用户控制，以获得相同的结果。


## <a name="next-steps"></a>后续步骤
为组织激活 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 之后，向用户和管理员推出 Azure 信息保护之前，可使用 [Azure 信息保护部署路线图](../plan-design/deployment-roadmap.md)来检查是否还需要执行其他配置步骤。 

例如，可能需要使用[模板](configure-policy-templates.md)使用户更方便地对文件应用信息保护，通过安装 [Rights Management 连接器](deploy-rms-connector.md)来连接本地服务器以使用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]，以及部署 [Azure 信息保护客户端](../rms-client/aip-client.md)以便对所有设备上的所有文件类型进行保护。 

Exchange Online 和 SharePoint Online 等 Office 服务需要进行其他配置，然后才能使用其信息权限管理 (IRM) 功能。 有关应用程序如何使用权限管理服务的信息，请参阅[应用程序如何支持 Azure Rights Management 服务](../understand-explore/applications-support.md)。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
