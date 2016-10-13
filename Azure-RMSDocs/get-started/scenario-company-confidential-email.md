---
title: "方案 - 发送公司机密电子邮件 | Azure 信息保护"
description: "此方案和支持性的用户文档使用 Azure Rights Management 保护，以便组织中的任何用户可安全发送组织外无法查阅的电子邮件通信。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 950799e9-2289-48c7-b95a-f54a8ead520a
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ea299f402e5e188b498bf6e3cacf9d4dc7e0f6e8
ms.openlocfilehash: 9fafe78b8393ae36defeecccceb8f4a2d36a3b79


---

# 方案 - 发送公司机密电子邮件

>*适用于：Azure 信息保护、Office 365*

此方案和支持性的用户文档使用 Azure 信息保护中的 Azure Rights Management 技术，以便组织中的任何用户可安全发送组织外无法查阅的电子邮件通信。 例如，如果某人将电子邮件转发给其他组织的人员或个人电子邮件帐户。 该电子邮件和所有附件将受 Azure Rights Management 和用户从电子邮件客户端选择的模板保护。

启用此方案最简单的方法是使用一个内置默认模板，该模板会自动限制对你的组织中所有用户的访问。 但如有必要，可以通过创建自定义模板使其更具限制性，例如，限制对用户子集的访问或具有其他限制（例如只读或到期日期）或在电子邮件客户端中禁用“转发”按钮。

> [!IMPORTANT]
> 在此方案中，虽然你可以直接从所配置的自定义模板中删除“转发”，且这会在电子邮件客户端中禁用“转发”按钮，但此配置无法防止用户与其他已授权的用户共享电子邮件。 收件人可保存电子邮件（以及任何附件），然后通过使用其他共享机制来共享信息。
> 
> 例如，Bob 使用自定义模板向 Alice 发送电子邮件，此模板将“保存文件和编辑内容”自定义权限应用到“营销”组，且不包含“转发”权限。 虽然 Alice 无法将电子邮件转发给其他人，但她可以将电子邮件以及任何附件保存到 U 盘或文件服务器共享，如果“营销”组的任何成员有访问这些文件的权限，则均可对其进行阅读和编辑。 没有在“营销”组的用户将不能打开该内容。

这些指令适用于下面一组情况：

-   组织内的任何用户想在组织内与其他用户共享信息，但该信息不应在组织外共享。

-   要共享的信息可以包含在电子邮件或附件内。

-   用户必须从其电子邮件客户端内手动选择模板。

## 部署说明
![Azure RMS 快速部署的管理员指令](../media/AzRMS_AdminBanner.png)

在进入用户文档前，请确保已满足以下要求。

## 本方案的要求
要让针对此方案的说明生效，必须做好以下准备：

|要求|需要更多信息|
|---------------|--------------------------------|
|已准备好 Office 365 或 Azure Active Directory 的帐户和组|[准备 Azure 信息保护](../plan-design/prepare.md)|
|Azure 信息保护租户密钥由 Microsoft 管理；没有使用 BYOK|[计划和实施 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)|
|已激活 Azure Rights Management|[激活 Azure 权限管理](../deploy-use/activate-service.md)|
|下列情况之一：<br /><br />- 已为 Azure Rights Management 启用了 Exchange Online<br /><br />- 已为 Exchange 内部部署安装和配置了 RMS 连接器|对于 Exchange Online，请参阅 [Office 365：客户端和联机服务的配置](../deploy-use/configure-office365.md)中的 **Exchange Online：IRM 配置**部分。<br /><br />对于 Exchange 内部部署：请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)|
|你未存档默认 Azure Rights Management 模板**&lt;组织&gt; - 机密**。 或者，你已为此配置了自定义模板，因为你需要更严格的设置或者仅组织中的用户子集应能够查阅受保护的电子邮件。|[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)<br /><br />提示：如果你需要更严格的使用策略设置，但对于组织中的所有用户，复制、然后编辑的是一个默认模板，而不是从头创建一个模板。<br /><br />对于此方案中的电子邮件客户端，已更新的模板不会立即刷新。 有关信息，请查看[为用户刷新模板](../deploy-use/refresh-templates.md)一文。|
|发送受保护电子邮件的用户具有 Outlook 2013 或 Outlook 2016 或 Outlook Web Access。<br /><br />收到电子邮件的用户具有支持 Azure Rights Management 的电子邮件客户端。|你可使用 Outlook 2010，但必须[安装适用于 Windows 的 Rights Management 共享应用程序](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)，并相应地调整用户说明。<br /><br />有关支持 Azure Rights Management 的电子邮件客户端的列表，请参阅 [Azure RMS 要求：应用程序](../get-started/requirements-applications.md)表中的**电子邮件**列。|

## 用户文档说明
使用以下模板，将此用户说明复制并粘贴到最终用户的通信中，并进行这些修改以反映你的环境：

1.  将*&lt;组织名称&gt;*所有实例替换为你的组织的名称。

2.  将*&lt;组织名称 - 机密&gt;*的所有实例替换为默认或自定义模板的名称。

3.  替换屏幕截图，使其显示组织模板名称。

4.  将*&lt;联系人详细信息&gt;*替换为有关用户如何与技术支持联系的说明，例如网站链接、电子邮件地址或电话号码。

