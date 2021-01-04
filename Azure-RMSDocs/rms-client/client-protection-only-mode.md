---
title: Azure 信息保护的仅保护模式
description: 此信息适用于以仅保护模式运行 Azure 信息保护客户端的用户。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: af64fc43cd137bfe9f9f05c4237d4a617fd0898d
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807223"
---
# <a name="user-guide-protection-only-mode-for-the-azure-information-protection-client"></a>用户指南：Azure 信息保护客户端的仅保护模式

>***适用于**： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>相关内容：*[适用于 Windows 的 Azure 信息保护经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

当 Azure 信息保护客户端没有用于对文档和电子邮件进行分类的标签，它将在仅保护模式下运行。 例如，在此模式中，当使用 Windows 文件资源管理器，右键单击“分类和保护”，可能会看到以下项：

![仅保护模式](../media/protection-only-mode.png)

仅保护模式将在以下情况下运行：

- 你的组织没有 Azure 信息保护订阅，该订阅包含分类和标签功能，但包含使用 Azure Rights Management 服务的 Microsoft 365 的订阅。 
    
    - 可以使用 Azure 信息保护客户端保护文件和查看受保护的文件。 无法对文档和电子邮件进行分类或添加标签。

- 贵组织仅为部分用户订阅了 Azure 信息保护：
    
    - 对于此组合订阅，管理员有责任确保仅部分用户可以使用分类和标签功能。 其余用户应在仅保护模式下运行 Azure 信息保护客户端。 

- 你的组织订阅了 Azure 信息保护，但你没有为自己配置任何标签。
    
    - 如果全局策略中的所有标签都被禁用，且你的帐户未添加到作用域策略中，则会发生此情况。 这可能是因为你的 IT 部门才刚开始推出 Azure 信息保护，但尚未向你提供标签来对文档和电子邮件进行分类。 在这段期间，可以使用 Azure 信息保护客户端保护文件和查看受保护的文件。

- 你的组织已订阅 Azure 信息保护，但是你无法下载 Azure 信息保护策略。 
    
    - 这可能是因为配置不正确，也可能是因为你没有成功登录。 请联系技术支持或管理员，但在此期间，你可以使用 Azure 信息保护客户端保护文件和查看受保护的文件。

- 你的组织仅使用 Active Directory Rights Management Services (AD RMS)。 


## <a name="limitations-for-protection-only-mode"></a>仅保护模式的限制

- 在 Office 应用程序中，Azure 信息保护栏将不显示。 单击 "**保护**  >  "**显示栏** 时，此菜单选项不可用。

- 在文件资源管理器中使用“分类和保护 - Azure 信息保护”对话框时，不会看到分类标签。 相反，如上图所示，你将看到一个用于选择 Rights Management (RMS) 模板的选项。 

## <a name="supported-tasks-for-protection-only-mode"></a>仅保护模式支持的任务

- 通过使用 office 信息 Rights Management (IRM) 功能，来保护 (和取消保护) 文档和电子邮件，例如：单击 "**文件**  >  **信息**" "  >  **保护文档**" "  >  **限制访问**"。 有关详细信息，请参阅[在 Office 365、Office 2019、Office 2016 或 Office 2013 中使用信息保护](../help-users.md#using-information-protection-with-office365-office-2019-office-2016-or-office2013)。

- 通过使用 Windows 文件资源管理器保护（和取消保护）文件：右键单击单个文件、多个文件或文件夹 >“分类和保护”。 若要应用管理员已配置的保护，请在“分类和保护 - Azure 信息保护”对话框中，单击“选择模版”，然后选择任一可用模板。

- 通过使用 Azure 信息保护查看器查看受保护的文件。

- 从 Office 应用程序访问文档跟踪站点。 但是，必须具有用于跟踪和撤销来自此站点的文档的有效订阅。
  
