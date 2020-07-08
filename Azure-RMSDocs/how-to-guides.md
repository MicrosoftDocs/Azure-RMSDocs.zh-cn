---
title: Azure 信息保护的操作说明常见方案
description: 确定使用 Azure 信息保护来分类和保护组织数据的用例。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5059215c9883552e1a4ccf3b902664d1d357e51a
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048436"
---
# <a name="how-to-guides-for-common-scenarios-that-use-azure-information-protection"></a>使用 Azure 信息保护的常见应用场景的操作方法指南

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

可以通过多种方式使用 Azure 信息保护对组织的文档和电子邮件进行分类和选择性保护。 

最成功的部署是那些能够确定为组织提供最大业务优势的特定用例的部署。 使用以下常见应用场景和说明列表来实现部署。

## <a name="common-scenarios"></a>常见方案

|应用场景：我想要实现以下目标……|说明|
|----------------|---------------|
|查找我的组织在本地存储的敏感信息|[快速入门：查找在本地存储的文件中的敏感信息](quickstart-findsensitiveinfo.md)|
|让用户可以轻松保护包含敏感信息的电子邮件|[快速入门：为用户配置标签，以便轻松保护包含敏感信息的电子邮件](quickstart-label-dnf-protectedemail.md)|
|让用户可以轻松地在创建或编辑数据时对数据进行分类，并在数据包含敏感信息时对其进行保护| [教程：编辑策略并创建新标签](infoprotect-quick-start-tutorial.md)|
|让用户易于针对受保护的文档进行协作|[使用 Azure 信息保护配置可靠的文档协作](secure-collaboration-documents.md)|
|自动保护在组织外部发送的用户电子邮件| [配置 Azure 信息保护标签的邮件流规则](configure-exo-rules.md)
|自动对本地数据存储中的现有数据进行分类和保护|[部署 Azure 信息保护扫描程序](deploy-aip-scanner.md)|
|用我自己的密钥来保护组织数据| [计划和实现你的租户密钥](plan-implement-tenant-key.md)|
|从 AD RMS 中迁移|[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)|

## <a name="additional-deployment-instructions"></a>其他部署说明

我们的[Azure 信息保护技术博客](https://aka.ms/AIPblog)包含来自实践经验教训的其他指导。

例如，为业务决策者和 IT 实施者提供最佳做法的方法：

- [Azure 信息保护部署加速指南](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Deployment-Acceleration-Guide/ba-p/334423)

分步说明：

- [如何生成自定义 AIP 跟踪门户](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-Build-a-Custom-AIP-Tracking-Portal/ba-p/875849)

- [利用 Microsoft 信息保护创建更丰富的报表，并 Azure AD 登录数据](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Create-richer-reports-with-Microsoft-Information-Protection-and/ba-p/392713)

- [利用 Microsoft Cloud App Security 在云中应用 Azure 信息保护标签](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Leverage-Microsoft-Cloud-App-Security-to-apply-Azure-Information/ba-p/388638)

- [如何准备 Azure 信息保护 "云退出" 计划](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631)

- [跨租户标签可视化](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cross-Tenant-Label-Visualization/ba-p/356588)

- [Using Azure Information Protection to protect PDF’s and Adobe Acrobat Reader to view them](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Using-Azure-Information-Protection-to-protect-PDF-s-and-Adobe/ba-p/282010)（使用 Azure 信息保护来保护 PDF 和 Adobe Acrobat Reader 以查看它们）

- [Cataloging your Sensitive Data with AIP, Even Before Configuring Labels!](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cataloging-your-Sensitive-Data-with-AIP-Even-Before-Configuring/ba-p/267241)（使用 AIP 编录敏感数据，甚至在配置标签之前！）

- [Azure Information Protection Scanner Express Installation](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Scanner-Express-Installation/ba-p/265424)（Azure 信息保护扫描程序快速安装）

- [Discovery of Sensitive Data Using the AIP Scanner (AIP Premium P1)](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discovery-of-Sensitive-Data-Using-the-AIP-Scanner-AIP-Premium-P1/ba-p/252040)（使用 AIP 扫描程序 (AIP 高级 P1) 发现敏感数据）

## <a name="next-steps"></a>后续步骤

没有列出你的应用场景？ 请查看[部署路线图](deployment-roadmap.md)，了解有关规划和部署步骤的完整列表。

如果你是初次接触 Azure 信息保护，请查看[什么是 Azure 信息保护？](what-is-information-protection.md)，快速了解服务，以便开始部署。
