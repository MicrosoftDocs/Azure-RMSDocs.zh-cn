---
title: Azure RMS 的工作原理 - Azure 信息保护
description: 详细解说 Azure RMS 的工作原理、它使用的加密控件以及此过程工作原理的分步图示。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ed2f66ba5fe953f2717d8c0ad9e0730ffbcc30fc
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39370993"
---
# <a name="how-does-azure-rms-work-under-the-hood"></a>Azure RMS 的工作原理 揭秘

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

了解 Azure RMS 工作原理时的一个要点是，Azure 信息保护的这种数据保护服务不会在保护过程中查看或存储你的数据。 要保护的信息永远不会发送或存储到 Azure 中，除非你将其显式存储在 Azure 中，或者使用其他可在 Azure 中存储数据的云服务。 Azure RMS 只会在文档中保存数据，除已获授权的用户和服务以外，其他任何人都无法读取该文档：

- 数据在应用程序级别进行加密，并包含策略用于定义该文档的授权用法。

- 当合法用户使用受保护的文档，或者已获授权的服务处理文档时，将会解密文档中的数据，并强制实施策略中定义的权限。

下图在较高级别显示了此过程的工作方式。 包含机密公式的文档将受到保护，然后成功地由已获授权的用户或服务成功打开。 文档由内容密钥 （图中的绿色钥匙）保护。 每个文档的内容密钥都是唯一的，它放置在文件标头中，并受 Azure 信息保护租户根密钥（图中的红色钥匙）保护。 可以生成并由 Microsoft 管理你的租户密钥，你也可以生成和管理自己的租户密钥。

在整个保护过程中，当 Azure RMS 加密、解密、授权以及强制实施限制时，机密公式永远不会发送到 Azure。

![Azure RMS 如何保护文件](../media/AzRMS_SecretColaFormula_final.png)

有关所发生情况的详细说明，请参阅本文中的 [Azure RMS 工作原理演练：首次使用、内容保护、内容使用](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) 部分。

有关 Azure RMS 使用的算法和密钥长度的技术详细信息，请参阅下一部分。

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Azure RMS 使用的加密控制：算法和密钥长度
即使你不太了解此技术的工作原理，也可能会被问到它使用的加密控件。 例如，确认安全保护是否符合行业标准时。


