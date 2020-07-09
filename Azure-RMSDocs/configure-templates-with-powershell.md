---
title: 保护模板的 PowerShell - Azure 信息保护
description: 使用 PowerShell 创建和管理 Azure 信息保护的保护模板。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 38d5a71e6820c4ad95395c06dffea5d5e57ee7d6
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136783"
---
# <a name="powershell-reference-for-protection-templates"></a>保护模板的 PowerShell 参考

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure 信息保护的保护设置保存在保护模板中。 在 Azure 门户中创建和管理保护设置所需执行的一切操作均可使用 PowerShell 从命令行执行。 

此外，还可导出和导入保护模板。 通过这两个操作，可以在租户间复制保护模板，也可以执行复杂属性的批量编辑，如多语言名称和说明。

还可通过导出和导入来备份和还原保护模板。 定期备份模板是一种最佳做法。 如果意外更改了保护设置，可轻松还原至先前版本。

有关安装说明，请参阅[安装 AIPService PowerShell 模块](install-powershell.md)。

支持创建和管理保护模板的 cmdlet：

- [AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)

- [导出-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)

- [AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)

- [AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)

- [导入-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetpd)

- [新-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)

- [AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)

- [AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)

## <a name="see-also"></a>另请参阅
[配置和管理 Azure 信息保护的模板](configure-policy-templates.md)

