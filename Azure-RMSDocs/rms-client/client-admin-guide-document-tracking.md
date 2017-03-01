---
title: "Azure 信息保护的文档跟踪"
description: "管理员配置和使用 Azure 信息保护的文档跟踪的说明和信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: aa3b80b7369348f87adc440d6f7a91977aa0fc7c
ms.lasthandoff: 02/24/2017


---


# <a name="configuring-and-using-document-tracking-for-azure-information-protection"></a>配置和使用 Azure 信息保护的文档跟踪

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

如果你有[支持文档跟踪的订阅](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)，则默认情况下，已经为你组织中的所有用户启用了文档跟踪站点。 文档跟踪会显示尝试访问用户共享的受保护文档的人员的电子邮件地址、其尝试访问这些文档的时间以及他们所在的位置。 如果你的组织出于隐私要求而要禁止显示此类信息，你可以使用 [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) cmdlet 来禁用对文档跟踪站点的访问。 你随时可以使用 [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) 来重新启用对该站点的访问，并可以使用 [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) 来查看当前是已启用还是已禁用这种访问。

若要运行这些 cmdlet，必须安装最低版本为 **2.3.0.0**，适用于 Windows PowerShell 的 Azure Rights Management 模块。 有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。

> [!TIP]
> 如果你以前已下载并安装过该模块，请通过运行以下命令检查版本号：`(Get-Module aadrm –ListAvailable).Version`

以下 URL 用于文档跟踪，必须允许使用它们（例如，如果你使用的是具有增强的安全性的 Internet Explorer，则将它们添加到你的受信任站点）：

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > 此 URL 用于 Bing 映射。

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## <a name="tracking-and-revoking-documents-for-users"></a>为用户跟踪和撤销文档

用户登录到文档跟踪站点时，他们可以跟踪和撤销通过使用 Azure 信息保护客户端保护或通过使用 Rights Management 共享应用程序共享的文档。 以 Azure 信息保护管理员（全局管理员）的身份登录时，可以单击“管理员”图标，切换到管理员模式，这样就可以看到组织中的用户已共享的文档：

![文档跟踪站点中的“管理员”图标](../media/tracking-site-admin-icon.png)

在管理员模式下执行的操作会经过审核并记录在使用情况日志文件中，必须确认后才能继续。 有关此日志记录的详细信息，请参阅下一节。

处于管理员模式时，可以按用户或文档进行搜索。 如果按用户搜索，将看到指定用户共享的所有文档。 如果按文档搜索，将看到组织中共享该文档的所有用户。 之后，如有必要，你可以钻取到搜索结果，以便跟踪用户共享的文档以及撤销这些文档。 

若要离开管理员模式，请单击“退出管理员模式”旁边的“X”：

![在文档跟踪站点中退出管理员模式](../media/tracking-site-exit-admin-icon.png)

有关如何使用文档跟踪站点的说明，请参阅用户指南中的[跟踪和撤销文档](client-track-revoke.md)。

## <a name="usage-logging-for-the-document-tracking-site"></a>文档跟踪站点的使用情况日志记录

使用情况日志文件中的以下两个字段适用于文档跟踪：**AdminAction** 和 **ActingAsUser**。

**AdminAction** — 当管理员在管理员模式下使用文档跟踪站点时，例如，代表用户撤销文档或查看其共享时间，此字段的值为 true。 当用户登录到文档跟踪站点时，此字段为空。

**ActingAsUser** — 当 AdminAction 字段为 true 时，此字段包含管理员代表的所搜索的用户或文档所有者的用户名。 当用户登录到文档跟踪站点时，此字段为空。 

此外，还有记录用户和管理员如何使用文档跟踪站点的请求类型。 例如，**RevokeAccess** 是用户或代表用户的管理员已撤销文档跟踪站点中的文档时的请求类型。 通过将此请求类型与 AdminAction 字段结合使用，可确定是用户撤销了自己的文档（AdminAction 字段为空），还是管理员代表用户撤销了文档（AdminAction 为 true）。


有关使用情况日志记录的详细信息，请参阅[记录和分析 Azure 权限管理服务的使用情况](../deploy-use/log-analyze-usage.md)



## <a name="next-steps"></a>后续步骤
现在你配置了 Azure 信息保护客户端的文档跟踪站点，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

