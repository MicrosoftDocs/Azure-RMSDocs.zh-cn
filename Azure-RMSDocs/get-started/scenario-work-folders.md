---
title: "AIP 方案 - 为 RMS 保护配置工作文件夹"
description: "此方案和支持性的用户文档使用 Azure Rights Management 保护对工作文件夹中的 Office 文档应用持续保护。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1f189345-a69e-4bf5-8a45-eb0fe5bb542b
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5da891cb6f2220d252704e33486b6450f38375cf
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="scenario---configure-work-folders-for-persistent-protection"></a>方案 - 配置工作文件夹的持续保护

>*适用于：Azure 信息保护、Office 365*

此方案和支持性的用户文档使用 Azure 信息保护中的 Azure Rights Management 技术对[工作文件夹](https://technet.microsoft.com/library/dn265974.aspx)中的 Office 文档应用持续保护。 工作文件夹使用运行 Windows Server 的文件服务器的角色服务，它使用户可以一种一致的方式从他们的 PC 和设备访问其工作文件夹。 尽管工作文件夹会提供它自己的加密来保护文件，但如果文件被移动到工作文件夹环境之外的话，这种保护便会消失。 例如，用户复制同步文件并将其保存到不在 IT 部门控制下的存储器中，或者通过电子邮件将文件发送给其他人。

Azure Rights Management 提供的额外保护通过阻止组织外的人员查看文件来帮助防止意外的数据丢失。 你可以使用内置的默认权限策略模板之一来达到此目的。 然而，在部署此方案之前，请考虑用户是否可能需要与组织外的人员合法共享这些文件。 例如，在研究了草拟的价目表之后，用户要将最终版本通过电子邮件发送给其处于另一组织中的客户。 当你对工作文件夹使用默认 Rights Management 模板时，其他组织中的客户便无法读取此通过电子邮件发送的文档。 可以通过创建让用户可将新权限策略应用到文件的自定义模板来解决此要求，这会替换所有员工对邮件中指定的人员的原始限制。

> [!NOTE]
> 当使用为此方案记录的自定义模板时，虽然用户可能会有意与你未在模板中定义的人员共享文件，但你通过 Azure Rights Management 所应用的额外保护便可起到相应的作用。 如果内容被移动到工作文件夹边界外，此额外保护可防止意外的数据丢失，因为该内容仍受保护，未经授权的用户无法访问，不论它是处于空闲状态还是传输中。 例如，一位用户丢失了正在使用工作文件夹的设备，或此设备被盗，或同步到此设备和从此设备同步的内容通过不安全的基础结构传输。
> 
> 如果用户与另一组织中的某人共享内容，通过从 Rights Management 共享应用程序使用“共享保护项”功能，用户可以将原始保护替换为他们自己的保护策略。 由此，内容仍受保护以防止未经授权的访问，只有用户指定的人员才可以访问内容。

你可以将此持续保护应用到用户的工作文件夹中的所有 Office 文档，或仅应用到包含敏感或业务影响巨大的数据的文件。

这些指令适用于下面一组情况：

-   你要使用持续保护来保护的工作文件夹文件是 Office 文件。 这些文件可以由 Azure Right Management 进行本机保护，且请勿更改其文件扩展名或要求不同的工作流来打开它们。

-   你想将持续保护应用到用户的工作文件夹中的所有 Office 文件，或应用到通过使用 Windows Server 中文件服务器资源管理器的文件分类基础结构标识的选择性文件。

-   对于必须与未在权限策略模板中指定的人员共享的文件（例如另一组织中的用户），用户必须应用新的权限策略以替换原始权限策略保护。

## <a name="deployment-instructions"></a>部署说明
![Azure RMS 快速部署的管理员指令](../media/AzRMS_AdminBanner.png)

请确保已满足以下要求，然后在进入到用户文档环节前按照支持过程的说明进行操作。

## <a name="requirements-for-this-scenario"></a>本方案的要求
要让针对此方案的说明生效，必须做好以下准备：

|要求|需要更多信息|
|---------------|--------------------------------|
|已激活 Azure Rights Management|[激活 Azure Rights Management](../deploy-use/activate-service.md)|
|你已将本地 Active Directory 用户帐户（包括其电子邮件地址）与 Azure Active Directory 或 Office 365 同步。 这对所有使用工作文件夹的用户都是必需的。|[准备 Azure 信息保护](../plan-design/prepare.md)|
|下列情况之一：<br /><br />如果要针对所有用户使用不允许用户应用新权限策略的默认模板：你尚未存档默认模板，**&lt;组织名称&gt; - 机密**<br /><br />- 如果要使用允许用户应用新权限策略的适用的自定义模板：使用随后的说明来创建自定义模板|[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)|
|已为 Windows Server 计算机安装并授权 Rights Management 连接器，且已为 **FCI 服务器**角色配置了该连接器。|[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)|
|已将 Rights Management 共享应用程序部署到运行 Windows 的用户计算机|[自动部署 Microsoft Rights Management 共享应用程序](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)|

### <a name="configuring-the-custom-rights-policy-template-so-that-users-can-share-work-folders-files-outside-the-organization"></a>配置自定义权限策略模板，以便用户可以将工作文件夹文件共享到组织外

1.  登录到 Azure 经典门户，并导航至 Azure Rights Management 模板。

2.  复制**&lt;组织名称&gt; - 机密**模板，并为该工作文件夹方案提供名称和说明。 我们提供以下建议:

    -   名称：**工作文件夹保护的内容**

    -   说明：**此内容受工作文件夹保护，且仅限公司员工使用。若要与组织外的人员共享此内容，请将文档附加到电子邮件消息并使用共享保护项功能。**

3.  在“权限”页上：

    -   将现有的权限从“自定义”更改为“共有者”。

4.  在“配置”页上：

    -   确保“状态”设置为“发布”

    -   对于**名称和说明**，删除你不使用的语言的条目。 对于你确实要使用的语言，使用指定的语言更新“名称”和“说明”以使其匹配你为此模板提供的名称和说明。

5.  保存该模板。

### <a name="configuring-work-folders-to-apply-persistent-protection-to-office-file"></a>配置工作文件夹以对 Office 文件应用持续保护

1.  为你的用户实现工作文件夹，以便本地保存的文件同步到名为*同步共享*的文件服务器文件夹。 文件服务器上的同步共享不能位于运行 Rights Management 连接器的服务器上。

    此解决方案需要服务器管理器中的工作文件夹角色服务以获得文件和存储服务角色。 文件服务器所能运行的最低版本为 Windows Server 2012 R2，该文件服务器可以在本地运行或位于 Azure 中的虚拟机上。 有关工作文件夹的详细信息，请参阅[工作文件夹概述](https://technet.microsoft.com/library/dn265974.aspx)。

    有关部署说明，请参阅[部署工作文件夹](https://technet.microsoft.com/library/dn528861.aspx)。 确保选择内置加密（**加密工作文件夹**选项），它将与 Azure Rights Management 加密一起应用。 此外：

    -   当你在同步服务器上绑定 SSL 证书时（步骤 4）：使用 netsh 命令（而非 IIS 管理控制台）将证书绑定到默认网站 HTTPS 接口。

    -   若要避免用户收到工作文件夹设置错误**应用安全策略时出现错误**，以及避免他们必须为其加入域的计算机上的本地管理员这一要求：使用具有 PasswordAutolockExcludeDomain 参数的 [Set-SyncShare](https://technet.microsoft.com/library/dn296649%28v=wps.630%29.aspx) cmdlet，并指定这些计算机驻留的域的名称（如 contoso.com）。

2.  完成 Rights Management 连接器的配置：

    1.  使用文件服务器资源管理器创建将同步共享文件夹标识为范围的文件管理任务。

    2.  要执行此操作，选择“RMS 加密”，然后选择模板：

        -   如果你因为不希望用户与组织外的其他人共享文件而未创建自定义模板，请选择**&lt;组织名称&gt; - 机密**的模板名称。 例如，**VanArsdel, Ltd - 机密**。

        -   如果你使用前述说明创建了自定义模板，请选择该模板。 例如，**工作文件夹保护的内容**。

    3.  指定计划，即允许 Azure Rights Management 使用充足的时间对所有 Office 文件进行加密，并指定**连续对新文件运行**的选项。

3.  若要手动测试该配置，请确保文件夹包含一些 Office 文件，然后使用“立即运行文件管理任务”选项，并选择“等待任务完成”。

    等待“运行文件管理任务”对话框关闭，然后在自动显示的报告中查看结果  。 你应在“文件”字段中看到所选文件夹中的文件数  。 确认所选文件夹中的文件现已受 Azure Rights Management 保护。 例如，打开一个文件并确认在文档顶部看到显示有 Rights Management 模板名称和说明的信息横幅。

4.  如果你决定通过使用文件分类基础结构选择性地保护文件，请配置你的分类规则和计划，然后修改文件管理任务以将此分类属性作为条件包括在内。

## <a name="user-documentation-instructions"></a>用户文档说明
如果你通过 Azure Rights Management 保护的文件不需要与组织外的人员进行共享，则除了向用户提供使用工作文件夹的说明，无需再提供任何其他说明。 当用户打开受 Azure Rights Management 保护的文件和默认模板时，文件的打开方式与平常在 Office 中打开一样，唯一区别就是系统可能会提示用户进行身份验证，他们将在文档顶部看到一个信息栏，告诉他们文件内容包含仅供内部用户使用的私有信息。

如果你配置了为此方案记录的自定义模板，用户将在信息栏中看到模板说明：**此内容受工作文件夹保护，且仅限公司员工使用。若要与组织外的人员共享此内容，请将文档附加到电子邮件并使用共享保护项功能。** 虽然此说明提供了如何将文件共享到组织外的摘要，但用户可能需要有关如何完成操作的详细说明，尤其是在他们前几次执行此操作的时候。 要支持此后续方案，请使用[方案 - 与另一组织中的用户共享 Office 文件](scenario-share-office-file-externally.md)中的管理员和最终用户说明。

> [!TIP]
> 如果你因为不想让用户在没有 IT 监督的情况下与组织外的人共享这些文件，而决定不使用这些说明中的自定义模板，请告知技术支持，以便如果共享要求合法时，可以通过使用最合适你业务的机制来适应此要求。 例如，身份为[超级用户](../deploy-use/configure-super-users.md)的某人可以将新模板应用到授予请求用户完全控制权限的内容，以便该用户能够使用共享保护项功能。
> 
> 一段时间后，如果你发现存在许多这样的请求，可能会决定为该方案定义你自己的模板，该模板仅授予特定用户（如管理人员或技术支持）共有者选项，同时授予标准用户合著者或任何你认为合适的[权限](../deploy-use/configure-usage-rights.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]