---
title: Azure 信息保护的 HYOK 保护
description: 具有 Azure 信息保护的 HYOK (AD RMS) 保护概述、其支持的方案、限制、先决条件和建议。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/01/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.openlocfilehash: 5ded2edb2ea3fe05cc09750c4cdb53bc03d5fbae
ms.sourcegitcommit: 87d73477b7ae9134b5956d648c390d2027a82010
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="hold-your-own-key-hyok-protection-for-azure-information-protection"></a>用于 Azure 信息保护的保留自己的密钥 (HYOK) 保护

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)

使用以下信息了解什么是用于 Azure 信息保护的保留自己的密钥 (HYOK)，以及它与默认的基于云的保护有何不同。 使用 HYOK 保护前，请确保了解适用情况、支持的方案、限制和需求。 

## <a name="cloud-based-protection-vs-hyok"></a>基于云的保护与HYOK

使用 Azure 信息保护来保护最敏感的文档和电子邮件时，通常会应用使用 Azure 权限管理 (Azure RMS) 保护的基于云的密钥，以便从以下优势中受益：

- 无需任何服务器基础结构，从而使该解决方案能够以比本地解决方案更快、更经济高效的方式进行部署和维护。

- 通过使用基于云的身份验证，与合作伙伴和来自其他组织的用户更轻松地进行共享。

- 与其他 Azure 和 Office 365 服务紧密集成，如搜索、Web 查看器、透视视图、反恶意软件、电子数据展示和 Delve。

- 针对已共享的敏感文档的文档跟踪、撤销和电子邮件通知。

基于云的密钥通过为组织使用由 Microsoft 管理的私钥（默认）或你自己管理的私钥（“自带密钥”或 BYOK 方案）来保护组织的文档和电子邮件。 有关租户密钥选项的详细信息，请参阅[计划和实施 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)。

可将保护的文档和电子邮件存储在云端或本地。 有关保护过程是否适用于此基于云的密钥的详细信息，请参阅[什么是 Azure Rights Management？](../understand-explore/what-is-azure-rms.md )

面向租户的 Office 365 服务和基于云的应用程序可与 Azure 信息保护集成，以便重要的业务功能（如搜索、索引、归档和反恶意软件服务）继续无缝地作用于受 Azure 信息保护所保护的内容。 这些方案中读取加密内容的能力通常称为“基于数据的推理”。 例如，Exchange Online 通过此功能解密电子邮件，以便进行恶意软件扫描，并对加密电子邮件运行数据丢失防护 (DLP) 规则。

但是，出于法规要求，少数组织可能需要使用与云隔离的密钥加密内容。 此隔离意味着仅本地应用程序和本地服务可读取加密内容。 Azure 信息保护支持此密钥管理选项，它被称为“保留自己的密钥”或“HYOK”。 使用具有 HYOK 的 Azure 信息保护 时，租户同时拥有基于云的密钥和本地密钥。

## <a name="hyok-guidance-and-best-practices"></a>HYOK 指导和最佳做法

仅对需要将加密密钥与云隔离的文档和电子邮件使用 HYOK 保护。 HYOK 保护不提供上面列出的那些使用基于云的密钥保护时可获得的好处，而且它通常以“数据不透明”为代价。 这个词意味着只有本地应用程序和服务才能打开受 HYOK 保护的数据，基于云的服务和应用程序无法对受 HYOK 保护的数据进行推理。

即使对使用 HYOK 保护的组织而言，它通常也适用于少量需要保护的文档。 提示：请仅将此用于满足以下所有标准的文档：

- 内容在组织中具有最高分类（“顶级机密”），并且访问权限仅限于少数人

- 不会在组织外部共享该内容

- 仅在内部网络中使用内容

由于 HYOK 保护是管理员的标签配置选项，因此无论保护使用基于云的密钥还是 HYOK，用户工作流都保持不变。

[作用域策略](configure-policy-scope.md)是一个不错的方法，可确保只有需要应用 HYOK 保护的用户才能查看为 HYOK 保护配置的标签。 

## <a name="supported-scenarios-for-hyok"></a>HYOK 支持的方案

若要应用 HYOK 保护，请使用 Azure 信息保护标签。 

下表列出了使用为 HYOK 配置的标签保护内容及打开（使用）受 HYOK 保护的内容的受支持方案。

