---
title: 为用户安装 Azure 信息保护统一标签客户端
description: 管理员用于在企业网络上部署 Azure 信息保护统一标签客户端的说明和信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f818a94e954b245d329a2cdb2dc1ce419e83c4ce
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560095"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>管理员指南：为用户安装 Azure 信息保护统一标签客户端

>***适用于**： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，Windows 8，Windows Server 2019，Windows Server 2016，windows Server 2012 R2，windows server 2012 *
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP 和旧版 Windows 和 office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。*
>
>*适用 **于**： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [经典客户端管理员指南](client-admin-guide-install.md)。 *

在企业网络上安装 Azure 信息保护统一标签客户端之前，请检查计算机是否具有 Azure 信息保护所需的操作系统版本和应用程序： [Azure 信息保护要求](../requirements.md) ，以及 [在企业网络上安装统一标签客户端的其他要求](reqs-ul-client.md)。

## <a name="supported-applications-for-the-unified-labeling-client"></a>统一标签客户端支持的应用程序

Azure 信息保护统一标签客户端可以使用 Office 应用程序的 Word、Excel、PowerPoint 和 Outlook 通过以下任一 Office 版本来标记和保护文档和电子邮件：

- Office 应用，对于[各更新通道中受支持的 Microsoft 365 应用版本表](/officeupdates/update-history-microsoft365-apps-by-date)中列出的版本，从 Microsoft 365 商业应用版或 Microsoft 365 商业高级版，前提是已为用户分配了 Azure Rights Management（亦称为“适用于 Microsoft 365 的 Azure 信息保护”）许可证
- Microsoft 365 企业应用版
- Office 专业增强版 2019
- Office 专业增强版 2016
- Office 专业增强版 2013 Service Pack 1
- Office 专业增强版 2010 Service Pack 2

其他版本的 Office (如 **standard**) 无法使用 Rights Management 服务来保护文档和电子邮件。 对于这些版本，仅支持 Azure 信息保护以便进行 **标记** 。 

因此，应用保护的标签不会向用户显示 Azure 信息保护敏感度按钮或栏。

有关支持保护服务的 Office 版本的信息，请参阅[支持 Azure Rights Management 数据保护的应用程序](../requirements-applications.md)。

