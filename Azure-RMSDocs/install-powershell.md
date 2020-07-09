---
title: 安装适用于 Azure 信息保护的 AIPService PowerShell 模块
description: 说明如何从 Azure 信息保护中为保护服务安装 PowerShell。 此模块的名称为 AIPService。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 23c18236413aaa2056d3eaaa30a64430de1e608b
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136832"
---
# <a name="installing-the-aipservice-powershell-module"></a>安装 AIPService PowerShell 模块

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

使用以下信息来帮助你为 Azure 信息保护中的保护服务安装 Windows PowerShell 模块。 此模块的名称为 AIPService，它将替换名为 AADRM 的以前的版本。

通过使用具有 internet 连接且满足下一节列出的先决条件的任何 Windows 计算机，你可以使用此 PowerShell 模块从命令行管理保护服务（Azure Rights Management）。 适用于 Azure 信息保护的 Windows PowerShell 支持自动化脚本，或者可能是高级配置方案所必需的。 有关模块支持的管理任务和配置的详细信息，请参阅[使用 PowerShell 管理 Azure 信息保护中的保护](administer-powershell.md)。

## <a name="prerequisites"></a>必备条件

此表列出了安装和使用适用于 Azure 信息保护中的保护服务的 AIPService PowerShell 模块的先决条件。

|要求|详细信息|
|---------------|--------------------|
|Windows PowerShell 的最低版本：3.0|你可在 PowerShell 会话中键入 `$PSVersionTable`，以确认正在运行的 Windows PowerShell 的版本。 <br /><br /> 如需安装更高版本的 Windows PowerShell，请参阅[升级现有 Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell)。|
|Microsoft .NET Framework 的最低版本：4.5<br /><br />请注意：较高版本的操作系统都附带此版本的 Microsoft .NET Framework，因此只有在你的客户端操作系统低于 Windows 8.0 或服务器操作系统低于 Windows Server 2012 的情况下，才需要手动安装它。|如果尚未安装 Microsoft .NET Framework 的最低版本，则可以下载[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)。<br /><br />AIPService 模块使用的某些类需要此最低版本的 Microsoft .NET 框架。|

## <a name="if-you-have-the-aadrm-module-installed"></a>如果已安装 AADRM 模块

AIPService 模块取代了较旧的模块 AADRM。 如果安装了较旧的模块，请将其卸载，然后安装 AIPService 模块。

较新的模块具有较旧模块中的 cmdlet 名称的别名，因此，任何现有脚本都将继续工作。 不过，计划在旧模块不支持之前更新这些引用。 AADRM 模块的支持将于2020年7月15日结束。

如果从 PowerShell 库安装了 AADRM 模块，若要卸载它，请使用 "以**管理员身份运行**" 选项启动 PowerShell 会话，然后键入：

```ps
Uninstall-Module -Name AADRM
```

如果使用 Azure Rights Management 管理工具安装了 AADRM 模块，请使用 "**程序和功能**" 卸载**Windows Azure AD Rights Management 管理**。

## <a name="how-to-install-the-aipservice-module"></a>如何安装 AIPService 模块

AIPService 模块位于[PowerShell 库](https://www.powershellgallery.com/)上，不能从 Microsoft 下载中心获取。

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>从 PowerShell 库安装 AIPService 模块

如果不熟悉 PowerShell 库，请参阅 [PowerShell 库入门](https://docs.microsoft.com/powershell/scripting/gallery/getting-started?view=powershell-6)。 按照库要求的说明进行操作，其中包括安装 PowerShellGet 模块和 NuGet 提供程序的说明。

若要查看 PowerShell 库上的 AIPService 模块的详细信息，请访问[AIPService 页](https://www.powershellgallery.com/packages/AIPService)。

若要安装 AIPService 模块，请使用 "以**管理员身份运行**" 选项启动 PowerShell 会话，然后键入：

```ps
Install-Module -Name AIPService
```

如果从不受信任的存储库安装，将收到警告，可以按 Y 键确认。 或者，按 N 并使用命令将 PowerShell 库配置为受信任的存储库， `Set-PSRepository -Name PSGallery -InstallationPolicy Trusted` 然后重新运行命令以安装 AIPService 模块。  

如果从库中安装了以前版本的 AIPService 模块，请键入以下内容将其更新为最新版本：

```ps
Update-Module -Name AIPService
```

## <a name="next-steps"></a>后续步骤

在 Windows PowerShell 会话中，确认已安装模块的版本。 如果从较旧版本进行升级，则此检查非常重要：

```ps
(Get-Module AIPService –ListAvailable).Version
```

> [!NOTE]
> 如果此命令失败，请首先运行**Import-module AIPService**。
> 

若要查看可用的 cmdlet，请键入以下命令：

```ps
Get-Command -Module AIPService
```

使用 `Get-Help <cmdlet_name>` 命令查看有关特定 cmdlet 的帮助，使用 **-online** 参数以在 Microsoft 文档网站上查看最新的帮助。 例如:

```powershell
Get-Help Connect-AipService -online
```

更多相关信息：

- 可用 cmdlet 的完整列表： [AIPService 模块](/powershell/module/aipservice/?view=azureipps#aipservice)

- 支持 PowerShell 的主要配置方案的列表：[使用 Powershell 管理 Azure 信息保护的保护](administer-powershell.md)

必须先使用[AipService](/powershell/module/aipservice/connect-aipservice) cmdlet 连接到服务，然后才能运行任何命令来配置保护服务。

完成运行配置命令后，最佳做法是使用[AipService](/powershell/module/aipservice/disconnect-aipservice) cmdlet 断开与服务的连接。 如果不断开连接，处于不活动状态一段时间后将自动断开连接。 鉴于自动断开连接行为，你可能发现你需要在 PowerShell 会话中偶尔执行重新连接。

> [!NOTE]
> 如果保护服务尚未激活，可以在使用[AipService](/powershell/module/aipservice/enable-aipservice) cmdlet 连接到服务后执行此操作。
