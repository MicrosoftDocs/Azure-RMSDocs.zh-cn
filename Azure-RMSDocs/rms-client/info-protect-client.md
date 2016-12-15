---
title: "安装 Azure 信息保护客户端 | Azure 信息保护"
description: "有关安装客户端（将信息保护栏添加到 Office 应用程序）以便为文档和电子邮件选择分类标签的说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 23c437479c756f2a9335606e686f117d514a38f6
ms.openlocfilehash: 71972b0a057b1958dfa5e5b4af41b65d5080a086


---

# <a name="installing-the-azure-information-protection-client"></a>安装 Azure 信息保护客户端

>*适用于：Azure 信息保护*

若要使用 Azure 信息保护对文档和电子邮件进行分类，必须首先安装 Azure 信息保护客户端。 此安装将信息保护栏添加到 Office 应用程序（Word、Excel、PowerPoint、Outlook）以显示组织的分类标签，而且“**主页**”选项卡（Word、Excel、PowerPoint）上的新“**保护**”组具有名为“**保护**”的按钮：

下图显示了此信息保护栏和 [默认策略](../deploy-use/configure-policy-default.md)(#默认策略) 中的标签：

![具有默认策略的 Azure 信息保护栏](../media/info-protect-bar-default.png)

从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)(#microsoft-下载中心) 下载 Azure 信息保护客户端。 目前可安装正式 (GA) 版和预览版。 预览版包括用于评估的新功能，随时有可能更改。 有关详细信息，请参阅以下博客文章公告：[Azure 信息保护 12 月预览版现已可用](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/)

安装客户端之前，请检查是否具有 Azure 信息保护客户端所需的操作系统版本和应用程序：[Azure 信息保护要求](../get-started/requirements-azure-rms.md)。 此外，对于客户端的预览版本，运行 Windows 7 SP1 的计算机需要 [KB 2533623](https://support.microsoft.com/en-us/kb/2533623)，其可在安装客户端后安装。 如果需要此更新但尚未安装，系统会提示你进行安装。

## <a name="to-install-the-azure-information-protection-client-manually"></a>手动安装 Azure 信息保护客户端

1. [下载客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)后，运行可执行文件，例如 **AzInfoProtection.exe** 并按照提示安装客户端。 此安装需要本地管理权限。

    如果无法连接到 Office 365 或 Azure Active Directory，但想要通过使用本地策略看到和体验 Azure 信息保护的客户端以用于演示目的，选择此选项以安装演示策略。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。 

2. 开始使用 Azure 信息保护客户端：如果计算机运行 Office 2010，请重新启动计算机。 对于其他版本的 Office，重新启动任何 Office 应用程序。

## <a name="to-install-the-azure-information-protection-client-for-users"></a>为用户安装 Azure 信息保护客户端

可以编写脚本，并通过使用命令行选项自动安装 Azure 信息保护客户端。 若要查看安装选项，请使用 **/help** 运行可执行文件。 例如：`AzInfoProtection.exe /help`。

以无提示方式安装客户端的示例：`AzInfoProtection.exe /passive | quiet`

Microsoft 更新目录中也包含 Azure 信息保护客户端的正式版，因此可以通过使用该目录的任何软件更新服务来安装和更新客户端。 客户端的预览版不包括在 Microsoft 更新目录中。

## <a name="to-uninstall-the-azure-information-protection-client"></a>卸载 Azure 信息保护客户端

可以使用以下任何选项：

- 使用控制面板卸载程序：单击“**Microsoft Azure 信息保护** > **卸载**”

- 重新运行可执行文件（如 **AzInfoProtection.exe**），并从“修改安装程序”页上，单击“卸载”。 

- 使用 **/uninstall** 运行可执行文件。 例如： `AzInfoProtection.exe /uninstall`


## <a name="to-verify-installation-connection-status-or-report-a-problem"></a>验证安装、连接状态或报告问题

1. 打开 Office 应用程序，在“**主页**”选项卡的“**保护**”组中单击“**保护**”，然后单击“**帮助和反馈**”。

2. 在“**Microsoft Azure 信息保护**”对话框中，注意以下各项：

    - 在“客户端状态”部分：使用“版本”值来验证安装是否成功。 此外，还会看到客户端上一次连接到组织的 Azure 信息保护服务的时间，以及上一次安装或更新 Azure 信息保护策略的时间。 当客户端连接到该服务时，如果它发现其当前策略中存在更改，它会自动下载最新的策略。 如果在显示时间后完成策略更改，关闭并重新打开 Office 应用程序。
    
        还可以看到标识用于向 Azure 信息保护进行身份验证的帐户的显示用户名。 此用户名必须与用于 Office 365 或 Azure Active Directory 的帐户，以及属于为 Azure 信息保护所配置的某个租户的帐户相匹配。

    - 在“帮助和反馈”部分中：**告诉我详细信息链接**默认转到 [Azure 信息保护](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection)网站；但作为 Azure 信息保护策略中的一个[策略设置](../deploy-use/configure-policy-settings.md)，它也可配置为自定义 URL。
        
        使用**发送反馈**链接，自动将客户端日志附加到电子邮件以发送到信息保护团队进行问题调查。 
    
        若要获取诊断信息以及重置客户端，请单击“运行诊断”。 诊断测试完成后，单击“复制结果”将信息粘贴到电子邮件中，以发送给支持人员或 Microsoft 支持部门。 测试完成后，还可以重置客户端。
        
        有关“重置”选项的详细信息：
        
        - 不是本地管理员也能使用此选项，并且不会在事件查看器中记录此操作。 
        
        - 除非文件被锁定，否则此操作将删除 **%localappdata%\Microsoft\MSIPC** 中的所有文件，该路径用于存储客户端证书和权限管理模板。 此操作不会删除 Azure 信息保护策略或客户端日志文件，也不会注销用户。
        
        - 会删除以下注册表项和设置：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**。 如果为此注册表项配置设置（例如，由于要从 AD RMS 迁移并且网络上仍有服务连接点，因此配置用于重定向到 Azure 信息保护租户的设置），那么重置客户端后必须重新配置注册表设置。
        
        - 重置客户端后，必须重新初始化用户环境（也称为“引导”），下载客户端证书和最新模板。 为了执行此操作，请关闭 Office 的所有实例，然后重新启动 Office 应用程序。 此操作还会检查是否已下载最新的 Azure 信息保护策略。 完成此操作之前，请勿再次运行诊断测试。


## <a name="usage-logging"></a>使用情况日志记录

**[此功能需要客户端的预览版本，随时可能更改。]**

对于 Azure 信息保护客户端的预览版本，客户端将用户活动记录到本地 Windows **应用程序和服务**事件日志和 **Azure 信息保护**中。 这些事件包括以下信息：

- 日期、客户端版本、策略 ID

- 登录的用户名、计算机名称

- 文件名和位置

- 操作:

    - 设置标签：信息 ID 101
    
    - 设置标签（较低）：信息 ID 102
    
    - 设置标签（较高）：信息 ID 103
    
    - 删除标签：信息 ID 104
   
    - 建议提示：信息 105
    
    - 应用自定义保护：信息 ID 201
    
    - 删除自定义保护：信息 ID 202
    
    - 登录（操作）：信息 ID 902
    
    - 下载策略（操作）：信息 ID 901
    
- 操作源：
    
    - 手动 
    
    - 建议
    
    - 自动  
    
    - 系统（用于登录和下载策略）
    
- 操作前后的标签 
    
- 操作前后的保护
    
- 用户理由（如果适用）
    

## <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Azure 信息保护栏的键盘快捷方式

若要使用键盘快捷方式访问 Azure 信息保护栏，请使用以下组合键：

- 按 **Ctrl** + **Shift** + **~** 

然后，使用 Tab 键选择标签和保护栏上的其他控件（“隐藏标签”图标和“删除标签”图标），按 Enter 键以将其选中。


## <a name="file-locations"></a>文件位置

客户端文件：   

- 对于 64 位操作系统：**\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 对于 32 位操作系统：**\Program Files\Microsoft Azure Information Protection**

客户端日志文件和当前安装的策略文件：

- 对于 64 位和 32 位操作系统：**%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>后续步骤

若要更改信息保护栏上的标签，必须配置 Azure 信息保护策略。 有关详细信息，请参阅 [配置 Azure 信息保护策略](../deploy-use/configure-policy.md)(#配置-azure-信息保护策略)。

有关如何自定义默认策略并在 Office 应用程序是查看所产生行为的示例，请尝试 [Azure 信息保护快速入门教程](../get-started/infoprotect-quick-start-tutorial.md)(#azure-信息保护快速入门教程)。

若要检查客户端的发行版本信息，请参阅[版本发行历史记录](client-version-release-history.md)。



<!--HONumber=Dec16_HO1-->