|平台|应用程序|支持|
|----------------------|----------|-----------|
|Windows|带有 Office 2016 和 Office 2013 的 Azure 信息保护客户端 <br /><br />- Word、Excel、PowerPoint|保护：是<br /><br />使用：是|
|Windows|带有 Office 2016 和 Office 2013 的 Azure 信息保护客户端 <br /><br />- Outlook|保护：是<br /><br />使用：是|
|Windows|具有文件资源管理器的 Azure 信息保护客户端|保护：是 <br /><br />使用：是|
|Windows|Azure 信息保护查看器|保护：不适用<br /><br />使用：是|
|Windows|带有 PowerShell 标签 cmdlet 的 Azure 信息保护客户端|保护：是<br /><br />使用：是|
|Windows|Azure 信息保护扫描程序|保护：是<br /><br />使用：是|
|Windows|权限管理共享应用|保护：否<br /><br />使用：是|
|MacOS|Office for Mac <br /><br /> - Word、Excel、PowerPoint|保护：否<br /><br />使用：是|
|MacOS|Office for Mac<br /><br />- Outlook|保护：否<br /><br />使用：是|
|MacOS|权限管理共享应用|保护：否<br /><br />使用：是|
|iOS|Office Mobile <br /><br />- Word、Excel、PowerPoint|保护：否<br /><br />使用：是|
|iOS|Office Mobile <br /><br />-Outlook|保护：否<br /><br />使用：否|
|iOS|Azure 信息保护查看器|保护：不适用<br /><br />使用：是|
|Android|Office Mobile <br /><br />- Word、Excel、PowerPoint|保护：否<br /><br />使用：是|
|Android|Office Mobile <br /><br />- Outlook|保护：否<br /><br />使用：否|
|Android|Azure 信息保护查看器|保护：不适用<br /><br />使用：是|
|Web|Web 上的 Outlook|保护：否<br /><br />使用：否|
|Web|Office Online <br /><br />- Word、Excel、PowerPoint|保护：否<br /><br />使用：否|
|通用|Office 通用应用<br /><br />- Word、Excel、PowerPoint|保护：否<br /><br />使用：否|


## <a name="additional-limitations-when-using-hyok"></a>使用 HYOK 时的其他限制

此外，对 Azure 信息保护标签使用 HYOK 保护具有以下限制：

- 不支持 Office 2010 或 Office 2007。

- Office 365 服务和其他在线服务将无法解密受 HYOK 保护的文档和电子邮件以检查内容并对其采取相应措施。 此限制适用于使用 Rights Management 连接器保护的受 HYOK 保护的文档和电子邮件。 
    
    这将导致受 HYOK 保护的电子邮件功能受损，包括恶意软件扫描程序、数据丢失防护 (DLP) 解决方案、邮件传递规则、日志记录、电子数据展示、归档解决方案和 Exchange ActiveSync。 此外，用户不了解为什么某些设备无法打开受 HYOK 保护的电子邮件，这可能导致其致电技术支持。 由于这些限制，不建议对电子邮件使用 HYOK 保护。

## <a name="implementing-hyok"></a>实现 HYOK

如果 Active DirectoryRights Management Services (AD RMS) 部署符合下节中记录的要求，则 Azure 信息保护支持 HYOK。 在此方案中，在本地管理和保留保护这些策略的使用权策略和组织的私钥，然而仍在 Azure 中管理和存储用于标记和分类的 Azure 信息保护策略。 

请勿将 HYOK 和 Azure 信息保护与使用 AD RMS 和 Azure 信息保护的完整部署混淆，也不要将其作为将 AD RMS 迁移到 Azure 信息保护的替代方案。 仅通过应用标签支持 HYOK，不提供 AD RMS 的功能奇偶一致性，也不支持所有 AD RMS 部署配置：

