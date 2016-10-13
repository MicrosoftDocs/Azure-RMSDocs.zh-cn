---
title: "方案 - 保护文件服务器共享上的文件 | Azure 信息保护"
description: "此方案和支持性的用户文档使用 Azure Rights Management 保护批量保护想要在文件服务器上保护的所有文件，确保只有组织的员工可以访问这些文件，即使它们被复制并保存到不受 IT 部门控制的存储器中，或已通过电子邮件发送给其他人。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b61b7068e67103c45aea139cf95dacb851fe70e2
ms.openlocfilehash: a12276bcf2072ac812ae6b68d9e1cdacbe46adaa


---

# 方案 - 保护文件服务器共享上的文件

>*适用于：Azure 信息保护、Office 365*

此方案和支持性的用户文档使用 Azure 信息保护中的 Azure Rights Management 技术批量保护想要在文件服务器上保护的所有文件，确保只有组织的员工可以访问这些文件，即使它们被复制并保存到不受 IT 部门控制的存储器中，或已通过电子邮件发送给其他人。

这些说明使用其中一个默认模板，这会限制具有全部使用权限的所有员工的访问权限。 但是，如有必要，可以通过配置自定义模板而非使用默认模板进一步限制访问和使用权限。

这些指令适用于下面一组情况：

-   需要保护所有文件类型，而不只是 Office 文件。 无法受 Azure RMS 本机保护的文件将受常规保护。

-   指定路径中的所有文件（包括子文件夹）都将受到保护。

-   按计划对所有文件重新应用保护，确保对权限策略模板所做的任何更改都能应用到受保护文件中。

## 部署说明
![Azure RMS 快速部署的管理员指令](../media/AzRMS_AdminBanner.png)

请确保已满足以下要求，然后在进入到用户文档环节前按照支持过程的说明进行操作。

## 本方案的要求
要让针对此方案的说明生效，必须做好以下准备：