|加密控件|在 Azure RMS 中使用|
|-|-|
|算法：AES<br /><br />密钥长度：128 位和 256 位 [[1]](#footnote-1)|文档保护|
|算法：RSA<br /><br />密钥长度：2048 位 [[2]](#footnote-2)|密钥保护|
|SHA-256|证书签名|

###### <a name="footnote-1"></a>脚注 1 

当文件具有扩展名 .ppdf 或者是受保护的文本文件或图像文件（例如 .ptxt 或 .pjpg）时，Azure 信息保护客户端和 Rights Management 共享应用程序使用 256 位进行常规保护和本机保护。

###### <a name="footnote-2"></a>脚注 2

2048 位是激活 Azure Rights Management 服务时的密钥长度。 1024 位支持以下可选方案：

- 在从本地进行迁移的过程中 - 如果 AD RMS 群集在加密模式 1 中运行。

- 在从本地进行迁移后 - 如果 AD RMS 群集使用 Exchange Online。

- 用于迁移前在本地创建的存档密钥，以便迁移后可以继续通过 Azure Rights Management 服务打开先前由 AD RMS 保护的内容。

- 如果客户选择使用 Azure Key Vault 来创建其自己的密钥 (BYOK)。 Azure 信息保护支持的密钥长度是 1024 位和 2048 位。 为了提高安全性，建议使用长度为 2048 位的密钥。

### <a name="how-the-azure-rms-cryptographic-keys-are-stored-and-secured"></a>如何存储和保护 Azure RMS 加密密钥

对于受 Azure RMS 保护的每个文档或电子邮件，Azure RMS 都会创建一个 AES 密钥（称为“内容密钥”），并将该密钥嵌入到文档中，并在文档的所有版本中进行保存。 

内容密钥作为文档中的策略的一部分，使用组织的 RSA 密钥（称为“Azure 信息保护租户密钥”）进行保护，并且策略也由文档的作者签名。 此租户密钥由受 Azure Rights Management 服务保护的组织的所有文档和电子邮件共有，如果组织使用的是客户管理的租户密钥（称为“自带密钥”或 BYOK），则此密钥只能由 Azure 信息保护管理员更改。 

此租户密钥在 Microsoft Online Services 中、在高度控制的环境中和严密监视下进行保护。 当你使用客户托管的租户密钥 (BYOK) 时，通过在每个 Azure 区域中使用一组高端硬件安全模块 (HSM) 增强了此安全性，从而在任何情况下都无法提取、导出或共享这些密钥。 有关租户密钥和 BYOK 的详细信息，请参阅[计划和实施 Azure 信息保护租户密钥](../plan-design/plan-implement-tenant-key.md)。

发送到 Windows 设备的许可证和证书使用客户端设备私钥（用户在设备上第一次使用 Azure RMS 时创建）进行保护。 而该私钥则使用客户端上的 DPAPI 进行保护，DPAPI 使用从用户的密码派生的密钥来保护这些机密。 在移动设备上，只使用这些密钥一次，因此由于这些密钥不存储在客户端上，而无需在设备上保护这些密钥。 


## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Azure RMS 工作原理演练：首次使用、内容保护、内容使用
为了更详细地了解 Azure RMS 的工作原理，让我们通过在[激活 Azure Rights Management 服务](../deploy-use/activate-service.md)之后，当用户首次在其 Windows 计算机上使用权限管理服务（有时称为**初始化用户环境**或引导的过程）时，**保护内容**（文档或电子邮件），然后**使用**（打开并使用）被其他某人保护的内容，来演练一个典型的工作流。

初始化用户环境后，该用户可以保护文档，或使用该计算机上的受保护文档。

> [!NOTE]
> 如果此用户移至另一台 Windows 计算机，或另一个用户使用这同一台 Windows 计算机，请重复该初始化过程。

### <a name="initializing-the-user-environment"></a>初始化用户环境
在用户可以保护内容或使用 Windows 计算机上的受保护内容之前，必须在设备上准备用户环境。 这是一次性的过程，当用户尝试保护或使用受保护内容时会自动发生，无需用户干预：

![RMS 客户端激活流程 - 步骤 1，对客户端进行身份验证](../media/AzRMS.png)

**步骤 1 中发生的情况**：计算机上的 RMS 客户端首先连接到 Azure Rights Management 服务，并通过使用其 Azure Active Directory 帐户对用户进行身份验证。

将用户的帐户与 Azure Active Directory 联合时，会自动进行这种身份验证，并且不会提示用户输入凭据。

![RMS 客户端激活-步骤 2，证书已下载到客户端](../media/AzRMS_useractivation2.png)

**步骤 2 中发生的情况**：对用户进行身份验证后，连接将自动重定向到组织的 Azure 信息保护租户，该租户将颁发证书，让用户在 Azure Rights Management 服务上进行身份验证，以便使用受保护内容并脱机保护内容。

其中一个证书是通常缩写为 RAC 的权限帐户证书。 此证书对 Azure Active Directory 用户进行身份验证，有效期为 31 天。 如果用户帐户仍然在 Azure Active Directory 中并且启用了该帐户，RMS 客户端将自动续订证书。 该证书不可由管理员进行配置。 

证书副本存储在 Azure 中，因此，如果用户转移到另一台设备，将使用相同的密钥创建证书。

### <a name="content-protection"></a>内容保护
当用户保护文档时，RMS 客户端将对未受保护的文档执行以下操作：

![RMS 文档保护 - 步骤 1，文档已加密](../media/AzRMS_documentprotection1.png)

**步骤 1 中发生的情况**：RMS 客户端创建一个随机密钥 （内容密钥），并结合使用此密钥与 AES 对称加密算法来加密该文档。

![RMS 文档保护 - 步骤 2，策略已创建](../media/AzRMS_documentprotection2.png)

**步骤 2 中发生的情况**：RMS 客户端随后会为文档创建一个包含策略的证书，策略包括用户或组的[使用权](../deploy-use/configure-usage-rights.md)和其他限制，例如过期日期。 这些设置可在管理员之前配置的模板中进行定义，或在内容受保护时进行指定（有时称为“临时策略”）。   

用于标识所选用户和组的主要 Azure AD 属性是 Azure AD proxyAddresses 属性，该属性用于存储用户或组的所有电子邮件地址。 但是，如果用户帐户的 AD ProxyAddresses 属性中没有任何值，则改用用户的 UserPrincipalName 值。

然后，RMS 客户端使用初始化用户环境时获取的组织密钥，并使用此密钥来加密策略和对称内容密钥。 RMS 客户端还使用初始化用户环境时获得的用户证书对策略进行签名。

![RMS 文档保护 - 步骤 3，策略已嵌入到文档中](../media/AzRMS_documentprotection3.png)

**步骤 3 中发生的情况**：最后，RMS 客户端将该策略嵌入到一个文件中，该文件包含以前已加密的文档的正文，并与该文档共同构成了受保护文档。

可将此文档存储在任意位置，或者使用任何方法将其共享，加密的文档始终附带该策略。

### <a name="content-consumption"></a>内容使用
当用户想要使用受保护的文档时，将通过请求对 Azure Rights Management 服务的访问来启动 RMS 客户端：

![RMS 文档使用 - 步骤 1，用户已通过身份验证并获取权限列表](../media/AzRMS_documentconsumption1.png)

**步骤 1 中发生的情况**：经过身份验证的用户将文档策略和用户的证书发送到 Azure Rights Management 服务。 服务解密并评估该策略，并生成用户对该文档拥有的权限列表（如果有）。 若要标识用户，可将 Azure AD ProxyAddresses 属性用于用户的帐户和该用户所属的组。 出于性能原因，会[缓存](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection)组成员身份。 如果用户帐户的 Azure AD ProxyAddresses 属性中没有任何值，则改用 Azure AD UserPrincipalName 中的值。

![RMS 文档使用 - 步骤 2，使用许可证已返回到客户端](../media/AzRMS_documentconsumption2.png)

**步骤 2 中发生的情况**：然后，服务将从已解密的策略中提取 AES 内容密钥。 然后，使用通过请求获取的用户公共 RSA 密钥来加密此密钥。

重新加密的内容密钥将连同用户权限列表一起嵌入到加密的使用许可证中，随后使用许可证将返回到 RMS 客户端。

![RMS 文档使用 - 步骤 3，文档已解密并且权限已强制实施](../media/AzRMS_documentconsumption3.png)

**步骤 3 中发生的情况**：最后，RMS 客户端将采用加密的使用许可证，并使用其自身的用户私钥来解密该许可证。 这样，RMS 客户端便可以根据需要解密文档的正文，并在屏幕上呈现其内容。

客户端还将解密权限列表，并将其传递到应用程序，应用程序将在应用程序的用户界面中强制实施这些权限。

> [!NOTE]
> 组织外部的用户使用你保护的内容时，使用流程是相同的。 对于此方案，有所更改的是如何对用户进行身份验证。 有关详细信息，请访问[如果我与公司之外的用户共享受保护文档，该用户如何进行身份验证？](../get-started/faqs-rms.md#when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated)


### <a name="variations"></a>变体
前面的演练包括标准方案，但存在一些变体：

- **电子邮件保护**：将 Exchange Online 和具有新功能的 Office 365 消息加密用于保护电子邮件消息时，还可通过社会标识提供者或使用一次性密码进行联合身份验证。 其中，流程非常相似，而出站电子邮件临时缓存副本中的 Web 浏览器会话服务端发生内容使用的除外。

- **移动设备**：当移动设备通过 Azure Rights Management 服务保护或使用文件时，流程要简单得多。 因为每个事务（保护或使用内容）是独立的，移动设备首先不会经历用户初始化过程。 与 Windows 计算机一样，移动设备将连接到 Azure Rights Management 服务并进行身份验证。 为了保护内容，移动设备将提交一个策略，然后 Azure Rights Management 服务将为移动设备发送一个发布许可证和对称密钥用于保护文档。 为了使用内容，当移动设备连接到 Azure Rights Management 服务并进行身份验证时，它们将文档策略发送到 Azure Rights Management 服务，并请求一个使用许可证以使用文档。 在响应中，Azure Rights Management 服务会将所需的密钥和限制发送到移动设备。 这两个进程使用 TLS 来保护密钥交换和其他通信。

- **RMS 连接器**：当 Azure Rights Management 服务与 RMS 连接器结合使用时，流程保持不变。 唯一的差别在于，连接器充当本地服务（如 Exchange Server 和 SharePoint Server）与 Azure Rights Management 服务之间的中继。 连接器本身不执行任何操作，例如用户环境初始化，或者加密或解密。 它只会中继通常要定向到 AD RMS 服务器的通信，处理每一端使用的协议之间的转换。 此方案使你可以将 Azure Rights Management 服务与本地服务结合使用。

- **常规保护 (.pfile)**：当 Azure Rights Management 服务对文件提供一般性保护时，流程基本上与内容保护相同，不过，RMS 客户端将创建一个授予所有权限的策略。 使用该文件时，会先将它解密，然后将它传递到目标应用程序。 这种方案允许你保护所有文件，即使它们本机不支持 RMS。

- **受保护的 PDF (.ppdf)**：Azure Rights Management 服务本机保护 Office 文件时，还会创建该文件的副本，并以相同的方法保护该副本。 唯一的差别在于，文件副本采用 PPDF 文件格式，Azure 信息保护客户端查看器和 RMS 共享应用程序只知道如何打开该格式进行查看。 这种方案允许你通过电子邮件发送受保护的附件，知道移动设备上的收件人始终能够读取它们，即使移动设备没有相应的应用可本机支持受保护的 Office 文件。

- “Microsoft 帐户”：使用 Microsoft 帐户对电子邮件地址进行身份验证时，Azure 信息保护可以授权其可供使用。 但是，并非所有应用程序都可以在使用 Microsoft 帐户进行身份验证时打开受保护的内容。 [详细信息](../get-started/secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)。

## <a name="next-steps"></a>后续步骤

若要了解 Azure Rights Management 服务的详细信息，请参阅**了解和探索**部分中的其他文章（如[应用程序如何支持 Azure Rights Management 服务](applications-support.md)），了解你的现有应用程序如何通过与 Azure Rights Management 集成来提供信息保护解决方案。 

请查看 [Azure 信息保护术语](../get-started/terminology.md)，以便熟悉在配置和使用 Azure Rights Management 服务时可能遇到的术语。此外，还要确保在开始部署前查看 [Azure 信息保护的要求](../get-started/requirements-azure-rms.md)。 如果你要进一步研究并亲自尝试一下，请使用 [Azure 信息保护快速入门教程](../get-started/infoprotect-quick-start-tutorial.md)。

当做好开始为组织部署数据保护的准备时，请使用 [Azure 信息保护部署路线图](../plan-design/deployment-roadmap.md)获取部署步骤和操作说明链接。

> [!TIP]
> 有关其他信息和帮助，请使用 [Azure 信息保护的信息和支持](../get-started/information-support.md)中的资源和链接。
