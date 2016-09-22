---
title: "用户如何注册个人 RMS | Azure RMS"
description: "此免费帐户的注册说明以及有关此过程工作原理的技术信息。"
author: cabailey
manager: mbaldwin
ms.date: 09/01/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0bd53bde0bfa9b44203b9d2f0f429265a013476c
ms.openlocfilehash: 25c2ddac40c9eff78101cfaf42d4398be4e8a5cc


---

# 用户如何注册个人 RMS

>*适用于：Azure Rights Management*

若要注册这种免费帐户，可以通过访问 [Microsoft Azure Rights Management 页](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)发出请求，并提供你的工作电子邮件地址。 将你导向此注册页面的最常见方式是接收带有受保护附件的电子邮件，这包含有关如何注册的说明。 你将收到 Microsoft 的回应电子邮件，然后完成注册过程，方法是输入详细信息来创建帐户。 完成后，将出现可在其中下载适用于不同设备的共享应用程序的页面、用户指南链接和本身就支持 Rights Management 保护的应用程序当前列表链接。 

## 注册个人 RMS

1.  使用 Windows、Mac 计算机或移动设备，访问 [Microsoft Azure Rights Management 页](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)。

2.  键入你用作组织电子邮件的电子邮件地址，例如 **janetm@contoso.com** 或 **p.dover@fabrikam.com**。

    > [!IMPORTANT]
    > 不支持个人电子邮件地址，因此请不要输入 Microsoft 帐户（以前称为 Microsoft Live ID 帐户）或可能在家使用的由 Internet 服务提供商提供的其他个人帐户。

3.  单击“注册”。

    Microsoft 使用电子邮件地址检查你的组织是否已经具有[包括 Azure RMS 的付费订阅](../get-started/requirements-subscriptions.md)。 如果是这种情况，你无需使用个人 RMS，因此可以立即登录并且个人 RMS 的自助注册将取消。 如果没有找到 Azure RMS 的付费订阅，你将继续到下一步。

4.  等待确认电子邮件发送至你提供的地址。 Office 365 团队 (support@email.microsoftonline.com) 将发送主题为**完成注册 Microsoft Azure Rights Management** 的电子邮件。

5.  收到该电子邮件后，请单击“是本人”来验证电子邮件地址并完成注册过程。

6.  然后将出现“最后一项操作...”页，用于完善你的帐户信息。 键入你的名字和姓氏，输入并确认你选择的密码，然后单击“开始”。

7. 创建帐户后，将出现新的 Microsoft Rights Management 页，可以在其中下载和安装共享应用程序，或单击[详细信息](../rms-client/sharing-app-user-guide.md)链接阅读共享应用程序用户指南。

现在你的帐户已经创建，你可以随时开始保护文件并读取其他人保护的文件。 若提示登录以便保护文件或读取受保护文件，请输入你用于创建个人 RMS 帐户的电子邮件地址和密码。

## 注册过程的技术概述
个人 RMS 使用自助注册过程，该过程也可由其他使用 Microsoft 基于云的技术对用户进行身份验证的服务使用。

以下是用户注册个人 RMS 但其组织没有 Office 365 订阅或 Azure 订阅，因此 Azure 中没有目录可对用户进行身份验证时后台发生的情况：

1.  当组织的第一位用户请求个人 RMS 订阅时，系统会检查其电子邮件地址中提供的域名，查看该域名是否已与某个 Azure 租户相关联。 如果不存在现有租户，将自动为组织创建新租户和 Azure 目录，这包含此首位用户的帐户。 与 Azure 的付费订阅不同，此第一个帐户不是全局管理员，而是标准用户。 新帐户使用用户提供的电子邮件地址和密码。

    > [!NOTE]
    > 某些域名不能用于创建目录，因此不能用于个人 RMS。

    如果找到了现有租户，将对其进行检查以查看它是否具有 Azure RMS 订阅。 当没有找到订阅时，可以添加免费的个人 RMS 订阅。