- 有关 HYOK 支持的保护内容和使用受保护内容的方案的详细信息，请参阅 [HYOK 支持的方案](#supported-scenarios-for-hyok)部分。

- 有关 AD RMS 的迁移说明，请参阅[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

- 有关 AD RMS 部署要求的详细信息，请参阅下节。

### <a name="requirements-for-ad-rms-to-support-hyok"></a>AD RMS 支持 HYOK 的要求

AD RMS 部署必须满足以下要求，才能为 Azure 信息保护标签提供 HYOK 保护。

- AD RMS 配置：
    
    - 最小版本的 Windows Server 2012 R2：生产环境需要此版本，但用于测试或评估时，可以使用带 Service Pack 1 的 Windows Server 2008 R2 的最小版本。
    
    - 以下拓扑之一：
        
        - 具有单个 AD RMS 根群集的单个林。 
        
        - 具有独立 AD RMS 根群集的多个林，用户无法访问由其他林的用户保护的内容。
        
        - 多个林，每个林中有 AD RMS 群集。 每个 AD RMS 群集共享指向相同 AD RMS 群集的许可 URL。 在此 AD RMS 群集上，必须从所有其他 AD RMS 群集导入所有受信任用户域 (TUD) 证书。 有关此拓扑的详细信息，请参阅 [受信任的用户域](https://technet.microsoft.com/library/dd983944(v=ws.10\).aspx)。
        
    如果单独的林中具有多个 AD RMS 群集，删除应用 HYOK (AD RMS) 保护并为每个群集配置[作用域策略](configure-policy-scope.md)的全局策略中的任何标签。 将每个群集的用户分配到其作用域策略，确保不使用会导致用户分配到多个作用域策略的组。 结果应是每个用户仅有一个 AD RMS 群集的标签。 
    
    - [加密模式 2](https://technet.microsoft.com/library/hh867439.aspx)：可以通过检查 AD RMS 群集属性、“常规”选项卡来确认该模式。
    
    - 每个 AD RMS 服务器都针对证书 URL 进行了配置。 [说明](#configuring-ad-rms-servers-to-locate-the-certification-url) 
    
    - Active Directory 中未注册服务连接点 (SCP)：结合使用 AD RMS 保护和 Azure 信息保护时未使用 SCP。 
    
        - 如果已就 AD RMS 部署注册了 SCP，必须将其删除，以便 Azure 权限管理保护功能成功[发现服务](../rms-client/client-deployment-notes.md#rms-service-discovery)。 
        
        - 如果你正在为 HYOK 安装新的 AD RMS 群集，则跳过在配置第一个节点期间注册 SCP 的步骤。 对于每个其他节点，请确保在添加 AD RMS 角色并加入现有群集前，服务器已针对证书 URL 进行了配置。
    
    - 配置 AD RMS 服务器，以搭配使用 SSL/TLS 和受连接的客户端信任的有效 x.509 证书：生产环境需要，但用于测试或评估时不需要。
    
    - 已配置的权限模板。
    
    - 未为 Exchange IRM 配置。
    
    - 对于移动设备和 Mac 计算机：已安装并配置 [Active Directory Rights Management 服务移动设备扩展](https://technet.microsoft.com/library/dn673574.aspx)。

- 在本地 Active Directory 和 Azure Active Directory 之间配置了目录同步，并且为将使用 HYOK 保护的用户配置了单一登录。

- 如果与组织外的其他人共享由 HYOK 保护的文档或电子邮件：请通过受信任用户域 (TUD) 或使用 Active Directory 联合身份验证服务 (AD FS) 创建的联合信任，在与其他组织的直接点对点关系中为 AD RMS 配置显式定义的信任。

- 用户拥有的 Office 版本为 Office 2016 Professional Plus 或 Office 2013 Professional Plus Service Pack 1，并且在 Windows 7 Service Pack 1 或更高版本上运行。 请注意，此方案不支持 Office 2010 和 Office 2007。
    
    - 对于 Office 2016，基于 Microsoft Installer (.msi) 的版本：你已安装[于 2018 年 3 月 6 日发布的 Microsoft Office 2016 更新 4018295](https://support.microsoft.com/en-us/help/4018295/march-6-2018-update-for-office-2016-kb4018295)。

> [!IMPORTANT]
> 为了实现 HYOK 保护提供的高确定性，建议不要将 AD RMS 服务器放在外围网络中，并且只能由受管理设备使用这些服务器。 
> 
> 我们还建议 AD RMS 群集使用硬件安全模块 (HSM)，以便在 AD RMS 部署被破坏或泄露时，你的服务器许可方证书 (SLC) 的私钥不会被公开或盗取。 

有关 AD RMS 的部署信息和说明，请参阅 Windows Server 库中的 [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx)。 


### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>配置 AD RMS 服务器以找到证书 URL

1. 在群集中的每个 AD RMS 服务器上，创建以下注册表项：

    `Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    
    对于 \<字符串值 >，请指定下列值之一：
    
    - 对于使用 SSL/TLS 的 AD RMS 群集：

            https://<cluster_name>/_wmcs/certification/certification.asmx
    
    - 对于不使用 SSL/TLS 的 AD RMS 群集（仅测试网络）：
        
            http://<cluster_name>/_wmcs/certification/certification.asmx

2. 重新启动 IIS。

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>查找相关信息以使用 Azure 信息保护标签指定 AD RMS 保护

配置用于 HYOK (AD RMS) 保护的标签时，必须指定 AD RMS 群集的授权 URL。 此外，必须指定已为要授予用户的权限配置的模板，或者让用户定义权限和用户。 

可以从 Active Directory Rights Management Services 控制台中找到模板 GUID 和授权 URL 的值：

- 要找到模板 GUID：请展开该群集，并单击“权限策略模板”。 随后，从“分布式权限策略模板”信息中，可以复制要使用的模板中的 GUID。 例如：82bf3474-6efe-4fa1-8827-d1bd93339119

- 若要查找授权 URL：请单击群集名称。 从“群集详细信息”信息中，复制除 **/_wmcs/licensing** 字符串以外的“授权”值。 例如：https://rmscluster.contoso.com 
    
    如果你有一个 Extranet 授权值和一个 Intranet 授权值，并且两个值不同：仅当与定义为具有显式点对点信任关系的合作伙伴共享受保护的文档或电子邮件时，才指定 Extranet 值。 否则使用 Intranet 值，并确保针对 Azure 信息保护使用 AD RMS 保护的所有客户端计算机均通过 Intranet 连接进行连接（例如，远程计算机使用 VPN 连接）。


## <a name="next-steps"></a>后续步骤

若要配置用于 HYOK 保护的标签，请参阅[如何配置标签以进行 Rights Management 保护](../deploy-use/configure-policy-protection.md)。 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]