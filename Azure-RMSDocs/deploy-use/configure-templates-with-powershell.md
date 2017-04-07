---
title: "适用于 Azure RMS 自定义模板的 PowerShell - AIP"
description: "在 Azure 经典门户中创建和管理权限管理模板所执行的一切操作均可使用 PowerShell 从命令行执行。 此外，你还能够导出和导入模板，因此能够在租户之间复制模板，或者在模板中执行对复杂属性（例如多语言名称和描述）的批量编辑。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 40db2ba3856cab24f0162a1b46960816b85a5089
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="powershell-reference-for-custom-templates"></a>自定义模板的 PowerShell 参考

>*适用于：Azure 信息保护、Office 365*

在 Azure 经典门户中创建和管理权限管理模板所执行的一切操作均可使用 PowerShell 从命令行执行。 此外，你还能够导出和导入模板，因此能够在租户之间复制模板，或者在模板中执行对复杂属性（例如多语言名称和描述）的批量编辑。

你还可以使用导出和导入来备份和还原自定义模板，最好是经常备份你的自定义模板，这样一来，如果你发现所做的更改不是你想要的，即可轻松还原到以前的版本。

> [!IMPORTANT]
> 若要使用 Windows PowerShell 来创建和管理 Azure Rights Management 模板，必须安装至少 2.0.0.0 版的[适用于 Azure RMS 的 Windows PowerShell 模块](http://go.microsoft.com/fwlink/?LinkId=257721)。
> 
> 如果之前已经安装了此 PowerShell 模块，请在 PowerShell 窗口中运行以下命令以检查版本号：`(Get-Module aadrm -ListAvailable).Version`

有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。

支持创建和管理模板的 cmdlet：

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## <a name="see-also"></a>另请参阅
[为 Azure Rights Management 配置自定义模板](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]