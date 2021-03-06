---
title: 从 AD RMS 迁移到 Azure 信息保护 - 第 3 阶段
description: 从 AD RMS 迁移到 Azure 信息保护的第 3 阶段涉及从 AD RMS 迁移到 Azure 信息保护中的步骤 7。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d0c643ea787d8ef9a977930aee270af5023c89a7
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97381521"
---
# <a name="migration-phase-3---client-side-configuration"></a>迁移第 3 阶段 - 客户端配置

>***适用** 于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的阶段 3。 这些过程涉及了[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)中的步骤 7。

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>步骤 7. 重新配置 Windows 计算机以使用 Azure 信息保护

使用以下方法之一重新配置 Windows 计算机以使用 Azure 信息保护：

- **DNS 重定向**。 最简单和首选方法（如果支持）。 

    支持使用 Office 2016 或更高版本的桌面应用程序的 Windows 计算机，其中包括：

    - Microsoft 365 应用
    - Office 2019
    - Office 2016 单击以运行桌面应用

    要求您创建一个新的 SRV 记录，并为用户在 AD RMS 发布端点上设置 NTFS 拒绝权限。

    有关详细信息，请参阅 [使用 DNS 重定向重新配置客户端](#client-reconfiguration-by-using-dns-redirection)。

- **编辑注册表**。 适用于所有受支持的环境，包括：

    - 使用 Office 2016 或更高版本的 Windows 计算机，如上面列出的那样运行桌面应用
    - 使用其他应用的 Windows 计算机
    
    手动进行所需的注册表更改，或编辑并部署可下载的脚本，以使注册表更改。

    有关详细信息，请参阅 [使用注册表编辑重新配置客户端](#client-reconfiguration-by-using-registry-edits)。


> [!TIP]
> 如果混合使用的 Office 版本可以且不能使用 DNS 重定向，则可以结合使用 DNS 重定向和编辑注册表，或者将注册表编辑为适用于所有 Windows 计算机的单个方法。


## <a name="client-reconfiguration-by-using-dns-redirection"></a>通过 DNS 重定向重新配置客户端

此方法仅适用于运行 Microsoft 365 应用和 Office 2016 (或更高版本) 单击即可运行桌面应用程序的 Windows 客户端。 

1. 创建使用以下格式的 DNS SRV 记录：
    
    ```sh
    _rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.
    ```
    
    对于 *\<AD RMS cluster>* ，指定 AD RMS 群集的 FQDN。 例如 **rmscluster.contoso.com**。
    
    或者，如果你在该域中只有一个 AD RMS 群集，可以指定该 AD RMS 群集的域名。 在本示例中，即 **contoso.com**。 在此记录中指定域名时，重定向将应用到该域中的所有 AD RMS 群集。
    
    *\<port>* 忽略该数字。
    
    对于 *\<your tenant URL\>* ，为你的租户指定你自己的 [Azure RIGHTS MANAGEMENT 服务 URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)。
    
    如果在 Windows Server 上使用 DNS 服务器角色，可使用下表作为示例，在 DNS 管理器控制台中指定 SRV 记录属性。
    
    |字段|值|  
    |-----------|-----------|  
    |**域**|_tcp.rmscluster.contoso.com|  
    |**服务**|_rmsredir|  
    |**协议**|_http|  
    |**Priority**|0|  
    |**Weight**|0|  
    |**端口号**|80|  
    |**提供此服务的主机**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  
    | | |

2. 为运行 Microsoft 365 应用或 Office 2016 (或更高) 版本的用户 AD RMS 发布终结点设置拒绝权限：

    a. 在群集中的某个 AD RMS 服务器上，启动 Internet Information Services (IIS) 管理器控制台。

    b. 导航到 " **默认** 网站"，然后展开 **_wmcs**。

    c. 右键单击 " **授权** "，然后选择 " **切换到内容视图**"。

    d. 在详细信息窗格中，右键单击 " **license**" "  >  **属性**" "  >  **编辑**"

    e. 在 " **license 的权限** " 对话框中，选择 " **用户** " （如果要为所有用户设置重定向），或单击 " **添加** "，然后指定包含要重定向的用户的组。
    
    即使所有用户都使用支持 DNS 重定向的 Office 版本，最好还是先指定部分用户来进行分阶段迁移。
    
    f. 对于所选组，为“**读取和执行**”及“**读取**”权限选择“**拒绝**”，然后两次单击“**确定**”。

    g. 若要确认此配置按预期工作，请尝试从浏览器直接连接到 licensing.asmx 文件。 应会看到以下错误消息，它将触发运行 Microsoft 365 应用或 Office 2019 或 Office 2016 的客户端查找 SRV 记录：
    
    **错误消息 401.3: 无权使用所提供的凭据查看此目录或页面（由于访问控制列表，访问被拒绝）。**


## <a name="client-reconfiguration-by-using-registry-edits"></a>使用注册表编辑重新配置客户端

此方法适用于所有 Windows 客户端，如果这些客户端未运行 Microsoft 365 应用或 Office 2016 (或更高版本) ，则应该使用此方法。 此方法使用两个迁移脚本重新配置 AD RMS 客户端：

- Migrate-Client.cmd

- Migrate-User.cmd

客户端配置脚本 (Migrate-Client.cmd) 在注册表中配置计算机级别设置，这意味着它必须在可进行这些更改的安全上下文中运行。 这通常指以下方法之一：

- 使用组策略，将该脚本作为计算机启动脚本运行。

- 使用组策略软件安装，将脚本分配给计算机。

- 使用软件部署解决方案，将脚本部署给计算机。 例如，使用 System Center Configuration Manager [包和程序](/sccm/apps/deploy-use/packages-and-programs)。 在包和程序的属性中，在“运行模式”下，指定在设备上使用管理权限运行该脚本。 

- 如果用户具有本地管理员特权，请使用登录脚本。

用户配置脚本 (Migrate-User.cmd) 配置用户级别设置，并清除客户端许可证存储。 这意味着此脚本必须在实际用户上下文中运行。 例如：

- 使用登录脚本。

- 使用组策略软件安装来发布脚本供用户运行。

- 使用软件部署解决方案，将脚本部署给用户。 例如，使用 System Center Configuration Manager [包和程序](/sccm/apps/deploy-use/packages-and-programs)。 在包和程序的属性中，在“运行模式”下，指定使用该用户的权限运行该脚本。 

- 用户登录到他们的计算机时要求其运行该脚本。

这两个脚本包含一个版本号并且不会重新运行，除非更改该版本号。 也就是说，可以一直在原位保留这两个脚本，直到迁移完成。 但如果确实对想要计算机和用户在 Windows 计算机上重新运行的脚本进行了更改，可将这两个脚本中的以下行更新为较高的值：

```sh
SET Version=20170427
```

用户配置脚本专门设计在客户端配置脚本之后运行，并在此检查中使用版本号。 如果版本相同的客户端配置脚本未运行，它将停止。 此检查可确保这两个脚本以正确的顺序运行。 

如果无法同时迁移所有 Windows 客户端，请分批对客户端运行以下过程。 对于批次中具有要迁移的 Windows 计算机的每个用户，将用户添加到之前创建的 **AIPMigrated** 组。

### <a name="modifying-the-scripts-for-registry-edits"></a>修改脚本以实现注册表编辑

1. 返回到迁移脚本 Migrate-Client.cmd 和 Migrate-User.cmd 中，这是之前在[准备阶段](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration)下载这些脚本时提取的。

2. 按照 **migrate-client.cmd** 中的说明修改脚本，使其包含租户的 Azure RIGHTS MANAGEMENT 服务 URL，以及你的 AD RMS 群集 EXTRANET 授权 url 和 INTRANET 授权 url 的服务器名称。 然后，使上述脚本版本递增。 跟踪脚本版本的一个好方法是使用当天的日期，格式如下： YYYYMMDD
    
   > [!IMPORTANT]
   > 仍然注意，不要在地址前后引入多余空格。
   > 
   > 此外，如果 AD RMS 服务器使用 SSL/TLS 服务器证书，请检查字符串中许可 URL 值是否包括端口号 **443**。 例如：https://rms.treyresearch.net:443/_wmcs/licensing。 单击群集名称并查看“**群集详细信息**”时，Active Directory Rights Management Services 中会显示此信息。 如果端口号 443 包含在此 URL 中，修改脚本时请将该值包括在内。 例如 https://rms.treyresearch.net:<strong>443</strong>。 
    
   如果需要检索 *&lt; YourTenantURL &gt;* 的 azure Rights Management 服务 url，请参阅返回以 [识别 azure Rights Management 服务 url](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)。

3. 使用此步骤开始处的说明，配置脚本部署方法，在由 AIPMigrated 组成员使用的 Windows 客户端计算机上运行 Migrate-Client.cmd 和 Migrate-User.cmd。 

## <a name="next-steps"></a>后续步骤

若要继续迁移，请转到[第 4 阶段 - 支持服务配置](migrate-from-ad-rms-phase4.md)。
