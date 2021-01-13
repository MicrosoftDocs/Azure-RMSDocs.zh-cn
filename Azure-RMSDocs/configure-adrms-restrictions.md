---
title: 在 Azure 信息保护中保留你自己的密钥 (HYOK) 保护
description: 具有 Azure 信息保护的 HYOK (AD RMS) 保护概述、其支持的方案、限制、先决条件和建议。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/13/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ROBOTS: NOINDEX
ms.subservice: hyok
ms.custom: admin
ms.openlocfilehash: 9b608b8f38c157320558cf5ae5011ef601773b2e
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164226"
---
# <a name="hold-your-own-key-hyok-details-for-azure-information-protection"></a>保存你自己的密钥 (Azure 信息保护的 HYOK) 详细信息

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标记客户端，请参阅 [双重密钥加密](plan-implement-tenant-key.md#double-key-encryption-dke)。 *

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

保留你自己的密钥 (HYOK) 配置使使用经典客户端的 AIP 客户能够在保持对密钥的完全控制的同时保护高度敏感的内容。 HYOK 使用一种附加的客户端密钥，该密钥存储在本地以实现高度敏感的内容，同时还使用用于其他内容的基于云的默认保护。 

有关默认的基于云的租户根密钥的详细信息，请参阅 [计划和实现 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

## <a name="cloud-based-protection-vs-hyok"></a>基于云的保护与 HYOK

通常，使用 Azure 信息保护来保护敏感文档和电子邮件时，使用的是 [由 Microsoft](plan-implement-tenant-key.md#tenant-root-keys-generated-by-microsoft) 或 [客户使用 BYOK 配置](byok-price-restrictions.md)生成的基于云的密钥。 

基于云的密钥在 Azure Key Vault 中进行管理，这为客户提供以下好处：

- **无服务器基础结构要求**。 云解决方案比本地解决方案更快速、更经济高效。

- 通过 **基于云的身份验证**，可以更方便地与其他组织的合作伙伴和用户共享。 

- **与其他 Azure 和 Microsoft 365 服务的紧密集成**，如搜索、web 查看器、透视视图、反恶意软件、电子数据展示和 Delve。

- 已共享的敏感文档的 **文档跟踪**、**吊销** 和 **电子邮件通知**。

但是，某些组织可能具有要求使用与云中隔离的密钥来加密特定内容的法规要求。 此隔离意味着加密内容只能由本地应用程序和本地服务读取。

使用 HYOK 配置，客户租户既有 [基于云的密钥](plan-implement-tenant-key.md) 可用于存储在云中的内容，也有必须在本地保护的内容的本地密钥。

## <a name="hyok-guidance-and-best-practices"></a>HYOK 指导和最佳做法

配置 HYOK 时，请考虑以下建议：

- [适用于 HYOK 的内容](#content-suitable-for-hyok)
- [定义可以查看 HYOK 配置的标签的用户](#define-the-users-who-can-see-hyok-configured-labels)
- [HYOK 和电子邮件支持](#hyok-and-email-support)

> [!IMPORTANT]
> Azure 信息保护的 HYOK 配置不是完全 AD RMS 和 Azure 信息保护部署的替代方案，也不是将 [AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的替代方法。 
>
> HYOK 仅通过应用标签来支持，不提供与 AD RMS 的功能奇偶校验，并且不支持所有 AD RMS 的部署配置。

### <a name="content-suitable-for-hyok"></a>适用于 HYOK 的内容

HYOK 保护不提供基于云的保护的优点，并且通常以 "数据不透明度" 的成本提供，因为内容只能由本地应用程序和服务访问。 即使对于使用 HYOK 保护的组织来说，它通常仅适用于少量的文档。 

建议仅将 HYOK 用于满足以下条件的内容：

- 你的组织中具有最高分类的内容 ( "顶级机密" ) ，其中的访问权限仅限于少数人
- 不在组织外共享的内容
- 仅在内部网络上使用的内容。

### <a name="define-the-users-who-can-see-hyok-configured-labels"></a>定义可以查看 HYOK 配置的标签的用户

若要确保只有需要应用 HYOK 保护的用户，请参阅 HYOK 配置的标签，为具有 [作用域内策略](configure-policy-scope.md)的用户配置策略。

### <a name="hyok-and-email-support"></a>HYOK 和电子邮件支持

Microsoft 365 服务和其他联机服务无法对 HYOK 保护的内容进行解密。

对于电子邮件，此功能损失包括恶意软件扫描器、仅加密保护、数据丢失防护 (DLP) 解决方案、邮件路由规则、日记、电子数据展示、存档解决方案和 Exchange ActiveSync。

用户可能不理解为什么某些设备无法打开受 HYOK 保护的电子邮件，从而导致对技术支持的额外呼叫。 在通过电子邮件配置 HYOK 保护时，请注意这些严重限制。

## <a name="supported-applications-for-hyok"></a>HYOK 支持的应用程序

使用 Azure 信息保护标签对特定文档和电子邮件应用 HYOK。 Office 版本2013和更高版本支持 HYOK。

HYOK 是标签的管理员配置选项，无论内容使用的是基于云的密钥还是 HYOK，工作流都保持不变。

下表列出了使用 HYOK 配置的标签保护和使用内容的支持方案：

- [Windows 应用程序对 HYOK 的支持](#windows-application-support-for-hyok)
- [HYOK 的 macOS 应用程序支持](#macos-application-support-for-hyok)
- [适用于 HYOK 的 iOS 应用程序支持](#ios-application-support-for-hyok)
- [适用于 HYOK 的 Android 应用程序支持](#android-application-support-for-hyok)

> [!NOTE]
> HYOK 不支持 Office Web 和通用应用程序。

### <a name="windows-application-support-for-hyok"></a>Windows 应用程序对 HYOK 的支持

|应用程序  |保护  |消耗  |
|---------|---------|---------|
|Azure 信息保护客户端 Microsoft 365 应用、Office 2019、Office 2016 和 Office 2013：</br>Word、Excel、PowerPoint、Outlook     | ![是](media/yes-icon.png)        | ![是](media/yes-icon.png)        |
|具有文件资源管理器的 Azure 信息保护客户端     | ![是](media/yes-icon.png)        | ![是](media/yes-icon.png) |
|Azure 信息保护查看器     |   不适用      |  ![是](media/yes-icon.png)       |
|带有 PowerShell 标签 cmdlet 的 Azure 信息保护客户端     | ![是](media/yes-icon.png)        | ![是](media/yes-icon.png)        |
|Azure 信息保护扫描程序     |![是](media/yes-icon.png)       |   ![是](media/yes-icon.png)      |
| | | |

### <a name="macos-application-support-for-hyok"></a>HYOK 的 macOS 应用程序支持

|应用程序|保护|消耗|
|----------------------|----------|-----------|
|Office for Mac： </br>Word、Excel、PowerPoint、Outlook|![否](media/no-icon.png)|![是](media/yes-icon.png)|
| | | |

### <a name="ios-application-support-for-hyok"></a>适用于 HYOK 的 iOS 应用程序支持

|应用程序|保护|消耗|
|----------------------|----------|-----------|
|Office Mobile： </br>Word、Excel、PowerPoint|![否](media/no-icon.png)| ![是](media/yes-icon.png)|
|Office Mobile： </br>仅 Outlook|![否](media/no-icon.png)|![否](media/no-icon.png)|
|Azure 信息保护查看器|不适用|![是](media/yes-icon.png)|

### <a name="android-application-support-for-hyok"></a>适用于 HYOK 的 Android 应用程序支持

|应用程序|保护|消耗|
|----------------------|----------|-----------|
|Office Mobile： </br>Word、Excel、PowerPoint|![否](media/no-icon.png)| ![是](media/yes-icon.png)|
|Office Mobile： </br>仅 Outlook|![否](media/no-icon.png)|![否](media/no-icon.png)|
|Azure 信息保护查看器|不适用| ![是](media/yes-icon.png)|


## <a name="implementing-hyok"></a>实现 HYOK

当你的 Active Directory Rights Management Services (AD RMS) 符合 [下面列出](#requirements-for-ad-rms-to-support-hyok)的所有要求时，Azure 信息保护支持 HYOK。

保护这些策略的使用权限策略和组织的私钥是在本地管理和保留的，而用于标记和分类的 Azure 信息保护策略仍保持托管并存储在 Azure 中。

实现 HYOK 保护：

1. [请确保系统符合 AD RMS 要求](#requirements-for-ad-rms-to-support-hyok)
1. [查找要保护的信息](#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

准备就绪后，请继续使用 [如何为 Rights Management 保护配置标签](configure-policy-protection.md)。

### <a name="requirements-for-ad-rms-to-support-hyok"></a>AD RMS 支持 HYOK 的要求

若要为 Azure 信息保护标签提供 HYOK 保护，AD RMS 部署必须满足以下要求：

|要求  |说明  |
|---------|---------|
|**AD RMS 配置**     |你的 AD RMS 系统必须以特定方式配置为支持 HYOK。 有关详细信息，请参阅 [下文](#ad-rms-configuration-requirements)。          |
|**目录同步**     |必须在本地 Active Directory 与 Azure Active Directory 之间配置目录同步。 </br></br>要使用 HYOK 保护标签的用户必须配置为使用单一登录。         |
|**明确定义信任的配置**     |如果与组织外的其他人共享 HYOK 保护的内容，则必须在与其他组织的直接点对点关系中为显式定义的信任配置 AD RMS。 </br></br>使用受信任的用户域 (Tud) 或使用 Active Directory 联合身份验证服务 (AD FS) 创建的联合信任来完成此操作。         |
|**Microsoft Office 支持的版本**     | 保护或使用受 HYOK 保护的内容的用户必须具有： </br></br>-支持 Rights Management (IRM 的信息的 Office 版本)  </br>-在 Windows 7 Service Pack 1 或更高版本上运行 Microsoft Office Professional Plus 版本2013或更高版本 Service Pack 1。 </br>-对于 Office 2016 Microsoft Installer ( .msi) 版本，你必须将 [更新4018295用于 Microsoft Office 2016，年3月 6 2018 日发布](https://support.microsoft.com/help/4018295/march-6-2018-update-for-office-2016-kb4018295)。 </br></br>**注意**：不支持 office 2010 和 office 2007。  有关详细信息，请参阅 [AIP For Windows And Office 版本中的扩展支持](known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。      |

> [!IMPORTANT]
> 为了满足 HYOK protection 提供的高确定性，建议执行以下操作：
> - 在 DMZ 外查找 AD RMS 服务器，并确保这些服务器仅供托管设备使用。
>
> - 使用 (HSM) 的硬件安全模块配置 AD RMS 群集。 这有助于确保服务器许可方证书 (SLC) 私钥在你的 AD RMS 部署应被破坏或破坏时无法公开或被盗。

> [!TIP]
> 有关 AD RMS 的部署信息和说明，请参阅 Windows Server 库中的 [Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831364(v=ws.11))。 

#### <a name="ad-rms-configuration-requirements"></a>AD RMS 配置要求

若要支持 HYOK，请确保 AD RMS 系统具有以下配置：

|要求  |说明  |
|---------|---------|
|**Windows 版本**     |至少，以下 Windows 版本之一： </br></br>**生产环境**： Windows Server 2012 R2</br>**测试/评估环境**： Windows Server 2008 R2 Service Pack 1        |
|**拓扑**     |HYOK 需要以下拓扑之一： </br>-具有单个 AD RMS 群集的单个林 </br>-多个林，其中每个林都有 AD RMS 群集。 </br></br>**多个林的许可**</br> 如果有多个林，则每个 AD RMS 群集共享一个指向同一 AD RMS 群集的授权 URL。 </br>在此 AD RMS 群集上，将所有受信任的用户域 (TUD) 所有其他 AD RMS 群集中的证书。 </br>有关此拓扑的详细信息，请参阅 [可信用户域](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd983944(v=ws.10))。 </br></br>**多个林的全局策略标签**</br>如果单独的林中具有多个 AD RMS 群集，删除应用 HYOK (AD RMS) 保护并为每个群集配置[作用域策略](configure-policy-scope.md)的全局策略中的任何标签。 <br>将每个群集的用户分配到其作用域内策略，确保不会使用将导致用户分配到多个作用域内策略的组。</br>结果应是每个用户仅有一个 AD RMS 群集的标签。          |
|**加密模式**     | 你的 AD RMS 必须配置为 [加密模式 2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh867439(v=ws.10))。 </br>检查模式，方法是选中 "群集属性" AD RMS " **常规** " 选项卡。        |
|**证书 URL 配置**     | 必须为每个 AD RMS 服务器配置证书 URL。 </br>有关详细信息，请参阅 [下文](#configuring-ad-rms-servers-to-locate-the-certification-url)。        |
|**服务连接点**     | 将 AD RMS 保护与 Azure 信息保护结合使用时，不使用 (SCP) 的服务连接点。 </br></br>**如果为 AD RMS 部署注册了 SCP**，请将其删除，以确保 [服务发现](./rms-client/client-deployment-notes.md#rms-service-discovery) 对于 Azure Rights Management 保护成功。 </br></br>**如果要为 HYOK 安装新的 AD RMS 群集**，请不要在配置第一个节点时注册 SCP。 对于每个其他节点，请确保在添加 AD RMS 角色并加入现有群集前，服务器已针对证书 URL 进行了配置。         |
|**SSL/TLS**     |在生产环境中，必须将 AD RMS 服务器配置为使用 SSL/TLS，其中包含由连接客户端信任的有效 x.509 证书。 </br></br>这对于测试或评估目的不是必需的。         |
|**权限模板**     |您必须为您的 AD RMS 配置权限模板。         |
|**Exchange IRM**    |不能为 Exchange IRM 配置你的 AD RMS。         |
|**移动设备/Mac 计算机**     | 必须安装并配置 [Active Directory Rights Management Services 移动设备扩展](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11)) 。        |


#### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>配置 AD RMS 服务器以找到证书 URL

1. 在群集中的每个 AD RMS 服务器上，创建以下注册表项：

    ```sh
    Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    ```

    对于 \<string value> ，请指定以下字符串之一：

    |环境  |字符串值  |
    |---------|---------|
    |**生产** </br>使用 SSL/TLS (AD RMS 群集)      | `https://<cluster_name>/_wmcs/certification/certification.asmx`        |
    |**测试/评估** </br>不 (SSL/TLS)      |`http://<cluster_name>/_wmcs/certification/certification.asmx`         |

2. 重新启动 IIS。

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>查找相关信息以使用 Azure 信息保护标签指定 AD RMS 保护

配置 HYOK-保护标签需要指定 AD RMS 群集的授权 URL。 

此外，您必须指定已使用您要授予用户的权限配置的模板，或允许用户定义权限和用户。 

执行以下操作以从 Active Directory Rights Management Services 控制台查找模板 GUID 和授权 URL 值：

#### <a name="locate-a-template-guid"></a>查找模板 GUID

1. 展开群集，并单击“权限策略模板”。 

1. 从 " **分布式权限策略模板** " 信息中，复制要使用的模板中的 GUID。 

例如： **82bf3474-6efe-4fa1-8827-d1bd93339119** 

#### <a name="locate-the-licensing-url"></a>找到许可 URL

1. 单击群集名称。
 
1. 从“群集详细信息”信息中，复制除 **/_wmcs/licensing** 字符串以外的“授权”值。 

例如：**https://rmscluster.contoso.com** 
    
> [!NOTE]
> 如果你有不同的 extranet 和 intranet 授权值，则仅当你将与合作伙伴共享受保护的内容时，才指定 extranet 值。 共享受保护内容的合作伙伴必须通过显式的点到点信任来定义。 
> 
> 如果你不共享受保护的内容，则使用 intranet 值，并确保 AD RMS 使用 Azure 信息保护的所有客户端计算机通过 intranet 连接进行连接。 例如，远程计算机必须使用 VPN 连接。
> 

## <a name="next-steps"></a>后续步骤

将系统配置为支持 HYOK 时，请继续为 HYOK 保护配置标签。 有关详细信息，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)。