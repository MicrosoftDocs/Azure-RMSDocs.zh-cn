---
# required metadata

title: AD RMS 服务器 | Azure RMS
description: Rights Management Services (RMS) 的服务器组件通过一组在 Microsoft Internet Information Services 上运行的 Web 服务实现。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a7f11e25-9d27-4083-b604-a2d437671d91

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# AD RMS 服务器

本主题介绍 RMS 服务器的用途和功能。

Rights Management Services (RMS) 的服务器组件通过一组在 [Microsoft Internet Information Services](http://www.iis.net/overview) (IIS) 上运行的 Web 服务实现。 还可以通过 Azure 上的 RMS 使用基于云的实现。 有关使用 Azure Rights Management 服务的详细信息，请参阅 [使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

对于本地服务器，从 Windows Server 2008 开始，可以通过将 RMS 服务作为角色进行添加来安装和配置它。 若要在以前的操作系统上安装该服务，请从 Microsoft 下载中心下载它（地址是 [Microsoft Windows Rights Management Services with Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)）。

在安装的多个 Web 服务中，以下服务对于应用程序开发十分重要。

**管理** - 承载使你可以管理 RMS 的管理网站。 该服务在根认证服务器和授权服务器上运行。 可以使用 [Active Directory Rights Management Services 脚本编写 API](https://msdn.microsoft.com/library/Bb968797) 来编写管理脚本。

**帐户认证** - 创建在 RMS 证书层次结构中标识计算机的计算机证书以及将用户与特定计算机关联的权限帐户证书。 有关详细信息，请参阅 [激活用户](https://msdn.microsoft.com/library/Cc530378)。

此服务在根认证服务器上运行。

**授权** - 向最终用户颁发使最终用户可以使用受保护内容的许可证。 该服务在根认证服务器和授权服务器上运行。

**发布** - 创建 [创建颁发许可证](https://msdn.microsoft.com/library/Aa362355)。 该服务在根认证服务器和授权服务器上运行。

**预认证** - 使服务器可以代表用户请求权限帐户证书 (RAC)。 RAC 使用来自 RMS 激活的计算机证书将用户帐户绑定到特定计算机或计算机组，用于使使用者可以使用受保护内容。 该服务在根认证服务器和授权服务器上运行。

**服务定位器** - 向 Active Directory 提供帐户认证、授权和发布服务的 URL，以便 RMS 客户端可以发现它们。 该服务在根认证服务器和授权服务器上运行。

 

## 相关主题 ##
* [概述](ad-rms-overview.md)
* [Microsoft Internet Information Services](http://www.iis.net/overview)
* [使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services Service pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [Active Directory Rights Management Services 脚本编写 API](https://msdn.microsoft.com/library/Bb968797)
* [激活计算机](https://msdn.microsoft.com/library/Cc530377)
* [激活用户](https://msdn.microsoft.com/library/Cc530378)
* [创建颁发许可证](https://msdn.microsoft.com/library/Aa362355)

 

 


<!--HONumber=Apr16_HO3-->

