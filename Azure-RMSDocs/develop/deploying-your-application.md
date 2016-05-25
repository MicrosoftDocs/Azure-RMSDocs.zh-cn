---
# required metadata

title: 部署应用程序 | Azure RMS
description: 本主题概述并引导你完成启用权限的应用程序的部署选项
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 部署应用程序


本主题概述并引导你完成启用权限的应用程序的部署选项。

> [!IMPORTANT]
> 推荐的最佳做法是首先依据 RMS 服务器使用 RMS 预生产环境测试 Rights Management Services SDK 2.1 应用程序。 然后，如果你希望客户能通过 Azure RMS 服务使用你的应用程序，可在此环境中测试。 有关详细信息，请参阅[使服务应用程序可与基于云的 RMS 一起使用](how-to-use-file-api-with-aadrm-cloud.md)。

 

## Active Directory Rights Management Services Client 2.1 的安装选项

一旦使用生产证书创建清单文件，即说明你的应用程序已为部署做好准备。 假设你使用 RMS SDK 2.1，那么你将需要在最终用户计算机上部署 Active Directory Rights Management Services Client 2.1。

### AD RMS Client 2.1

AD RMS Client 2.1 是为客户端计算机而设计的软件，可帮助保护对流经使用 RMS 的应用程序（无论是安装在本地还是 Microsoft 数据中心内）的信息的访问和使用。

AD RMS Client 2.1 不是 Windows 操作系统组件。 AD RMS Client 2.1 作为可选下载提供，在确认和接受其许可协议的情况下，可以通过第三方软件自由地分发它，从而支持客户端访问在你的环境中使用和部署 RMS 服务器时，权限受保护的内容。

> [!IMPORTANT]
> AD RMS Client 2.1 特定于体系结构，必须与目标操作系统的体系结构匹配。


## AD RMS Client 2.1 的安装选项

-   **重新分发 AD RMS Client 2.1**

    建议的方法是使用首选的安装技术，将 RMS 客户端安装程序包与应用程序或解决方案进行捆绑。 可以通过其他应用程序和 IT 解决方案自由地重新分发和捆绑 RMS 客户端。

    通过启动 AD RMS Client 2.1 安装程序，可以选择以交互方式安装 AD RMS Client 2.1 或无提示安装。 集成步骤将为：

    -   下载 RMS Client 2.1 安装程序
    -   集成与应用程序安装程序一起运行的 AD RMS Client 2.1 安装程序

    将 AD RMS Client 2.1 与应用程序集成的两个很好的示例是 RMS SDK 2.1 安装程序包和权限受保护的文件夹资源管理器包。 尝试自行安装它们以便了解相关方法。

-   **使 AD RMS Client 2.1 成为应用程序安装的先决条件**

    在这种情况下，将创建先决条件，这样，如果最终用户计算机上不存在 AD RMS Client 2.1，应用程序安装将会失败。

    如果客户端不存在，则提供一条错误消息，告知用户何处可以下载 AD RMS Client 2.1

    如果客户端存在，则继续执行应用程序安装。

## 使用应用程序启用 Azure Rights Management Services

> [!NOTE]
> 如果已迁移到新的 ADAL 模型进行身份验证，则无需安装 SIA。 有关详细信息，请参阅适用于启用了 RMS 的应用程序的 ADAL 身份验证。

- **为 Windows 10 验证你的应用程序**：通过更新应用程序来使用 ADAL 身份验证，而不是 Microsoft Online 登录助手，你和你的客户将能够：
  - 使用多重身份验证
  - 安装 RMS 2.1 Client，而无需对计算机的管理特权
 
  为了使最终用户可以利用 Azure Rights Managemen 服务，必须部署 *Online Services 登录助手*。 作为应用程序开发人员，你不知道最终用户将会使用 RMS（本地）还是 Azure Rights Management Services（云服务）。

> [!IMPORTANT]
> 使用 Azure RMS 运行 RMS SDK 2.1 客户端应用程序需要请求 Azure RMS 租户。 将包含租户请求的邮件发送到 <rmcstbeta@microsoft.com>。

-   从 Microsoft 下载中心下载 [Microsoft Online Services 登录助手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)。
-   确保已启用权限的应用程序的部署中包括此服务选项的系统必备组件检查。
-   有关你自己的测试以及你的最终用户使用在线服务的信息，请参阅 TechNet 主题[配置 Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)。

有关使你的应用程序能够将 RMS 用于 Azure Rights Management Services 的详细信息，请参阅[使应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 相关主题

* [使用方法](how-to-use-msipc.md)
* [Microsoft Online Services 登录助手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [配置权限管理](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [使应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
 

 





<!--HONumber=Apr16_HO4-->


