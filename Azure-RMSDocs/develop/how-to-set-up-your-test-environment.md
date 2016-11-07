---
title: "测试应用程序 | Azure RMS"
description: "有关如何设置应用程序以进行测试的说明。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 719077671664dda3102949609874c569a691bbb8


---

# <a name="testing-your-application"></a>测试应用程序

本主题包含有关如何为应用程序测试进行设置的说明。

## <a name="instructions"></a>说明

### <a name="step-1-setup-for-testing"></a>步骤 1：为测试进行设置

可以使用 Azure RMS 或在 Windows Server 上运行的 RMS 服务器进行测试，我们建议在 Azure RMS 上开始测试，再根据部署的要求使用 RMS 服务器进行测试。

1. 如需使用 Azure RMS 进行测试，请参阅[操作说明：使用 ADAL 身份验证](how-to-use-adal-authentication.md)。
2. 有关使用 RMS 服务器进行测试，请参阅[操作说明：安装和配置 RMS 服务器](how-to-install-and-configure-an-rms-server.md)。
3. 下面介绍如何安装开发人员运行时。

   必须在要用于测试应用程序的计算机上安装具有 Rights Management Service 客户端 2.1。
   - 如果要在开发计算机之外的计算机上测试应用程序，则可以通过 [AD RMS 客户端下载页面](http://www.microsoft.com/en-us/download/details.aspx?id=38396) 在该计算机上安装 RMS 客户端 2.1。
   - 如果要在开发计算机上测试应用程序，则应该已安装了 Rights Management Services SDK 2.1。 RMS 客户端 2.1 当时会以无提示方式安装。

    有关如何安装 RMS SDK 2.1 的信息，请参阅[安装 SDK](install-the-rms-sdk.md)。

## <a name="remarks"></a>备注

本主题中的指南并不全面。 有关如何配置 RMS 客户端 2.1 的详细信息，请参阅 [RMS 客户端 2.1 部署说明](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)。

### <a name="related-topics"></a>相关主题

* [操作说明：安装和配置 RMS 服务器](how-to-install-and-configure-an-rms-server.md)
* [操作说明：使用 ADAL 身份验证](how-to-use-adal-authentication.md)
* [安装 SDK](install-the-rms-sdk.md)
* [RMS 客户端 2.1 部署说明](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 



<!--HONumber=Nov16_HO1-->


