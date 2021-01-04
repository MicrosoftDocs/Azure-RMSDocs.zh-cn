---
title: 使用 FCI 的 Windows 文件服务器 Azure RMS-AIP 的支持方式
description: 部署 RMS 连接器时如何将 Windows Server 文件分类基础结构与 Azure RMS 结合使用以自动保护 Office 文档。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ROBOTS: NOINDEX
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2de7d165c72dbd6c96f76d7027c1a2d3ba62bff1
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806186"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>使用 FCI 的 Windows 文件服务器如何支持 Azure Rights Management

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>相关内容：*[适用于 Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

当你将 Windows Server 配置为使用文件分类基础结构时，此文件服务器资源管理器功能可以扫描本地文件，并确定它们是否包含敏感数据。 

满足此条件的文件使用管理员定义的分类属性进行标记。 然后，文件分类基础结构可根据分类执行自动操作。 

其中一项操作包括使用 Azure Rights Management 和 Rights Management (连接器的部署（也称为 RMS 连接器) ）来应用信息保护。 然后，由 Azure RMS 自动保护 Office 文件。

> [!TIP]
> 若要保护所有文件类型，请不要使用 RMS 连接器，而是改为运行 Windows PowerShell 脚本，该脚本使用 [Azure 信息保护模块](./rms-client/client-admin-guide-powershell.md)中的 cmdlet。
> 

分类策略是完全可以配置的，并且具有高度的可扩展性，因此你可以防止未授权和已授权用户可能发生的数据泄漏。 它甚至有助于降低网络管理员的数据泄漏风险，因为你可以配置不要求这些管理员具有文件访问权限的策略。

有关为 Office 文件部署和配置 RMS 连接器的说明，请参阅 [部署 Azure Rights Management 连接器](deploy-rms-connector.md)。

有关对所有文件类型使用 Windows PowerShell 脚本的说明，请参阅 

- [采用 Windows Server 文件分类基础结构的 RMS 保护 &#40;FCI&#41;](./rms-client/configure-fci.md)
- [使用资源管理器 FCI 的文件服务器 Azure RMS 保护的 Windows PowerShell 脚本](rms-client/fci-script.md)


## <a name="next-steps"></a>后续步骤

至此，已了解应用程序和服务如何支持 Azure RMS，建议比较 Azure RMS 与本地版 Rights Management、Active Directory Rights Management Services (AD RMS)。 有关功能、要求和安全控制的比较，请参阅 [比较 Azure Rights Management 和 AD RMS](compare-on-premise.md)。


