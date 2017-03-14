---
title: "Azure 信息保护客户端管理员指南"
description: "面向负责部署适用于 Windows 的 Azure 信息保护客户端的企业网络管理员的说明和信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: adb444f7777304ed40b5b5f988e4efb73268ae14
ms.sourcegitcommit: cbdbabd626fa5b91c418d84cd6228c9ca94a2525
translationtype: HT
---
# <a name="azure-information-protection-client-administrator-guide"></a>Azure 信息保护客户端管理员指南

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7


如果你负责企业网络上的 Azure 信息保护客户端，或如果你想要获取除了 [Azure 信息保护客户端用户指南](client-user-guide.md)以外的更多技术信息，请使用以下信息。

Azure 信息保护客户端包括以下内容：

- 一个 Office 外接程序，可安装 Azure 信息保护栏以便用户选择分类标签；一个功能区上的“保护”按钮，可获取其他选项。

- Windows 文件资源管理器，便于用户将分类标签和保护应用到文件的右键单击选项。

- 一个查看器，可在本机应用程序无法将其打开时显示受保护的文件。

- 一个 PowerShell 模块，用于从文件应用和删除分类标签和保护。

- 权限管理客户端，可与 Azure 权限管理 (Azure RMS) 或 Active Directory Rights Management Services (AD RMS) 进行通信。

