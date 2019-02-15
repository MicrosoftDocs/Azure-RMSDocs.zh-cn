---
title: 快速入门教程 - 使用 Azure 信息保护扫描程序查找文件中的敏感信息 - AIP
description: 使用 Azure 信息保护扫描程序查找在本地存储的文件中的敏感信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/15/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 07baee062d994b6efd97084bf0b293adb2d5fb84
ms.sourcegitcommit: 89d2c2595bc7abda9a8b5e505b7dcf963e18c822
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56266006"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>快速入门：查找在本地存储的文件中的敏感信息

>适用于：*[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*

本快速入门教程介绍如何安装和配置 Azure 信息保护扫描程序，以查找存储在本地数据存储中的文件中的敏感信息。 例如，本地文件夹、网络共享或 SharePoint Server。

注意：本快速入门使用扫描程序的当前通用版本而不是使用 Azure 门户进行配置的预览版本。

在 10 分钟内即可完成此配置。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要具备以下条件：

1. 包含 Azure 信息保护计划 1 或计划 2 的订阅。
    
    如果没有上述任一订阅，可以为组织创建一个[免费](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

2. 计算机上已安装 Azure 信息保护客户端。 
    
    可以转到 [Microsoft下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection.exe，安装客户端。
    
3. 计算机上同时安装了 SQL Server Express。
    
    如果尚未安装此 SQL Server 版本，可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express)进行下载，并选择基本安装。

4. 你的域帐户已同步到 Azure AD。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

## <a name="prepare-a-test-folder-and-file"></a>准备测试文件夹和文件

执行初始测试以确认扫描程序正常工作：

1. 在计算机上创建一个本地文件夹。 例如，在本地 C 驱动器上创建 TestScanner。

2. 在该文件夹中创建一个 Word 文档并保存它，该文件夹包含文本“4242-4242-4242-4242”（用于测试的已知信用卡号）。

## <a name="install-the-scanner"></a>安装扫描程序

1. 使用“以管理员身份运行”选项打开 PowerShell 会话。

2. 使用以下命令安装扫描程序，指定你自己的计算机名：
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS
    
    出现提示时，请使用 \<域\用户名> 格式，然后使用密码为扫描程序提供自己的凭据。 

## <a name="specify-your-test-data-store"></a>指定测试数据存储区

在 PowerShell 会话中，键入以下命令：

    Add-AIPScannerRepository -Path C:\TestScanner

## <a name="configure-the-scanner-to-discover-all-information-types"></a>配置扫描程序以发现所有信息类型

在 PowerShell 会话中，键入以下命令：

    Set-AIPScannerConfiguration -Enforce Off -Schedule Manual -DiscoverInformationTypes All

此命令将扫描程序配置为对指定数据存储库中的所有文件进行一次性发现。 此扫描操作会查找所有已知的敏感信息类型，不必首先配置 Azure 信息保护标签或策略设置。

## <a name="start-the-scan-and-confirm-it-finished"></a>开始扫描并确认扫描完成

1. 在 PowerShell 会话中，键入以下命令以启动扫描程序：
    
        Start-AIPScan
    
    只有一个小文件需要检查，因此初始测试扫描速度非常快。 

2. 转到 Windows“事件查看器” > “应用程序和服务” > “Azure 信息保护”事件日志。 
    
    确认 Azure 信息保护显示 MSIP.Scanner 进程的信息事件 ID 911。 事件日志条目还包含扫描结果的摘要。

## <a name="see-detailed-results"></a>查看详细结果

使用文件在医院管理器，在 %localappdata%\Microsoft\MSIP\Scanner\Reports 中找到扫描程序报告。 打开 .csv 文件格式的详细报告文件。

在 Excel 中，前两列显示数据存储的存储库和文件名。 在查看列时，可以看到一个名为“信息类型名称”的列，这是你最感兴趣的列。 在我们的初始测试中，它显示“信用卡号”，这是扫描程序可以找到的许多敏感信息类型之一。

## <a name="scan-your-own-data"></a>扫描自己的数据

1. 再次运行 Add-AIPScannerRepository，这次指定要扫描敏感信息的本地数据存储。 
    
    可以为 SharePoint 站点或库指定本地文件夹，网络共享（UNC 路径）或 SharePoint Server URL。 
    
    - 本地文件夹的示例：
        
            Add-AIPScannerRepository -Path D:\Data\Finance
    
    - 网络共享的示例
        
            Add-AIPScannerRepository -Path \\NAS\HR
    
    - SharePoint 文件夹的示例：
        
            Add-AIPScannerRepository -Path "http://sp2016/Shared Documents"

2. 重新启动扫描程序：
    
        Start-AIPScan

3. 扫描完成后，查看新的结果。 
    
    扫描需要的时间取决于数据存储中的文件数量、文件大小以及文件类型。 

## <a name="clean-up-resources"></a>清理资源

在生产环境中，将使用对 Azure 信息保护服务进行无提示身份验证的服务帐户在 Windows Server 上运行扫描程序。 同时还使用企业级版本的 SQL Server，并可能指定多个数据存储库。 

若要清理资源，为该生产部署做好准备，请在 PowerShell 会话中运行以下命令以卸载扫描程序：

    Uninstall-AIPScanner

然后重新启动计算机。

此命令不会删除以下项目，如果你在学习本快速入门教程后不需要使用这些项目，必须手动删除它们：

- 安装 Azure 信息保护扫描程序时通过运行 Install-AIPScanner cmdlet创建的名为“AzInfoProtection”的 SQL Server 数据库。 

- 位于 %localappdata%\Microsoft\MSIP\Scanner\Reports 中的扫描程序报告。

- 向域帐户授予的针对本地计算机的“作为服务登录”用户权限分配。


## <a name="next-steps"></a>后续步骤

本快速入门教程包括最低配置，使用户可以快速查看扫描程序如何在网络共享中查找敏感信息。 如果你已准备好在生产环境中安装扫描程序，请参阅[部署 Azure 信息保护扫描程序以自动分类和保护文件](deploy-aip-scanner.md)。

如果要对包含敏感信息的文件进行分类和保护，必须配置 Azure 信息保护标签以实现自动分类和保护：

- [如何配置 Azure 信息保护的自动和建议分类的条件](configure-policy-classification.md)

- [如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
