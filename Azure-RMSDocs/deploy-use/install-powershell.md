---
title: "安装适用于 Azure Rights Management 的 PowerShell - AIP"
description: "安装适用于 Azure 信息保护中的 Azure Rights Management 服务的 Windows PowerShell 的说明 此模块的名称是 AADRM。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5dae84eea9e67be75530d69b6124b97c7c29f8a3
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="installing-windows-powershell-for-azure-rights-management"></a>安装适用于 Azure 权限管理的 Windows PowerShell

>*适用于：Azure 信息保护、Office 365*

使用以下信息帮助安装适用于 Azure 信息保护中的 Azure Rights Management 服务的 Windows PowerShell 模块。

在任何具有 Internet 连接且满足下一节列出的先决条件的计算机上，可以使用此 PowerShell 模块从命令行管理 Azure Rights Management 服务。 适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 支持脚本的自动化，或者可能是高级配置方案所必需的。 若要深入了解此模块支持的管理任务和配置，请参阅[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)。

## <a name="prerequisites"></a>先决条件
此表列出了安装和使用适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 的先决条件。

|要求|更多信息|
|---------------|--------------------|
|支持[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]管理模块的 Windows 版本|查看 [Azure Rights Management 管理工具下载页](http://go.microsoft.com/fwlink/?LinkId=257721)的“系统要求”部分中的受支持操作系统列表。|
|Windows PowerShell 的最低版本：2.0<br /><br /> |默认情况下，大多数 Windows 操作系统至少安装了 Windows PowerShell 2.0 版本。 如果你需要安装此受支持的最低版本，请参阅[安装 Windows PowerShell 2.0](https://msdn.microsoft.com/library/ff637750.aspx)。<br /><br />提示：你可在 PowerShell 会话中键入 `$PSVersionTable`，以确认正在运行的 Windows PowerShell 的版本。 <br /><br /> 如果你已安装此最低版本，需要在 PowerShell 会话中通过运行 `Import-Module AADRM` 手动加载模块，然后才能使用 Rights Management 管理模块中的任何 cmdlet。 如果你安装了 Windows PowerShell v3 及更高版本，该模块会自动加载，不需要再执行此命令。|
|Microsoft .NET Framework 的最低版本：4.5<br /><br />请注意：较高版本的操作系统都附带此版本的 Microsoft .NET Framework，因此只有在你的客户端操作系统低于 Windows 8.0 或服务器操作系统低于 Windows Server 2012 的情况下，才需要手动安装它。|如果尚未安装 Microsoft .NET Framework 的最低版本，则可下载 [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653)。<br /><br />此最低版本的 Microsoft .NET Framework 是 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理模块使用的某些类所必需的。|

> [!NOTE]
> 从 Rights Management 管理模块的 2.5.0.0 版本开始，不再需要 Microsoft Online Services 登录助手 。
> 
> 如果你安装有 Rights Management 管理模块的早期版本，请在安装最新版本之前使用“程序和功能”卸载 **Microsoft Azure AD Rights Management 管理**。


## <a name="how-to-install-the-rights-management-administration-module"></a>如何安装权限管理管理模块

1.  转到 Microsoft 下载中心并[下载 Azure Rights Management 管理工具](https://go.microsoft.com/fwlink/?LinkId=257721)，其中包含 Windows PowerShell 的 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 管理模块。

2.  从你下载和保存[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]安装程序文件的本地文件夹，双击你为平台下载的可执行文件（WindowsAzureADRightsManagementAdministration_x64 或 WindowsAzureADRightsManagementAdministration_x86.exe），以启动 Azure AD 权限管理管理设置向导。

3.  完成向导。

适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 现已安装。

## <a name="next-steps"></a>后续步骤
启动 Windows PowerShell 会话，并确认已安装模块的版本。 如果从较旧版本进行升级，则此检查非常重要：

```
(Get-Module AADRM –ListAvailable).Version
```

注意：如果此命令失败，则首先运行 **Import-Module AADRM**。

若要查看可用的 cmdlet，请键入以下命令：

```
Get-Command -Module AADRM
```

使用 `Get-Help <cmdlet_name>` 命令查看有关特定 cmdlet 的帮助，使用 **-online** 参数以在 Microsoft 文档网站上查看最新的帮助。 例如：

```
Get-Help Connect-AadrmService -online
```


参考信息：

-   可用 cmdlet 的完整列表：[AADRM 模块](/powershell/aadrm/vlatest/rightsmanagement)

-   支持 PowerShell 的主要配置方案的列表：[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)

必须先使用 [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) cmdlet 连接到服务，才可运行任何用于配置 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服务的命令。 

在完成运行配置命令之后，作为最佳做法，请使用 [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) cmdlet 断开与服务的连接。 如果不断开连接，处于不活动状态一段时间后将自动断开连接。 鉴于自动断开连接行为，你可能发现你需要在 PowerShell 会话中偶尔执行重新连接。 

> [!NOTE]
> 如果尚未激活 Azure Rights Management 服务，则可在连接到服务之后，使用[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm) cmdlet 进行激活。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]