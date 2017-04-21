---
title: "跟踪和撤销文档 - Azure 信息保护"
description: "保护文档后，可跟踪用户如何使用它们。 如果用户不应再阅读这些文档，还可撤销其对这些文档的访问权限（如有必要）。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b95b699b63e6a30cdec0af11670a973eb24323dc
ms.sourcegitcommit: 7b773ca5bf1abf30e527c34717ecb2dc96f88033
translationtype: HT
---
# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>使用 Azure 信息保护时跟踪和撤销文档

>适用于：Azure 信息保护、Windows 10、Windows 8.1、Windows 8 以及具有 SP1 的 Windows 7

使用 Azure 信息保护来保护你的文档后，可跟踪用户如何使用这些文档。 如果用户不应再阅读这些文档，还可撤销其对这些文档的访问权限（如有必要）。 若要进行此操作，你可以使用**文档跟踪站点**，这些站点可以通过 Windows 计算机、Mac 计算机甚至平板电脑和手机进行访问。

访问该站点时，登录即可对文档进行跟踪。 如果你的组织有一个[支持文档跟踪和吊销的订阅](https://www.microsoft.com/cloud-platform/azure-information-protection-features)，而你已被分配了一个该订阅的许可证，你就可以看到谁曾经尝试打开受保护的文件，以及这些用户是否已成功（即成功完成了身份验证）。 还会看到他们访问文档的每一次尝试，以及访问时所在的位置。 此外：

-   如果你需要停止共享文档：单击“撤消访问” ，请注意文档将继续可用的时间段，并确定是否允许用户知道你撤消了对之前共享的文档的访问权限，然后提供一条自定义消息。 撤销某个文档时，它并不会删除你共享的文档，但获得授权的用户将不再能够打开该文档：
    
    ![撤销文档跟踪站点中的访问图标](../media/tracking-site-revoke-access-icon.png)

-   如果想要导出到 Excel：单击“导出到 CSV”，以便随后修改数据，并创建自己的视图和图形：
    
    ![导出到文档跟踪站点中的 CSV 图标](../media/tracking-site-export-icon.png)

-   如果想要配置电子邮件通知：单击“设置”并选择在访问该文档时是否通过电子邮件发送通知以及发送方式：
    
    ![导出到文档跟踪站点中的 CSV 图标](../media/tracking-site-settings-email.png)

- 如果想要为其他人跟踪和撤销共享文档：Azure 信息保护管理员可以通过单击“管理员”图标为其他人跟踪和撤销受保护的文档。 只有管理员才能看到该图标：
    
    ![文档跟踪站点中的“管理员”图标](../media/tracking-site-admin-icon.png)

若要跟踪受保护的文档，必须在文档跟踪站点中注册此文档。 为此，请使用文件资源管理器或 Office 应用程序。

## <a name="using-office-to-track-or-revoke-the-document"></a>使用 Office 跟踪或撤销文档

对于 Office 应用程序（Word、Excel、PowerPoint 和 Outlook）： 

1. 打开要跟踪或撤销的受保护文档。

2. 在“**开始**”选项卡上的“**保护**”组中，依次单击“**保护**” > “**跟踪和撤销**”：

    ![跟踪使用情况选项](../media/track-usage-callout.png)

如果在 Office 应用程序中看不到这些选项，则很可能你的计算机上未安装 Azure 信息保护，必须重新启动 Office 应用程序或重新启动计算机才能完成此安装。 有关如何安装 Azure 信息保护客户端的详细信息，请参阅[下载并安装 Azure 信息保护客户端](install-client-app.md)。

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>使用文件资源管理器跟踪或撤销文档

1. 右键单击受保护的文件，然后选择“分类和保护”。

2. 从“分类和保护 - Azure 信息保护”对话框中，选择“跟踪和撤销”。

    ![从“分类和保护 - Azure 信息保护”对话框中跟踪和撤销图标](../media/track-and-revoke.png)


### <a name="using-a-web-browser-track-and-revoke-documents-that-you-have-registered"></a>使用 Web 浏览器跟踪和撤销已注册的文档

使用 Office 应用程序或文件资源管理器注册受保护的文档后，可以使用支持的 Web 浏览器跟踪和撤销这些文档：

- 使用 Windows 电脑、Mac 计算机或移动设备，访问[文档跟踪站点](https://go.microsoft.com/fwlink/?LinkId=529562)。

    **支持的浏览器**：建议使用最低版本为 10 的 Internet Explorer，但你可以通过以下任一浏览器使用文档跟踪站点：

    -   Internet Explorer：最低版本 10

    -   至少具有 2012 年 6 月 12 日发布的 Internet Explorer 累积安全更新 MS12-037 的 Internet Explorer 9

    -   Mozilla Firefox：最低版本 12

    -   Apple Safari 5：最低版本 5

    -   Google Chrome：最低版本 18


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]