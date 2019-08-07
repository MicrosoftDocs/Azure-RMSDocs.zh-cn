---
title: 保护模板的 PowerShell - Azure 信息保护
description: 在 Azure 门户中创建和管理保护模板所需执行的一切操作均可使用 PowerShell 从命令行执行。 此外, 可以在租户之间复制模板, 或者在模板中执行复杂属性的批量编辑, 如多语言名称和说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 105286f907df4f8c8f0f329e4467d4dc1d95422e
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68791546"
---
# <a name="powershell-reference-for-protection-templates"></a>保护模板的 PowerShell 参考

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

Azure 信息保护的保护设置保存在保护模板中。 在 Azure 门户中创建和管理保护设置所需执行的一切操作均可使用 PowerShell 从命令行执行。 

此外，还可导出和导入保护模板。 通过这两个操作，可以在租户间复制保护模板，也可以执行复杂属性的批量编辑，如多语言名称和说明。

还可通过导出和导入来备份和还原保护模板。 定期备份模板是一种最佳做法。 如果意外更改了保护设置，可轻松还原至先前版本。

有关安装说明, 请参阅[安装 AIPService PowerShell 模块](install-powershell.md)。

支持创建和管理保护模板的 cmdlet：

- [Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)

- [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)

- [Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)

- [Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)

- [Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetpd)

- [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)

- [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)

- [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)



## <a name="see-also"></a>请参阅
[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)

