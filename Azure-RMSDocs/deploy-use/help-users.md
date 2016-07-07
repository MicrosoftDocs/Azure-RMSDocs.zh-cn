---
title: "帮助用户使用 Azure Rights Management 保护文件 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b6dcd8bb1091e9c484e02042adbf993381581a9d
ms.openlocfilehash: d48616cb638522e6cda61e7ae96db9480fc14099


---

# 帮助用户使用 Azure Rights Management 保护文件

*适用于：Azure Rights Management、Office 365*

在你为组织部署和配置 Azure Rights Management (Azure RMS) 之后，请为用户、管理员和你的技术支持提供以下帮助和指导：

-   **最终用户信息：**

    让用户知道如何以及何时保护包含敏感信息的文档和电子邮件。 只要有可能，都应该提供其现有工作流的这些信息，使他们可以将附加的步骤合并到熟知的过程中，而不是引入全新的过程。 请务必让他们知道你的业务的相关优势（和风险），并提供有关何时应该保护文件和电子邮件的指导。 如果你配置了 [自定义模板](configure-custom-templates.md)，请提供有关在模板名称和描述不足以帮助用户选择正确模板时应该选择哪个模板的说明。

    > [!TIP]
    > 最终用户示例视频
    >
    > -   [Azure RMS 用户体验](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Azure RMS 文档跟踪和撤销](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **管理员信息：**

    有些应用程序使用管理员配置的策略和设置来自动应用信息保护。 你可能需要为管理这些应用程序和服务的其他管理员提供这些应用程序的说明。 有关详细信息，请参阅 [应用程序如何支持 Azure Rights Management](../understand-explore/applications-support.md) 和 [为 Azure Rights Management 配置应用程序](configure-applications.md)。

-   **技术支持信息：**

    为技术支持人员提供的最有用工具之一是 [RMS 分析器](https://www.microsoft.com/en-us/download/details.aspx?id=46437)。 技术支持操作员可以配合 Azure RMS 管理员选项运行该工具，并且可以要求用户配合 Azure RMS 用户选项运行该工具。 此工具不仅可以帮助识别问题，而且还能修复找到的问题，并且不能修复，则会记录跟踪日志。

    如果有人合法请求对受保护文档的完全访问权限（例如，某位离职后，法律部门或经理发出此类请求），请确保技术支持人员使用 Azure RMS [超级用户功能](configure-super-users.md) 并遵循相应的流程来处理此请求。

    此外，下面是用户可能会报告的一些典型问题：

    -   **登录帮助：**

        当 Azure RMS 需要对用户进行身份验证且无法使用缓存的凭据时，可能提示用户提供凭据。 该凭据是用户的工作或学校帐户和密码，与你的 Office 365 租户或 Azure Active Directory 租户相关联。 它不是 Microsoft 帐户（以前的 Microsoft Live ID）或用户的个人电子邮件帐户，因为 Azure RMS 当前不支持这些帐号。 为用户和你的技术支持提供说明，阐明在 Azure RMS 上使用这些应用程序的情况下，当提示用户提供凭据时，应该使用何种帐户。

    -   **与保护或使用内容相关的问题：**

        确保用户获得了有关他们所用应用程序的相应说明，并使用 Azure RMS 支持的应用程序和设备。 有关支持的应用程序和设备的详细信息，请参阅 [Azure Rights Management 的要求](../get-started/requirements-azure-rms.md)。

        如果用户在尝试保护或使用内容时看到错误，请要求他们以 Azure RMS 用户的身份运行 [RMS 分析器](https://www.microsoft.com/en-us/download/details.aspx?id=46437) 。

        如果用户报告他们可以打开受保护的内容，但没有所需的权限，请要求他们以 Azure RMS 用户的身份运行 [RMS 分析器](https://www.microsoft.com/en-us/download/details.aspx?id=46437) ，并下载和查看模板。 这将会确认他们已成功下载模板，以及模板提供的权限。 问题的原因可能是，该用户不在针对模板配置的正确组中，或者需要为该用户重新配置模板。

请参阅以下关于应用程序特定信息的部分，帮助用户保护敏感的文档和电子邮件。

## 使用权限管理共享应用程序提供的信息保护
如果用户使用 Office 2010，则权限管理 (RMS) 共享应用程序是他们进行内容保护和使用受保护内容所必需的。另外，我们还建议将其用于支持 Azure RMS 的所有计算机和移动设备。

除了使用户更轻松地保护重要文档以外，RMS 共享应用程序还允许用户跟踪他们保护的文档，并根据需要撤消对文档的访问权限。

有关如何将此应用程序用于 Windows 计算机的说明，请参阅 [Rights Management 共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)。

对于移动设备，请参阅 [适用于移动平台的 Microsoft Rights Management 共享应用程序的常见问题](http://technet.microsoft.com/dn451248)。

> [!TIP]
> 有关带屏幕截图的高级示例方案，请参阅[用户与移动用户安全地共享附件](../understand-explore/what-admins-users-see.md#users-safely-share-attachments-with-mobile-users)。

## 在 Office 365、Office 2016 或 Office 2013 中使用信息保护
如果你使用 Azure RMS，但尚未安装权限管理共享应用程序，则用户将不会在功能区上看到 **“共享保护”**按钮，也不会在文件资源管理器中看到帮助他们更加轻松地保护文件的 **“保护现有”** 选项。 对于这些用户，他们必须遵循类似以下的说明。

> [!TIP]
> 若要查找应用程序特定帮助，以及有关在这些应用程序中使用信息保护的说明，请搜索 **IRM** 和应用程序名称及版本。

#### 在 Word 2013 中保护文档

1.  在 Microsoft Word 中创建一个新文档。

2.  在 **“文件”** 菜单中，依次单击 **“信息”**、**“保护文档”**、**“限制访问”**，然后选择一个模板以快速应用相应的使用权限，或者选择 **“限制访问”** 并自行选择使用权限。

    > [!NOTE]
    > 如果这是你第一次使用权限管理，你需要联系 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服务，它将提示你提供凭据，以便配置 Office IRM 客户端。

3.  保存文档。

当其他人打开文档时，首先会对他们进行身份验证。 如果他们未被授权打开文档，则文档不会打开。 如果他们已被授权打开文档，则文档将会打开，并提供为该用户指定的受限使用权限。 例如，“仅查看”使用权限不允许用户编辑或保存文档，即便先将文档复制到其他位置也是如此。 这些使用权限以限制横幅方式显示在文档顶部。 该横幅可能显示适用于文档的权限，或者提供显示权限的链接。

#### 使用 Outlook 2013 和 Exchange Online 保护电子邮件

1.  在 Outlook 中，创建一封发送至组织内部收件人的新电子邮件。

2.  在 **“选项”** 选项卡中，单击 **“权限”**，然后选择某个选项。 例如：**不得转发**、**&lt;公司名称&gt; - 机密**或**&lt;公司名称&gt; - 机密，仅供查阅**。

3.  发送电子邮件。

与查看受保护文档相似，当收件人接收电子邮件时，首先会对他们进行身份验证。 如果他们已被授权查看电子邮件，则电子邮件将会打开，并提供为该用户指定的受限使用权限。 例如，如果你选择了“不要转发”，则功能区上的“转发”按钮不可用 。

#### 使用 Outlook Web App 保护电子邮件

1.  在 Outlook Web App 中，创建一封发送至组织内部收件人的新电子邮件。

2.  单击 **“...”**，再单击 **“设置权限”**，然后选择某个选项。 例如：**不得转发**、**不要全部回复**、**&lt;公司名称&gt; - 机密**或**&lt;公司名称&gt; - 机密，仅供查阅**。

3.  发送电子邮件。

与查看受保护文档相似，当收件人接收电子邮件时，首先会对他们进行身份验证。 如果他们已被授权查看电子邮件，则电子邮件将会打开，并提供为该用户指定的受限使用权限。 例如，如果你选择了 **“不要全部答复”**，则电子邮件窗口中的 **“全部答复”** 选项不可用。





<!--HONumber=Jun16_HO4-->


