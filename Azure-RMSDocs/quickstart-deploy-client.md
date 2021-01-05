---
title: 快速入门 - 部署 Azure 信息保护 (AIP) 统一标记客户端
description: 部署 Azure 信息保护 (AIP) 统一标记客户端的快速介绍
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 468cbe031b22ba07127b75295da98ee9a081048a
ms.sourcegitcommit: 73befea74644d272e2d8d1d4b95df55c7741ccbe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "97762326"
---
# <a name="quickstart-deploying-the-azure-information-protection-aip-unified-labeling-client"></a>快速入门：部署 Azure 信息保护 (AIP) 统一标记客户端

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 相关内容：**[用于 Windows 的 Azure 信息保护统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

Azure 信息保护 (AIP) 统一标记客户端是 [Microsoft 信息保护](https://aka.ms/MIPdocs) 解决方案的一部分，它扩展了 Microsoft 365 提供的敏感度标记的内置功能。 

除了 Office 应用程序之外，客户端还为文件资源管理器和 PowerShell 中的标签和保护提供最终用户支持。 借助统一标签客户端随附的扫描程序，管理员可以扫描网络和内容共享，以发现敏感内容。 

对于没有信息保护平台的组织，客户端为使用 Microsoft 信息保护的其他组织保护的内容提供查看器。

## <a name="review-aip-client-prerequisites"></a>查看 AIP 客户端先决条件

使用下面链接的文章帮助你了解在组织中部署 Azure 信息保护统一标记的先决条件：

- [Azure 信息保护要求](requirements.md)。 描述在组织中部署 AIP 客户端的详细系统要求，例如 Azure 信息保护订阅和 Azure Active Directory。 还列出受支持的客户端设备和受支持的应用程序。

- [统一标记客户端要求](./rms-client/reqs-ul-client.md)。 列出安装 AIP 客户端的每台计算机的系统要求。

## <a name="install-the-aip-client"></a>安装 AIP 客户端

AIP 提供下列客户端安装选项：

- [下载并运行 .exe 文件](rms-client/clientv2-admin-guide-install.md#install-the-aip-unified-labeling-client-using-the-executable-installer)。 对于大多数用例，建议使用此安装。 安装可以交互或静默运行。

    安装完成后，系统可能会提示你重启计算机或 Office 软件。 根据需要重启以继续。

- [下载并运行 .msi 文件](rms-client/clientv2-admin-guide-install.md#install-the-unified-labeling-client-using-the-msi-installer)。 支持使用集中部署机制的无提示安装，如组策略、Configuration Manager 或 Microsoft Intune。

[Microsoft 下载站点](https://www.microsoft.com/download/details.aspx?id=53018)提供 AIP 客户端安装文件。 

有关详细信息，请参阅[管理员指南：为用户安装 Azure 信息保护统一标记客户端](rms-client/clientv2-admin-guide-install.md)。

> [!TIP]
> 若要测试运行 AIP 客户端的最新功能，请在测试系统上部署公共预览版本。 有关详细信息，请参阅 AIP 统一标记客户端[版本发布历史记录](rms-client/unifiedlabelingclient-version-release-history.md)。
> 

## <a name="next-steps"></a>后续步骤

请参阅以下任何快速入门和教程以开始使用 Azure 信息客户端：

- [教程：安装 Azure 信息保护 (AIP) 统一标记扫描程序](tutorial-install-scanner.md)
- [教程：使用 Azure 信息保护 (AIP) 扫描程序发现敏感内容](tutorial-scan-networks-and-content.md)
- [教程：使用 Azure 信息保护 (AIP) 防止过度共享](tutorial-preventing-oversharing.md)
- [教程：从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端](tutorial-migrating-to-ul.md) 

另请参阅：

- [已知问题 - Azure 信息保护](known-issues.md) 
- [有关 Azure 信息保护的常见问题](faqs.md) 
- [管理员指南：Azure 信息保护统一标记客户端的自定义配置](rms-client/clientv2-admin-guide-customizations.md)        
    
