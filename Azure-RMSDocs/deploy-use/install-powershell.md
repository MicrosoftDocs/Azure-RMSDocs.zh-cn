---
title: 安装适用于 AADRM 的 PowerShell - AIP
description: 安装适用于 Azure 信息保护中的 Azure Rights Management 服务的 Windows PowerShell 的说明 此模块的名称是 AADRM。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d061a7e65bce1e5072e4e06fd3ed1ef2132810c8
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="installing-the-aadrm-powershell-module"></a>安装 AADRM PowerShell 模块

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用以下信息帮助安装适用于 Azure 信息保护中的 Azure Rights Management 服务的 Windows PowerShell 模块。 此模块的名称是 AADRM。

在任何具有 Internet 连接且满足下一节列出的先决条件的计算机上，可以使用此 PowerShell 模块从命令行管理 Azure Rights Management 服务。 适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 支持脚本的自动化，或者可能是高级配置方案所必需的。 若要深入了解此模块支持的管理任务和配置，请参阅[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)。

## <a name="prerequisites"></a>必备条件
此表列出了安装和使用适用于 Azure 信息保护中的 Azure Rights Management 服务的 AADRM PowerShell 模块的先决条件。

|要求|详细信息|
|---------------|--------------------|
|Windows PowerShell 的最低版本：3.0|你可在 PowerShell 会话中键入 `$PSVersionTable`，以确认正在运行的 Windows PowerShell 的版本。 <br /><br /> 如果需要安装更高版本的 Windows PowerShell，请参阅[升级现有的 Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell)。|
|Microsoft .NET Framework 的最低版本：4.5<br /><br />请注意：较高版本的操作系统都附带此版本的 Microsoft .NET Framework，因此只有在你的客户端操作系统低于 Windows 8.0 或服务器操作系统低于 Windows Server 2012 的情况下，才需要手动安装它。|如果尚未安装 Microsoft .NET Framework 的最低版本，则可下载 [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653)。<br /><br />此最低版本的 Microsoft .NET Framework 是 AADRM 模块使用的某些类所必需的。|

> [!NOTE]
> 从 AADRM 模块的 2.5.0.0 版本开始，不再需要 Microsoft Online Services 登录助手了。
> 
> 如果安装了 AADRM 模块的早期版本，请在安装最新版本之前使用“程序和功能”卸载 Windows Azure AD Rights Management 管理。


## <a name="how-to-install-the-aadrm-module"></a>如何安装 AADRM 模块

尽管 AADRM 模块将移至 [PowerShell 库](/powershell/gallery/readme)，但在有限的一段时间内也会在 Microsoft 下载中心中提供。 

### <a name="to-install-the-aadrm-module-from-the-powershell-gallery"></a>从 PowerShell 库安装 AADRM 模块

如果不熟悉 PowerShell 库，请参阅 [PowerShell 库入门](/powershell/gallery/psgallery/psgallery_gettingstarted)。 按照库要求的说明进行操作，其中包括安装 PowerShellGet 模块和 NuGet 提供程序的说明。

若要在 PowerShell 库上查看有关 AADRM 模块的详细信息，请访问 [AADRM 页面](https://www.powershellgallery.com/packages/AADRM)。

若要安装 AADRM 模块，请启动 PowerShell 会话并键入：

    Install-Module -Name AADRM


### <a name="to-install-the-aadrm-module-from-the-microsoft-download-center"></a>从 Microsoft 下载中心安装 AADRM 模块

1. 转到 Microsoft 下载中心，并找到 [Azure Rights Management 管理工具](https://go.microsoft.com/fwlink/?LinkId=257721)，其中包含 Windows PowerShell 的 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 管理模块。

2. 下载并保存 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 安装程序文件 WindowsAzureADRightsManagementAdministration_x64。 然后，双击此文件，以启动 Azure AD Rights Management 管理工具安装程序向导。

3.  完成此向导，这将安装 AADRM PowerShell 模块。

## <a name="next-steps"></a>后续步骤
在 Windows PowerShell 会话中，确认已安装模块的版本。 如果从较旧版本进行升级，则此检查非常重要：

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

必须先使用 [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) cmdlet 连接到服务，才可运行任何用于配置 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服务的命令。 在完成运行配置命令之后，作为最佳做法，请使用 [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) cmdlet 断开与服务的连接。 如果不断开连接，处于不活动状态一段时间后将自动断开连接。 鉴于自动断开连接行为，你可能发现你需要在 PowerShell 会话中偶尔执行重新连接。 

> [!NOTE]
> 如果尚未激活 Azure Rights Management 服务，则可在连接到服务之后，使用[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm) cmdlet 进行激活。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]