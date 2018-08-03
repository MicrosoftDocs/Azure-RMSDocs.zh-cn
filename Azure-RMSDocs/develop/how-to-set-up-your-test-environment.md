---
title: 测试应用程序 | Azure RMS
description: 有关如何设置应用程序以进行测试的说明。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 90013f4ee1285afbf112b1309a5e7b7826802584
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39374576"
---
# <a name="testing-your-application"></a>测试应用程序

在这里，你将学习如何准备应用程序测试。

## <a name="instructions"></a>说明

你可以使用 Azure RMS 或 Windows Server 上运行的 RMS 服务器进行测试。  开始使用 Azure RMS 和 RMS 服务器（如果部署需要）进行测试。

- 如需使用 Azure RMS 进行测试，请参阅[操作说明：使用 ADAL 身份验证](how-to-use-adal-authentication.md)。
- 有关使用 RMS 服务器进行测试，请参阅[操作说明：安装和配置 RMS 服务器](how-to-install-and-configure-an-rms-server.md)。
- 安装开发人员运行时：

   必须在要用于测试应用程序的计算机上安装具有 Rights Management Service 客户端 2.1。
   - 如果要在开发计算机之外的计算机上测试应用程序，则可以通过 [AD RMS 客户端下载页面](http://www.microsoft.com/en-us/download/details.aspx?id=38396)在该计算机上安装 RMS 客户端 2.1。
   - 你的开发计算机应该提前安装了 Rights Management Services SDK 2.1。

   要获取 RMS SDK 2.1 安装帮助，请参阅[安装 SDK](install-the-rms-sdk.md)。

## <a name="remarks"></a>备注

本指南并不全面。 要了解如何配置 RMS 客户端 2.1，请参阅 [RMS 客户端 2.1 部署说明](https://technet.microsoft.com/library/jj159267(WS.10).aspx)。

## <a name="related-topics"></a>相关主题

* [操作说明：安装和配置 RMS 服务器](how-to-install-and-configure-an-rms-server.md)
* [操作说明：使用 ADAL 身份验证](how-to-use-adal-authentication.md)
* [安装 SDK](install-the-rms-sdk.md)
* [RMS 客户端 2.1 部署说明](https://technet.microsoft.com/library/jj159267(WS.10).aspx)