> [!IMPORTANT]
> Office 2010 扩展支持于2020年10月13日结束。 有关详细信息，请参阅 [AIP 和旧版 Windows 和 Office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。

## <a name="unified-labeling-client-installation-options"></a>统一标签客户端安装选项

为用户安装客户端有两个选项：

|选项  |描述  | I
|---------|---------|
|**运行客户端的可执行 () 版本**     |   可以通过交互方式或无提示方式运行的建议的安装方式。 <br><br>此方法非常灵活，建议使用，因为安装程序会检查多个必备组件，并且可以自动安装缺少的必备组件。 <br><br>有关详细信息，请参阅 [使用可执行安装程序安装 AIP 统一标签客户端](#install-the-aip-unified-labeling-client-using-the-executable-installer)。|
|**( .msi) 版本的客户端部署 Windows installer**     |     仅支持使用集中部署机制的无提示安装，如组策略、Configuration Manager 和 Microsoft Intune。 <br><br>对于由 Intune 和移动设备管理 (MDM) 管理的 Windows 10 电脑而言，这是必要的方法，因为这些计算机不支持安装可执行文件。 <br><br> 但是，使用此安装方法时，必须手动检查并安装或卸载可执行文件的安装程序为每台计算机执行时依赖的软件。 <br><br>有关详细信息，请参阅 [使用 .msi 安装程序安装统一的标记客户端](#install-the-unified-labeling-client-using-the-msi-installer)。 |
|     |         |


安装 Azure 信息保护统一标签客户端之后，你可以通过重复所选的安装方法来更新此客户端，或者使用 Windows 更新来保持客户端自动升级。 

有关升级的详细信息，请参阅[升级和维护 Azure 信息保护客户端](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)部分。

## <a name="install-the-aip-unified-labeling-client-using-the-executable-installer"></a>使用可执行安装程序安装 AIP 统一标签客户端

使用以下说明来安装客户端时，使用的 *不* 是 Microsoft 更新目录或使用中心部署方法（如 Intune）[部署 **.msi**](#install-the-unified-labeling-client-using-the-msi-installer) 。

**使用 .exe 文件安装统一的标记客户端**：

1. 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载 Azure 信息保护统一标签客户端 (文件名 **AzInfoProtection_UL**) 的可执行版本。 
    
    > [!IMPORTANT]
    > 如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 
    >
 
1. 对于默认安装，只需运行可执行文件，例如 **AzInfoProtection_UL.exe**。 

    若要查看所有安装选项，请先通过 **/help** 运行可执行文件： `AzInfoProtection_UL.exe /help`

    例如： 
    - 若要以无提示方式安装客户端： `AzInfoProtection_UL.exe /quiet`
    
    - 若要以无提示方式安装 PowerShell cmdlet： `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    帮助屏幕中未列出的其他参数：
        
    |参数  |描述  |
    |---------|---------|
    |**AllowTelemetry = 0**     |    使用此参数来禁用安装选项“通过向 Microsoft 发送使用情况统计信息来帮助改进 Azure 信息保护”。     |
    |**ServiceLocation**     |  如果要在运行 Office 2010 的计算机上安装客户端，并且你的用户不是其计算机上的本地管理员，或者你不希望系统向他们发出提示，请使用此参数。 <br><br>**重要提示**： Office 2010 扩展支持于2020年10月13日结束。 有关详细信息，请参阅 [AIP 和旧版 Windows 和 Office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。 |
    | | |

1. 若要完成安装，请重新启动所有 Office 应用程序和文件资源管理器的所有实例。 

    > [!NOTE]
    > 如果计算机运行的是 [Office 2010](../known-issues.md#aip-and-legacy-windows-and-office-versions)，请重新启动计算机。 
    >
    > 如果未使用 **ServiceLocation** 参数安装客户端，则在首次打开使用 Azure 信息保护统一客户端 (（例如，Word) ）的某个 Office 应用程序时，必须在首次使用时确认要更新注册表的任何提示。 
    >
    > 利用[服务发现](client-deployment-notes.md#rms-service-discovery)功能填充注册表项。 
    > 
        
1. 检查安装日志文件（默认情况下在 **% temp%** 文件夹中创建），确认安装是否成功。 

    安装日志文件的命名格式如下： `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例如：**Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    在此日志文件中，搜索以下字符串： **Product： Microsoft Azure 信息保护--安装已成功完成**。 如果安装失败，此日志文件包含有助于标识并解决任何问题的详细信息。

    > [!TIP]
    > 可以用 **/log** 安装参数更改安装日志文件的位置。 
    >  
### <a name="more-information-about-the-servicelocation-installation-parameter"></a>详细了解 ServiceLocation 安装参数

当你为具有 [Office 2010](../known-issues.md#aip-and-legacy-windows-and-office-versions) 的用户安装客户端，并且这些用户没有本地管理权限时，请为你的 Azure Rights Management 服务指定 **SERVICELOCATION** 参数和 URL。 
    
> [!IMPORTANT]
> Office 2010 扩展支持于2020年10月13日结束。 有关详细信息，请参阅 [AIP 和旧版 Windows 和 Office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。
>

此参数和值将创建和设置以下注册表项：

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation`

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation`


**若要标识要为 ServiceLocation 参数指定的值**，请执行以下操作：

1. 在 PowerShell 会话中，首先运行 [AipService](/powershell/module/aipservice/connect-aipservice) 并指定管理员凭据以连接到 Azure Rights Management 服务。 然后运行 [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)。 
 
    如果尚未安装 Azure Rights Management 服务的 PowerShell 模块，请参阅 [安装 AIPService PowerShell 模块](../install-powershell.md)。

2. 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

    例如：LicensingIntranetDistributionPointUrl：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. 该值中，将 **/_wmcs/licensing** 从此字符串删除。 例如：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    剩余字符串就是要为 ServiceLocation 参数指定的值。

例如，若要以无提示方式安装 [Office 2010](../known-issues.md#aip-and-legacy-windows-and-office-versions) 和 Azure RMS 的客户端：

```powershell
AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
```


## <a name="install-the-unified-labeling-client-using-the-msi-installer"></a>使用 .msi 安装程序安装统一的标记客户端

对于中心部署，请使用特定于 Azure 信息保护统一标签客户端的 **.msi** 安装版本的下列信息。 

如果将 Intune 用于软件部署方法，请将这些说明与[使用 Microsoft Intune 添加应用](/mem/intune/apps/apps-add)一起使用。

**安装包含 .msi 文件的统一标签客户端**

1. 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载 Azure 信息保护统一标签客户端 (**AzInfoProtection_UL**) 的 **.msi** 版本。 
    
    > [!IMPORTANT]
    > 如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。
    > 

1. 对于运行 **.msi** 文件的每台计算机，必须确保以下软件依赖项已就位。 

    例如，将其打包为 **.msi** 版本的客户端，或仅部署到满足这些依赖项的计算机：
    
    |Office 版本|操作系统|软件|操作|
    |--------------------|--------------|----------------|---------------------|
    |**Office 365 1902 或更高版本之外的所有版本**|仅限于 Windows 10 版本 1809，操作系统内部版本早于 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|安装|
    |**Office 2016**|所有支持的版本|64 位：[KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 位：[KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> 版本：1.0|安装|
    |**Office 2013**|所有支持的版本|64 位：[KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 位：[KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />版本：1.0|安装|
    |[**Office 2010**](../known-issues.md#aip-and-legacy-windows-and-office-versions)|所有支持的版本|[Microsoft Online Services 登录助手](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> 版本：2.1|安装|
    |[**Office 2010**](../known-issues.md#aip-and-legacy-windows-and-office-versions)|Windows 8.1 和 Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|如果未安装 KB2843630 或 KB2919355，则进行安装|
    |[**Office 2010**](../known-issues.md#aip-and-legacy-windows-and-office-versions)|Windows 8 和 Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> 文件名中包含的版本号：v3|安装|
    | | | | |

    > [!IMPORTANT]
    > Office 2010 扩展支持于2020年10月13日结束。 有关详细信息，请参阅 [AIP 和旧版 Windows 和 Office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。
    >

1. 对于默认安装，将 .msi 与 /quiet/ 一起运行，例如，`AzInfoProtection_UL.msi /quiet`。

    可能需要指定其他安装参数。 有关详细信息，请参阅 [可执行安装程序说明](#install-the-aip-unified-labeling-client-using-the-executable-installer)。

    > [!NOTE]
    > 默认情况下，启用 " **通过将使用情况统计信息发送到 Microsoft 安装" 选项来帮助改进 Azure 信息保护** 。 若要禁用此选项，请确保执行下列操作之一：
    >
    >- 在安装过程中，指定 **AllowTelemetry = 0**
    >- 安装后，按如下所示更新注册表项： **EnableTelemetry = 0**。
    >

## <a name="next-steps"></a>后续步骤
现在，已安装 Azure 信息保护统一标签客户端，请参阅以下内容，了解支持此客户端所需的其他信息：

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)