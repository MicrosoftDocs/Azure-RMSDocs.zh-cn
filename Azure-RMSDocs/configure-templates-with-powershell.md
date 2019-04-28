---
title: 保护模板的 PowerShell - Azure 信息保护
description: 在 Azure 门户中创建和管理保护模板所需执行的一切操作均可使用 PowerShell 从命令行执行。 此外，你还能够导出和导入模板，因此能够在租户之间复制模板，或者在模板中执行对复杂属性（例如多语言名称和描述）的批量编辑。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e1915c327daaee35d9f0e8053f944fd1fcdbd7a
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60179672"
---
# <a name="powershell-reference-for-protection-templates"></a>保护模板的 PowerShell 参考

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

Azure 信息保护的保护设置保存在保护模板中。 在 Azure 门户中创建和管理保护设置所需执行的一切操作均可使用 PowerShell 从命令行执行。 

此外，还可导出和导入保护模板。 通过这两个操作，可以在租户间复制保护模板，也可以执行复杂属性的批量编辑，如多语言名称和说明。

还可通过导出和导入来备份和还原保护模板。 定期备份模板是一种最佳做法。 如果意外更改了保护设置，可轻松还原至先前版本。

有关安装说明，请参阅[安装 AADRM PowerShell 模块](install-powershell.md)。

支持创建和管理保护模板的 cmdlet：

- [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate)

- [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate)

- [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate)

- [Get-AadrmTemplateProperty](/powershell/module/aadrm/get-aadrmtemplateproperty)

- [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate)

- [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition)

- [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate)

- [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty)



## <a name="see-also"></a>请参阅
[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)

