---
# required metadata

title: 管理员和用户将看到什么？ | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 013e0eb4-49a7-4e81-9e4d-f56c0ceb017f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# 运行中的 Azure RMS：管理员和用户看到的内容
文章显示管理员和用户如何查看并使用 Azure Rights Management (Azure RMS) 来帮助保护敏感或机密信息的一些典型示例。

> [!NOTE]
> 在 Azure RMS 保护数据的所有这些示例中，内容所有者继续对数据（文件或电子邮件）具有完全访问权限，即使应用的保护向所有者不属于的组授予权限，或者即使应用的保护带有到期日期。
> 
> 同样，IT 部门始终可以通过使用 Rights Management 的超级用户功能（向你指定的授权用户或服务授予委托访问权限）来访问受保护的数据而没有限制。 此外，IT 部门还可以跟踪和监视受保护数据的使用情况（例如，谁正在访问该数据和访问时间）。

有关显示运行中的 RMS 的其他屏幕截图和视频，请查看 [Microsoft Rights Management 服务门户](http://www.microsoft.com/rms)和 [Microsoft Rights Management (RMS) 团队博客](http://blogs.technet.com/b/rms)。

## 激活和配置权限管理
尽管可以使用 Windows PowerShell 激活和配置 Azure RMS，但在管理门户中执行这些操作最简单。 激活该服务后，你立即获得两个默认模板，管理员和用户可以选择这两个模板来便捷地对文件应用信息保护。 但你也可以创建自己的自定义模板来提供其他选项和设置。

![](../media/AzRMS_StoryboardActivate_small1.png)


**管理员将在步骤 1 中看到：**可以使用 Office 365 管理中心（第一个图）或 Azure 经典门户（第二个图）来激活 RMS。<br /><br />只需单击一下激活，再单击一下确认，然后即可为你组织中的管理员和用户启用信息保护。

---

![](../media/AzRMS_TemplatesPortal_small.png)

**管理员将在步骤 2 中看到：**激活后，两个权限策略模板将自动可供你的组织使用。 一个模板用于只读访问（名称中包含“机密仅供查阅”****），另一个模板用于读取和修改访问（名称中包含“机密”****）。

将这两个模板应用于文件或电子邮件时，它们会限制你组织中用户的访问权限。 这是一个非常便捷的方法可帮助防止将你公司的数据泄露给组织外部人员。

> [!TIP]
> 你可以轻松识别这些默认模板，因为它们自动使用组织名称作为前缀。 在我们的示例中，**VanArsdel, Ltd**

如果你不希望用户看到这些模板，或者如果你要创建自己的模板，可以在 Azure 经典门户中执行此操作。 如此图所示，向导将指导你完成自定义模板创建过程。

---

![](../media/AzRMS_TemplatesSettings3.png)

**管理员将在步骤 3 中看到：**如果你决定创建自己的模板，则可以使用脱机访问、过期设置以及是否立即发布模板（使其在支持权限管理的应用程序中可见）等一些配置设置。

---

![](../media/AzRMS_TemplatesPortal_ExplorerWord3.png)

**用户将在步骤 4 中看到：**由于已发布这些模板，用户现在可以在文件资源管理器和 Microsoft Word 等应用程序中选择它们：

- 用户可以选择默认模板 **VanArsdel, Ltd - 机密**。 于是，只有 VanArsdel 组织的员工可以打开并使用该文档，即使后来将该文档通过电子邮件发送给组织外部的人员或保存到公共位置，也是如此。

- 用户可以选择管理员创建的自定义模板“销售和营销 - 仅供阅读和打印”****。 于是，不仅保护此文件不让组织外部的人员访问，而且还将此文件限制为只有“销售”和“营销”部门的员工才能访问。 而且，这些员工对该文档不具有完全权限，只能阅读和打印。 例如，他们不能对该文档进行修改，也不能从中复制。

---

**有关此方案的详细信息：**

- 有关分步说明，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md) 和[为 Azure Rights Management 配置自定义模板](../deploy-use/configure-custom-templates.md)。

- 若要帮助用户保护重要的公司文件，请参阅[通过使用 Azure Rights Management 帮助用户保护文件](../deploy-use/help-users.md)。

接下来，请参阅管理员如何应用模板以自动为文件和电子邮件配置信息保护的一些示例。

## 自动在运行 Windows Server 和文件分类基础结构的文件服务器上保护文件

此示例演示如何使用 Azure RMS 自动在至少运行 Windows Server 2012 且配置为使用文件分类基础结构的文件服务器上保护文件。

有多种方法可将分类值应用于文件。 例如，你可以检查文件的内容，并相应地应用内置分类（如机密性和个人身份信息）。 但是，在此示例中，管理员将创建自定义分类“营销”****，该分类将自动应用于“市场促销”****文件夹中保存的所有用户文档。 尽管此文件夹已使用 NTFS 权限进行保护以限制为只有营销组的成员才能访问，但管理员知道，如果该组中有人移动文件或通过电子邮件发送文件，则这些权限会丢失。 于是，未经授权的用户将可以访问这些文件中的信息。

