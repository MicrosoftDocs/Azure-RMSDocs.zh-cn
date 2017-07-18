---
title: "适用于 Azure RMS 自定义模板的 PowerShell - AIP"
description: "在 Azure 经典门户中创建和管理权限管理模板所执行的一切操作均可使用 PowerShell 从命令行执行。 此外，你还能够导出和导入模板，因此能够在租户之间复制模板，或者在模板中执行对复杂属性（例如多语言名称和描述）的批量编辑。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8da24d00f6b6cb62bc745404e68e691b5afc2cb8
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="powershell-reference-for-custom-templates"></a>自定义模板的 PowerShell 参考

>*适用于：Azure 信息保护、Office 365*

在 Azure 经典门户中创建和管理权限管理模板所执行的一切操作均可使用 PowerShell 从命令行执行。 此外，你还能够导出和导入模板，因此能够在租户之间复制模板，或者在模板中执行对复杂属性（例如多语言名称和描述）的批量编辑。

你还可以使用导出和导入来备份和还原自定义模板，最好是经常备份你的自定义模板，这样一来，如果你发现所做的更改不是你想要的，即可轻松还原到以前的版本。

> [!IMPORTANT]
> 若要使用 PowerShell 来创建和管理 Azure 权限管理模板，必须至少安装 2.0.0.0 版的[适用于 Azure RMS 的 Windows PowerShell 模块](https://go.microsoft.com/fwlink/?LinkId=257721)。
> 
> 如果之前已经安装了此 PowerShell 模块，请在 PowerShell 窗口中运行以下命令以检查版本号：`(Get-Module aadrm -ListAvailable).Version`

有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。

支持创建和管理模板的 cmdlet：

- [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate)

- [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate)

- [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate)

- [Get-AadrmTemplateProperty](/powershell/module/aadrm/get-aadrmtemplateproperty)

- [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate)

- [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition)

- [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate)

- [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty)



## <a name="see-also"></a>另请参阅
[为 Azure Rights Management 配置自定义模板](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]