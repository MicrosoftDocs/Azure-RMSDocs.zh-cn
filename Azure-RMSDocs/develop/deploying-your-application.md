---
title: 部署应用程序 - AIP
description: 本主题概述并引导你完成应用程序部署
keywords: 部署, RMS, AIP
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 300fb1d14bc4eda93b0e40ffbd9e6c2329c88517
ms.sourcegitcommit: e21fb3385de6f0e251167e5dc973e90f0e7f2bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
ms.locfileid: "28908079"
---
# <a name="deploy-into-production"></a>部署到生产环境

本主题引导你完成启用了 Azure 信息保护 (AIP) / Rights Management Services (RMS) 的应用程序的部署过程。

## <a name="request-an-information-protection-integration-agreement-ipia"></a>申请信息保护集成协议 (IPIA)
在可以发布使用 AIP/RMS 开发的应用程序之前，必须申请并完成与 Microsoft 的正式协议。

### <a name="begin-the-process"></a>开始流程
通过向 **IPIA@microsoft.com** 发送包含以下信息的电子邮件来获取你的 IPIA：

**主题：** 为 *Company Name* 申请 IPIA

在电子邮件的正文中，包括：
- 应用程序和产品名称
- 申请者的姓名
- 申请者的电子邮件地址

### <a name="next-steps"></a>后续步骤
收到你的 IPIA 申请时，我们会向你发送一个窗体（以 Word 文档形式）。
请查看 IPIA 的条款和条件，并将包含以下信息的窗体返回给 **IPIA@microsoft.com**：
- 公司的法定名称
- 公司所在的州/省（美国/加拿大）或国家/地区
- 公司 URL
- 联系人的电子邮件地址
- 公司的其他地址（可选）
- 公司应用程序的名称
- 应用程序的简短说明
- *Azure 租户 ID*
- 应用程序的*应用 ID*
- 用于紧急情况通信的公司联系人、电子邮件和电话

### <a name="completing-the-agreement"></a>完成协议
收到你的窗体后，我们将向你发送最终 IPIA 链接来进行电子签名。 在你签名后，相应的 Microsoft 代表将对其进行签名，从而完成协议。

### <a name="already-have-a-signed-ipia"></a>已拥有已签名的 IPIA？
如果你已拥有已签名的 IPIA 并且希望为你发布的应用程序添加新的*应用 ID*，请向 **IPIA@microsoft.com** 发送电子邮件并向我们提供以下信息：
- 公司应用程序的名称
- 应用程序的简短说明
- Azure 租户 ID（即使与之前的相同也要提供）
- 应用程序的应用 ID
- 用于紧急情况通信的公司联系人、电子邮件和电话

在发送电子邮件时，请留出最多 72 小时来等待接收确认。

## <a name="deploying-to-the-client-environment"></a>部署到客户端环境

若要部署内置了 Azure 信息保护 (AIP) / Rights Management Services (RMS) 工具的应用程序，需要在最终用户的计算机上部署 RMS 客户端 2.1。

### <a name="rms-client-21"></a>RMS 客户端 2.1
在使用和访问流经启用了 AIP/RMS 的应用程序的信息时，RMS 客户端 2.1 可以提供相应的保护，无论这些应用程序安装在内部部署中还是安装在 Microsoft 数据中心。

RMS 客户端 2.1 不是 Windows 操作系统组件。 该客户端作为可选下载提供，它随你的应用程序免费分发，可以通过承认并接受其许可协议进行下载。

> [!IMPORTANT]
> RMS 客户端 2.1 特定于体系结构，并且必须与目标操作系统的体系结构相匹配。


## <a name="rms-client-21-installation-options"></a>RMS 客户端 2.1 安装选项

### <a name="creating-your-deployment-package"></a>创建部署包

建议使用你喜欢的安装技术将 RMS 客户端安装程序包与你的应用程序或解决方案捆绑在一起。 可以随其他应用程序和解决方案免费重新分发 RMS 客户端。

可以选择通过启动 RMS 客户端 2.1 安装程序以交互方式安装 RMS 客户端 2.1，也可以选择以无提示方式安装它。 集成步骤如下所述：

-   下载 RMS 客户端 2.1 安装程序
-   将要运行的 RMS 客户端 2.1 安装程序与你的应用程序安装程序进行集成

[Rights Protected Folder Explorer](https://technet.microsoft.com/library/rights-protected-folder-explorer(v=ws.10).aspx) 包是将 RMS 客户端 2.1 与应用程序集成的一个示例。 尝试自己进行安装来了解此方法。

### <a name="make-rms-client-21-a-pre-requisite-for-your-application-install"></a>使 RMS 客户端 2.1 成为安装你的应用程序的先决条件

在这种情况下，你将创建一个先决条件来指示：如果最终用户计算机上不存在 RMS 客户端 2.1，则应用程序安装将失败。

如果该客户端不存在，则提供一条错误消息来告知用户可以到哪里下载 RMS 客户端 2.1 的副本

如果该客户端存在，则继续进行应用程序安装。

## <a name="enabling-azure-information-protection-services-with-your-application"></a>随应用程序启用 Azure 信息保护服务

> [!NOTE]
> 如果已经迁移到用于身份验证的新 ADAL 模型，则不必安装 **SIA**。 有关详细信息，请参阅[针对启用了 RMS 的应用程序的 ADAL 身份验证](adal-auth.md)。
> 另外，还可以**针对 Windows 10 验证应用程序** - 通过将应用程序更新为使用 ADAL 身份验证而非 Microsoft Online Sign-in Assistant，你和你的客户将能够：利用多重身份验证，在不需要提供管理权限的情况下将 RMS 客户端 2.1 安装到计算机

为了使最终用户能够利用信息保护服务，必须部署 *Online Services 登录助手 (SIA)*。 作为应用程序开发人员，你不知道最终用户将通过 RMS（本地）还是通过 Azure 信息保护来使用信息保护。


> [!IMPORTANT]
> 如果要将客户端应用程序与基于 Azure 的 RMS 一起运行，则你需要创建自己的租户。 有关详细信息，请参阅 [Azure RMS 要求：支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md)。
> 有关与 Azure RMS 一起运行的详细信息，请参阅[使服务应用程序能够与基于云的 RMS 一起工作](how-to-use-file-api-with-aadrm-cloud.md)。

-   从 Microsoft 下载中心下载 [Microsoft Online Services 登录助手](http://www.microsoft.com/download/details.aspx?id=28177)。
-   确保启用了权利的应用程序的部署包括一个先决条件检查来验证是否选择了此服务。
-   若要了解自己进行测试以及最终用户对联机服务的使用，请参阅 TechNet 主题[配置 Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx)。

还需要使用以下指南来配置应用 - [如何将应用服务应用程序配置为使用 Azure Active Directory 登录](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)。

有关使应用程序能够使用 Azure Rights Management 服务中的 RMS 的详细信息，请参阅[使应用程序能够与基于云的 RMS 一起工作](how-to-use-file-api-with-aadrm-cloud.md)。

## <a name="related-topics"></a>相关主题

* [Microsoft Online Services 登录助手](http://www.microsoft.com/download/details.aspx?id=28177)
* [配置 Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx)
* [使应用程序能够与基于云的 RMS 一起工作](how-to-use-file-api-with-aadrm-cloud.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
