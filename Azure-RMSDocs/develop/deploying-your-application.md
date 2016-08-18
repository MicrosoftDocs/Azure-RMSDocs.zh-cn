---
title: "部署应用程序 | Azure RMS"
description: "本主题概述并引导你完成启用权限的应用程序的部署选项"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 982021a2e972023b04e6483348a7c27aa029e198
ms.openlocfilehash: 8308e2db84e13c6b8c85a1a3ae6c01fc0aabee75


---

# 部署到生产


本主题概述并引导你完成启用权限的应用程序的部署选项。

## 请求生产许可协议

 必须先申请生产许可证协议以获取生产证书，才能发布使用 Rights Management Services SDK 2.1 开发的应用程序。

> [!IMPORTANT]
> 如果要使用基于 Azure 的 RMS 运行客户端应用程序，你需要创建自己的租户。 有关详细信息，请参阅 [Azure RMS 要求：支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md)。
> 有关使用 Azure RMS 运行的详细信息，请参阅[使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

通过申请生产许可证协议，即可获得证书。

发送电子邮件信息至 [RMLA@microsoft.com](mailto:rmla@microsoft.com) 并包含以下信息：

- 完整的公司名称
- 实体企业地址（包括城市、省/市/自治区、国家或地区，以及邮政编码）
- 企业通讯地址（包括城市、省/市/自治区、国家或地区，以及邮政编码）
- 公司电话和传真号码
- 公司 URL
- 企业所位于的公司或地区
- 应用程序或产品名称
- 请求者的姓氏和名字
- 请求者的职务或职位
- 请求者的电子邮件地址

电子邮件帐户不是严格需要，但申请过程中通常需要通过电子邮件进行通信。 你可以在 Microsoft Outlook.com 上获取免费的电子邮件帐户。 如果你没有电子邮件帐户又不想申请免费帐户，则可以将打印版本的申请寄送到以下地址：

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

请求协议时，请执行以下操作：
- 提交信息，以英文书写，与协议上显示的一样。
- 发送所有请求的信息。 信息缺失或不完整可能造成请求处理延迟。

Active Directory Rights Management 许可协议 (ADRMLA) 团队将在三个工作日内回复你通过电子邮件发送的请求，如果你是使用邮政服务发送请求，则所需时间更长。 回复中将包括许可证协议表单和进一步说明。 阅读协议中的所有内容，签名后返回给 ADRMLA 团队。 请勿更改许可证协议的字体或改变段落格式。

请务必遵循 ADRMLA 团队给出的说明。 说明中列出了你的证书请求获批所需的数字信息项目。 通过遵循逐步说明，可减少延迟。

证书创建完成后，ADRMLA 团队会将你的生产证书转发给你。 请注意，ADRMLA 团队通过电子邮件将你的证书回复给你可能需要最多 15 个工作日，如果是使用邮政服务进行通信，则所需时间更长。


## Rights Management 服务客户端 2.1 的安装选项和要求

假设你使用 RMS SDK 2.1，那么你将需要在最终用户计算机上部署 Active Directory Rights Management Services Client 2.1。

### RMS 客户端 2.1

RMS 客户端 2.1 是为客户端计算机而设计的软件，可帮助保护对流经使用 RMS 的应用程序（无论是安装在本地还是 Microsoft 数据中心内）的信息的访问和使用。

RMS 客户端 2.1 不是 Windows 操作系统组件。 RMS 客户端 2.1 作为可选下载提供，在确认和接受其许可协议的情况下，可以通过第三方软件自由地分发它，从而支持客户端访问在你的环境中使用和部署 RMS 服务器时，权限受保护的内容。


> [!IMPORTANT]
> AD RMS Client 2.1 特定于体系结构，必须与目标操作系统的体系结构匹配。


## RMS 客户端 2.1 的安装选项

-   **重新分发 RMS 客户端 2.1**

    建议的方法是使用首选的安装技术，将 RMS 客户端安装程序包与应用程序或解决方案进行捆绑。 可以通过其他应用程序和 IT 解决方案自由地重新分发和捆绑 RMS 客户端。

    通过启动 RMS 客户端 2.1 安装程序，可以选择以交互方式安装 RMS 客户端 2.1 或无提示安装。 集成步骤将为：

    -   下载 RMS Client 2.1 安装程序
    -   集成与应用程序安装程序一起运行的 RMS 客户端 2.1 安装程序

    将 RMS 客户端 2.1 与应用程序集成的两个很好的示例是 RMS SDK 2.1 安装程序包和权限受保护的文件夹资源管理器包。 尝试自行安装它们以便了解相关方法。

-   **使 RMS 客户端 2.1 成为应用程序安装的先决条件**

    在这种情况下，将创建先决条件，这样，如果最终用户计算机上不存在 RMS 客户端 2.1，应用程序安装将会失败。

    如果客户端不存在，则提供一条错误消息，告知用户何处可以下载 RMS 客户端 2.1

    如果客户端存在，则继续执行应用程序安装。

## 使用应用程序启用 Azure Rights Management Services

> [!NOTE]
> 如果已迁移到新的 ADAL 模型进行身份验证，则无需安装 SIA。 有关详细信息，请参阅[适用于启用了 RMS 的应用程序的 ADAL 身份验证](adal-auth.md)。
> 你还可以**验证适用于 Windows 10 的应用程序** - 通过将应用程序更新为使用 ADAL 身份验证而不使用 Microsoft Online 登录助手，你和你的客户将能够：使用多重身份验证；无需计算机的管理权限而安装 RMS 客户端 2.1


为了使最终用户可以利用 Azure Rights Managemen 服务，必须部署 *Online Services 登录助手 (SIA)*。 作为应用程序开发人员，你不知道最终用户将会使用 RMS（本地）还是 Azure Rights Management Services（云服务）。


> [!IMPORTANT]
> 使用 Azure RMS 运行 RMS SDK 2.1 客户端应用程序需要创建你自己的租户。 有关详细信息，请参阅 [Azure RMS 要求：支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md)。

-   从 Microsoft 下载中心下载 [Microsoft Online Services 登录助手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)。
-   确保已启用权限的应用程序的部署中包括此服务选项的系统必备组件检查。
-   有关你自己的测试以及你的最终用户使用在线服务的信息，请参阅 TechNet 主题[配置 Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)。

有关使你的应用程序能够将 RMS 用于 Azure Rights Management Services 的详细信息，请参阅[使应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 相关主题

* [Microsoft Online Services 登录助手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [配置权限管理](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [使应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
 

 



<!--HONumber=Jul16_HO1-->