|要求|需要更多信息|
|---------------|--------------------------------|
|已激活 Azure Rights Management|[激活 Azure 权限管理](../deploy-use/activate-service.md)|
|你已将本地 Active Directory 用户帐户（包括其电子邮件地址）与 Azure Active Directory 或 Office 365 同步。 对于所有需要访问受 FCI 和 Azure Rights Management 保护的文件的用户来说，这都是必需的。|[准备 Azure 信息保护](../plan-design/prepare.md)|
|下列情况之一：<br /><br />若要为所有用户使用默认模板：你尚未存档默认模板，&lt;组织名称&gt; - 机密<br /><br />- 若要为特定用户使用自定义模板：你已创建并发布此自定义模板|[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)|
|已将 Rights Management 共享应用程序部署到运行 Windows 的用户计算机|[自动部署 Microsoft Rights Management 共享应用程序](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)|
|已下载 RMS 保护工具并已配置 Azure RMS 的必备组件|有关下载此工具和必备组件的说明，请参阅 [RMS 保护 Cmdlet](https://msdn.microsoft.com/library/mt433195.aspx)<br /><br />若要配置 Azure RMS 的其他必备项，如服务主体帐户，请参阅 [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)|

### 使用 Azure RMS 和带有文件分类基础结构的文件服务器资源管理器来配置保护所有文件的文件服务器。

1.  启动 Windows PowerShell 会话。 无需以管理员身份运行此会话。

2.  对 Azure RMS 进行身份验证：

    ```
    Set-RMSServerAuthentication
    ```
    出现提示时，请提供作为 RMS 保护 cmdlet 的必备项而创建的服务主体帐户值。

3.  运行以下命令标识将用于保护文件的模板 ID：

    ```
    Get-RMSTemplate
    ```
    若要使用限制具有全部使用权限的所有员工的访问权限的默认模板。请查找**&lt;组织名称&gt; - 机密**的模板名。 例如，**VanArsdel, Ltd - 机密**。

4.  按照[使用 Windows Server 文件分类基础结构 (FCI) 的 RMS 保护](../rms-client/configure-fci.md)中的分步说明进行操作。

    这些说明包括一个指定在文件服务器资源管理器中作为自定义可执行文件运行的 Windows PowerShell 脚本。 还包括验证这些文件是否受 Azure Rights Management 保护的方式。

## 用户文档说明
如果保护的文件仅为 Office 文件，则不需要向用户提供有关受保护文件的说明。 已授权的用户打开这些文档的方式与往常在 Office 中的一样，唯一区别在于可能会提示用户进行身份验证，用户可能会看到文档顶部有一个告知你文档已受保护的信息栏。

如果受保护文件具有 **.ppdf** 文件扩展名，或者该文件为受保护的文本或图像文件（例如，其中包含 **.ptxt** 或 **pjpg** 文件扩展名），则现在这些文件为只读文件，无法对其进行编辑。 用户可以使用 RMS 共享应用程序查看器来查看文件，查看器将为这些文件类型自动加载。 这些文件受 Azure RMS 本机保护，并会从你应用的模板中应用所有策略设置，使用权限除外，因为该文件本身为只读文件。 除非你知道以后要保护这些文件类型，否则不太可能需要此方案的用户说明，但应向技术支持发出警告，他们可能需要向用户解释无法对这些文件进行编辑的原因。

如果受保护的文件具有 **.pfile** 文件扩展名，用户就可以查看这些文件，但是如果用户想要进行编辑并保存更改，则需将其保存为初始文件名（删除 .pfile 文件扩展名）。 这些文件受 Azure RMS 常规保护，且无法从应用的模板强制实施使用权限，这意味着如果使用新名称保存文件，则文件会失去保护。 此方案需要用户说明。

使用以下模板，为最终用户复制并粘贴此说明，以便其了解如何编辑受常规保护的文件。 进行这些修改以反映你的环境：

-   将*&lt;文件类型&gt;*和*&lt;文件服务器共享&gt;*替换为将受常规保护的文件类型和文件服务器共享的名称。

-   将*&lt;组织名称&gt;*替换为你组织的名称，会显示在默认的 Azure Rights Management 模板上。

-   将*&lt;组织名称&gt;*替换为你组织的名称。

-   将*&lt;有关如何保存文件并删除 .pfile 文件扩展名的说明&gt;*替换为此文件类型的特定于应用程序的说明。

-   将联系人详细信息替换为有关用户如何与技术支持联系的说明，例如网站链接、电子邮件地址或电话号码。

-   对此组说明进行其他任何所需的修改，然后将其发送给这些用户。

示例文档演示了在你完成自定义后，用户看到这些说明的可能形式。

![Azure RMS 快速部署的用户文档模板](../media/AzRMS_UsersBanner.png)

### 如何从&lt;文件服务器共享编辑&lt;文件类型&gt;&gt;

1.  双击该文件以将其打开。 系统可能会提示你输入凭据。

2.  你会从 Microsoft Rights Management 共享应用程序中看到一个**受保护文件**对话框，提示你应慎重使用**&lt;组织名称&gt; - 机密**的权限。 这意味着你不应与&lt;组织名称&gt;员工以外的人员共享此文档。

3.  单击“打开”。

4.  若要编辑文件，首先保存该文件并删除 .pfile 文件扩展名：

    -   &lt;有关如何保存文件并删除 .pfile 文件扩展名的说明&gt;

5.  现在就可以正常编辑和保存文件了。

系统将定期保护再次添加了 .pfile 文件扩展名的文件，这就需要你重复以上步骤。

**需要帮助吗?**

-   其他信息：

    -   [保护你通过电子邮件共享的文件](../rms-client/sharing-app-view-use-files.md)

-   与技术支持联系：

    -   *&lt;联系人详细信息&gt;*

### 自定义用户文档示例
![Azure RMS 快速部署的用户文档示例](../media/AzRMS_ExampleBanner.png)

#### 如何从 ProjectNextGen 共享中编辑 CAD 绘图

1.  双击该文件以将其打开。 系统可能会提示你输入凭据。

2.  你会从 Microsoft Rights Management 共享应用程序中看到一个**受保护文件**对话框，提示将授予你对 **VanArsdel, Ltd - 机密**的访问权限。 也就是说系统不允许与不是 VanArsdel, Ltd 的员工共享此文档。

3.  单击“打开”。

4.  若要编辑文件，首先保存该文件并删除 .pfile 文件扩展名：

    -   **文件** &gt; **另存为**

    -   删除文件名末尾的 **.pfile**，然后单击“确定”。

5.  现在就可以正常编辑和保存文件了。

系统将定期保护再次添加了 .pfile 文件扩展名的文件，这就需要你重复以上步骤。

**需要帮助吗?**

-   其他信息：

    -   [保护你通过电子邮件共享的文件](../rms-client/sharing-app-view-use-files.md)

-   请联系技术支持：helpdesk@vanarsdelltd.com




<!--HONumber=Sep16_HO4-->


