---
title: 快速入门 - 使用 Azure 信息保护扫描程序查找敏感信息
description: 使用 Azure 信息保护扫描程序查找在本地存储的文件中的敏感信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 04e114e6b719288a26663bd5534af4b1f1b73ac8
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91587875"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>快速入门：查找在本地存储的文件中的敏感信息

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：[适用于 Windows 的 Azure 信息保护经典客户端或统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

本快速入门将介绍如何使 SharePoint 允许扫描，以及安装和配置 Azure 信息保护扫描程序，以查找存储在本地数据存储中的任何敏感数据。

所需时间：在 15 分钟内即可完成此配置。

## <a name="prerequisites"></a>必备条件

若要完成本快速入门，你需要：

|要求  |说明  |
|---------|---------|
|支持订阅     |  你将需要包含 [Azure 信息保护计划 1 或计划 2](https://azure.microsoft.com/pricing/details/information-protection/) 的订阅。 </br></br>如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。       |
|客户端已安装    |   你将需要在计算机上安装经典客户端或统一标记客户端。 </br></br>- 若要安装统一标记客户端，请转到 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection_UL.exe。 </br>- 若要部署 AIP 经典客户端，请打开支持票证以获取下载访问权限。       |
|SQL Server Express     | 你将需要在计算机上安装 SQL Server Express。 </br></br> 若要安装，请转到 [Microsoft 下载中心](https://www.microsoft.com/sql-server/sql-server-editions-express)，然后在“快速”选项下选择“立即下载”。 在安装程序中，选择“基本”安装类型。        |
|Azure AD     |  你的域帐户必须同步到 Azure AD。 </br></br>如果你不确定你的帐户，请联系你的系统管理员。      |
|**SharePoint 访问**     | 若要启用 SharePoint 扫描，你将需要 SharePoint 策略的访问权限和权限。 |
| | |

## <a name="prepare-a-test-folder-and-file"></a>准备测试文件夹和文件

执行初始测试以确认扫描程序正常工作：

1. 在可访问的网络共享上创建新文件夹。 例如，将此文件夹命名为 TestScanner。

1. 在该文件夹中创建一个 Word 文档并保存它，该文件夹包含文本“信用卡：4242-4242-4242-4242”。

## <a name="permission-users-to-scan-sharepoint-repositories"></a>许可用户扫描 SharePoint 存储库

若要跨 SharePoint 存储库使用扫描程序，请为 Azure 信息保护指定站点 URL，以发现该 URL 下的所有站点并进行扫描。

若要实现跨存储库扫描，请为要用于扫描的用户添加以下 SharePoint 权限：

1. 打开 SharePoint，选择“权限策略”，然后选择“添加权限策略级别”。

    ![为特定用户创建新的权限策略级别](./media/aip-quick-set-sp-permissions.png)

1. 在“网站集权限”下，选择“网站收集器审核程序”选项。

1. 在“权限”下，为“查看应用程序页面”选项选择“授权”，然后选择“保存”更改。  

    ![为特定用户选择网站收集器审核程序和权限选项](./media/aip-quick-set-site-permissions.png)

1. 确认更改后，在打开的“Web 应用程序策略”消息中单击“确定”。

1. 在“添加用户”页面的“选择用户”字段中，添加要用于扫描的用户。 在“选择权限”下，选择“网站集”选项，然后单击“完成”，将创建的权限应用于已添加或选择的用户。

    ![向新权限选项添加用户](./media/aip-quick-set-user-permissions.png)

## <a name="configure-a-profile-for-the-scanner"></a>配置扫描程序的配置文件

在安装扫描程序之前，在 Azure 门户中为其创建一个配置文件。 此配置文件包含扫描程序设置以及要扫描的数据存储库的位置。

1. 打开新的浏览器窗口，[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”窗格。

    例如，在资源、服务和文档的搜索框中：开始键入“信息”并选择“Azure 信息保护”。

1. 在左侧窗格中找到“扫描程序”选项，然后选择“配置文件” 。

1. 在“Azure 信息保护 - 配置文件”窗格上，选择“添加”：

    :::image type="content" source="media/scanner-add-profile.png" alt-text="添加 Azure 信息保护扫描程序的配置文件":::

1. 在“添加新配置文件”窗格上，指定扫描程序的名称，该名称用于标识扫描程序的配置设置和要扫描的数据存储库。 例如，对于本快速入门，可以指定“快速入门”。 以后安装扫描程序时，将需要指定相同的配置文件名称。

    （可选）指定用于管理的说明，以帮助识别扫描程序的配置文件名称。

1. 找到“策略实施”部分，在此快速入门中，只选择一个设置：对于“实施”，选择“关闭”。 然后，选择“保存”，但不要关闭窗格。

    这些设置将扫描程序配置为对指定数据存储库中的所有文件进行一次性发现。 此扫描操作会查找所有已知的敏感信息类型，不必首先配置 Azure 信息保护标签或策略设置。

1. 现已创建并保存配置文件，接下来你可返回到“配置存储库”选项，将网络文件夹指定为要扫描的数据存储。

    仍在“添加新配置文件”窗格上，选择“配置存储库”以打开“存储库”窗格：

    :::image type="content" source="./media/scanner-repositories-bar.png" alt-text="添加 Azure 信息保护扫描程序的配置文件":::

1. 在“存储库”窗格上，选择“添加”：

    :::image type="content" source="media/scanner-repository-add.png" alt-text="添加 Azure 信息保护扫描程序的配置文件":::

1. 在“存储库”窗格上，指定之前创建的文件夹。 例如：`\\server\TestScanner`

    对于此窗格上的其余设置，请不要进行更改，而是将其保留为配置文件默认设置，这意味着数据存储库将从扫描程序配置文件继承设置。

    选择“保存”。

1. 返回到“Azure 信息保护 - 配置文件”窗格，现在将看到列出的配置文件，同时“计划”列显示“手动”且“实施”列为空。

    “节点”列显示“0”，因为尚未为此配置文件安装扫描程序 。

现在可随时使用已创建的扫描程序配置文件安装扫描程序。

## <a name="install-the-scanner"></a>安装扫描程序

1. 使用“以管理员身份运行”选项打开 PowerShell 会话。

1. 使用以下命令安装扫描程序，指定你的网络共享的名称和你保存在 Azure 门户中的配置文件名称：

    ```ps
    Install-AIPScanner -SqlServerInstance <your network share name>\SQLEXPRESS -Profile <profile name>
    ```

    出现提示时，请使用 \<domain\user name> 格式，然后使用密码为扫描程序提供自己的凭据。

## <a name="start-the-scan-and-confirm-it-finished"></a>开始扫描并确认扫描完成

1. 返回 Azure 门户，刷新“Azure 信息保护 - 配置文件”窗格，此时应看到“节点”列现在显示“1”。

1. 选择配置文件名称，然后选择“立即扫描”选项：

    :::image type="content" source="media/scanner-scan-now.png" alt-text="添加 Azure 信息保护扫描程序的配置文件":::

    如果在选择配置文件后，此选项不可用，则扫描程序不会连接到 Azure 信息保护。 查看配置和 Internet 连接。

1. 只有一个小文件需要检查，因此初始测试扫描速度很快：

    请稍候，直到看到“上次扫描结果”和“上次扫描（结束时间）”列显示的值。

> [!TIP]
> 或者，仅对于经典客户端中的扫描程序：
>
> 查看本地 Windows 应用程序和服务事件日志和 Azure 信息保护。 确认 MSIP.Scanner 进程的信息事件 ID 911。 事件日志条目还包含扫描结果的摘要。
>
## <a name="see-detailed-results"></a>查看详细结果

使用文件资源管理器，在 %localappdata%\Microsoft\MSIP\Scanner\Reports 中找到扫描程序报告。 打开 .csv 文件格式的详细报告文件。

在 Excel 中：

- 前两列显示数据存储的存储库和文件名。
- 在查看列时，可以看到一个名为“信息类型名称”的列，这是你最感兴趣的列。

    在我们的初始测试中，它显示“信用卡号”，这是扫描程序可以找到的许多敏感信息类型之一。

## <a name="scan-your-own-data"></a>扫描自己的数据

1. 编辑扫描程序配置文件并添加新的数据存储库，这次指定要扫描敏感信息的本地数据存储。

    为 SharePoint 站点或库指定网络共享（UNC 路径）或 SharePoint Server URL。

    例如：

    - 对于网络共享：`\\NAS\HR`
    - 对于 SharePoint 文件夹：`http://sp2016/Shared Documents`

1. 再次重启扫描程序。

    在“Azure 信息保护 - 配置文件”窗格上，确保选中配置文件，然后选择“立即扫描”选项：

    :::image type="content" source="media/scanner-scan-now.png" alt-text="添加 Azure 信息保护扫描程序的配置文件":::

1. 扫描完成后，查看新的结果。

    扫描需要的时间取决于数据存储中的文件数量、文件大小以及文件类型。

## <a name="clean-up-resources"></a>清理资源

在生产环境中，将使用对 Azure 信息保护服务进行无提示身份验证的服务帐户在 Windows Server 上运行扫描程序。 同时还使用企业级版本的 SQL Server，并可能指定多个数据存储库。

若要清理资源并准备好系统用于生产部署，请在 PowerShell 会话中运行以下命令以卸载扫描程序：

```ps
Uninstall-AIPScanner
```

然后重新启动计算机。

此命令不会删除以下项目，如果你在学习本快速入门教程后不需要使用这些项目，必须手动删除它们：

- 安装 Azure 信息保护扫描程序时通过运行 Install-AIPScanner cmdlet 创建的 SQL Server 数据库：

    - 对于经典客户端：AIPScanner_\<profile>
    - 对于统一标签客户端：AIPScannerUL_\<profile_name>

- 位于 %localappdata%\Microsoft\MSIP\Scanner\Reports 中的扫描程序报告。

- 向域帐户授予的针对本地计算机的“作为服务登录”用户权限分配。

## <a name="next-steps"></a>后续步骤

本快速入门教程包括最低配置，使用户可以快速查看扫描程序如何在本地数据存储中查找敏感信息。 如果你已准备好在生产环境中安装扫描程序，请参阅[部署 Azure 信息保护扫描程序以自动分类和保护文件](deploy-aip-scanner.md)。

如果要对包含敏感信息的文件进行分类和保护，必须配置标签以实现自动分类和保护：

对于经典客户端：

- [如何配置 Azure 信息保护的自动和建议分类的条件](configure-policy-classification.md)
- [如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)

对于统一标记客户端：

- [将敏感度标签自动应用到内容](/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [通过在敏感度标签中使用加密来限制对内容的访问](/microsoft-365/compliance/encryption-sensitivity-labels)