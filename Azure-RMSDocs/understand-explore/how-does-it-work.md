---
title: "Azure RMS 的工作原理 | Azure 信息保护"
description: "详细解说 Azure RMS 的工作原理、它使用的加密控件以及此过程工作原理的分步图示。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2c0f3b58a2f1b5233c262bb67cc4a485557ba997
ms.openlocfilehash: 5efa5bdf9e11e55ec190c3abe95b1bdc33026c63


---


# Azure RMS 的工作原理 揭秘

>*适用于：Azure 信息保护、Office 365*

了解 Azure RMS 工作原理时，一个要点是权限管理服务，另外，在信息保护过程中，Microsoft 不要查看或存储你的数据。 要保护的信息永远不会发送或存储到 Azure 中，除非你显式将其存储在 Azure 中，或者使用其他可用于在 Azure 中存储数据的云服务。 Azure RMS 只会在文档中保存数据，除已获授权的用户和服务以外，其他任何人都无法读取该文档：

-   数据在应用程序级别进行加密，并包含策略用于定义该文档的授权用法。

-   当合法用户使用受保护的文档，或者已获授权的服务处理文档时，将会解密文档中的数据，并强制实施策略中定义的权限。

下图在较高级别显示了此过程的工作方式。 包含机密公式的文档将受到保护，然后成功地由已获授权的用户或服务成功打开。 文档由内容密钥 （图中的绿色钥匙）保护。 每个文档的内容密钥都是唯一的，它放置在文件标头中，并受 RMS 租户根密钥（图中的红色钥匙）保护。 可以生成并由 Microsoft 管理你的租户密钥，你也可以生成和管理自己的租户密钥。

在整个保护过程中，当 Azure RMS 加密、解密、授权以及强制实施限制时，机密公式永远不会发送到 Azure。

![Azure RMS 如何保护文件](../media/AzRMS_SecretColaFormula_final.png)

有关所发生情况的详细说明，请参阅本文中的 [Azure RMS 工作原理演练：首次使用、内容保护、内容使用](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) 部分。

有关 Azure RMS 使用的算法和密钥长度的技术详细信息，请参阅下一部分。

## Azure RMS 使用的加密控制：算法和密钥长度
尽管你不需要知道 RMS 的工作原理，但可能会有人询问你使用的加密控制，以确保安全保护符合行业标准。


