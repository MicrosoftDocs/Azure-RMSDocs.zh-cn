---
title: 使用 Azure RMS 帮助用户保护文件 - AIP
description: 此信息可帮助你在部署和配置 Azure 信息保护中的 Azure Rights Management 之后，为用户、管理员和技术支持提供指导。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a2b69b7744b17c4f5ccce32a1513015fb4e4cbcc
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2020
ms.locfileid: "95565361"
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>使用 Azure Rights Management 服务帮助用户保护文件

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

为组织部署和配置 Azure 信息保护之后，请为用户、管理员和技术支持提供以下帮助和指导：

-   **最终用户信息**
    
    让用户知道如何以及何时保护包含敏感信息的文档和电子邮件。 尽可能为现有工作流提供此信息，以便可以将附加步骤并入已熟悉的过程，而不是引入新过程。 请务必让他们知道你的业务的相关优势（和风险），并提供有关何时应该保护文件和电子邮件的指导。 如果已配置[模板](configure-policy-templates.md)，请提供有关在模板名称和描述不足以帮助用户选择正确模板时应该选择哪个模板的说明。
    
    > [!TIP]
    > 最终用户示例视频
    > -   [Microsoft Azure 信息保护](https://youtu.be/ToShAUdlrPo?list=PL8nfc9haGeb6qSm1kLU8n3Zqg398764h5)
    > -   [Azure RMS 文档跟踪和撤销](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **管理员信息**
    
    有些应用程序使用管理员配置的策略和设置来自动应用信息保护。 你可能需要为管理这些应用程序和服务的其他管理员提供这些应用程序的说明。 
    
    有关详细信息，请参阅[应用程序如何支持 Azure Rights Management 服务](applications-support.md)和[为 Azure Rights Management 服务配置应用程序](configure-applications.md)。
    
-   **技术支持信息**
    
    如果用户拥有 Azure 信息保护客户端，支持人员可要求他们使用“帮助和反馈”选项，获取例如 Office 版本是否无法支持保护，以及当前登录的用户帐户等信息。 还可使用此选项收集日志文件并重置客户端。 有关详细信息，请参阅管理员指南：[安装检查和疑难解答](./rms-client/client-admin-guide.md#installation-checks-and-troubleshooting)。
    
    如果有合法请求对受保护文档拥有完全访问权限，请确保技术支持使用 Azure 信息保护 [超级用户功能](configure-super-users.md)来请求此访问权限。 例如，法律部门或经理可能会在某员工离职后发出此类请求。
    
    此外，用户可能会报告的一些典型问题分为以下几类：
    
    - **登录帮助**
        
        当 Azure Rights Management 服务需要对用户进行身份验证且无法使用缓存的凭据时，可能提示用户提供凭据。 所需的凭据通常是用户的工作或学校帐户和密码，与 Office 365 租户或 Azure Active Directory 租户相关联。 尽管 Azure Rights Management 服务可以对 Azure AD 帐户进行身份验证，但某些应用程序也可以在使用 Microsoft 帐户进行身份验证时打开受保护的内容。 [详细信息](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 
        
        为用户和你的技术支持提供说明，阐明在具有使用 Azure 权限管理服务的应用程序时，如果提示用户提供凭据，应该使用何种帐户。
        
    - **保护或使用内容时出现问题**
        
        确保用户获得了有关他们所用应用程序的相应说明，并使用 Azure 权限管理服务支持的应用程序和设备。 有关支持的应用程序和设备的详细信息，请参阅 [Azure 信息保护的要求](requirements.md)。
        
        若要确认 Azure Active Directory 能否授权特定用户或组保护或使用受保护内容，请使用[准备用户和组以便使用 Azure 信息保护](prepare.md)中的验证检查。
        
        如果用户报告称可以打开受保护内容，但没有相应权限，问题可能在于用户不在为 Rights Management 模板配置的正确组中。 或者，问题可能在于[需要重新为用户或组配置模板](configure-policy-templates.md)。 
        
        如果用户拥有的权限与预期不同，请查看[使用权限表](configure-usage-rights.md#usage-rights-and-descriptions)中的权限说明和任何特定于应用程序的实现。

请参阅以下关于应用程序特定信息的部分，帮助用户保护文档和电子邮件。

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>在 Azure 信息保护客户端中使用信息保护

如果用户使用 Office 2010，则需要使用 Azure 信息保护客户端来保护和使用受保护文档和电子邮件。 不过，还建议将 Azure 信息保护客户端用于支持此服务的所有计算机和移动设备。

使用 Azure 信息保护客户端，除了可以更轻松地保护文档和电子邮件之外，用户还可以跟踪受保护文档。 如果之前获得授权的用户无法再访问跟踪的文档，还可以撤销这些文档。

有关如何将此客户端用于 Windows 计算机的说明，请参阅 [Azure 信息保护客户端用户指南](./rms-client/client-user-guide.md)。


## <a name="using-information-protection-with-office365-office-2019-office-2016-or-office2013"></a>在 Office 365、Office 2019、Office 2016 或 Office 2013 中使用信息保护
如果使用的是 Azure 权限管理服务，但尚未安装 Azure 信息保护客户端，那么用户就不会在 Office 桌面应用程序中看到 Azure 信息保护栏。 他们也不会在功能区上看到“保护”按钮，或在文件资源管理器中看到“分类和保护”。 这些附加内容有助于用户更轻松地保护文档和电子邮件。 对于这些用户，他们必须遵循类似以下步骤的说明。

> [!TIP]
> 若要查找应用程序特定帮助，以及有关在这些应用程序中使用信息保护的说明，请搜索 **IRM** 和应用程序名称及版本。

#### <a name="to-protect-a-document-in-word-from-office-365-proplus"></a>使用 Office 365 专业增强版保护 Word 文档的具体步骤

1.  在 Microsoft Word 中，创建一个文档。

2.  从 "**文件**" 菜单： "**信息**  >  **保护文档**" "  >   **限制访问**"。

3. 选择用于快速应用相应使用权限的模板，或选择“限制访问”，再自行选择使用权限。

    > [!NOTE]
    > 如果之前没有在计算机上使用过 Rights Management，那么“限制访问”选项会连接到 Azure Rights Management 服务，并提示输入凭据，以便配置 Office IRM 客户端。 然后，可以选择模板或使用权限。

3.  保存文档。

当其他人打开文档时，首先会对他们进行身份验证。 如果他们未被授权打开文档，则文档不会打开。 如果他们已被授权打开文档，将使用为该用户指定的受限 [使用权限](configure-usage-rights.md) 打开它。 

例如，“仅查看”使用权限不允许用户编辑或保存文档，即便先将文档复制到其他位置也是如此。 

这些使用权限以限制横幅方式显示在文档顶部。 该横幅可能显示适用于文档的权限，或者提供显示权限的链接。

#### <a name="to-protect-an-email-message-using-outlook-from-office-365-proplus-connecting-to-exchange-online"></a>若要使用 Office 365 专业增强版中的 Outlook 保护电子邮件，请连接到 Exchange Online

1.  在 Outlook 中，创建一封发送给组织内收件人地址的邮件。

2.  从 " **选项** " 选项卡： **权限** > 选择一个选项。 例如：**不要转发**、或 **\<Company Name> -机密** 或 **\<Company Name> -机密查看**。

3.  发送消息。

与查看受保护文档相似，当收件人打开受保护电子邮件时，首先需要进行身份验证。 如果他们已被授权查看电子邮件，则将使用为该用户指定的受限 [使用权限](configure-usage-rights.md) 打开它。 

例如，如果电子邮件受“不转发”选项保护，便无法使用功能区上的“转发”按钮。

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>使用 Outlook 网页版保护电子邮件的具体步骤

1. 使用 Outlook 网页版创建一封电子邮件，发送给组织内的收件人。

2. 选择“保护”。 除非管理员已更改默认设置，否则自动选中“不要转发”选项。 如果要更改默认设置，请选择 " **更改权限** "，然后从下拉选项中选择一个选项。 例如：**加密** 或 **\<Company Name> 机密**。

3. 发送消息。

与查看受保护文档相似，当收件人打开电子邮件时，首先需要进行身份验证。 如果他们已被授权查看电子邮件，则将使用为该用户指定的受限 [使用权限](configure-usage-rights.md) 打开它。 

例如，选中默认的“不要转发”选项后，便无法选中消息窗口内的“转发”选项。
