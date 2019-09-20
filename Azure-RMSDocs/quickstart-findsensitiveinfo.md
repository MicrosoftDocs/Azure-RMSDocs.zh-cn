---
title: 快速入门 - 使用 Azure 信息保护扫描程序查找敏感信息
description: 使用 Azure 信息保护扫描程序查找在本地存储的文件中的敏感信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/17/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 5b8ca224dff45fcb589a888ef1fa0728ccebe368
ms.sourcegitcommit: 908ca5782fe86e88502dccbd0e82fa18db9b96ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71060203"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>快速入门：查找在本地存储的文件中的敏感信息

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明： *[适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

本快速入门教程介绍如何安装和配置 Azure 信息保护扫描程序，以查找存储在本地数据存储中的文件中的敏感信息。 例如，本地文件夹、网络共享或 SharePoint Server。

注意：本快速入门使用扫描程序的当前通用版本（使用 Azure 门户进行配置），而不是早期版本使用的 PowerShell cmdlet。

在 10 分钟内即可完成此配置。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要具备以下条件：

1. 包含 Azure 信息保护计划 1 或计划 2 的订阅。
    
    如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

2. 计算机上已安装 Azure 信息保护客户端（经典）。 
    
    可以转到 [Microsoft下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection.exe  ，安装客户端。
    
3. 计算机上同时安装了 SQL Server Express。
    
    如果尚未安装此 SQL Server 版本，可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express)进行下载，并选择基本安装。

4. 你的域帐户已同步到 Azure AD。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

## <a name="prepare-a-test-folder-and-file"></a>准备测试文件夹和文件

执行初始测试以确认扫描程序正常工作：

1. 在计算机上创建一个本地文件夹。 例如，在本地 C 驱动器上创建 TestScanner  。

2. 在该文件夹中创建一个 Word 文档并保存它，该文件夹包含文本“4242-4242-4242-4242”  （用于测试的已知信用卡号）。

## <a name="configure-a-profile-for-the-scanner"></a>配置扫描程序的配置文件

在安装扫描程序之前，在 Azure 门户中为其创建一个配置文件。 此配置文件包含扫描程序设置以及要扫描的数据存储库的位置。

1. 打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”  边栏选项卡。 
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”   。 选择“Azure 信息保护”。 
    
2. 找到“扫描程序”  菜单选项，然后选择“配置文件”  。

3. 在“Azure 信息保护 - 配置文件”  边栏选项卡上，选择“添加”  ：
    
    ![添加 Azure 信息保护扫描程序的配置文件](./media/scanner-add-profile.png)

4. 在“添加新配置文件”  边栏选项卡上，指定扫描程序的名称，该名称用于标识扫描程序的配置设置和要扫描的数据存储库。 例如，对于本快速入门，可以指定“快速入门”  。 以后安装扫描程序时，将需要指定相同的配置文件名称。
    
    （可选）指定用于管理的说明，以帮助识别扫描程序的配置文件名称。

5. 找到“策略实施”  部分，在此快速入门中，只选择一个设置：对于“实施”  ，选择“关闭”  。 然后，选择“保存”  ，但不要关闭边栏选项卡。
    
    这些设置将扫描程序配置为对指定数据存储库中的所有文件进行一次性发现。 此扫描操作会查找所有已知的敏感信息类型，不必首先配置 Azure 信息保护标签或策略设置。

6. 现在已创建并保存配置文件，即可返回到“配置存储库”  选项以将本地文件夹指定为要扫描的数据存储。
    
    仍在“添加新配置文件”  边栏选项卡上，选择“配置存储库”  以打开“存储库”  边栏选项卡：
    
    ![为 Azure 信息保护扫描程序配置数据存储库](./media/scanner-repositories-bar.png)

7. 在“存储库”  边栏选项卡上，选择“添加”  ：
    
    ![为 Azure 信息保护扫描程序添加数据存储库](./media/scanner-repository-add.png)

8. 在“存储库”  边栏选项卡上，指定第一步中创建的本地文件夹。 例如：`C:\TestScanner`
    
    对于此边栏选项卡上的其余设置，请不要更改它们，而是将其保留为“配置文件默认值”  。 这意味着数据存储库从扫描程序配置文件继承设置。 
    
    选择“保存”  。

9. 返回到“Azure 信息保护 - 配置文件”  边栏选项卡，现在将看到列出的配置文件，同时“计划”  列显示“手动”  且“实施”  列为空。 
    
    “节点”  列显示“0”  ，因为尚未为此配置文件安装扫描程序。

现在可随时使用刚刚创建的扫描程序配置文件安装扫描程序。

## <a name="install-the-scanner"></a>安装扫描程序

1. 使用“以管理员身份运行”  选项打开 PowerShell 会话。

2. 使用以下命令安装扫描程序，指定自己的计算机名称以及 Azure 门户中保存的配置文件名称：
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS -Profile <profile name>
    
    出现提示时，请使用 \<域\用户名> 格式，然后使用密码为扫描程序提供自己的凭据。 

## <a name="start-the-scan-and-confirm-it-finished"></a>开始扫描并确认扫描完成

1. 返回 Azure 门户，刷新“Azure 信息保护 - 配置文件”  边栏选项卡，此时应看到“节点”  列现在显示“1”  。

2. 选择配置文件名称，然后选择“立即扫描”  选项：
    
    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)
    
    如果在选择配置文件后，此选项不可用，则扫描程序不会连接到 Azure 信息保护。 查看配置和 Internet 连接。

