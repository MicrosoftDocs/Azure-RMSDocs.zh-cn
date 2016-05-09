---
# required metadata

title: 设置测试环境 | Azure RMS
description: 启用权限的应用程序可以使用不同服务器选项进行测试。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4d32682c-754d-4e30-977d-95b08e0662cc

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 设置测试环境

启用权限的应用程序可以使用不同服务器选项进行测试。

**重要说明**  推荐的最佳做法是首先依据 AD RMS 服务器使用 AD RMS 预生产环境测试 Rights Management Services SDK 2.1 应用程序。 然后，如果你希望客户能通过 Azure RMS 服务使用你的应用程序，可在此环境中测试。 有关详细信息，请参阅[使服务应用程序可与基于云的 RMS 一起使用](how-to-use-file-api-with-aadrm-cloud.md)。

 

### 先决条件

-   [安装 SDK](create-your-first-rights-aware-application.md)

说明

### 步骤 1：设置测试环境

若要测试启用权限的应用程序，必须针对为预生产配置的 RMS 服务器运行它。 预生产 RMS 服务器使用预生产/ISV 证书层次结构加密和解密文件。

有关 AD RMS 证书层次结构的详细信息，请参阅 [了解证书链](understanding-certificate-chains.md)。

有两个选项可用于针对 RMS 服务器测试应用程序：

-   **可以在单框 AD RMS ISV 环境中运行应用程序**。 如果在运行 Windows Server 2012、Windows Server 2008 R2 或 Windows Server 2008，并且安装了 Hyper-V，则可以通过使用 AD RMS 单框 VHD 构建虚拟机来部署单框 AD RMS ISV 环境。 单框 AD RMS ISV 环境提供为预生产配置的 RMS 服务器，还安装了 Active Directory Rights Management Services 客户端 2.1。 已配置了 RMS 服务器和客户端的注册表设置。 若要测试应用程序，请在部署单框环境的虚拟机上运行它。
-   **可以针对为预生产而配置并且部署在网络上的 RMS 服务器运行应用程序**。 在这种情况下，还必须在将运行应用程序的计算机上安装并配置 AD RMS 客户端 2.1。 有关如何执行此操作的信息，请参阅 [配置客户端](how-to-configure-the-ad-rms-client-2-0.md)。 有关如何部署 RMS 服务器并为预生产而配置它的信息，请参阅 [安装并配置服务器](how-to-install-and-configure-an-rms-server.md)。

### 相关主题

* [使用方法](how-to-use-msipc.md)
* [AD RMS SDK 网络研讨会附件下载页面](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
* [配置客户端](how-to-configure-the-ad-rms-client-2-0.md)
* [安装 SDK](create-your-first-rights-aware-application.md)
* [安装并配置服务器](how-to-install-and-configure-an-rms-server.md)
* [了解证书链](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


