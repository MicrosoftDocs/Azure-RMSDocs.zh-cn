---
# required metadata

title: Rights Management 共享应用程序的对话框选项 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 权限管理共享应用程序的的对话框选项

*适用于：Active Directory Rights Management Services、Azure Rights Management、Windows 10、具有 SP1 的 Windows 7、Windows 8、Windows 8.1*

使用此信息帮助你指定 RMS 共享应用程序“添加保护”  对话框或“共享保护”  对话框中的选项。 当你[保护要共享的文件](sharing-app-protect-by-email.md)或[就地保护文件](sharing-app-protect-in-place.md)以及选择自定义权限时，将看到此对话框。

> [!IMPORTANT]
> 如果你看到的选项与此处记录的不同，可能是没有安装最新版的共享应用程序。 你可以从 [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) 页面下载最新版本。
> 
> 你如何知道是否拥有最新版本？ 查找程序和功能中列出的 **Microsoft Rights Management 共享应用程序** ，查看相应的版本号。 若要查看并使用表中的选项，版本最低应是“1.0.1770.0” 。 你可以从下载页检查最新版本号。

除了可以选择的选项之外，你可能还想知道：

-   [自动创建的 .ppdf 文件是什么文件？](#what-s-the-ppdf-file-that-s-automatically-created-)

-   [一般性保护和内置（本机）保护的区别是什么？](#what-s-the-difference-between-generic-protection-and-built-in-native-protection-)

|选项|说明|
|----------|---------------|
|**用户**|如果你还没有从 Outlook 指定电子邮件地址，请键入你希望能够打开文件的用户的电子邮件地址。<br /><br />请注意，RMS 共享应用并不支持所有电子邮件地址。<br /><br />如果你的组织使用本地版本的 Rights Management (AD RMS)，你可以指定的电子邮件地址仅限于组织中的用户。 如果应用此操作，并且你尝试指定外部电子邮件地址，将看到一则消息，说明你公司的配置仅允许在公司内共享受保护内容。 <br /><br /> 如果你的组织使用 Azure RMS，那么你指定的电子邮件地址可以是组织中用户的电子邮件地址，也可以是其他组织中用户的电子邮件地址。<br /><br />例如：**janetm@contoso.com；p.dover@fabrikam.com**<br /><br />RMS 共享应用当前不支持个人电子邮件地址。|
|**一般性保护**|如果选择此选项，则意味着无法本机保护所选文件。 有关详细信息，请参阅： 本页中的[一般性保护和内置（本机）保护的区别是什么？](#what-s-the-difference-between-generic-protection-and-built-in-native-protection-)。|
|**查看器 – 仅查看**<br /><br />**审阅者 – 查看和编辑**<br /><br />**合著者 – 查看、编辑、复制和打印**<br /><br />**共同所有者 – 所有权限**<br /><br />注意：所有这些选项的名称前都有圆形图标，表示地球仪。 使用此图标的原因是，通常情况下，你在向其他组织的用户发送附件时会选择这些选项之一。|如果你想要定义受保护文档的权限，请选择这些选项之一。 单击每个选项以查看说明。<br /><br />选择这些选项之一时，只有你在“用户”  中指定的用户具有打开和使用文档的指定权限。 例如，将无法打开转发给其他人的文档。|
|你的管理员配置的策略模板。<br /><br />例如，如果公司名称为“Contoso, Ltd”：**“Contoso, Ltd - 机密，仅供查阅”**<br /><br />注意：所有这些选项的名称前都有方形图标，表示办公楼。 使用此图标的原因是，通常情况下，你在向本组织的用户发送附件时会选择这些选项之一。|当与同事共享文档时，你将看到管理员配置的可用策略模板。 如果文档不应该共享到组织外部，请选择这些选项之一。<br /><br />选择这些选项之一时，你的管理员将定义文档权限和可以打开文档的用户。|
|**这些文档的到期日期**|仅为时间敏感的文件选择此选项，在指定日期后，所选用户将不能打开文件。 你仍可以打开原始文件，但在指定日期的午夜（当前时区）过后，其他用户将无法打开该文件。<br /><br />如果你选择管理员配置的策略模板，此选项将不可用。|
|**当有人尝试打开这些文档时，给我送发电子邮件**|注意：此选项当前在预览版中提供。<br /><br />如果你想要在有人试图打开你保护的文档时接收电子邮件通知，请选择此选项。 该电子邮件将显示谁试图打开文档、打开的时间以及是否成功。<br /><br />此选项仅在你的组织使用 Azure RMS 时才可用。 如果你的组织使用本地版本的 Rights Management (AD RMS)，你将不会看到此选项。|
|**允许我立即撤消对这些文档的访问权限**|如果你以后需要使用文档跟踪站点撤销对文档的访问权限，并且撤销需要立即生效，请选择此选项。 但是，设置此选项意味着，如果文档没有撤销，用户在每次访问文档时将始终需要 Internet 连接才能读取该文档。 在有些情况下，用户无法将设备连接到 Internet，并且无法按预期方式读取文档。<br /><br />如果你不选择此选项，仍可以在以后使用文档跟踪站点撤销文档。 但是，因为用户并不始终需要 Internet 连接才能阅读文档，他们只有到下一次使用 Azure RMS 进行身份验证时才会立即明白，文档已撤销，并且可以继续阅读。 默认情况下，可以继续阅读已经撤销的受保护文档的最大天数是 30 天，但是管理员可以将此值更改为小于或大于 30 天。<br /><br />此选项仅在你的组织使用 Azure RMS 时才可用。 如果你的组织使用本地版本的 Rights Management (AD RMS)，你将不会看到此选项。|

## 一般性保护和内置（本机）保护的区别是什么？

-   当你 **以一般方式保护文件**时，未授权用户无法打开文件。 但授权用户打开文件后，他们可以随后将不受保护的文件转发给其他用户，或将其保存在其他用户可以访问的位置。 但是，他们会看到一则消息，告知他们对该文件拥有哪些权限，并要求他们遵守这些权限，但此保护不会强制执行。 此外，以一般方式保护文件时，你可以限制的权限只在授权内。 例如，你无法将内容限制为仅查看或不能打印。

    > [!NOTE]
    > 以一般方式保护的文件始终具有 **.pfile** 文件扩展名。.

-   相比之下，将使用 Rights Management 的**内置（本机）保护**和支持它的应用程序（如 Office 文件）一起使用时，该保护将应用于该文件，即使该文件已经发送给其他用户或保存在其他位置。 并且，保护这些文件时，你可以使用限制性权限（如只读）或编辑（而不是打印或复制）权限。 例如，你可以选择“查看器 - 仅查看” ，使得内容不可编辑、打印或复制。

有关其他技术信息，请参阅 [Rights Management 共享应用程序管理员指南](sharing-app-admin-guide.md)中的[保护级别 – 本机和通用](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)部分.

## 自动创建的 .ppdf 文件是什么文件？

-   当你通过电子邮件共享受保护文件（共享保护）时，RMS 共享应用程序将自动创建 **.ppdf** 版本的 Word、Excel、PowerPoint 或 PDF 文件。 这是仅授权用户可以打开的只读的受保护版本文件，并且它确保收件人可以始终读取附件，即使他们使用缺少在本机上支持管理权限的应用程序的移动设备。 假设这些用户安装了 RMS 共享应用，他们将能够读取附件。

    不像以一般方式保护的文件，在本方案中将强制执行使用限制。 收件人将无法保存此版本的文件，并且如果他们向其他用户转发附件，原始限制将保留在该文档上。 仅授权可以使用受保护文档的用户能够打开它。

    > [!NOTE]
    > 在你共享保护（通过电子邮件共享）时，将自动创建 .ppdf 文件，但就地保护不会创建该文件。

## 示例和其他说明
有关如何使用 Rights Management 共享应用程序以及操作说明的示例，请参阅以下 Rights Management 共享应用程序用户指南部分：

-   [使用 RMS 共享应用程序的示例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [要执行什么操作？](sharing-app-user-guide.md#what-do-you-want-to-do-)

## 另请参阅
[权限管理共享应用程序用户指南](sharing-app-user-guide.md)



<!--HONumber=May16_HO2-->


