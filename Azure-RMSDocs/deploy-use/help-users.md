---
title: "使用 Azure RMS 帮助用户保护文件 - AIP"
description: "此信息可帮助你在部署和配置 Azure 信息保护中的 Azure Rights Management 之后，为用户、管理员和技术支持提供指导。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8bc262e8f79b0c0485104b5bb0152dd0609c35c5
ms.sourcegitcommit: 1c3ebf4ad64b55db4fec3ad007fca71ab7d38c02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2017
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>使用 Azure Rights Management 服务帮助用户保护文件

>*适用于：Azure 信息保护、Office 365*

为组织部署和配置 Azure 信息保护之后，请为用户、管理员和技术支持提供以下帮助和指导：

-   **最终用户信息：**

    让用户知道如何以及何时保护包含敏感信息的文档和电子邮件。 尽可能为现有工作流提供此信息，以便可以将附加步骤并入已熟悉的过程，而不是引入新过程。 请务必让他们知道你的业务的相关优势（和风险），并提供有关何时应该保护文件和电子邮件的指导。 如果你配置了 [自定义模板](configure-custom-templates.md)，请提供有关在模板名称和描述不足以帮助用户选择正确模板时应该选择哪个模板的说明。

    > [!TIP]
    > 最终用户示例视频
    >
    > -   [Azure RMS user experience](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)（Azure RMS 用户体验）
    > -   [Azure RMS Document Tracking and Revocation](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)（Azure RMS 文档跟踪和撤消）

-   **管理员信息：**

    有些应用程序使用管理员配置的策略和设置来自动应用信息保护。 你可能需要为管理这些应用程序和服务的其他管理员提供这些应用程序的说明。 有关详细信息，请参阅[应用程序如何支持 Azure Rights Management 服务](../understand-explore/applications-support.md)和[为 Azure Rights Management 服务配置应用程序](configure-applications.md)。

-   **技术支持信息：**

    
    如果用户运行 Azure 信息保护客户端，技术支持操作人员可要求用户使用“帮助和反馈”、“运行诊断”选项，然后重置客户端。 不过，重置既不会注销用户，也不会重启客户端，并且不提供自动修正。

    如果有人合法请求获取对受保护文档的完全访问权限，请确保支持人员可以按流程操作，使用 Azure Rights Management [超级用户功能](configure-super-users.md)请求获取此访问权限。 例如，法律部门或经理可能会在某员工离职后发出此类请求。 

    此外，用户可能会报告的一些典型问题分为以下几类：

    -   **登录帮助：**

        当 Azure Rights Management 服务需要对用户进行身份验证且无法使用缓存的凭据时，可能提示用户提供凭据。 所需的凭据是用户的工作或学校帐户和密码，与 Office 365 租户或 Azure Active Directory 租户相关联。 所需的凭据不是 Microsoft 帐户（前身为 Microsoft Live ID）或用户的个人电子邮件帐户，因为 Azure Rights Management 服务暂不支持这些帐户。 向用户和支持人员提供说明，阐明当用户对应用程序使用 Azure Rights Management 服务时，如果看到需要提供凭据的提示，应使用哪个帐户。

    -   **与保护或使用内容相关的问题：**

        确保用户获得了有关他们所用应用程序的相应说明，并使用 Azure Rights Management 服务支持的应用程序和设备。 有关支持的应用程序和设备的详细信息，请参阅 [Azure Rights Management 的要求](../get-started/requirements-azure-rms.md)。

        身份验证和授权依赖 Azure Active Directory 中的帐户和组。 若要确认能否授权特定用户或组使用受保护内容，请使用[准备用户和组以便使用 Azure 信息保护](../plan-design/prepare.md)中的验证检查。

        如果用户报告称可以打开受保护内容，但没有相应权限，问题可能在于用户不在为 Rights Management 模板配置的正确组中。 或者，问题可能在于[需要重新为用户或组配置模板](configure-policy-template.md)。 
        
        如果用户拥有的权限与预期不同，请查看[使用权限表](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions)中的权限说明和任何应用程序专属实现代码。