![](../media/AzRMS_FCI_ConnectorSmall.png)

**管理员将在步骤 1 中看到：**管理员安装并配置权限管理 (RMS) 连接器，该连接器充当本地服务器与 Azure RMS 之间的中继。

---

![](../media/AzRMS_ExampleFCI_ConfigurationSmall.png)

**管理员将在步骤 2 中看到：**在文件服务器上，管理员配置分类规则和任务，以使“市场促销”****文件夹中的所有用户文件自动归类为“营销”****并使用 RMS 加密进行保护。

她选择我们在第一个示例中创建的自定义 RMS 模板（限制为只有“销售”和“营销”部门的成员才能访问）： **销售和营销 - 仅供阅读和打印**。

因此，该文件夹中的所有文档将自动配置有“营销”分类并受“销售和营销”RMS 模板保护。

---

![](../media/AzRMS_FCI_EmailSmall.png)

**用户将在步骤 3 中看到：**RMS 如何帮助防止将数据泄露给不应有权访问敏感或机密信息的人：

- 营销部的 Janet 通过电子邮件发送了“市场促销”文件夹中的机密报告。 此报告包含新产品功能和广告计划，是出差的同事请求发送的。 但是，Janet 错误地将电子邮件发送给了错误的人 - 她没有注意到她意外地选择了另一家公司中具有类似名称的收件人。<br><br>
该收件人无法阅读此机密报告，因为他不是“销售”和“营销”组的成员。

---

**有关此方案的详细信息：**

- 有关分步说明，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

## 使用 Exchange Online 和数据丢失预防策略自动保护电子邮件

前一示例显示了如何自动保护包含敏感或机密信息的文件，但如果信息不在文件中而在电子邮件中，该怎么办？ 这就是 Exchange Online 数据丢失防护 (DLP) 策略派上用场的地方，它会提示用户（通过使用策略提示）应用信息保护或自动为用户应用信息保护（通过使用传输规则）。

在此示例中，管理员将配置一个策略，以确保组织符合保护个人身份信息数据的美国法规要求，但也可以为其他合规性要求或你定义的自定义规则配置规则。

![](../media/AzRMS_DLPExample1.png)

**管理员将在步骤 1 中看到：**在 Exchange 管理中心，名为“美国个人身份信息 (PII) 数据”****的 Exchange 模板由管理员使用来创建和配置新的 DLP 策略。 此模板在电子邮件中查找身份证号和驾驶证号等信息。

已配置规则，以便对包含这些信息并发送到组织外部的电子邮件自动使用 RMS 模板应用权限保护以限制为只有公司员工才能访问这些邮件。

此处将规则配置为使用其中一个默认模板，即我们的第一个示例中的“VanArsdel, Ltd - 机密” ****。 但你还可以看到模板选项如何包括你已创建的任何自定义模板以及特定于 Exchange 的“不要转发”选项 **** 。

---

![](../media/AzRMS_DLPUnprotectedEmail_small.png)

**用户将在步骤 2 中看到：**招聘经理撰写的电子邮件包含最近雇用的员工的身份证号。 他将此电子邮件发送给人力资源部的 Sherrie。

---

![](../media/AzRMS_DLPProtectedEmail_small.png)

**用户将在步骤 3 中看到：**如果将此电子邮件发送或转发给组织外部的某人，DLP 规则将自动应用权限保护。

电子邮件离开组织的基础结构时将进行加密，这样，此电子邮件在传输过程中或在收件人的收件箱中时，将无法读取其中的身份证号。 除非收件人是 VanArsdel 员工，否则将无法读取此邮件。

---

**有关此方案的详细信息：**

-   有关如何配合 Exchange Online 使用 Azure RMS 的详细信息，请参阅[应用程序如何支持 Azure Rights Management](applications-support.md) 中的 [Exchange Online 和 Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) 部分。

