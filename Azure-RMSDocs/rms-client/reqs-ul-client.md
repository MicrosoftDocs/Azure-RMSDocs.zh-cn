---
title: 安装 Azure 信息保护统一标签客户端的其他要求
description: 针对需要了解在企业网络上安装统一标签客户端的其他系统要求的管理员的信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c93b0a338f25b058e517c4c2bb746ccaa6e41a69
ms.sourcegitcommit: 0ac52ea741f205692406f0f82c74c65c23ee3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/27/2020
ms.locfileid: "97792307"
---
# <a name="additional-requirements-for-installing-the-unified-labeling-client-on-enterprise-networks"></a>在企业网络上安装统一标签客户端的其他要求

>***适用于**： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，Windows 8，Windows Server 2019，Windows Server 2016，windows Server 2012 R2，windows server 2012 *
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP For Windows And office 版本中的扩展支持](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。*
>
>***适用于以下内容的说明**： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [经典客户端管理员指南](client-admin-guide-install.md)。 *

在企业网络上安装 Azure 信息保护统一标签客户端之前，请检查计算机是否具有 Azure 信息保护所需的操作系统版本和应用程序： [Azure 信息保护的要求](../requirements.md)。 

然后，验证你是否具有安装 Azure 信息保护统一标签客户端所需的附加项。

> [!NOTE]
> 并非所有这些要求都由安装软件验证。
>

## <a name="microsoft-net-framework-requirements"></a>Microsoft .NET Framework 要求

默认情况下，默认情况下，Azure 信息保护统一标签客户端完全安装需要 Microsoft .NET Framework 4.6.2 的最低版本。 

如果缺少此框架，则可执行安装程序中的安装向导将尝试下载并安装此必备组件。 在客户端安装过程中安装此必备项后，将重启计算机。  

如果要自行安装 [Azure 信息保护查看器](clientv2-view-use-files.md) ，则必须具有最低版本的 Microsoft .NET Framework 4.5.2。 

> [!IMPORTANT]
> 如果查看器安装缺少 Microsoft .NET Framework 4.5.2 的最低版本，则安装 *软件不会下载或* 安装该软件。
> 

### <a name="disable-exploit-protection-net-2-or-3-only"></a>禁用 Exploit protection ( 仅限 .NET 2 或 3) 

使用启用了 [Exploit protection](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) 的 .net 2 或3的计算机不支持 AIP 客户端。 

在这种情况下，我们建议升级 .NET 版本。 

如果必须保留 .NET 版本2或3，请在安装 AIP 客户端之前确保 [禁用 Exploit protection](../known-issues.md#known-issues-for-aip-and-exploit-protection) 。

## <a name="windows-powershell-minimum-requirements"></a>Windows PowerShell 最低要求

适用于客户端的 PowerShell 模块需要最低版本的 Windows PowerShell 4.0。

如果正在使用较旧的操作系统，可能需要手动 insall PowerShell。 有关详细信息，请参阅[如何：安装 Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)。 

> [!IMPORTANT]
> 安装 *程序不会检查或* 安装此必备组件。 
>
> 若要确认正在运行的 Windows PowerShell 的版本，请在 PowerShell 会话中键入 `$PSVersionTable`。  
> 


## <a name="screen-resolution-requirements"></a>屏幕分辨率要求

当你在文件资源管理器中右键单击文件或文件夹时，分辨率为 **800x600** 或更低的客户端计算机无法完全显示 " **分类和保护-Azure 信息保护** " 对话框。   

## <a name="admin-permissions"></a>管理员权限

若要安装 Azure 信息保护统一标签客户端，你必须对客户端计算机具有本地管理权限。
        
## <a name="windows-10-requirements"></a>Windows 10 要求

运行 Office 2010 的计算机需要 **Microsoft Online Services 登录助手版本 7.250.4303.0**，此版本包含在客户端安装中。 

如果有登录助手的更高版本，请先卸载它，然后再安装 Azure 信息保护统一标签客户端。 

例如，通过使用 **"控制面板" "**  >  **程序和功能**"  >  **卸载或更改程序** 来检查版本并卸载登录助手。 

仅适用于 Windows 10 版本 1809，操作系统内部版本早于 17763.348，安装 [2019 年 3 月 1 日—KB4482887 (OS 内部版本 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) 以确保信息保护栏在 Office 应用程序中正确显示。 如果已有 Office 365 1902 或更高版本，则不需要此更新。    

## <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>配置组策略以阻止禁用 AIP

对于 Office 版本2013及更高版本，建议配置组策略，以确保始终启用适用于 Office 应用程序的 **Microsoft Azure 信息保护** 外接程序。  如果没有此外接程序，用户将无法在 Office 应用程序中标记其文档或电子邮件。   

对于 Word、Excel、PowerPoint 和 Outlook，使用 [由于 Office 2013 和 office 2016 程序的组策略设置](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)中所述的 **托管外** 接程序的组策略设置列表。 

为 AIP 指定 (ProgID) 的以下编程标识符，并将选项设置为 **1：始终启用外接程序**。

|应用程序  |ProgID  |
|---------|---------|
|Word     |     `MSIP.WordAddin`    |
|Excel     |  `MSIP.ExcelAddin`       |
|PowerPoint     |   `MSIP.PowerPointAddin`      |
|Outlook | `MSIP.OutlookAddin` |
| | | 
    

## <a name="next-steps"></a>后续步骤

继续  [管理指南：为用户安装 Azure 信息保护统一标签客户端](clientv2-admin-guide-install.md)。

有关详细信息，请参阅：

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)