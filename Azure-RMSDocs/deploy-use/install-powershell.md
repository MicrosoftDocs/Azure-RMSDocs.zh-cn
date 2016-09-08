---
title: "安装适用于 Azure Rights Management 的 Windows PowerShell | Azure RMS"
description: "使用以下信息可帮助安装适用于 Microsoft Azure RMS 的 Windows PowerShell。"
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0d665ed6-b1de-4d63-854a-bc57c1c49844
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 0f22d69387b89a590b516d3a93148fec82b23acd


---

# 安装适用于 Azure 权限管理的 Windows PowerShell

>*适用于：Azure Rights Management、Office 365*

使用以下信息可帮助安装适用于 Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 的 Windows PowerShell。

在使用任何具有 Internet 连接且满足下一节列出的先决条件的计算机上，你可以使用此 PowerShell 模块从命令行管理 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。 适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 支持脚本的自动化，或者可能是高级配置方案所必需的。 若要深入了解此模块支持的管理任务和配置，请参阅[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)。

## 先决条件
此表列出了安装和使用适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 的先决条件。

|要求|更多信息|
|---------------|--------------------|
|支持[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]管理模块的 Windows 版本|查看 [Azure Rights Management 管理工具下载页](http://go.microsoft.com/fwlink/?LinkId=257721)的“系统要求”部分中的受支持操作系统列表。|
|Windows PowerShell 的最低版本：2.0|Windows PowerShell 2.0 引入了对 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理模块的支持。<br /><br />默认情况下，大多数 Windows 操作系统至少安装了 Windows PowerShell 2.0 版本。 如果你需要安装 Windows PowerShell 2.0，请参阅 [安装 Windows PowerShell 2.0](http://msdn.microsoft.com/library/ff637750.aspx)。<br /><br />提示：你可在 PowerShell 会话中键入 `$PSVersionTable`，以确认正在运行的 Windows PowerShell 的版本。|
|Microsoft .NET Framework 的最低版本：4.5<br /><br />请注意：较高版本的操作系统都附带此版本的 Microsoft .NET Framework，因此只有在你的客户端操作系统低于 Windows 8.0 或服务器操作系统低于 Windows Server 2012 的情况下，才需要手动安装它。|如果尚未安装 Microsoft .NET Framework 的最低版本，则可下载 [Microsoft .NET Framework 4.5](http://www.microsoft.com/download/details.aspx?id=30653)。<br /><br />此最低版本的 Microsoft .NET Framework 是 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理模块使用的某些类所必需的。|

> [!NOTE]
> 从 Rights Management 管理模块的 2.5.0.0 版本开始，不再需要 Microsoft Online Services 登录助手 。
> 
> 如果你安装有 Rights Management 管理模块的早期版本，请在安装最新版本之前使用“程序和功能”卸载 **Microsoft Azure AD Rights Management 管理**。


## 如何安装权限管理管理模块

1.  转到 Microsoft 下载中心并[下载 Azure Rights Management 管理工具](https://go.microsoft.com/fwlink/?LinkId=257721)，其中包含 Windows PowerShell 的 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 管理模块。

2.  从你下载和保存[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]安装程序文件的本地文件夹，双击你为平台下载的可执行文件（WindowsAzureADRightsManagementAdministration_x64 或 WindowsAzureADRightsManagementAdministration_x86.exe），以启动 Azure AD 权限管理管理设置向导。

3.  完成向导。

适用于 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 的 Windows PowerShell 现已安装。

## 后续步骤
若要查看有哪些可用的 cmdlet，请使用“以管理员身份运行”选项启动 Windows PowerShell，并键入以下内容  ：

```
Get-Command -Module aadrm
```
使用 `the Get-Help <cmdlet_name>` 命令查看有关特定 cmdlet 的帮助。

参考信息：

-   可用 cmdlet 的完整列表： [Azure 权限管理 Cmdlet](https://msdn.microsoft.com/library/windowsazure/dn629398.aspx)

-   支持 Windows PowerShell 的主要配置方案的列表：[使用 Windows PowerShell 管理 Azure Rights Management](administer-powershell.md)

你必须先使用 [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) cmdlet 连接到服务，才可运行任何用于配置 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服务的命令。 在完成运行所需的配置命令之后，请使用 [Disconnect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet 断开与服务的连接。

> [!NOTE]
> 如果你尚未激活 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]，则可在连接到服务之后，使用 [Enable-Aadrm](https://msdn.microsoft.com/library/windowsazure/dn629412.aspx) cmdle 进行激活。

## 另请参阅
[使用 Windows PowerShell 管理 Azure 权限管理](administer-powershell.md)



<!--HONumber=Aug16_HO4-->


