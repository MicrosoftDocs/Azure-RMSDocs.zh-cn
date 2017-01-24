---
title: "使用 Azure 信息保护时跟踪和撤销已保护的文档 | Azure 信息保护"
description: "保护文档后，可跟踪用户如何使用它们。 如果用户不应再阅读这些文档，还可撤销其对这些文档的访问权限（如有必要）。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 54abc32a6065bb3863cf55b42466250f8fc9c634


---

# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>使用 Azure 信息保护时跟踪和撤销文档

>适用于：Azure 信息保护、Windows 10、Windows 8.1、Windows 8 以及具有 SP1 的 Windows 7

**[此版本的客户端为预览版，随时可能更改。]**

使用 Azure 信息保护来保护你的文档后，可跟踪用户如何使用这些文档。 如果用户不应再阅读这些文档，还可撤销其对这些文档的访问权限（如有必要）。 若要进行此操作，你可以使用**文档跟踪站点**，这些站点可以通过 Windows 计算机、Mac 计算机甚至平板电脑和手机进行访问。

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

访问该站点时，登录即可对文档进行跟踪。 如果你的组织有一个[支持文档跟踪和吊销的订阅](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)，而你已被分配了一个该订阅的许可证，你就可以看到谁曾经尝试打开受保护的文件，以及这些用户是否已成功（即成功完成了身份验证）。 还会看到他们访问文档的每一次尝试，以及访问时所在的位置。 此外：

-   如果你需要停止共享文档：单击“撤消访问” ，请注意文档将继续可用的时间段，并确定是否允许用户知道你撤消了对之前共享的文档的访问权限，然后提供一条自定义消息。 撤消某个文档时，它并不会删除你共享的文档，但获得授权的用户将不再能够打开该文档。

-   如果你想要导出到 Excel：单击“导出到 CSV”，以便你随后修改数据，并创建你自己的视图和图形。

-   如果你想要配置电子邮件通知：单击“设置”  并选择在访问该文档时是否通过电子邮件发送通知以及发送方式。

- 如果想要为其他人跟踪和撤销共享文档：Azure 信息保护管理员可以通过单击“管理员”图标为其他人跟踪和撤销受保护的文档。 只有管理员才能看到该图标。

-   如有疑问或想要提供有关文档跟踪站点的反馈：单击“帮助”图标访问 [文档跟踪常见问题](http://go.microsoft.com/fwlink/?LinkId=523977)。

## <a name="using-office-to-access-the-document-tracking-site"></a>使用 Office 访问文档跟踪站点

-   对于 Office 应用程序（Word、Excel、PowerPoint 和 Outlook）：在“开始”选项卡的“保护”组中，单击“保护” > “跟踪使用情况”。

如果在 Office 应用程序中看不到这些选项，则很可能你的计算机上未安装 Azure 信息保护，必须重新启动 Office 应用程序或重新启动计算机才能完成此安装。 有关如何安装 Azure 信息保护客户端的详细信息，请参阅[下载并安装 Azure 信息保护客户端](install-client-app.md)。


### <a name="other-ways-to-track-and-revoke-your-documents"></a>跟踪和撤消文档的其他方法
除了使用 Office 应用程序在 Windows 计算机上跟踪受保护的文档以外，还可以使用以下替代方法：

-   **使用 Web 浏览器**：此方法适用于所有受支持的设备。

-   **使用文件资源管理器**：此方法适用于 Windows 计算机。

#### <a name="using-a-web-browser-to-access-the-doc-tracking-site"></a>使用 Web 浏览器访问文档跟踪站点

-   使用受支持的浏览器转到 [文档跟踪站点](https://go.microsoft.com/fwlink/?LinkId=529562)。

    支持的浏览器：建议使用最低版本为 10 的 Internet Explorer，但你可以通过以下任一浏览器使用文档跟踪站点：

    -   Internet Explorer：最低版本 10

    -   至少具有 2012 年 6 月 12 日发布的 Internet Explorer 累积安全更新 MS12-037 的 Internet Explorer 9

    -   Mozilla Firefox：最低版本 12

    -   Apple Safari 5：最低版本 5

    -   Google Chrome：最低版本 18

#### <a name="using-file-explorer-to-access-the-doc-tracking-site"></a>使用文件资源管理器访问文档跟踪站点

-   右键单击该文件，选择“分类和保护(预览)”，然后从“Azure信息保护查看器”中选择跟踪使用情况图标。


## <a name="other-instructions"></a>其他说明
有关操作方法的说明，请参阅 Azure 信息保护用户指南中的以下部分：

-   [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