3. 只有一个小文件需要检查，因此初始测试扫描速度非常快：
    
    请稍候，直到看到“上次扫描结果”  和“上次扫描（结束时间）”  列显示的值。
    
    - 或者，查看本地 Windows 应用程序和服务  事件日志和 Azure 信息保护  。 确认 MSIP.Scanner  进程的信息事件 ID 911  。 事件日志条目还包含扫描结果的摘要。

## <a name="see-detailed-results"></a>查看详细结果

使用文件在医院管理器，在 %localappdata  %\Microsoft\MSIP\Scanner\Reports 中找到扫描程序报告。 打开 .csv 文件格式的详细报告文件。

在 Excel 中，前两列显示数据存储的存储库和文件名。 在查看列时，可以看到一个名为“信息类型名称”  的列，这是你最感兴趣的列。 在我们的初始测试中，它显示“信用卡号”  ，这是扫描程序可以找到的许多敏感信息类型之一。

## <a name="scan-your-own-data"></a>扫描自己的数据

1. 编辑扫描程序配置文件并添加新的数据存储库，这次指定要扫描敏感信息的本地数据存储。 
    
    可以为 SharePoint 站点或库指定本地文件夹，网络共享（UNC 路径）或 SharePoint Server URL。 
    
    - 本地文件夹的示例：
        
            D:\Data\Finance
    
    - 网络共享的示例
        
            \\NAS\HR
    
    - SharePoint 文件夹的示例：
        
            http://sp2016/Shared Documents

2. 再次重启扫描程序：在“Azure 信息保护 - 配置文件”  边栏选项卡上，确保选中配置文件，然后选择“立即扫描”  选项：
    
    ![启动 Azure 信息保护扫描程序扫描](./media/scanner-scan-now.png)

3. 扫描完成后，查看新的结果。 
    
    扫描需要的时间取决于数据存储中的文件数量、文件大小以及文件类型。 

## <a name="clean-up-resources"></a>清理资源

在生产环境中，将使用对 Azure 信息保护服务进行无提示身份验证的服务帐户在 Windows Server 上运行扫描程序。 同时还使用企业级版本的 SQL Server，并可能指定多个数据存储库。 

若要清理资源，为该生产部署做好准备，请在 PowerShell 会话中运行以下命令以卸载扫描程序：

    Uninstall-AIPScanner

然后重新启动计算机。

此命令不会删除以下项目，如果你在学习本快速入门教程后不需要使用这些项目，必须手动删除它们：

- 安装 Azure 信息保护扫描程序时通过运行 Install-AIPScanner cmdlet 创建的名为“AIPScanner_\<profile>”  的 SQL Server 数据库。 

- 位于 %localappdata  %\Microsoft\MSIP\Scanner\Reports 中的扫描程序报告。

- 向域帐户授予的针对本地计算机的“作为服务登录”  用户权限分配。


## <a name="next-steps"></a>后续步骤

本快速入门教程包括最低配置，使用户可以快速查看扫描程序如何在本地数据存储中查找敏感信息。 如果你已准备好在生产环境中安装扫描程序，请参阅[部署 Azure 信息保护扫描程序以自动分类和保护文件](deploy-aip-scanner.md)。

如果要对包含敏感信息的文件进行分类和保护，必须配置 Azure 信息保护标签以实现自动分类和保护：

- [如何配置 Azure 信息保护的自动和建议分类的条件](configure-policy-classification.md)

- [如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)
