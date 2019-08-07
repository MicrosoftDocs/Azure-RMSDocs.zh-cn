---
title: 跟踪和撤销文档 - Azure 信息保护
description: 保护文档后，可跟踪用户如何使用它们。 如果用户不应再阅读这些文档，还可撤销其对这些文档的访问权限（如有必要）。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 4c95177d767d6047071b4f9c578de4d374e28bfe
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793489"
---
# <a name="user-guide-track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>用户指南：使用 Azure 信息保护时跟踪和撤销文档

>适用范围： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）*
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

使用 Azure 信息保护来保护你的文档后，可跟踪用户如何使用这些文档。 如果用户不应再阅读这些文档，还可撤销其对这些文档的访问权限（如有必要）。 若要执行此操作，请使用“文档跟踪站点”。 可以通过 Windows 计算机、Mac 计算机甚至平板电脑和手机访问此站点。

访问该站点时，登录即可对文档进行跟踪。 如果你的组织有一个[支持文档跟踪和吊销的订阅](https://www.microsoft.com/cloud-platform/azure-information-protection-features)，而你已被分配了一个该订阅的许可证，你就可以看到谁曾经尝试打开受保护的文件，以及这些用户是否已成功（即成功完成了身份验证）。 还会看到他们访问文档的每一次尝试，以及访问时所在的位置。 但是，在极少数情况下，报告的位置可能不准确。 例如，当用户使用 VPN 连接打开受保护的文档时，或当其计算机具有 IPv6 地址时。

可在文档跟踪站点中执行的操作是：

- 如果你需要停止共享文档： 
    
    - 单击“撤销访问权限”。 请注意文档持续可用的时间段。 决定是否通过提供自定义消息让用户知道你正在撤销对之前共享的文档的访问权限。 撤销某个文档时，它并不会删除你共享的文档，但获得授权的用户无法再打开该文档：
        
        ![撤销文档跟踪站点中的访问图标](../media/tracking-site-revoke-access-icon.png)
        
- 如果你想要导出到 Excel： 
    
    - 单击“导出到 CSV”，方便随后修改数据，并创建你自己的视图和图形：
         
        ![导出到文档跟踪站点中的 CSV 图标](../media/tracking-site-export-icon.png)
         
- 如果你想要配置电子邮件通知： 
     
    - 单击“设置”并选择在访问该文档时是否通过电子邮件发送通知以及发送方式：
        
        ![在文档跟踪站点中配置电子邮件通知](../media/tracking-site-settings-email.png)

- 如果想要为其他人跟踪和撤销共享文档：
    
    - Azure 信息保护管理员可以单击管理员图标，在用户通过文档跟踪站点注册文档后，跟踪和撤销这些用户的受保护文档。 只有管理员才能看到该图标：
        
        ![文档跟踪站点中的“管理员”图标](../media/tracking-site-admin-icon.png)
        
        如果是全局管理员，但看不到此图标，则是因为你尚未分享任何文档。 在这种情况下，请使用以下 URL 访问文档跟踪站点： https://portal.azurerms.com/#/admin

除非你是管理员，否则只能跟踪和撤销你所保护的文档。 你无法通过使用文档跟踪站点来跟踪受保护的电子邮件。

> [!NOTE] 
> 如果管理员已为文档跟踪站点配置了隐私控制，你可能无法看到组织中的用户访问你所跟踪的文档的时间。管理员可以豁免所有用户或仅豁免某些用户。 但是，你始终可以撤销对你所跟踪文档的访问权限。

要跟踪已保护的文档，必须使用 Windows 计算机将其注册到文档跟踪站点。 为此，请使用文件资源管理器或 Office 应用程序。

如果具有 Azure 信息保护客户端的当前通用版本, 则在将*bre-walkthrough-enabletracking*参数与[set-aipfilelabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) cmdlet 结合使用时, 还可以使用 PowerShell 注册受保护的文档。

## <a name="using-office-to-track-or-revoke-the-document"></a>使用 Office 跟踪或撤销文档

对于 Office 应用程序（Word、Excel 和 PowerPoint）： 

1. 打开要跟踪或撤销的受保护文档。

2. 在“**开始**”选项卡上的“**保护**”组中，依次单击“**保护**” > “**跟踪和撤销**”：

    ![跟踪使用情况选项](../media/track-usage-callout.png)
    
    如果在 Office 应用程序中看不到这些选项，可能是由于以下原因之一：
    
    - 计算机上未安装 Azure 信息保护客户端。
    
    - 必须重新启动 Office 应用程序。
    
    - 必须重新启动计算机才能完成安装。
    
有关如何安装 Azure 信息保护客户端的详细信息，请参阅[下载并安装 Azure 信息保护客户端](install-client-app.md)。

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>使用文件资源管理器跟踪或撤销文档

1. 右键单击受保护的文件，然后选择“分类和保护”。

2. 从“分类和保护 - Azure 信息保护”对话框中，选择“跟踪和撤销”。

    ![从“分类和保护 - Azure 信息保护”对话框中跟踪和撤销图标](../media/track-and-revoke.png)


### <a name="using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered"></a>使用 Web 浏览器跟踪和撤销已注册的文档

使用 Office 应用程序或文件资源管理器注册受保护的文档后，可以使用支持的 Web 浏览器跟踪和撤销这些文档：

- 使用 Windows 电脑、Mac 计算机或移动设备，访问[文档跟踪站点](https://go.microsoft.com/fwlink/?LinkId=529562)。

    **支持的浏览器**：建议使用最低版本为10的 Internet Explorer, 但你可以使用以下任一浏览器来使用文档跟踪站点:

    - Internet Explorer:至少版本10

    - 包含至少 MS12 的 Internet Explorer 9-037:Internet Explorer 的累积安全更新:2012年6月12日

    - Mozilla Firefox:最低版本12

    - Apple Safari 5:最低版本5

    - Google Chrome:最低版本18


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅[管理员指南](client-admin-guide.md)中的[配置和使用 Azure 信息保护的文档跟踪](client-admin-guide-document-tracking.md)。