|加密控件|在 Azure RMS 中使用|
|-|-|
|算法：AES<br /><br />密钥长度：128 位和 256 位 [[1]](#footnote-1)|文档保护|
|算法：RSA<br /><br />密钥长度：2048 位|密钥保护|
|SHA-256|证书签名|

###### 脚注 1 

当文件具有扩展名 .ppdf 或者是受保护的文本文件或图像文件（例如 .ptxt 或 .pjpg）时，Rights Management 共享应用程序使用 256 位进行常规保护和本机保护。

如何存储和保护加密密钥：

- 对于受 Azure RMS 保护的每个文档或电子邮件，Azure RMS 都会创建一个 AES 密钥（称为“内容密钥”），并将该密钥嵌入到文档中，并在文档的所有版本中进行保存。 

- 内容密钥作为文档中的策略的一部分，使用组织的 RSA 密钥（称为“Azure RMS 租户密钥”）进行保护，并且策略也由文档的作者签名。 此租户密钥由受 Azure RMS 保护的组织的所有文档和电子邮件共有，如果组织使用的是客户管理的租户密钥（称为“自带密钥”或 BYOK），则此密钥只能由 Azure RMS 管理员更改。 

    此租户密钥在 Microsoft Online Services 中、在高度控制的环境中和严密监视下进行保护。 当你使用客户管理的租户密钥 (BYOK) 时，通过在每个 Azure 区域中使用一组高端硬件安全模块 (HSM) 增强了此安全性，从而在任何情况下都无法提取、导出或共享这些密钥。 有关租户密钥和 BYOK 的详细信息，请参阅 [计划和实现你的 Azure Rights Management 租户密钥](../plan-design/plan-implement-tenant-key.md)。

- 发送到 Windows 设备的许可证和证书使用客户端设备私钥（用户在设备上第一次使用 Azure RMS 时创建）进行保护。 而该私钥则使用客户端上的 DPAPI 进行保护，DPAPI 使用从用户的密码派生的密钥来保护这些机密。 在移动设备上，只使用这些密钥一次，因此由于这些密钥不存储在客户端上，而无需在设备上保护这些密钥。 



## Azure RMS 工作原理演练：首次使用、内容保护、内容使用
为了更详细地了解 Azure RMS 的工作原理，让我们通过在 [激活 Azure RMS 服务](../deploy-use/activate-service.md) 之后，当用户首次在其 Windows 计算机上使用 RMS（有时称为 **初始化用户环境** 或引导的过程）时，**保护内容**（文档或电子邮件），然后 **使用**（打开并使用）其他某人保护的内容，演练一个典型的工作流。

初始化用户环境后，该用户可以保护文档，或使用该计算机上的受保护文档。

> [!NOTE]
> 如果此用户移至另一台 Windows 计算机，或另一个用户使用这同一台 Windows 计算机，请重复该初始化过程。

### 初始化用户环境
在用户可以保护内容或使用 Windows 计算机上的受保护内容之前，必须在设备上准备用户环境。 这是一次性的过程，当用户尝试保护或使用受保护内容时会自动发生，无需用户干预：

![RMS 客户端激活 - 步骤 1](../media/AzRMS.png)

**步骤 1 中发生的情况**：计算机上的 RMS 客户端首先连接到 Azure RMS，并通过使用其 Azure Active Directory 帐户对用户进行身份验证。

将用户的帐户与 Azure Active Directory 联合时，会自动进行这种身份验证，并且不会提示用户输入凭据。

![RMS 客户端激活 - 步骤 2](../media/AzRMS_useractivation2.png)

**步骤 2 中发生的情况**：对用户进行身份验证后，连接将自动重定向到组织的 RMS 租户，该租户将颁发证书，让用户在 Azure RMS 上进行身份验证，以便使用受保护内容以及脱机保护内容。

用户证书的副本存储在 Azure RMS 中，因此，如果用户移到另一台设备，将使用相同的密钥创建证书。

### 内容保护
当用户保护文档时，RMS 客户端将对未受保护的文档执行以下操作：

![RMS 文档保护 - 步骤 1](../media/AzRMS_documentprotection1.png)

**步骤 1 中发生的情况**：RMS 客户端创建一个随机密钥 （内容密钥），并结合使用此密钥与 AES 对称加密算法来加密该文档。

![RMS 文档保护 - 步骤 2](../media/AzRMS_documentprotection2.png)

**步骤 2 中发生的情况**：然后，RMS 客户端将会基于模板或者通过指定文档的特定权限为该文档创建包含策略的证书。 此策略包括不同用户或组的权限和其他限制，例如过期日期。

然后，RMS 客户端使用初始化用户环境时获取的组织密钥，并使用此密钥来加密策略和对称内容密钥。 RMS 客户端还使用初始化用户环境时获得的用户证书对策略进行签名。

![RMS 文档保护 - 步骤 3](../media/AzRMS_documentprotection3.png)

**步骤 3 中发生的情况**：最后，RMS 客户端将该策略嵌入到一个文件中，该文件包含以前已加密的文档的正文，并与该文档共同构成了受保护文档。

可将此文档存储在任意位置，或者使用任何方法将其共享，加密的文档始终附带该策略。

### 内容使用
当用户想要使用受保护的文档时，将通过请求对 Azure RMS 服务的访问来启动 RMS 客户端：

![RMS 文档占用 - 步骤 1](../media/AzRMS_documentconsumption1.png)

**步骤 1 中发生的情况**：经过身份验证的用户将文档策略和用户的证书发送到 Azure RMS。 服务解密并评估该策略，并生成用户对该文档拥有的权限列表（如果有）。

![RMS 文档占用 - 步骤 2](../media/AzRMS_documentconsumption2.png)

**步骤 2 中发生的情况**：然后，服务将从已解密的策略中提取 AES 内容密钥。 然后，使用通过请求获取的用户公共 RSA 密钥来加密此密钥。

重新加密的内容密钥将连同用户权限列表一起嵌入到加密的使用许可证中，随后使用许可证将返回到 RMS 客户端。

![RMS 文档使用 - 步骤 3](../media/AzRMS_documentconsumption3.png)

**步骤 3 中发生的情况**：最后，RMS 客户端将采用加密的使用许可证，并使用其自身的用户私钥来解密该许可证。 这样，RMS 客户端便可以根据需要解密文档的正文，并在屏幕上呈现其内容。

客户端还将解密权限列表，并将其传递到应用程序，应用程序将在应用程序的用户界面中强制实施这些权限。

### 变体
前面的演练包括标准方案，但存在一些变体：

-   **移动设备**：当移动设备通过 Azure RMS 保护或使用文件时，流程要简单得多。 因为每个事务（保护或使用内容）是独立的，移动设备首先不会经历用户初始化过程。 与 Windows 计算机一样，移动设备将连接到 Azure RMS 服务并进行身份验证。 为了保护内容，移动设备将提交一个策略，然后 Azure RMS 将为移动设备发送一个发布许可证和对称密钥用于保护文档。 为了使用内容，当移动设备连接到 Azure RMS 服务并进行身份验证时，它们将文档策略发送到 Azure RMS，并请求一个使用许可证以使用文档。 在响应中，Azure RMS 会将所需的密钥和限制发送到移动设备。 这两个进程使用 TLS 来保护密钥交换和其他通信。

-   **RMS 连接器**：当 Azure RMS 与 RMS 连接器结合使用时，流程保持不变。 唯一的差别在于，连接器充当本地服务（如 Exchange Server 和 SharePoint Server）与 Azure RMS 之间的中继。 连接器本身不执行任何操作，例如用户环境初始化，或者加密或解密。 它只会中继通常要定向到 AD RMS 服务器的通信，处理每一端使用的协议之间的转换。 这种方案允许你将 Azure RMS 与本地服务结合使用。

-   **常规保护 (.pfile)**：当 Azure RMS 对文件提供一般性保护时，流程基本上与内容保护相同，不过，RMS 客户端将创建一个授予所有权限的策略。 使用该文件时，会先将它解密，然后将它传递到目标应用程序。 这种方案允许你保护所有文件，即使它们本机不支持 RMS。

-   **受保护的 PDF (.ppdf)**：Azure RMS 本机保护 Office 文件时, 还会创建该文件的副本，并以相同的方法保护该副本。 唯一的差别在于，文件副本采用 PPDF 文件格式，RMS 共享应用程序只知道如何打开该格式以查看。 这种方案允许你通过电子邮件发送受保护的附件，知道移动设备上的收件人始终能够读取它们，即使移动设备没有相应的应用程序可本机支持受保护的 Office 文件。

## 后续步骤

若要了解 Azure RMS 的详细信息，请参阅 **了解和探索** 部分中的其他文章（如 [应用程序如何支持 Azure Rights Management](applications-support.md)），了解你的现有应用程序如何通过与 Azure RMS 集成来提供信息保护解决方案。 

请查看 [Azure Rights Management术语](../get-started/terminology.md)，以便熟悉在配置和使用 Azure RMS 时可能遇到的术语。此外，还要确保在开始部署前查看 [Azure Rights Management 的要求](../get-started/requirements-azure-rms.md)。 如果你要进一步研究并亲自尝试一下，请使用 [Azure Rights Management 快速入门教程](../get-started/quick-start-tutorial.md)。

当你做好开始为组织部署 Azure RMS 的准备时，请使用 [Azure Rights Management 部署路线图](../plan-design/deployment-roadmap.md) 获取部署步骤和操作说明链接。

> [!TIP]
> 有关其他信息和帮助，请使用 [Azure Rights Management 的信息和支持](../get-started/information-support.md)中的资源和链接。



<!--HONumber=Sep16_HO4-->


