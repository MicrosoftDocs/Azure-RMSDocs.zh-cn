---
title: 使用 Azure 信息保护的常见应用场景的操作方法说明。
description: 通过使用 Azure 信息保护，确定对组织数据进行分类和保护的用例。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 7986648999a830985c4dbd1f31855bb222a443c2
ms.sourcegitcommit: 2a1c0882d2b0400f4da6370dbc1830df09867e3d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53218368"
---
# <a name="how-to-guides-for-common-scenarios-that-use-azure-information-protection"></a>使用 Azure 信息保护的常见应用场景的操作方法指南

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

可以通过多种方式使用 Azure 信息保护对组织的文档和电子邮件进行分类和选择性保护。 

最成功的部署是那些能够确定为组织提供最大业务优势的特定用例的部署。 使用以下常见应用场景和说明列表来实现部署。

## <a name="common-scenarios"></a>常见方案

|方案：我希望…|说明|
|----------------|---------------|
|查找我的组织在本地存储的敏感信息|[快速入门：查找在本地存储的文件中的敏感信息](quickstart-findsensitiveinfo.md)|
|让用户可以轻松保护包含敏感信息的电子邮件|[快速入门：为用户配置标签以便轻松保护包含敏感信息的电子邮件](quickstart-label-dnf-protectedemail.md)|
|让用户可以轻松地在创建或编辑数据时对数据进行分类，并在数据包含敏感信息时对其进行保护| [教程：编辑策略并创建新标签](infoprotect-quick-start-tutorial.md)|
|让用户易于针对受保护的文档进行协作|[使用 Azure 信息保护配置可靠的文档协作](secure-collaboration-documents.md)|
|自动保护在组织外部发送的用户电子邮件| [配置 Azure 信息保护标签的邮件流规则](configure-exo-rules.md)
|自动对本地数据存储中的现有数据进行分类和保护|[部署 Azure 信息保护扫描程序](deploy-aip-scanner.md)|
|用我自己的密钥来保护组织数据| [计划和实现你的租户密钥](plan-implement-tenant-key.md)|
|从 AD RMS 中迁移|[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)|

## <a name="additional-deployment-instructions"></a>其他部署说明

我们的[Azure 信息保护技术博客](https://aka.ms/AIPblog)有来自客户体验工程团队提供的其他分步说明。 例如：

- [Using Azure Information Protection to protect PDF’s and Adobe Acrobat Reader to view them](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Using-Azure-Information-Protection-to-protect-PDF-s-and-Adobe/ba-p/282010)（使用 Azure 信息保护来保护 PDF 和 Adobe Acrobat Reader 以查看它们）

- [Cataloging your Sensitive Data with AIP, Even Before Configuring Labels!](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cataloging-your-Sensitive-Data-with-AIP-Even-Before-Configuring/ba-p/267241)（使用 AIP 编录敏感数据，甚至在配置标签之前！）

- [Azure Information Protection Scanner Express Installation](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Scanner-Express-Installation/ba-p/265424)（Azure 信息保护扫描程序快速安装）

- [Discovery of Sensitive Data Using the AIP Scanner (AIP Premium P1)](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discovery-of-Sensitive-Data-Using-the-AIP-Scanner-AIP-Premium-P1/ba-p/252040)（使用 AIP 扫描程序 (AIP 高级 P1) 发现敏感数据）

## <a name="next-steps"></a>后续步骤

没有列出你的应用场景？ 请查看[部署路线图](deployment-roadmap.md)，了解有关规划和部署步骤的完整列表。

如果你是初次接触 Azure 信息保护，请查看[什么是 Azure 信息保护？](what-is-information-protection.md)，快速了解服务，以便开始部署。
