---
title: 个人 RMS 和 Azure 信息保护
description: 介绍了 RMS 个人版，这是免费的自助式订阅，适用于已收到受保护文件，但无法进行身份验证的用户，因为 IT 部门没有在 Azure 中为他们托管帐户。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ac5b596c87649e32d27da8e2797bafe5b9745792
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384785"
---
# <a name="rms-for-individuals-and-azure-information-protection"></a>个人 RMS 和 Azure 信息保护

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 *

>[!NOTE] 
> 为了提供统一且简化的客户体验，Azure 门户中的 **Azure 信息保护经典客户端** 和 **标签管理** 将于 **2021 年3月31日** 被 **弃用**。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

RMS 个人版是免费的自助式订阅，适用于需要打开受 Azure 信息保护保护的文件的用户。 如果 Azure Active Directory 无法对这些用户进行身份验证，此免费登录服务会在 Azure Active Directory 中为用户创建一个帐户。 因此，这些用户现在可以使用其公司电子邮件地址进行身份验证，然后在计算机或移动设备上阅读受保护的文件。

RMS 个人版采用 Azure Active Directory 自助式注册。 如果用户已使用此订阅为组织创建帐户，作为组织管理员，你可以声明所有权，并[控制这些帐户](/azure/active-directory/users-groups-roles/domains-admin-takeover#external-admin-takeover)。 

若要注册此免费帐户，用户可以转到 [Microsoft Azure 信息保护页](https://aka.ms/rms-signup)，并提供其工作电子邮件地址。 他们将收到 Microsoft 的回应电子邮件，然后通过输入详细信息以创建帐户，从而完成注册过程。 

创建帐户后，最终页面显示各种设备的 Azure 信息保护客户端或查看器的下载链接、用户指南链接，以及本机支持 Rights Management 保护的当前应用程序列表的链接。 

### <a name="alternatives-use-office-365-message-encryption-or-microsoft-accounts"></a>替代方法：使用 Office 365 消息加密或 Microsoft 帐户

个人 RMS 是一个选项，可帮助确保组织外部的授权人员始终可以读取组织所保护的文件。 

替代选项包括：

- **使用 [带有新功能的 Office 365 消息加密](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)发送电子邮件。** 此电子邮件解决方案适用于所有设备上的所有电子邮件地址，并且是与组织外部人员安全地共享信息和在浏览器中查看 Office 文档的建议方式。
 
- **使用 Microsoft 帐户。** 当 Microsoft 帐户用于身份验证时，并非所有应用程序都可以打开受保护的内容。 [详细信息](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 


## <a name="to-sign-up-for-rms-for-individuals"></a>注册个人 RMS

1. 使用 Windows 或 Mac 计算机或移动设备，访问 [Microsoft Azure 信息保护页](https://aka.ms/rms-signup)。

2. 键入用于保护需要打开的文档的电子邮件地址。

3. 单击 " **注册**"。

    Microsoft 使用你的电子邮件地址来检查你的组织是否已拥有 [Azure 信息保护高级版](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 或 [Office 365 订阅的订阅，该订阅包含使用 azure 信息保护的数据保护](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)。 如果找到任一订阅，则无需使用个人 RMS。 可以立即登录且个人 RMS 的自助注册将取消。 如未找到任一订阅，则继续下一步。

4. 等待确认电子邮件发送至你提供的地址。 它将来自 Microsoft 365 团队 (support@email.microsoftonline.com) ，并 **为 Microsoft Azure 信息保护完成注册**。

5. 收到该电子邮件后，请单击“是本人”来验证电子邮件地址并完成注册过程。

6. 然后将出现“最后一项操作...”页，用于完善你的帐户信息。 键入你的名字和姓氏，输入并确认你选择的密码，然后单击“开始”。

7. 创建帐户后，将看到新的 Microsoft Azure 信息保护页面，可以在其中下载和安装 Azure 信息保护客户端，或单击[用户指南](./rms-client/client-user-guide.md)链接获取 Windows 计算机的操作说明。

此时，帐户已创建。如果看到登录以读取受保护文件的提示，请输入创建 RMS 个人版帐户所用的相同电子邮件地址和密码。

> [!IMPORTANT]
> 尽管现在还可以使用此帐户保护文件，但不建议这样做，除非组织有 Azure 信息保护的[试用或付费订阅](https://azure.microsoft.com/pricing/details/information-protection/)。 如果通过使用此免费订阅保护文件和电子邮件，然后帐户受组织控制，可能会导致无法访问以前保护的内容。


## <a name="next-steps"></a>后续步骤
个人 RMS 是使用 Azure Active Directory 支持的自助服务注册功能的一个示例。 有关此功能的工作原理的详细信息，请参阅 Azure Active Directory 文档中的 [什么是 Self-Service 注册 Azure Active Directory？](/azure/active-directory/users-groups-roles/directory-self-service-signup) 。

