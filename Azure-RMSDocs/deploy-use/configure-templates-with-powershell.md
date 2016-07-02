---
title: "自定义模板的 PowerShell 参考 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: 645f9ed4080e3b38fcda9afe148923c021046724


---



# 自定义模板的 PowerShell 参考

*适用于：Azure Rights Management、Office 365*

在 Azure 经典门户中创建和管理模板所需执行的操作均可使用 PowerShell 从命令行执行。 此外，你还能够导出和导入模板，因此能够在租户之间复制模板，或者在模板中执行对复杂属性（例如多语言名称和描述）的批量编辑。

你还可以使用导出和导入来备份和还原自定义模板，最好是经常备份你的自定义模板，这样一来，如果你发现所做的更改不是你想要的，即可轻松还原到以前的版本。

> [!IMPORTANT]
> 若要使用 Windows PowerShell 来创建和管理 Azure RMS 权限策略模板，必须安装至少 2.0.0.0 版的 [适用于 Azure RMS 的 Windows PowerShell 模块](http://go.microsoft.com/fwlink/?LinkId=257721)。
> 
> 如果之前已经安装了此 PowerShell 模块，请在 PowerShell 窗口中运行以下命令以检查版本号： `(Get-Module aadrm -ListAvailable).Version`

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



## 另请参阅
[为 Azure Rights Management 配置自定义模板](configure-custom-templates.md)


<!--HONumber=Jun16_HO4-->


