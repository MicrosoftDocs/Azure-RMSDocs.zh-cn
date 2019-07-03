---
title: 安装用于 Azure 信息保护 AIPService PowerShell 模块
description: 若要安装 Azure 信息保护中保护服务的 PowerShell 的说明。 此模块的名称是 AIPService。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c986b34f3138a3410cb0d675c016206a752ad0c8
ms.sourcegitcommit: a2542aec8cd2bf96e94923740bf396badff36b6a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67535018"
---
# <a name="installing-the-aipservice-powershell-module"></a>安装 AIPService PowerShell 模块

>适用对象：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

使用以下信息来帮助你安装 Azure 信息保护中保护服务的 Windows PowerShell 模块。 此模块的名称是 AIPService，和它将替换以前的版本，名为 AADRM。

您可以使用此 PowerShell 模块管理保护服务 (Azure Rights Management) 从命令行使用任何计算机具有 Internet 连接且满足下一节中列出的先决条件。 适用于 Azure 信息保护的 Windows PowerShell 支持自动化脚本，或者可能是高级的配置方案所必需的。 有关管理任务和配置该模块支持的详细信息，请参阅[使用 PowerShell 管理 Azure 信息保护中的保护](administer-powershell.md)。

## <a name="prerequisites"></a>先决条件
此表列出了安装和使用 Azure 信息保护中保护服务 AIPService PowerShell 模块的先决条件。

|要求|更多信息|
|---------------|--------------------|
|Windows PowerShell 的最低版本：3.0|你可在 PowerShell 会话中键入 `$PSVersionTable`，以确认正在运行的 Windows PowerShell 的版本。 <br /><br /> 如果需要安装更高版本的 Windows PowerShell，请参阅[升级现有的 Windows PowerShell](/powershell/scripting/setup/installing-windows-powershell#upgrading-existing-windows-powershell)。|
|Microsoft.NET framework 的最低版本：4.5<br /><br />注意：此版本的 Microsoft.NET Framework 是附带更高版本的操作系统，因此应需要手动安装它，仅当将客户端操作系统低于 Windows 8.0 或服务器操作系统低于 Windows Server 2012。|如果尚未安装 Microsoft .NET Framework 的最低版本，则可下载 [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)。<br /><br />Microsoft.NET Framework 的此最小版本是必需的某些 AIPService 模块使用的类。|

## <a name="if-you-have-the-aadrm-module-installed"></a>如果已安装了 AADRM 模块

AIPService 模块将替换较旧的模块，AADRM。 如果你已安装较旧的模块，将其卸载，然后安装 AIPService 模块。

较新模块了到较旧的模块中的 cmdlet 名称的别名，因此，任何现有的脚本将继续工作。 但是，计划先旧模块超出支持更新这些引用。 有关 AADRM 模块支持将结束于 2020 年 7 月 15 日。

如果使用 Azure Rights Management 管理工具安装 AADRM 模块，使用**程序和功能**卸载**Windows Azure AD Rights Management 管理**。


## <a name="how-to-install-the-aipservice-module"></a>如何安装 AIPService 模块

AIPService 模块位于[PowerShell 库](/powershell/gallery/readme)，不能从 Microsoft 下载中心获得。 

### <a name="to-install-the-aipservice-module-from-the-powershell-gallery"></a>若要从 PowerShell 库安装 AIPService 模块

如果不熟悉 PowerShell 库，请参阅 [PowerShell 库入门](/powershell/gallery/psgallery/psgallery_gettingstarted)。 按照库要求的说明进行操作，其中包括安装 PowerShellGet 模块和 NuGet 提供程序的说明。

若要在 PowerShell 库上查看有关 AIPService 模块的详细信息，请访问[AIPService 页](https://www.powershellgallery.com/packages/AIPService)。

若要安装 AIPService 模块，请启动一个 PowerShell 会话**以管理员身份运行**选项，然后键入：

    Install-Module -Name AIPService

如果从不受信任的存储库安装，将收到警告，可以按 Y 键确认。 或者，按 N 键并使用该命令将 PowerShell 库配置为受信任的存储库`Set-PSRepository -Name PSGallery -InstallationPolicy Trusted`，然后重新运行命令以安装 AIPService 模块。  

如果必须从库中安装 AIPService 模块的早期版本，请更新到最新通过键入：

    Update-Module -Name AIPService


## <a name="next-steps"></a>后续步骤
在 Windows PowerShell 会话中，确认已安装模块的版本。 如果从较旧版本进行升级，则此检查非常重要：

```
(Get-Module AIPService –ListAvailable).Version
```

注意：如果此命令会失败，第一次运行**导入模块 AIPService**。

若要查看可用的 cmdlet，请键入以下命令：

```
Get-Command -Module AIPService
```

使用 `Get-Help <cmdlet_name>` 命令查看有关特定 cmdlet 的帮助，使用 **-online** 参数以在 Microsoft 文档网站上查看最新的帮助。 例如：

```
Get-Help Connect-AipService -online
```

参考信息：

-   可用的 cmdlet 的完整列表：[AIPService 模块](/powershell/module/aipservice/?view=azureipps#aipservice)

-   支持 PowerShell 的主要配置方案的列表：[使用 PowerShell 管理 Azure 信息保护中的保护](administer-powershell.md)

在可以运行配置保护服务的任何命令之前，您必须通过使用连接到服务[Connect AipService](/powershell/module/aipservice/connect-aipservice) cmdlet。

完成运行配置命令之后，最佳做法，从服务使用断开[断开连接 AipService](/powershell/module/aipservice/disconnect-aipservice) cmdlet。 如果不断开连接，处于不活动状态一段时间后将自动断开连接。 鉴于自动断开连接行为，你可能发现你需要在 PowerShell 会话中偶尔执行重新连接。 

> [!NOTE]
> 如果尚未激活保护服务，你可以执行此操作后使用连接到服务，[启用 AipService](/powershell/module/aipservice/enable-aipservice) cmdlet。

