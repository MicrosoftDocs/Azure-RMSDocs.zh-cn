---
title: AD RMS 服务器 | Azure RMS
description: Rights Management Services (RMS) 的服务器组件通过一组在 Microsoft Internet Information Services 上运行的 Web 服务实现。
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 224139de1e23ace70923aefe508e5d6ccb2969b8
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251102"
---
# <a name="server"></a>Server

本主题介绍适用于 Azure 和 Windows Server 的 RMS 服务器的用途和功能。

**Azure RMS** - 有关使用 Azure Rights Management 服务的信息，请参阅[使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

> [!IMPORTANT] 
> 我们建议通过 Azure RMS 开发和测试你的应用程序。

**Windows Server** - 对于本地服务器上的 RMS，从 Windows Server 2008 开始，可以通过将 RMS 服务作为角色进行添加来安装和配置它。 若要在以前的操作系统上安装该服务，请从 Microsoft 下载中心下载它（地址是 [Microsoft Windows Rights Management Services with Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909)）。

在安装的多个 Web 服务中，以下服务对于 Windows Server 上的 RMS 服务器的应用程序开发十分重要。

| 服务 | 描述 |
|---------|-------------|
| Administration | 承载使你可以管理 RMS 的管理网站。 该服务在根认证服务器和授权服务器上运行。 可以使用 Active Directory Rights Management Services 脚本 API 来编写管理脚本。|
| 帐户认证 |创建在 RMS 证书层次结构中标识计算机的计算机证书以及将用户与特定计算机关联的权限帐户证书。 有关详细信息，请参“阅激活计算机”和“激活用户”。<p><p>此服务在根认证服务器上运行。 |
|许可 | 发布*最终用户许可*。 该服务在根认证服务器和授权服务器上运行。|
|发布 | 创建*颁发许可证*，用于定义可在最终用户许可中枚举的策略。 有关详细信息，请参阅[创建颁发许可证](https://msdn.microsoft.com/library/Aa362355)。<p><p>该服务在根认证服务器和授权服务器上运行。|
|预认证 | 使服务器可以代表用户请求*权限帐户证书*。 该服务在根认证服务器和授权服务器上运行。|
|服务定位器 | 向 Active Directory 提供帐户认证、授权和发布服务的 URL，以便它们能被 RMS 客户端发现。 该服务在根认证服务器和授权服务器上运行。|

## <a name="related-topics"></a>相关主题 ##
* [概述](ad-rms-overview.md)
* [Microsoft Internet Information Services](https://www.iis.net/overview)
* [使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909)
* [Active Directory Rights Management Services Scripting API](https://msdn.microsoft.com/library/Bb968797)（Active Directory Rights Management Services 脚本编写 API）
* [Activating a Computer](https://msdn.microsoft.com/library/Cc530377)（激活计算机）
* [Activating a User](https://msdn.microsoft.com/library/Cc530378)（激活用户）
* [Creating an Issuance License](https://msdn.microsoft.com/library/Aa362355)（创建颁发许可证）