2.  将授予组织个人 RMS 订阅。 现在，此用户可使用 Azure 进行身份验证，然后可以使用 Azure Rights Management 来保护文件并读取其他人保护的文件。 若要保护文件和读取受保护文件，用户必须具有启用 RMS 的应用程序，如免费的 [Rights Management 共享应用程序](../rms-client/sharing-app-windows.md)。

3.  当同一个组织的第二个用户请求个人 RMS 订阅时，将使用该组织的个人 RMS 订阅将一个新用户帐户添加到前面创建的 Azure 目录。 这第二个用户能够执行第一个用户能够执行的所有操作（保护文件和读取受保护文件），但除此之外，这两位用户现在还能够更加轻松地安全协作，因为他们可以快速将默认模板应用于文件，以仅允许其组织的 Azure 目录中的帐户访问这些文件。

4.  来自同一个组织的后续用户遵循相同的模式，向该组织的 Azure 目录添加用户帐户（当新用户注册时）。 添加到目录的帐户越多，能够与同事和合作伙伴进行安全协作的用户就越多，此外还能更加轻松地防止未授权人员读取他们没有访问权限的文件。

在这整个过程中，不会向组织收取任何费用，也不需要 IT 部门做任何工作。 但是，IT 部门可以选择采用以下某种管理方式：

-   **管理帐户和注册过程**：IT 管理员可以获得 Azure 中自动创建的目录和帐户的所有权。 然后，他们就可以通过实现密码同步和单一登录等目录集成解决方案来管理帐户。 或者，他们可以阻止用户创建帐户或注册个人 RMS。

    有关详细信息，请参阅[管理员如何才能控制为个人 RMS 创建的帐户](rms-for-individuals-take-control.md)。

-   **管理 Rights Management**：IT 管理员可以将组织的个人 RMS 订阅转换为包括 Azure 权限管理的付费订阅。 当他们执行此操作时，现有 Azure 目录和帐户将会保留，以便使用个人 RMS 的现有用户能够进行无缝转换。 用户以前保护的所有文件仍将使用相同策略进行保护，他们向其授予文件使用权限的人员仍将能够通过相同方式使用文件。

    当你执行此操作过程时，你的组织能够将权限管理集成到其工作流、服务和数据存储并从中受益。 此外，你现在还能够管理权限管理，因为你控制了组织的 Azure 权限管理租户密钥。 你现在可以执行以下操作：

    -   配置 Exchange 和 SharePoint 以支持 Azure Rights Management，即便它们在本地运行也能做到。 本机支持 Exchange 和 SharePoint 以实现联机服务，通过本地服务器的连接器为它们提供支持。 有关详细信息，请参阅以下内容：

        -   [Office 365：客户端和联机服务的配置](../deploy-use/configure-office365.md)中的 Exchange Online 和 SharePoint Online 部分

        -   [部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)

    -   对公司拥有的数据执行电子发现，如果需要，还可解密使用权限管理保护的文件。 有关详细信息，请参阅[为 Azure Rights Management 和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

    -   记录在组织中使用的所有权限管理活动。 这是一项非常强大的功能，因为你不仅能够监视哪些文件受到保护，哪些用户成功访问了那些受保护文件，还能够识别试图访问受保护文件的未授权用户的潜在可疑行为。 有关详细信息，请参阅[记录和分析 Azure Rights Management 使用情况](../deploy-use/log-analyze-usage.md)。

    -   如果这些 [Azure RMS 订阅](https://technet.microsoft.com/dn858608)支持这些功能，请提供用户跟踪和撤销其受保护的文档的功能。 有关详细信息，请参阅 [RMS 共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)中的[跟踪和撤消文件](../rms-client/sharing-app-track-revoke.md)。

    -   实现“自带密钥”解决方案 (BYOK)，以便能够根据你的 IT 策略，在本地生成 Azure 权限管理的租户密钥，并使用硬件安全模块 (HSM) 将该密钥安全传输到 Microsoft。 有关详细信息，请参阅[计划和实施你的 Azure Rights Management 租户密钥](../plan-design/plan-implement-tenant-key.md)。


## 后续步骤
请参阅[管理员如何才能控制为个人 RMS 创建的帐户](rms-for-individuals-take-control.md)。





<!--HONumber=Sep16_HO2-->


