---
title: Azure 信息保护部署路线图
description: 使用这些步骤，为组织准备、实施和管理 Azure 信息保护。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 251b193012dc32518a0a236cf1ee751545d4391e
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382388"
---
# <a name="azure-information-protection-deployment-roadmap"></a>Azure 信息保护部署路线图

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


>[!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

> [!TIP]
> 或者，您可能正在查找以下文章之一：
> - [使用 Azure 信息保护的常见方案的操作指南](how-to-guides.md)
>- [Azure 信息保护发布路线图](information-support.md#information-about-new-releases-and-updates)

使用以下路线图页面中的步骤作为建议，帮助你为组织准备、实施和管理 Azure 信息保护。

## <a name="identify-your-deployment-roadmap"></a>标识部署路线图

在部署 AIP 之前，请查看 [AIP 系统要求](./requirements.md)。

然后，根据组织的需求和 [订阅](https://azure.microsoft.com/pricing/details/information-protection/)选择以下路线图之一：

- **使用分类、标记和保护**：

    对于具有支持订阅的任何客户，建议使用。 其他功能包括发现敏感信息以及标记文档和电子邮件以进行分类。 

    标签还可以应用保护，以便为用户简化此步骤。 

    使用经典客户端创建的 AIP 标签和使用 [统一标签平台](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)的灵敏度标签都支持此路线图。

    有关详细信息，请参阅 [AIP 路线图：对数据进行分类、标记和保护](deployment-roadmap-classify-label-protect.md)。

- **仅使用保护**： 

    建议用于订阅不支持分类和标签的客户，但不支持带标签的保护。 必须安装经典客户端。

    有关详细信息，请参阅 [仅适用于数据保护的 AIP 路线图](deployment-roadmap-protect-only.md)。

## <a name="next-steps"></a>后续步骤

部署 Azure 信息保护时，你可能会发现检查 [常见问题](faqs.md)，以及其他资源的 [信息和支持](information-support.md) 页面非常有用。