请参阅以下关于应用程序特定信息的部分，帮助用户保护敏感的文档和电子邮件。

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>在 Azure 信息保护客户端中使用信息保护
如果用户使用 Office 2010，必须使用 Azure 信息保护客户端（或旧版应用程序 RMS 共享应用程序）保护和使用受保护文档和电子邮件。 不过，还建议将 Azure 信息保护客户端用于所有计算机和移动设备。

使用 Azure 信息保护客户端，除了可以更轻松地保护重要文档和电子邮件之外，用户还可以跟踪受保护文档。 如果之前获得授权的用户无法再访问跟踪的文档，还可以撤销这些文档。

有关如何将此客户端用于 Windows 计算机的说明，请参阅 [Azure 信息保护客户端用户指南](../rms-client/client-user-guide.md)。


## <a name="using-information-protection-with-office-365-office-2016-or-office-2013"></a>在 Office 365、Office 2016 或 Office 2013 中使用信息保护
如果使用的是 Azure Rights Management 服务，但尚未安装 Azure 信息保护客户端，那么用户就不会在 Office 桌面应用程序中看到 Azure 信息保护栏，不会在功能区上看到“保护”按钮，也不会在文件资源管理器中看到“分类和保护”。 这些附加内容有助于用户更轻松地保护文档和电子邮件。 对于这些用户，他们必须遵循类似以下步骤的说明。

> [!TIP]
> 若要查找应用程序特定帮助，以及有关在这些应用程序中使用信息保护的说明，请搜索 **IRM** 和应用程序名称及版本。

#### <a name="to-protect-a-document-in-word-2013"></a>在 Word 2013 中保护文档

1.  在 Microsoft Word 中，创建一个文档。

2.  在“文件”菜单中，依次单击“信息”、“保护文档”和“限制访问”。

3. 选择用于快速应用相应使用权限的模板，或选择“限制访问”，再自行选择使用权限。

    > [!NOTE]
    > 如果之前没有在计算机上使用过 Rights Management，那么“限制访问”选项会连接到 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服务，并提示输入凭据，以便配置 Office IRM 客户端。 然后，可以选择模板或使用权限。

3.  保存文档。

当其他人打开文档时，首先会对他们进行身份验证。 如果他们未被授权打开文档，则文档不会打开。 如果已获得授权可以打开文档，将通过为相应用户指定的受限[使用权限](../deploy-use/configure-usage-rights.md)打开文档。 

例如，“仅查看”使用权限不允许用户编辑或保存文档，即便先将文档复制到其他位置也是如此。 

这些使用权限以限制横幅方式显示在文档顶部。 该横幅可能显示适用于文档的权限，或者提供显示权限的链接。

#### <a name="to-protect-an-email-message-using-outlook-2013-and-exchange-online"></a>使用 Outlook 2013 和 Exchange Online 保护电子邮件

1.  在 Outlook 中，创建一封电子邮件，发送给组织内的收件人。

2.  在 **“选项”** 选项卡中，单击 **“权限”**，然后选择某个选项。 例如：**不得转发**、**&lt;公司名称&gt; - 机密**或**&lt;公司名称&gt; - 机密，仅供查阅**。

3.  发送电子邮件。

与查看受保护文档相似，当收件人打开受保护电子邮件时，首先需要进行身份验证。 如果已获得授权可以查看电子邮件，将通过为相应用户指定的受限[使用权限](../deploy-use/configure-usage-rights.md)打开电子邮件。 

例如，如果电子邮件受“不转发”选项保护，便无法使用功能区上的“转发”按钮。

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>使用 Outlook 网页版保护电子邮件的具体步骤

1.  使用 Outlook 网页版创建一封电子邮件，发送给组织内的收件人。

2.  单击 **“...”**，再单击 **“设置权限”**，然后选择某个选项。 例如：**不得转发**、**不要全部回复**、**&lt;公司名称&gt; - 机密**或**&lt;公司名称&gt; - 机密，仅供查阅**。

3.  发送电子邮件。

与查看受保护文档相似，当收件人打开电子邮件时，首先需要进行身份验证。 如果已获得授权可以查看电子邮件，将通过为相应用户指定的受限[使用权限](../deploy-use/configure-usage-rights.md)打开电子邮件。 

例如，如果你选择了 **“不要全部答复”**，则电子邮件窗口中的 **“全部答复”** 选项不可用。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

