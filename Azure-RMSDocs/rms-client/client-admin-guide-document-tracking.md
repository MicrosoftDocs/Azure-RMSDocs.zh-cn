---
title: Azure 信息保护的文档跟踪
description: 管理员配置和使用 Azure 信息保护的文档跟踪的说明和信息。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.subservice: doctrack
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0f521630953971971cf650c69d80165f260c18be
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75743849"
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>管理员指南：配置和使用 Azure 信息保护的文档跟踪

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、windows 8、带 SP1 的 windows 7、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *适用于[Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*


如果你有[支持文档跟踪的订阅](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)，则默认情况下，已经为你组织中的所有用户启用了文档跟踪站点。 文档跟踪为用户和管理员提供有关受保护文档访问时间的信息，如有必要，可以撤销已跟踪的文档。

## <a name="using-powershell-to-manage-the-document-tracking-site"></a>使用 PowerShell 管理文档跟踪站点

以下各节包含有关如何使用 PowerShell 管理文档跟踪站点的信息。 有关 PowerShell 模块的安装说明，请参阅[安装 AIPService PowerShell 模块](../install-powershell.md)。

有关每个 cmdlet 的详细信息，请使用提供的链接。

### <a name="privacy-controls-for-your-document-tracking-site"></a>文档跟踪站点的隐私控制

如果在你的组织中由于隐私要求而禁止显示所有文档跟踪信息，你可以使用[AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) cmdlet 禁用文档跟踪。 

此 cmdlet 禁用对文档跟踪站点的访问，以使组织中的所有用户无法跟踪或撤销对已保护文档的访问权限。 你随时可以使用 [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature) 来重新启用文档跟踪，并可以使用 [Get-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature) 来查看当前是已启用还是已禁用文档跟踪。 

启用文档跟踪站点后，它会默认显示尝试访问受保护文档的人员的电子邮件地址、这些人员尝试访问这些文档的时间以及他们所在的位置等信息。 这个级别的信息有助于确定使用共享文档的方式，以及在发现可疑活动时，是否应撤销这些文档。 但是，出于隐私原因，你可能需要为部分或所有用户禁用此用户信息。 

如果你有不应由其他用户跟踪此活动的用户，请将其添加到存储在 Azure AD 中的组，并使用[AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Set-AipServiceDoNotTrackUserGroup) cmdlet 指定此组。 运行此 cmdlet 时，必须指定单个组。 不过，该组可以包含嵌套组。 

对于这些组成员，当相应活动与这些组成员与用户共享的文档相关时，用户在文档跟踪站点上看不到任何活动。 另外，不会向共享文档的用户发送电子邮件通知。

使用此配置时，所有用户仍可以使用文档跟踪站点，以及撤销对已保护文档的访问权限。 但是，他们看不到使用 AipServiceDoNotTrackUserGroup cmdlet 指定的用户的活动。

此设置仅会影响最终用户。 Azure 信息保护的管理员可以始终跟踪所有用户的活动，即使这些用户是使用 AipServiceDoNotTrackUserGroup 指定的。 有关管理员如何跟踪用户文档的详细信息，请参阅[跟踪和撤销用户文档](#tracking-and-revoking-documents-for-users)部分。


### <a name="logging-information-from-the-document-tracking-site"></a>文档跟踪站点中的日志记录信息

你可以使用以下 cmdlet 从文档跟踪站点下载日志记录信息：

- [Get-AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)
    
    此 cmdlet 向指定用户返回有关受保护文档的跟踪信息，该用户为文档提供保护（Rights Management 颁发者）或已访问受保护的文档。 使用此 cmdlet 来帮助回答问题“指定用户跟踪或访问了哪些受保护的文档？”

- [Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)
    
    如果用户为文档提供保护（Rights Management 颁发者）或者是文档的 Rights Management 所有者，或者受保护的文档被配置为直接授予该用户访问权限，那么此 cmdlet 会对该指定用户返回有关跟踪文档的保护信息。 使用此 cmdlet 来帮助回答问题“如何保护指定用户的文档？”

## <a name="destination-urls-used-by-the-document-tracking-site"></a>文档跟踪站点使用的目标 URL

以下 Url 用于文档跟踪，必须在运行 Azure 信息保护客户端和 internet 的客户端之间的所有设备和服务上允许。 例如，如果你使用的是具有增强安全性的 Internet Explorer，请将这些 URL 添加到防火墙，或添加到受信任的站点。

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

这些 URL 是 Azure 权限管理服务的标准，但用于必应地图以显示用户位置的 virtualearth.net URL 除外。

## <a name="tracking-and-revoking-documents-for-users"></a>为用户跟踪和撤销文档

用户登录到文档跟踪站点时，他们可以通过使用 Azure 信息保护客户端跟踪和撤销保护的文档。 以租户的 Azure AD 全局管理员身份登录时，可以单击“管理员”图标，以切换到管理员模式。 其他管理员角色不支持对文档跟踪网站使用此模式。 

![文档跟踪站点中的“管理员”图标](../media/tracking-site-admin-icon.png)

通过管理员模式，可以查看组织用户选择通过 Azure 信息保护客户端进行跟踪的文档。

> [!NOTE] 
> 如果是全局管理员，但仍看不到此图标，原因是尚未自行分享任何文档。 在这种情况下，请使用以下 URL 访问文档跟踪站点： https://portal.azurerms.com/#/admin

在管理员模式下执行的操作会经过审核并记录在使用情况日志文件中，必须确认后才能继续。 有关此日志记录的详细信息，请参阅下一节。

处于管理员模式时，可以按用户或文档进行搜索。 如果按用户进行搜索，可以查看指定用户通过 Azure 信息保护客户端选择进行跟踪的所有文档。 

如果按文档进行搜索，可以查看组织中通过 Azure 信息保护客户端跟踪该文档的所有用户。 之后，如有必要，你可以钻取到搜索结果，以便跟踪用户保护的文档以及撤销这些文档。 

若要离开管理员模式，请单击“退出管理员模式”旁边的“X”：

![在文档跟踪站点中退出管理员模式](../media/tracking-site-exit-admin-icon.png)

有关如何使用文档跟踪站点的说明，请参阅用户指南中的[跟踪和撤销文档](client-track-revoke.md)。

### <a name="using-powershell-to-register-labeled-documents-with-the-document-tracking-site"></a>使用 PowerShell 向文档跟踪站点注册标记的文档

若要跟踪和撤销文档，必须首先在文档跟踪站点中进行注册。 当用户在使用 Azure 信息保护客户端时从文件资源管理器或其 Office 应用中选择“跟踪和撤销”选项时，将执行此操作。

如果使用 [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) cmdlet 为用户标记和保护文件，可以使用 EnableTracking 参数将文件注册到文档跟踪站点。 例如：

    Set-AIPFileLabel -Path C:\Projects\ -LabelId ade72bf1-4714-4714-4714-a325f824c55a -EnableTracking

## <a name="usage-logging-for-the-document-tracking-site"></a>文档跟踪站点的使用情况日志记录

使用情况日志文件中的以下两个字段适用于文档跟踪：**AdminAction** 和 **ActingAsUser**。

**AdminAction** — 当管理员在管理员模式下使用文档跟踪站点时，例如，代表用户撤销文档或查看其共享时间，此字段的值为 true。 当用户登录到文档跟踪站点时，此字段为空。

**ActingAsUser** — 当 AdminAction 字段为 true 时，此字段包含管理员代表的所搜索的用户或文档所有者的用户名。 当用户登录到文档跟踪站点时，此字段为空。 

此外，还有记录用户和管理员如何使用文档跟踪站点的请求类型。 例如，**RevokeAccess** 是用户或代表用户的管理员已撤销文档跟踪站点中的文档时的请求类型。 通过将此请求类型与 AdminAction 字段结合使用，可确定是用户撤销了自己的文档（AdminAction 字段为空），还是管理员代表用户撤销了文档（AdminAction 为 true）。

有关使用日志记录的详细信息，请参阅[记录和分析 Azure 信息保护中的保护使用情况](../log-analyze-usage.md)

## <a name="next-steps"></a>后续步骤
现在你配置了 Azure 信息保护客户端的文档跟踪站点，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

