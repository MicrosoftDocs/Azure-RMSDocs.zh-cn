---
title: 保护模板的 PowerShell - Azure 信息保护
description: 使用 PowerShell cmdlet 来添加、获取、导出、导入、删除和配置 Azure 信息保护的保护模板。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ROBOTS: NOINDEX
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c8e4c54dee7494aaecadb6de943544e7a1f6c109
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806356"
---
# <a name="powershell-reference-for-protection-templates"></a>保护模板的 PowerShell 参考

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标签客户端，请参阅 Microsoft 365 文档中的 " [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) "。 *

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>

Azure 信息保护的保护设置保存在保护模板中。 在 Azure 门户中创建和管理保护设置所需执行的一切操作均可使用 PowerShell 从命令行执行。 

此外，还可导出和导入保护模板。 通过这两个操作，可以在租户间复制保护模板，也可以执行复杂属性的批量编辑，如多语言名称和说明。

还可通过导出和导入来备份和还原保护模板。 定期备份模板是一种最佳做法。 如果意外更改了保护设置，可轻松还原至先前版本。

有关安装说明，请参阅 [安装 AIPService PowerShell 模块](install-powershell.md)。

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

