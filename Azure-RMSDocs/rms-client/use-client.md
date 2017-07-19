---
title: "Azure 信息保护客户端"
description: "Microsoft Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的数据。 客户端（Azure 信息保护客户端或 Rights Management 客户端）与在计算机和移动设备上运行的应用程序集成。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ROBOTS: noindex,nofollow
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: eb09862e5a265b8c5c8f2b81a08582181547df84
ms.sourcegitcommit: 1c3ebf4ad64b55db4fec3ad007fca71ab7d38c02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2017
---
# <a name="the-client-side-of-azure-information-protection"></a>Azure 信息保护的客户端

>适用于：Active Directory Rights Management Services、Azure 权限管理、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

Azure 信息保护提供客户端-服务器解决方案，可帮助保护组织的文档和电子邮件：

- 客户端可以是 Azure 信息保护客户端或 Rights Management 客户端，此客户端与在计算机和移动设备上运行的应用程序集成。 

- 服务驻留在云中（Azure 信息保护，它使用 Azure Rights Management 服务进行数据保护）或本地 (Active Directory Rights Management Services)。 

除了保护之外，Azure 信息保护客户端还支持分类和标签。 此客户端与 Office 应用程序集成，必须单独安装。

某些应用程序将自动安装 Rights Management (RMS) 客户端，如 Office 应用程序、Azure 信息保护客户端和软件供应商提供的启用 RMS 的应用程序。 但是，该客户端也可以自行安装，这种安装方式能够为希望将 Rights Management 保护集成到业务线应用程序的开发人员提供支持。

当需要了解有关如何部署和使用这些客户端（可以通过 Azure 信息保护和 Active Directory Rights Management Services 使用该客户端保护你组织的数据）的详细信息时，请使用以下文档：

- [Azure 信息保护客户端](AIP-client.md)

- [RMS 客户端部署说明](client-deployment-notes.md)

- [使用 Windows Server 文件分类基础结构 (FCI) 的 RMS 保护](configure-fci.md)

- [适用于 Windows 的权限管理共享应用程序](sharing-app-windows.md)

请注意，适用于 Windows 的 Rights Management 共享应用程序和 RMS 保护工具现被 Azure 信息保护客户端替代。 


## <a name="see-also"></a>另请参阅
[比较 Azure 信息保护与 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]