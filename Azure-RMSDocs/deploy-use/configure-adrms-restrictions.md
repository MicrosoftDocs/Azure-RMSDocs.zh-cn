---
title: "Azure 信息保护的 HYOK 限制"
description: "如果选择具有 Azure 信息保护的 HYOK (AD RMS) 保护，请确定限制、先决条件和建议。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/17/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.openlocfilehash: ac4068885df92c58ecba2a90e7aa0aeaaa34e8e9
ms.sourcegitcommit: 12c9a4e3fe8e92d816f0a13003062f20dd2716df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2017
---
# <a name="hold-your-own-key-hyok-requirements-and-restrictions-for-ad-rms-protection"></a>AD RMS 保护的自留密钥 (HYOK) 要求和限制

>*适用于：Azure 信息保护*

保护最敏感的文档和电子邮件时，通常会为此应用 Azure 权限管理 (Azure RMS) 保护，以便从以下优势中受益：

- 无需任何服务器基础结构，从而使该解决方案能够以比本地解决方案更快、更经济高效的方式进行部署和维护。

- 通过使用基于云的身份验证，与合作伙伴和来自其他组织的用户更轻松地进行共享。

- 与 Office 365 服务紧密集成，如搜索、Web 查看器、透视视图、反恶意软件、电子数据展示和 Delve。

- 针对已共享的敏感文档的文档跟踪、撤销和电子邮件通知。

Azure RMS 通过为组织使用由 Microsoft 管理的私钥（默认）或你自己管理的私钥（“自带密钥”或 BYOK 方案）来保护组织的文档和电子邮件。 使用 Azure RMS 保护的信息永远不会发送到云；受保护的文档和电子邮件不会存储在 Azure 中，除非你显式将其存储在其中，或者使用另一个云服务将其存储在 Azure 中。 有关租户密钥选项的详细信息，请参阅[计划和实施 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)。 

但是，有些组织可能需要使用本地托管的密钥来保护文档和电子邮件的较小子集。 例如，可能出于法规和合规性方面的原因需要这样做。  

此配置有时称为“自留密钥”(HYOK)，当你有一个满足下节所述要求的有效 Active Directory Rights Management Services (AD RMS) 部署时，此配置受 Azure 信息保护支持。

在此 HYOK 方案中，权限策略和组织用于保护这些策略的私钥将在本地管理和保留，而 Azure 信息保护的标记和分类策略仍然在 Azure 中管理和存储。 与 Azure RMS 保护一样，使用 AD RMS 保护的信息永远不会发送到云。

> [!NOTE]
> 仅在必要时对需要此配置的文档和电子邮件使用此配置。 AD RMS 保护不提供上面列出的那些使用 Azure RMS 保护时可获得的好处，其用途在于“不惜任何代价确保数据不透明”。
>
> 甚至对于使用此配置的组织来说，它通常适用于需要保护的内容少于所有内容的 10% 的情况。 提示：请仅将此用于满足以下所有标准的文档或电子邮件：
> 
> - 内容在组织中具有最高分类（“顶级机密”），并且访问权限仅限于少数人。
> 
> - 绝不会在组织外部共享内容。
> 
> - 仅在内部网络中使用内容。
> 
> - 不会在 Mac 计算机或移动设备上使用内容。

当标签使用 AD RMS 保护，而非 Azure RMS 保护时，用户不会知道。 由于 AD RMS 保护所附带的局限性和限制，请确保明确指示用户何时应选择应用 AD RMS 保护的标签的例外情况。 

[作用域策略](configure-policy-scope.md)是一个不错的方法，可确保只有需要应用 AD RMS 保护的用户才能查看为 AD RMS 保护配置的标签。 

## <a name="additional-limitations-when-using-hyok"></a>使用 HYOK 时的其他限制

将 AD RMS 保护与 Azure 信息保护联用，不仅不支持使用 Azure RMS 保护时可获得的所列益处，还具有以下限制：

- 不支持 Office 2010 或 Office 2007。

