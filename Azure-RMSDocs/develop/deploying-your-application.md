---
title: 部署应用程序 - AIP
description: 本主题提供部署应用程序的概述和分步指导
keywords: 部署, RMS, AIP
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 03/13/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 2c8b3407f31819614605fb77fb86a86159a898fd
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "68788541"
---
# <a name="deploy-into-production"></a>部署到生产

本主题提供适用于已启用 Azure 信息保护 (AIP) / Rights Management Services (RMS) 的应用程序部署过程的分步指导。

## <a name="request-an-information-protection-integration-agreement-ipia"></a>请求信息保护集成协议 (IPIA)
必须先申请并与 Microsoft 签订正式的协议，才能发布使用 AIP/RMS 开发的应用程序。

### <a name="begin-the-process"></a>开始此过程
向 <strong>IPIA@microsoft.com</strong> 发送一封包含以下信息的电子邮件以获取 IPIA：

**主题：** 为公司名称请求 IPIA

电子邮件的正文中应包含：
- 应用程序和产品名称
- 请求者的姓氏和名字
- 请求者的电子邮件地址

### <a name="next-steps"></a>后续步骤
收到 IPIA 请求后，我们会将一份表格（Word 文档格式）发送给你。
请查看 IPIA 的条款和条件，然后将包含以下信息的表格通过电子邮件发送到 <strong>IPIA@microsoft.com</strong>：
- 公司依法登记的名称
- 公司注册地的州/省（美国/加拿大）或国家/地区
- 公司 URL
- 联系人的电子邮件地址
- 公司的其他地址（可选）
- 公司应用程序名称
- 应用程序的简要描述
- Azure 租户 ID
- 应用程序的*应用程序 ID*
- 用于紧急情况通信的公司联系人、电子邮件和电话号码

### <a name="completing-the-agreement"></a>完成协议
收到你的表格后，我们会将用于数字签名的最终 IPIA 链接发送给你。 你在协议上签名后，协议将由相应的 Microsoft 客户代表签名，协议就此完成。

### <a name="already-have-a-signed-ipia"></a>已有已签名的 IPIA？
如果已有已签名的 IPIA 并希望为要发布的应用程序添加新的应用程序 ID，请发送电子邮件至 <strong>IPIA@microsoft.com</strong>，向我们提供以下信息：
- 公司应用程序名称
- 应用程序的简要描述
- Azure 租户 ID（即使与以前提供的信息相同，也需要再次提供）
- 应用程序的应用程序 ID
- 用于紧急情况通信的公司联系人、电子邮件和电话号码

你发送电子邮件后，我们会在最多 72 小时内向你发送已收到邮件的确认信。

## <a name="deploying-to-the-client-environment"></a>部署到客户端环境

若要部署使用 Azure 信息保护 (AIP) / Rights Management Services (RMS) 工具生成的应用程序，需要在最终用户的计算机上部署 RMS 客户端 2.1。

### <a name="rmsclient21"></a>RMS 客户端 2.1
RMS 客户端 2.1 用于保护通过启用 AIP/RMS 的（安装在本地或 Microsoft 数据中心的）应用程序流动的信息的访问和使用。

RMS 客户端 2.1 不是 Windows 操作系统组件。 客户端作为可选下载随附，可以在确认和接受许可协议后通过应用程序自由分发。

> [!IMPORTANT]
> RMS 客户端 2.1 特定于体系结构，并且必须与目标操作系统的体系结构相匹配。


## <a name="rmsclient21-installation-options"></a>RMS 客户端 2.1 的安装选项

### <a name="creating-your-deployment-package"></a>创建部署包

建议使用首选安装技术将 RMS 客户端安装程序包与应用程序或解决方案进行捆绑。 可以通过其他应用程序和解决方案自由地重新分发 RMS 客户端。

通过启动 RMS 客户端 2.1 安装程序，可以选择以交互方式安装 RMS 客户端 2.1 或无提示安装。 集成步骤将为：

-   下载 RMS Client 2.1 安装程序
-   集成与应用程序安装程序一起运行的 RMS 客户端 2.1 安装程序

将 RMS 客户端 2.1 与应用程序集成的一个示例是 [Rights Protected Folder Explorer](https://technet.microsoft.com/library/rights-protected-folder-explorer(v=ws.10).aspx)（权限受保护的文件夹资源管理器）包。 请尝试自行安装以了解此方法。

### <a name="make-rmsclient21-a-pre-requisite-for-your-application-install"></a>使 RMS 客户端 2.1 成为应用程序安装的先决条件

在这种情况下，将创建先决条件，这样，如果最终用户计算机上不存在 RMS 客户端 2.1，应用程序安装将会失败。

如果客户端不存在，则提供一条错误消息，告知用户何处可以下载 RMS 客户端 2.1

如果客户端存在，则继续执行应用程序安装。

## <a name="enabling-azure-information-protection-services-with-your-application"></a>为应用程序启用 Azure 信息保护服务

> [!NOTE]
> 如果已迁移到新的 ADAL 模型进行身份验证，则无需安装 **SIA**。 有关详细信息，请参阅[适用于启用了 RMS 的应用程序的 ADAL 身份验证](adal-auth.md)。
> 你还可以**验证适用于 Windows 10 的应用程序** - 通过将应用程序更新为使用 ADAL 身份验证而不使用 Microsoft Online 登录助手，你和你的客户将能够：使用多重身份验证；无需计算机的管理权限而安装 RMS 客户端 2.1

为了让最终用户可以利用信息保护服务，必须部署 *Online Services 登录助手 (SIA)* 。 应用程序开发人员不知道最终用户将通过 RMS（本地），还是通过 Azure 信息保护使用信息保护。


> [!IMPORTANT]
> 如果要使用基于 Azure 的 RMS 运行客户端应用程序，你需要创建自己的租户。 有关详细信息，请参阅 [Azure RMS 要求：支持 Azure RMS 的云订阅](../requirements.md)。
> 有关使用 Azure RMS 运行的详细信息，请参阅[使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

-   从 Microsoft 下载中心下载 [Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=28177)。
-   确保已启用权限的应用程序的部署中包括此服务选项的系统必备组件检查。
-   有关你自己的测试以及你的最终用户使用在线服务的信息，请参阅 TechNet 主题[配置 Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx)。

还需要参阅以下指南来配置应用程序：[如何将应用服务应用程序配置为使用 Azure Active Directory 登录](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)。

有关使你的应用程序能够将 RMS 用于 Azure Rights Management Services 的详细信息，请参阅[使应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## <a name="related-topics"></a>相关主题

* [Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=28177)
* [配置 Rights Management](https://TechNet.Microsoft.Com/library/jj585002.aspx)
* [使应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)

