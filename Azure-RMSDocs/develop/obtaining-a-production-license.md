---
# required metadata

title: 获取生产许可证 | Azure RMS
description: 发布使用 RMS SDK 2.1 开发的应用程序时，需要生产许可证协议。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6749817E-FF34-4384-BF63-39AEA5C372CA
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 此 SDK 内容不是最新的。 在短时间内，请在 MSDN 上找到[最新版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)的文档。 **
# 获取生产许可证

必须先申请生产许可证协议以获取生产证书，才能发布使用 Rights Management Services SDK 2.1 开发的应用程序。

> [!IMPORTANT]
> 如果要使用基于 Azure 的 RMS 运行客户端应用程序，你需要申请 Azure RMS 租户。 将包含租户请求的邮件发送到 <rmcstbeta@microsoft.com>。

有关使用 Azure RMS 运行的详细信息，请参阅[使服务应用程序可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。


生产证书和预生产证书的功能相似，但预期使用环境不同。 两种证书的信任根处都包含带有 Microsoft 证书颁发机构 (CA) 证书的证书链，但预生产证书仅在开发 RMS 应用程序时才可使用。 生产证书是在发布后环境中使用。 使用生产证书和关联私钥来创建清单并对其签名，该清单用于标识可以或必须加载到应用程序的进程空间中的文件以及禁止加载的文件。

有关密钥的详细信息，请参阅[测试启用权限的应用程序](running-your-first-application.md)。

通过申请生产许可证协议，即可获得证书。

## 请求生产许可协议

-   发送电子邮件信息至 [RMLA@microsoft.com](mailto:rmla@microsoft.com) 并包含以下信息：

    -   完整的公司名称

    -   实体企业地址（包括城市、省/市/自治区、国家或地区，以及邮政编码）
    -   企业通讯地址（包括城市、省/市/自治区、国家或地区，以及邮政编码）
    -   公司电话和传真号码
    -   公司 URL
    -   企业所位于的公司或地区
    -   应用程序或产品名称
    -   请求者的姓氏和名字
    -   请求者的职务或职位
    -   请求者的电子邮件地址

    电子邮件帐户不是严格需要，但申请过程中通常需要通过电子邮件进行通信。 你可以在 Microsoft Outlook.com 上获取免费的电子邮件帐户。 如果你没有电子邮件帐户又不想申请免费帐户，则可以将打印版本的申请寄送到以下地址：

    `Active Directory Rights Management License Agreements (ADRMLA)`

    `Microsoft Corporation`

    `One Microsoft Way`

    `Redmond, WA 98052-6399`

    请求协议时，请执行以下操作：

    -   提交信息，以英文书写，与协议上显示的一样。
    -   发送所有请求的信息。 信息缺失或不完整可能造成请求处理延迟。

    Active Directory Rights Management 许可协议 (ADRMLA) 团队将在三个工作日内回复你通过电子邮件发送的请求，如果你是使用邮政服务发送请求，则所需时间更长。 回复中将包括许可证协议表单和进一步说明。 阅读协议中的所有内容，签名后返回给 ADRMLA 团队。 请勿更改许可证协议的字体或改变段落格式。

    请务必遵循 ADRMLA 团队给出的说明。 说明中列出了你的证书请求获批所需的数字信息项目。 通过遵循逐步说明，可减少延迟。

    证书创建完成后，ADRMLA 团队会将你的生产证书转发给你。 证书的创建是基于你所提供的许可证协议和数字信息（包括公钥）。 请注意，ADRMLA 团队通过电子邮件将你的证书回复给你可能需要最多 15 个工作日，如果是使用邮政服务进行通信，则所需时间更长。

## 相关主题

* [使用方法](how-to-use-msipc.md)
* [测试启用权限的应用程序](running-your-first-application.md)
 

 





<!--HONumber=Jun16_HO1-->