- 配置 Azure RMS 保护的标签时，请勿使用“不要转发”选项。 还必须指示用户不要在 Outlook 中手动选择此选项。 

    如果由标签或由用户手动应用了“不要转发”选项，则可能由 AD RMS 部署（而不是预期的 Azure 权限管理服务）应用该选项。 在此方案中，外部共享对象无法打开已应用此“不要转发”选项的电子邮件。
    
    自 1.9.58.0 版 Azure 信息保护客户端（当前处于预览阶段）起，Outlook 中的“不转发”按钮始终使用 Azure RMS。 此设置既不会影响 Outlook“不转发”菜单选项，也不会影响配置保护标签时使用的“不转发”选项。 如果不需要此行为，可以配置[高级客户端设置](../rms-client/client-admin-guide-customizations.md#hide-the-do-not-forward-button-in-outlook)，从而在 Outlook 中隐藏“不转发”按钮。

- 如果用户在你使用 AD RMS (HYOK) 保护和 Azure RMS 保护时配置自定义权限，则文档或电子邮件始终受 Azure 权限管理保护。

- 如果用户选择了应用 AD RMS 保护的 Outlook 中的标签，然后在发送电子邮件之前改变了主意，并选择了应用 Azure RMS 保护的标签，则无法应用新选择的标签。 用户将看到以下错误消息：**Azure 信息保护无法应用此标签。你无权执行此操作。**
    
    唯一的解决方法是关闭电子邮件并重新启动。 与此类似，如果用户首先选择了应用 Azure RMS 保护的标签，然后改为使用应用 AD RMS 保护的标签，也将产生相同的限制。

## <a name="requirements-for-hyok"></a>HYOK 要求

确保你的 AD RMS 部署满足以下要求，以便为 Azure 信息保护提供 AD RMS 保护。

- AD RMS 配置：
    
    - 最小版本的 Windows Server 2012 R2：生产环境需要此版本，但用于测试或评估时，可以使用带 Service Pack 1 的 Windows Server 2008 R2 的最小版本。
    
    - 单个 AD RMS 根群集。
    
    - [Cryptographic Mode 2](https://technet.microsoft.com/library/hh867439.aspx)（加密模式 2）：可以通过使用 [RMS Analyzer tool](https://www.microsoft.com/en-us/download/details.aspx?id=46437)（RMS Analyzer 工具）确认 AD RMS 群集加密模式的版本，及其总体运行状况。   
    
    - Active Directory 中未注册服务连接点 (SCP)：结合使用 AD RMS 保护和 Azure 信息保护时未使用 SCP。 如果已就 AD RMS 部署注册了 SCP，必须将其删除，以便 Azure 权限管理保护功能成功[发现服务](../rms-client/client-deployment-notes.md#rms-service-discovery)。
    
    - 配置 AD RMS 服务器，以搭配使用 SSL/TLS 和受连接的客户端信任的有效 x.509 证书：生产环境需要，但用于测试或评估时不需要。
    
    - 已配置的权限模板。

- 在本地 Active Directory 和 Azure Active Directory 之间配置了目录同步，并且为将使用 AD RMS 保护的用户配置了单一登录。

- 如果与组织外的其他人共享由 AD RMS 保护的文档或电子邮件：请通过受信任用户域 (TUD) 或使用 Active Directory 联合身份验证服务 (AD FS) 创建的联合信任，在与其他组织的直接点对点关系中为 AD RMS 配置显式定义的信任。

- 用户拥有的 Office 版本为 Office 2013 Pro Plus Service Pack 1 或 Office 2016 Pro Plus，并且在 Windows 7 Service Pack 1 或更高版本上运行。 请注意，此方案不支持 Office 2010 和 Office 2007。

> [!IMPORTANT]
> 为了实现此方案提供的高确定性，建议不要将 AD RMS 服务器放在外围网络中，并且只能由管理完善的计算机（例如，非移动设备或工作组计算机）使用这些服务器。 
> 
> 我们还建议 AD RMS 群集使用硬件安全模块 (HSM)，以便在 AD RMS 部署被破坏或泄露时，你的服务器许可方证书 (SLC) 的私钥不会被公开或盗取。 

有关 AD RMS 的部署信息和说明，请参阅 Windows Server 库中的 [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx)。 


## <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>查找相关信息以使用 Azure 信息保护标签指定 AD RMS 保护

在配置用于 **HYOK (AD RMS)** 保护的标签时，必须指定 AD RMS 群集的模板 GUID 和授权 URL。 你可以从 Active Directory Rights Management Services 控制台中找到这两个值：

- 若要找到模板 GUID：请展开该群集，并单击“权限策略模板”。 随后，从“分布式权限策略模板”信息中，可以复制要使用的模板中的 GUID。 例如：82bf3474-6efe-4fa1-8827-d1bd93339119

- 若要查找授权 URL：请单击群集名称。 从“群集详细信息”信息中，复制除 **/_wmcs/licensing** 字符串以外的“授权”值。 例如：https://rmscluster.contoso.com 
    
    如果你有一个 Extranet 授权值和一个 Intranet 授权值，并且两个值不同：仅当与定义为具有显式点对点信任关系的合作伙伴共享受保护的文档或电子邮件时，才指定 Extranet 值。 否则使用 Intranet 值，并确保针对 Azure 信息保护使用 AD RMS 保护的所有客户端计算机均通过 Intranet 连接进行连接（例如，远程计算机使用 VPN 连接）。

## <a name="next-steps"></a>后续步骤

若要了解有关此功能的详细信息和使用指南，请参阅博客文章公告 [Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/)（具有 HYOK（自留密钥）的 Azure 信息保护）。

若要配置用于 AD RMS 保护的标签，请参阅[如何配置标签以进行 Rights Management 保护](../deploy-use/configure-policy-protection.md)。 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]