-   有关为 Azure RMS 配置 Exchange Online 的分步说明，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)中的 [Exchange Online：IRM 配置](../deploy-use/configure-office365.md#exchange-online-irm-configuration)。

## 使用 SharePoint Online 和受保护的库自动保护文件

这将显示如何使用 SharePoint Online 和受保护的库轻松保护文档。

在此示例中，Contoso 的 SharePoint 管理员为每个部门创建了一个库，各部门的人员可以使用该库集中存储和签出文档进行编辑和版本控制。 例如，有一个库用于销售，一个库用于营销，一个库用于人力资源，等等。 当新文档上载或创建到其中一个受保护的库中时，该文档将继承库的保护（无需选择权限策略模板）并自动进行保护，即使该文档移到了 SharePoint 库外，也仍然受到保护。

![](../media/AzRMS_StoryboardSPO_small1.png)

**管理员将在步骤 1 中看到：**管理员为 SharePoint 站点启用信息权限管理。

---

![](../media/AzRMS_StoryboardSPO_small2.png)

**管理员将在步骤 2 中看到：**然后，她将为库启用权限管理。 虽然有其他选项，但这个简单设置通常涵盖了所有所需内容。

现在通过此库下载文档时，这些文档会自动受 Rights Management 的保护，继承针对此库所配置的保护。

---

![](../media/AzRMS_StoryboardSPO_small3.png)

**用户将在步骤 3 中看到：**当销售部的人员从库中签出此销售报表时，他们可以从顶部的信息横幅中清楚地看出这是限制访问权限的受保护文档。

即使用户将此文档重命名、保存到其他位置或通过电子邮件共享，此文档也仍然受到保护。 无论将此文件命名为什么名称、存储在什么位置，或是否通过电子邮件共享，都只有销售部的成员才能阅读它。

---

**有关此方案的详细信息：**

-   有关 Azure RMS 如何适用于 SharePoint 的详细信息，请参阅[应用程序如何支持 Azure Rights Management](applications-support.md) 中的 [SharePoint Online 和 SharePoint Server](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) 部分。

-   有关为 Azure RMS 配置 SharePoint 的分步说明，请参阅[为 Azure Rights Management 配置应用程序](../deploy-use/configure-applications.md)中的 [SharePoint Online 和 OneDrive for Business：IRM 配置](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)部分。

## 用户安全地与移动用户共享附件

前面的示例显示了管理员如何自动将信息保护应用于敏感数据和机密数据。 但在某些情况下，用户可能需要自己应用此保护。 例如，他们正在与另一组织中的合作伙伴协作，他们或许在前面的示例未涉及的临时情况下，需要自定义模板中未定义的权限或设置。 在这些情况下，用户可以自己应用 RMS 模板，或配置自定义权限。

此示例显示用户如何可以轻松地与另一家公司中的合作人员共享文档，但仍能保护该文档，并确信收件人可以阅读该文档，即使在主流移动设备中阅读也是如此。 此方案使用权限管理共享应用程序，你可以将其自动部署到组织中的 Windows 计算机上。 或者，用户可以自己安装它。

在此示例中，Contoso 的 Alice 通过电子邮件将一个机密的 Word 文档发送给了 Fabrikam 的 Bob。 Bob 在其 iPad 上阅读该文档，但他也能在 iPhone、Android 平板电脑或手机、Mac 计算机、Windows phone 或计算机上轻松地阅读该文档。

![](../media/AzRMS_StoryboardEmail_small1.png)

**用户将在步骤 1 中看到：**Alice 在其 Windows 电脑上创建了一封标准的电子邮件，并附加了文档。

她在功能区中单击“共享保护”****，此操作将从 RMS 共享应用程序中加载“共享保护”****对话框。

Alice 想要将 Bob 限制为只能查看和编辑该文档，而不想让他复制或打印该文档，因此她选择了 **“审阅者 - 查看和编辑”**。 她还希望当有人尝试打开该文档时向她发送电子邮件，如有必要，她可以吊销该文档，并且她知道吊销将立即生效。

---

![](../media/AzRMS_StoryboardEmail_small2.png)

**用户将在步骤 2 中看到：**Bob 在他的 iPad 上查看电子邮件。

除了 Alice 的邮件和附件外，还有他可以按照其在 iPad 上注册并安装 RMS 共享应用程序的说明。

---

![](../media/AzRMS_StoryboardEmail_small3.png)

**用户将在步骤 3 中看到：**现在，Bob 可以打开该附件。 首先，要求他登录以确认他是预期的收件人。

当 Bob 查看该文档时，他还看到了受限制的访问权限信息，告诉他可以查看和编辑该文档，但不能复制或打印。

---

![](../media/AzRMS_StoryboardEmail_small4.png)

**用户将在步骤 4 中看到：**Alice 收到了电子邮件，告诉她 Bob 已成功打开她发送的文档，以及他访问该文档的时间。

如果 Bob 转发带有该附件的电子邮件，或将其保存到其他人可以访问的位置，或在网络上截获该电子邮件，其他人将无法阅读该文档。

---

**有关此方案的详细信息：**

- 有关分步说明，请参阅 [Rights Management 共享应用程序用户指南](../rms-client/sharing-app-user-guide.md)中的[保护通过电子邮件共享的文件](../rms-client/sharing-app-protect-by-email.md)和[查看和使用已保护的文件](../rms-client/sharing-app-view-use-files.md)。

- [Azure Rights Management 快速入门教程](../get-started/quick-start-tutorial.md) 包含此方案的分步说明。

## 后续步骤

现在，你已看到 Azure RMS 可以执行哪些操作的一些示例，你可能会对其如何执行这些操作感兴趣。 有关 Azure RMS 的工作原理的技术信息，请参阅[ Azure RMS 的工作原理](how-does-it-work.md)

<!--HONumber=Apr16_HO3-->