Azure 信息保护客户端最适合用于其 Azure 服务；Azure 信息保护及其数据保护服务（Azure 权限管理）。 不过，Azure 信息保护客户端也可用于本地版本的 Rights Management ( AD RMS)，只是存在一些限制。 有关 Azure 信息保护和 AD RMS 所支持功能的全面比较，请参阅[比较 Azure信息保护和 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。 如果安装了 AD RMS，想迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

**是否有本文档未回答的问题？** 请访问 [Azure 信息保护 Yammer 站点](https://www.yammer.com/AskIPTeam)。 


## <a name="should-you-deploy-the-azure-information-protection-client"></a>你是否应该部署 Azure 信息保护客户端？

如果以下任一项适用，请部署 Azure 信息保护客户端：

- 想要通过从 Office 应用程序（Word、Excel、PowerPoint、Outlook）中选择标签对文档和电子邮件进行分类（或保护）。

- 想要通过使用文件资源管理器（支持其他文件类型、多选和文件夹）对文档和电子邮件进行分类（或保护）。

- 想要通过使用 PowerShell 命令运行对文档进行分类（或保护）的脚本。

- 想要在本机应用程序显示未安装文件或无法打开这些文档时查看受保护的文档。

- 只想通过使用文件资源管理器或使用 Powershell 命令保护文件。

- 想要用户和管理员能够跟踪和撤销受保护的文档。

- 想要从文件和容器（取消保护）批量删除加密，以进行数据恢复。

- 运行 Office 2010 并且想要通过使用 Azure 权限管理服务保护文档和电子邮件。

示例显示了 Office 应用程序中的 Azure 信息保护客户端外接程序、组织的分类标签，以及功能区上的新“保护”按钮：

![具有默认策略的 Azure 信息保护栏](../media/info-protect-bar-default.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>如何为用户安装 Azure 信息保护客户端

安装客户端之前，请检查是否具有 Azure 信息保护客户端所需的操作系统版本和应用程序：[Azure 信息保护要求](../get-started/requirements-azure-rms.md)。 

此外：

- 完整安装 Azure 信息保护客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装此必备项。 在客户端安装过程中安装此必备项后，将重启计算机。

- 如果单独安装 Azure 信息保护查看器，则要求的最低版本为 Microsoft .NET Framework 4.5.2，如果缺少此版本，安装程序会尝试下载并安装它。

- PowerShell 模块需要 Windows PowerShell 4.0 版本，此版本可能需要在旧版操作系统上安装。 有关详细信息，请参阅[如何：安装 Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)。 安装程序不会为你检查或安装此必备项。 若要确认正在运行的 Windows PowerShell 的版本，请在 PowerShell 会话中键入 **$PSVersionTable**。

- 运行 Windows 7 Service Pack 1 的计算机需要 KB 2533623。 有关此更新的详细信息，请参阅 [Microsoft 安全公告：不安全的库加载可能允许远程执行代码](https://support.microsoft.com/en-us/kb/2533623)。 可以直接安装此更新，也可以使用为你安装的另一个更新代替此更新。
    
    如果需要此更新且未安装，则客户端安装将警告你必须安装此更新。 可以在安装客户端后安装此更新，但某些操作将被阻止并再次显示该信息。  

> [!NOTE]
> 安装需要本地管理权限。

除了使用以下说明，Microsoft 更新目录中也包含 Azure 信息保护客户端，因此可通过使用该目录的任意软件更新服务来安装和更新客户端。 

1. 从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)(#microsoft-下载中心) 下载 Azure 信息保护客户端。 
    
    如果存在可用的预览版本，则保留此版本仅供测试使用。 它不用于生产环境中的最终用户。 

2. 对于默认安装，只需运行可执行文件，例如 **AzInfoProtection.exe**。 但是，若要查看安装选项，请先使用 **/help** 运行可执行文件：`AzInfoProtection.exe /help`

   有关无提示安装客户端的示例：`AzInfoProtection.exe /quiet`
   
   有关无提示仅安装 PowerShell cmdlet 的示例：`AzInfoProtection.exe  PowerShellOnly=true /quiet`
   
   此外，如果在运行 Office 2010 的计算机上安装客户端，并且你的用户不是其计算机的本地管理员，则须指定 **ServiceLocation** 参数（不包括在帮助屏幕中）。 有关详细信息，请参阅下一节。

3. 如果以交互方式安装，并且无法连接到 Office 365 或 Azure Active Directory，但出于演示目的，想要通过本地策略看到和体验 Azure 信息保护客户端，请选择此选项安装**演示策略**。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。
    
4. 若要完成安装： 

    - 如果计算机运行的是 Office 2010，请重新启动计算机。 
        
        如果未使用 ServiceLocation 参数安装客户端，首次打开一个使用 Azure 信息保护栏的 Office 应用程序（如 Word）时，必须确认是否有任何要求首次使用时更新注册表的提示。 利用[服务发现](../rms-client/client-deployment-notes.md#rms-service-discovery)功能填充注册表项。 
    
    - 对于其他版本的 Office，请重启任一 Office 应用程序和文件管理器的所有实例。 
        
5. 可通过查看 %temp% 文件夹中的安装日志文件，来确认安装已成功。 此文件具有以下命名格式：`Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例如：**Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    在此日志文件中搜索以下字符串：**Product: Microsoft Azure Information Protection -- Installation completed successfully**（产品：Microsoft Azure 信息保护 - 已成功完成安装）。 如果安装失败，此日志文件包含有助于标识并解决任何问题的详细信息。

### <a name="additional-instructions-for-office-2010-only"></a>仅适用于 Office 2010 的其他说明

如果为具有 Office 2010 的用户安装客户端，并且他们没有本地管理权限，请指定用于 Azure 权限管理服务的 ServiceLocation 参数和 URL。 此参数和值将创建和设置以下注册表项：

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

使用以下过程标识要为 ServiceLocation 参数指定的值。 

#### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>若要标识要为 ServiceLocation 参数指定的值

1. 对于 PowerShell 会话，请先运行 [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice)，并指定要连接到 Azure 权限管理服务的管理员凭据。 然后运行 [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration)。 
 
    如果尚未安装适用于 Azure 权限管理服务的 Windows PowerShell 模块，请参阅[安装适用于 Azure 权限管理的 Windows PowerShell](../deploy-use/install-powershell.md)。

2. 在输出中找到 **LicensingIntranetDistributionPointUrl** 值。

    示例：**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. 在该值中，将 **/_wmcs/licensing** 从此字符串删除。 例如：**https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    剩余字符串就是要为 ServiceLocation 参数指定的值。

有关为 Office 2010 和 Azure RMS 无提示安装客户端的示例：`AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


## <a name="to-uninstall-the-azure-information-protection-client"></a>卸载 Azure 信息保护客户端

可以使用以下任何选项：

- 使用控制面板卸载程序：单击“**Microsoft Azure 信息保护** > **卸载**”

- 重新运行可执行文件（如 **AzInfoProtection.exe**），并从“修改安装程序”页上，单击“卸载”。 

- 使用 **/uninstall** 运行可执行文件。 例如： `AzInfoProtection.exe /uninstall`


## <a name="additional-checks-to-verify-installation-connection-status-or-send-feedback"></a>其他检查：验证安装、连接状态或发送反馈

1. 打开 Office 应用程序，在“**主页**”选项卡的“**保护**”组中单击“**保护**”，然后单击“**帮助和反馈**”。

2. 在“**Microsoft Azure 信息保护**”对话框中，注意以下各项：

    - 在“客户端状态”部分：使用“版本”值来验证安装是否成功。 此外，还会看到客户端上一次连接到组织的 Azure 信息保护服务的时间，以及上一次安装或更新 Azure 信息保护策略的时间。 当客户端连接到该服务时，如果它发现其当前策略中存在更改，它会自动下载最新的策略。 如果在显示时间后完成策略更改，关闭并重新打开 Office 应用程序。
    
        还可以看到标识用于向 Azure 信息保护进行身份验证的帐户的显示用户名。 此用户名必须与用于 Office 365 或 Azure Active Directory 的帐户，以及属于为 Azure 信息保护所配置的某个租户的帐户相匹配。

    - 在“帮助和反馈”部分中：**告诉我详细信息链接**默认转到 [Azure 信息保护](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection)网站；但作为 Azure 信息保护策略中的一个[策略设置](../deploy-use/configure-policy-settings.md)，它也可配置为自定义 URL。
        
        使用“发送反馈”链接向信息保护团队发送建议或请求。 对于技术支持，请勿将此选项，而是参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)。 
    
        若要获取诊断信息以及重置客户端，请单击“运行诊断”。 诊断测试完成后，单击“复制结果”将信息粘贴到电子邮件中，以发送给支持人员或 Microsoft 支持部门。 测试完成后，还可以重置客户端。
        
        有关“重置”选项的详细信息：
        
        - 不是本地管理员也能使用此选项，并且不会在事件查看器中记录此操作。 
        
        - 除非文件被锁定，否则此操作将删除 **%localappdata%\Microsoft\MSIPC** 中的所有文件，该路径用于存储客户端证书和权限管理模板。 此操作不会删除 Azure 信息保护策略或客户端日志文件，也不会注销用户。
        
        - 会删除以下注册表项和设置：**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**。 如果为此注册表项配置设置（例如，由于要从 AD RMS 迁移并且网络上仍有服务连接点，因此配置用于重定向到 Azure 信息保护租户的设置），那么重置客户端后必须重新配置注册表设置。
        
        - 重置客户端后，必须重新初始化用户环境（也称为“引导”），下载客户端证书和最新模板。 为了执行此操作，请关闭 Office 的所有实例，然后重新启动 Office 应用程序。 此操作还会检查是否已下载最新的 Azure 信息保护策略。 完成此操作之前，请勿再次运行诊断测试。


## <a name="next-steps"></a>后续步骤
现在你已安装 Azure 信息保护客户端，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
