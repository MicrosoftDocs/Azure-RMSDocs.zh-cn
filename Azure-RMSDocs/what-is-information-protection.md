---
title: 什么是 Azure 信息保护 (AIP)？
description: Azure 信息保护 (AIP) 扩展了 Microsoft 信息保护 (MIP) 框架，以扩展 Microsoft 365 提供的标记和分类功能。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to extend Microsoft 365's labeling and classification functionality to the File Explorer, PowerShell, third party apps and services, and more.
ms.custom: contperfq1
search.appverid:
- MET150
ms.openlocfilehash: 5167d790c557661181b03f90055dfc75b0b1cf72
ms.sourcegitcommit: 1086cf04a29bb12cdb25c1fd8429f93d423bcc69
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2020
ms.locfileid: "94379236"
---
# <a name="what-is-azure-information-protection"></a>什么是 Azure 信息保护？

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

Azure 信息保护 (AIP) 是一种基于云的解决方案，可帮助组织通过将标签应用到内容来对文档和电子邮件进行发现、分类和保护。

AIP 是 Microsoft 信息保护 (MIP) 解决方案的一部分，它扩展了 Microsoft 365 提供的标记和分类功能。

下图显示了对 MIP 的 Azure 信息保护新增功能，包括[统一标记客户端](#aip-unified-labeling-client)、[扫描程序](#aip-on-premises-scanner)和 [SDK](#microsoft-information-protection-sdk)。

:::image type="content" source="media/what-is-mip.png" alt-text="Microsoft 信息保护框架的 Azure 信息保护区域":::

Microsoft 信息保护是 AIP 的统一标记客户端利用的通用信息保护堆栈。 有关详细信息，请参阅 [Microsoft 365 文档](/microsoft-365/compliance/protect-information)。

## <a name="aip-unified-labeling-client"></a>AIP 统一标记客户端

Azure 信息保护统一标记客户端将标记、分类和保护功能扩展到其他文件类型，如文件资源管理器和 PowerShell。 

例如，在文件资源管理器中，右键单击一个或多个文件，然后选择“分类和保护”以管理所选文件上的 AIP 功能。

:::image type="content" source="media/protect-from-file-explorer.png" alt-text="文件资源管理器的分类和保护":::

有关统一标记客户端的最新功能和公共预览版本的详细信息，请参阅 [Azure 信息保护统一标记客户端 - 版本发布历史记录和支持策略](rms-client/unifiedlabelingclient-version-release-history.md)。

从 [Microsoft Azure 信息保护下载页](https://www.microsoft.com/download/details.aspx?id=53018)下载客户端。
    
## <a name="aip-on-premises-scanner"></a>AIP 本地扫描程序

Azure 信息保护本地扫描程序使管理员能够扫描其网络和文件共享，以获取必须标记、分类和/或受保护的敏感内容。

使用作为统一标记客户端的一部分提供的 PowerShell cmdlet 安装本地扫描程序，并且可以使用 PowerShell 和 Azure 门户中的 Azure 信息保护区域进行管理。

例如，使用 Azure 门户上显示的扫描程序数据，查找网络上可能有存在风险的敏感内容的存储库：

:::image type="content" source="media/risky-repos-small.png" alt-text="检查已扫描的网络中是否有存在风险的存储库" lightbox="media/risky-repos.png":::

有关详情，请参阅：

- [什么是 AIP 统一标记扫描程序？](deploy-aip-scanner.md)
- [AIP 统一标记客户端 - 版本发布历史记录的](rms-client/unifiedlabelingclient-version-release-history.md)扫描程序部分

从 [Microsoft Azure 信息保护下载页面](https://www.microsoft.com/download/details.aspx?id=53018)下载扫描程序安装和客户端。


## <a name="microsoft-information-protection-sdk"></a>Microsoft 信息保护 SDK

Microsoft 信息保护 SDK 将敏感度标签扩展到第三方应用和服务。 开发人员可以使用 SDK 生成本机支持，以便为文件应用标签和保护。

例如，可以使用 MIP SDK：

- 向正在导出的文件应用分类标签的业务线应用程序。
- CAD/CAM 设计应用程序为 Microsoft 信息保护标记提供本机支持。
- 云访问安全代理或数据丢失防护解决方案推断使用 Azure 信息保护加密的数据。

有关详细信息，请参阅 [Microsoft 信息保护 SDK 概述](/information-protection/develop/overview)。

## <a name="next-steps"></a>后续步骤

若要开始使用 AIP，请下载并安装统一标记客户端和扫描程序。

- [注册免费试用](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)（企业移动版 + 安全性 E5）
- [下载客户端](https://www.microsoft.com/download/details.aspx?id=53018)
- [快速入门：部署统一标记客户端](quickstart-deploy-client.md)

使用以下初始教程熟悉 AIP：

- [教程：安装 Azure 信息保护 (AIP) 统一标记扫描程序](tutorial-install-scanner.md)
- [教程：使用 Azure 信息保护 (AIP) 扫描程序发现敏感内容](tutorial-scan-networks-and-content.md)
- [教程：使用 Azure 信息保护 (AIP) 防止 Outlook 中的过度共享](tutorial-preventing-oversharing.md)

准备好自定义 AIP 后，请参阅[管理员指南：Azure 信息保护统一标记客户端的自定义配置](rms-client/clientv2-admin-guide-customizations.md)。

若要入门 MIP SDK，请参阅 [Microsoft 信息保护 (MIP) SDK 安装和配置](/information-protection/develop/setup-configure-mip)。

### <a name="additional-resources"></a>其他资源

|资源  |链接和说明  |
|---------|---------|
|订阅选项和定价     |    [Azure 信息保护定价](https://azure.microsoft.com/pricing/details/information-protection)     |
|**常见问题解答和已知问题**     | [有关 Azure 信息保护的常见问题](faqs.md) </br> [已知问题 - Azure 信息保护](known-issues.md)       |
|**支持选项**     | [Azure 信息保护的支持选项](information-support.md)        |
|**Yammer**     |  [Azure 信息保护](https://www.yammer.com/AskIPTeam)       |
|Ignite 2020     |  - [在云、本地、终结点和远程工作环境中强化信息保护和管理](https://myignite.microsoft.com/sessions/ceba117f-9bc7-4426-9ebc-753d94c6a476)</br>- [通过智能数据保护和合规性解决方案成为风险管理英雄](https://myignite.microsoft.com/sessions/9a1e2716-55f5-4c3e-8626-0cb77e60eb87)</br>- [了解你的数据，保护你的数据，并通过 Microsoft 信息保护防止数据丢失](https://myignite.microsoft.com/sessions/46ff69cf-2c8f-4e61-a923-f72f5740f02f)</br>- [咨询专家：询问有关 Microsoft 合规性的任何信息：信息保护与管理、内部风险、合规性管理等](https://myignite.microsoft.com/sessions/5ce48b36-9827-4d60-8540-90546333063d)       |
|**新增功能**     | 在 Microsoft 365 和 SharePoint 管理中心中关注与 AIP 相关的新功能：   </br>[- Microsoft 365 管理中心有哪些新增功能？](/microsoft-365/admin/whats-new-in-preview) </br>- [Sharepoint 管理中心中有哪些新增功能？](/sharepoint/what-s-new-in-admin-center)     |
|     |         |

## <a name="aips-classic-client"></a>AIP 经典客户端

Azure 信息保护经典客户端是早期版本的 AIP，管理员可以通过它直接在 Azure 门户中管理分类标签。

在 Azure 门户中管理的 AIP 标签不受统一标记平台的支持，仅限用于 Azure 信息保护客户端和扫描程序以及 Microsoft Cloud App Security。 

建议迁移到统一标记以支持这些功能，以及 SharePoint、Microsoft 365 应用、适用于 Web 和移动设备 Outlook、PowerBI 数据保护等。 有关详细信息，请参阅[教程：从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端](tutorial-migrating-to-ul.md)。

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）和标签管理将于 2021 年 3 月 31 日弃用。 
>
> 在此时间框架内，所有当前 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记解决方案转换到统一标记。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