5.  **你可能想要进行的其他修改：**

    -   如果可以将说明限制到仅一个电子邮件客户端，为简单起见，请考虑进行此操作，并删除其他说明组。

    -   如果使用自定义模板，而不是建议的默认模板，请相应地修改用语：

        -   使标题更具针对性。

        -   在步骤 1 中指定要选择的用户或组。

        -   在步骤 2 中指定自定义模板的名称。

        -   修改最后一个段落，说明收件人将有的限制。

6.  对此组说明进行其他任何所需的修改，然后将其发送给这些用户。

7.  由于某些客户端不支持 Rights Management，你可能需要为这些受保护电子邮件的收件人提供指导和建议。 此信息将以你组织中使用的设备和电子邮件应用程序以及你的首选项为基础。 例如，建议 iOS 用户通过 iPad 和 iPhone 适用的 Outlook 查阅受保护电子邮件，而不是使用本机 iOS 电子邮件客户端查阅。

    有关电子邮件客户端的详细信息，请参阅[ Azure Rights Management 的要求](https://technet.microsoft.com/library/dn655136.aspx)中[客户端设备功能](https://technet.microsoft.com/library/dn655136.aspx)中的**电子邮件**列。

示例文档演示了在你完成自定义后，用户看到这些说明的可能形式。

![Azure RMS 快速部署的用户文档模板](../media/AzRMS_UsersBanner.png)

### 如何使用 Outlook 发送包含公司机密信息的电子邮件

1.  在 Outlook 中，创建新电子邮件，添加要包含的任何附件，然后从*&lt;组织名称&gt;*选择用户或组。

2.  在**选项**选项卡上，单击**权限**，然后选择**&lt;组织名称 - 机密&gt;**：

    ![屏幕截图：如何使用 Outlook 发送包含公司机密信息的电子邮件](../media/AzRMS_OutlookTemplate.PNG)

3.  发送电子邮件。

### 如何使用 Outlook Web App 发送包含公司机密信息的电子邮件

1.  在 Outlook Web App 中，创建新电子邮件，添加要包含的任何附件，然后从通讯簿选择*&lt;组织名称&gt;*用户或组。

2.  单击 **…**，单击**设置权限**，然后选择**&lt;组织名称 - 机密&gt;**：

    ![屏幕截图：如何使用 Outlook Web App 发送包含公司机密信息的电子邮件](../media/AzRMS_OWATemplate.png)

3.  发送电子邮件。

当**收件人**、**抄送**或**密件抄送**行中的某些人收到此电子邮件时，会提示他们先进行身份验证才能查阅电子邮件，以验证他们是*&lt;组织名称&gt;*中的用户。 在其他情况下，系统不会提示用户，因为已通过身份验证。

电子邮件收件人可将此电子邮件转发给其他人，但仅*&lt;组织名称&gt;*中的用户可查阅此电子邮件。 如果附加一个 Office 文档，它将具有相同的保护，即使将该附件保存为其他名称，保存在其他位置，也是如此。 但是，身份验证成功的用户可以从电子邮件或附件复制和粘贴或从其打印。 如果你需要可防止这类操作的更加严格的保护，请与技术支持人员联系。

**需要帮助吗?**

-   与技术支持联系：

    -   *&lt;联系人详细信息&gt;*

### 自定义用户文档示例
![Azure RMS 快速部署的用户文档示例](../media/AzRMS_ExampleBanner.png)

#### 如何使用 Outlook 发送包含公司机密信息的电子邮件

1.  在 Outlook 中，新建电子邮件，添加要包含的任何附件，然后从通讯簿选择 VanArsdel 用户或组。

2.  在“选项”选项卡中，单击“权限”，然后选择 **VanArsdel, Ltd - 机密**：

    ![屏幕截图：如何使用 Outlook 发送包含公司机密信息的电子邮件](../media/AzRMS_OutlookTemplate.PNG)

3.  发送电子邮件。

#### 如何使用 Outlook Web App 发送包含公司机密信息的电子邮件

1.  在 Outlook Web App 中，新建电子邮件，添加要包含的任何附件，然后从通讯簿选择 VanArsdel 用户或组。

2.  单击 **…**，单击“设置权限”，然后选择 **VanArsdel, Ltd - 机密**：

    ![屏幕截图：如何使用 Outlook Web App 发送包含公司机密信息的电子邮件](../media/AzRMS_OWATemplate.png)

3.  发送电子邮件。

当“收件人”、“抄送”或“密件抄送”行中的某些人收到此电子邮件时，会提示他们先进行身份验证才能查阅电子邮件，以验证他们是 VanArsdel, Ltd 中的用户。 在其他情况下，系统不会提示用户，因为已通过身份验证。

电子邮件收件人可将此电子邮件转发给其他人，但仅 VanArsdel, Ltd 中的用户可查阅此电子邮件。 如果附加一个 Office 文档，它将具有相同的保护，即使将该附件保存为其他名称，保存在其他位置，也是如此。 但是，身份验证成功的用户可以从电子邮件或附件复制和粘贴或从其打印。 如果你需要可防止这类操作的更加严格的保护，请与技术支持人员联系。

**需要帮助吗?**

-   与技术支持联系：

    -   电子邮件：helpdesk@vanarsdelltd.com




<!--HONumber=Sep16_HO4-->


