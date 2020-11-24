---
title: AD RMS 服务器 | Azure RMS
description: Rights Management Services (RMS) 的服务器组件通过一组在 Microsoft Internet Information Services 上运行的 Web 服务实现。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: eae7071115f417e6ea66a98c1bf8820440938718
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "95566125"
---
# <a name="server"></a>服务器

本主题介绍适用于 Azure 和 Windows Server 的 RMS 服务器的用途和功能。

**Azure RMS** - 有关使用 Azure Rights Management 服务的信息，请参阅 [使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

> [!IMPORTANT] 
> 我们建议通过 Azure RMS 开发和测试你的应用程序。

**Windows Server** - 对于本地服务器上的 RMS，从 Windows Server 2008 开始，可以通过将 RMS 服务作为角色进行添加来安装和配置它。 若要在以前的操作系统上安装该服务，请从 Microsoft 下载中心下载它（地址是 [Microsoft Windows Rights Management Services with Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909)）。

在安装的多个 Web 服务中，以下服务对于 Windows Server 上的 RMS 服务器的应用程序开发十分重要。

| 服务 | 说明 |
|---------|-------------|
| 管理 | 承载使你可以管理 RMS 的管理网站。 该服务在根认证服务器和授权服务器上运行。 可以使用 Active Directory Rights Management Services 脚本 API 来编写管理脚本。|
| 帐户认证 |创建在 RMS 证书层次结构中标识计算机的计算机证书以及将用户与特定计算机关联的权限帐户证书。 有关详细信息，请参“阅激活计算机”和“激活用户”。<p><p>此服务在根认证服务器上运行。 |
|许可 | 发布 *最终用户许可*。 该服务在根认证服务器和授权服务器上运行。|
|发布 | 创建 *颁发许可证*，用于定义可在最终用户许可中枚举的策略。 有关详细信息，请参阅[创建颁发许可证](/previous-versions/windows/desktop/adrms_sdk/creating-an-issuance-license)。<p><p>该服务在根认证服务器和授权服务器上运行。|
|预认证 | 使服务器可以代表用户请求 *权限帐户证书*。 该服务在根认证服务器和授权服务器上运行。|
|服务定位器 | 向 Active Directory 提供帐户认证、授权和发布服务的 URL，以便它们能被 RMS 客户端发现。 该服务在根认证服务器和授权服务器上运行。|

## <a name="related-topics"></a>相关主题 ##
* [概述](ad-rms-overview.md)
* [Microsoft Internet Information Services](https://www.iis.net/overview)
* [使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909)
* [Active Directory Rights Management Services Scripting API](/previous-versions/windows/desktop/adrms_script/adrms-script-portal)（Active Directory Rights Management Services 脚本编写 API）
* [Activating a Computer](/previous-versions/windows/desktop/adrms_sdk/activating-a-computer)（激活计算机）
* [Activating a User](/previous-versions/windows/desktop/adrms_sdk/activating-a-user)（激活用户）
* [Creating an Issuance License](/previous-versions/windows/desktop/adrms_sdk/creating-an-issuance-license)（创建颁发许可证）