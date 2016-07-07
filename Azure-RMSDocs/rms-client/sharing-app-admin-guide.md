---
title: "Rights Management 共享应用程序管理员指南 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: e67d0ab5537aa7444940a5e7ce3a653cc6e66993


---


# 权限管理共享应用程序管理员指南

*适用于：Active Directory Rights Management Services、Azure Rights Management、Windows 10、具有 SP1 的 Windows 7、Windows 8、Windows 8.1*


如果你负责企业网络上的 Microsoft Rights Management 共享应用程序，或者如果你希望获取除了 [Rights Management 共享应用程序用户指南](sharing-app-user-guide.md)或[适用于 Windows 的 Microsoft Rights Management 共享应用程序常见问题](http://go.microsoft.com/fwlink/?LinkId=303971)以外的更多技术信息，请使用以下信息。

RMS 共享应用程序最适合与 Azure RMS 配合使用，因为这种部署配置支持向另一组织中的用户发送受保护的附件，并提供电子邮件通知、文档跟踪和撤消等选项。  不过，它也能够与本地版本的 AD RMS 配合使用，只是存在一些限制。 有关 Azure RMS 和 AD RMS 支持的功能的全面比较，请参阅[比较 Azure Rights Management 和 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。 如果你安装了 AD RMS 并想要迁移到 Azure RMS，请参阅 [从 AD RMS 迁移到 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。

## 自动部署 Microsoft Rights Management 共享应用程序
Windows 版 RMS 共享应用程序支持脚本化安装，因此适合企业部署。

安装的唯一先决条件是，计算机运行最低版本的 Windows 7 Service Pack 1 且已安装 Microsoft Framework（最低版本为 4.0）。 如果你需要安装 Microsoft.NET Framework 4.0，可以 [从 Microsoft 下载中心下载并安装](http://www.microsoft.com/download/details.aspx?id=17718)。

### 下载要自动部署的 RMS 共享应用程序

1.  在 Microsoft 下载中心转到 [适用于 Windows 的 Rights Management 共享应用程序](http://www.microsoft.com/download/details.aspx?id=40857) 页，然后单击“下载”。 

2.  选择并下载所需文件。 有两个客户端安装包：一个适用于 64 位 Windows (Microsoft Rights Management sharing application x64.zip)，另一个适用于 32 位 Windows (Microsoft Rights Management sharing application x86.zip)。

3.  从压缩的安装包中提取文件，例如双击它们。 然后，将提取的文件复制到客户端计算机可以访问的网络位置。

RMS 共享应用程序的安装包支持不同的部署方案，包括以下方案：

|说明|部署方案|
|---------------|-----------------------|
|Microsoft Online 登录助手|Office 2010 和 Azure RMS<br /><br />Office 2013 和 Azure RMS（如果你尚未安装 [Office 2013 2015 年 6 月 9 日更新](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Office 修补程序 (KB 2596501)|Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS|
|用于启用 AD RMS 客户端 1.0 以与 Azure RMS 配合工作的修补程序 (KB 2843630)|Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS|
|AD RMS 客户端和 RMS 共享应用程序|Office 2016 或 Office 2013，以及 Azure RMS 或 Active Directory RMS<br /><br />Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS<br /><br />仅 RMS 共享应用程序和 Office 加载项|
|功能区的 Office 加载项|Office 2016 或 Office 2013，以及 Azure RMS 或 Active Directory RMS<br /><br />Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS<br /><br />仅 RMS 共享应用程序和 Office 加载项|
|Azure Active Directory Rights Management 准备工具|Office 2010 和 Azure RMS|
使用以下过程来确定为这些部署方案部署 RMS 共享应用程序所需的命令：

-   **Office 2016 或 Office 2013，以及 Azure RMS 或 Active Directory RMS**

    你的用户运行的是 Office 2016 或 Office 2013、你的组织使用的是 Azure RMS 或 Active Directory RMS，并且用户与使用 Azure RMS 或 Active Directory RMS 的其他组织进行协作。

-   **Office 2010 和 Azure RMS**

    你的用户运行的是 Office 2010、你的组织使用的是 Azure RMS，并且用户与使用 Azure RMS 或 Active Directory RMS 的其他组织进行协作。

-   **Office 2010 和 Active Directory RMS**

    你的用户运行的是 Office 2010、你的组织使用的是 AD RMS，并且用户与使用 Azure RMS 的其他组织进行协作。

-   **仅 RMS 共享应用程序和 Office 加载项**

    你的用户运行的是 Office 2016、Office 2013 或 Office 2010、你的组织使用的是 AD RMS，并且用户无需与使用 Azure RMS 的其他组织进行协作。 此安装仅允许你安装共享应用程序和 Office 加载项。

> [!NOTE]
> 在上述方案中，如果你的组织运行的是 AD RMS，则用户可以从使用 Azure RMS 的其他组织接收受保护内容，但他们无法将受保护的内容发送给使用 Azure RMS 的组织中的用户。 但是，如果你的组织运行的是 Azure RMS，则用户可以发送和接收来自其他组织的受保护内容。

若要针对每个步骤完成安装，必须重新启动计算机。 可以使用类似于 **shutdown /i** 的命令实现自动重新启动。

### 为 Office 2016 或 Office 2013 和 Azure RMS 或 Active Directory RMS 部署 RMS 共享应用程序

-   在要安装 RMS 共享应用程序及相关组件的每台计算机上，使用提升的权限运行以下命令：

    ```
    setup.exe /s
    ```

若要验证是否成功，请参阅本文中的[验证安装是否成功](#verifying-installation-success)部分。

### 为 Office 2010 和 Azure RMS 部署 RMS 共享应用程序

1.  你必须是 Office 365 或 Azure Active Directory 租户的全局管理员，才能通过运行 Azure Active Directory Rights Management 准备工具获取组织的证书服务 URL。 在单台计算机上，只需运行此工具一次。 在每台计算机上安装 RMS 共享应用程序时，你将使用证书服务 URL：

    1.  使用本地管理员帐户登录到计算机。

    2.  在该计算机上， [下载并安装 Microsoft Online 登录助手](http://www.microsoft.com/download/details.aspx?id=28177)。

    3.  运行以下命令以查看显示在屏幕上的证书服务 URL，然后可以复制并保存该 URL 以供下一步使用：

        -   对于 64 位 Windows 8.1 和 Windows 8：

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   对于 32 位 Windows 8.1 和 Windows 8：

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   对于 64 位 Windows 7：

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > 此命令可能会提示你输入 Azure 的凭据。 如果计算机未加入域，系统将会提示你加入。 如果计算机已加入域，该工具也许可以使用缓存的凭据。

2.  在要安装 RMS 共享应用程序的每台计算机上，使用提升的权限运行以下命令：

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  在要安装 RMS 共享应用程序的每台计算机上，用户必须运行以下命令（不需要使用提升的权限）。 可通过不同的方式来实现此目的，包括要求用户运行该命令（例如，在电子邮件中提供一个链接，或者在技术支持门户上提供一个链接），或者在用户的登录脚本中添加该命令：

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

若要验证是否成功，请参阅本文中的[验证安装是否成功](#verifying-installation-success)部分。

### 为 Office 2010 和 Active Directory RMS 部署 RMS 共享应用程序

1.  在要安装 RMS 共享应用程序的每台计算机上，使用提升的权限运行以下命令：

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  在要安装 RMS 共享应用程序的每台计算机上，用户必须运行以下命令（不需要使用提升的权限）。 可通过不同的方式来实现此目的，包括要求用户运行该命令（例如，在电子邮件中提供一个链接，或者在技术支持门户上提供一个链接），或者在用户的登录脚本中添加该命令：

    -   对于 64 位 Windows 10、Windows 8.1 和 Windows 8：

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   对于 32 位 Windows 10、Windows 8.1 和 Windows 8：

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   对于 64 位 Windows 7：

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

若要验证是否成功，请参阅本文中的[验证安装是否成功](#verifying-installation-success)部分。

### 仅安装 RMS 共享应用程序和 Office 加载项

1.  使用以下命令安装 AD RMS 客户端和 RMS 共享应用程序：

    -   对于 64 位 Windows：

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   对于 32 位 Windows：

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    例如： `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  使用以下命令安装 Office 加载项：

    -   对于 64 位版本的 Office：

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   对于 32 位版本的 Office：

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    例如： `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

若要验证是否成功，请参阅本文中的[验证安装是否成功](#verifying-installation-success)部分。

## 验证安装是否成功
可以使用安装日志文件来验证安装是否成功。

### 验证是否为 Office 2016 或 Office 2013 和 Azure RMS 或 Active Directory RMS 成功安装 RMS 共享应用程序

-   若要验证 Setup.exe 命令是否成功运行，请在每台计算机上的 *%temp%\RMS_installer_&lt;guid&gt;* 文件夹中搜索安装日志文件 **RMInstaller.log**，然后查看退出代码。

    如果退出代码为 0，则表示安装成功；如果退出代码为其他任何数字，则表示安装失败。

    示例日志文件名：**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### 验证是否为 Office 2010 和 Azure RMS 成功安装 RMS 共享应用程序

1.  若要验证 Setup.exe 命令是否成功运行，请在每台计算机上的 *%temp%\RMS_installer_&lt;guid&gt;* 文件夹中搜索安装日志文件 **RMInstaller.log**，然后查看退出代码。

    如果退出代码为 0，则表示安装成功；如果退出代码为其他任何数字，则表示安装失败。

    示例日志文件名：**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  若要验证 RMSSetup.exe 命令是否成功运行，用户应在其 *%localappdata%\microsoft\drm* 文件夹中创建以下文件：

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    CLC-&#42;.drm 文件示例：

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### 验证是否为 Office 2010 和 Active Directory RMS 成功安装 RMS 共享应用程序

1.  若要验证 Setup.exe 命令是否成功运行，请在每台计算机上的 *%temp%\RMS_installer_&lt;guid&gt;* 文件夹中搜索安装日志文件，然后查看退出代码。

    如果退出代码为 0，则表示安装成功；如果退出代码为其他任何数字，则表示安装失败。

    示例日志文件名：**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  若要验证 aadrmprep.exe 命令是否成功运行，请在安装日志文件中搜索以下文本： **aadrmprep.exe exited with status SUCCESS**

    > [!NOTE]
    > 有时，此安装可能会运行两次；第一次安装是失败的，第二次安装是成功的。

    如果你想要手动检查此工具所做的注册表更改，更改内容如下：

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14。0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### 验证仅安装 RMS 共享应用程序和 Office 加载项是否成功

1.  若要验证 Setup_ipviewer.exe 命令是否成功运行，请在安装日志文件中搜索以下文本：**安装成功或错误状态：0**

    成功安装时包含的示例行：

    **MSI (s) (F0:B8) [14:19:57:854]:Product:Active Directory Rights Management Services Client 2.1 -- Installation completed successfully.**

    **MSI (s) (F0:B8) [14:19:57:854]:Windows Installer installed the product. Product Name:Active Directory Rights Management Services Client 2.1. Product Version:1.0.1179.1. Product Language:1033. 制造商:Microsoft Corporation. 安装成功或错误状态：0.**

2.  若要验证 Office 加载项是否成功安装，请在安装日志文件中搜索以下文本：**安装成功或错误状态：0**

    成功安装时包含的示例行：

    **MSI (s) (9C:88) [18:49:04:007]:Product:Microsoft RMS Office Addins -- Installation completed successfully.**

    **MSI (s) (9C:88) [18:49:04:007]:Windows Installer installed the product. Product Name:Microsoft RMS Office Addins. Product Version:1.0.7. Product Language:1033. 制造商:Microsoft. 安装成功或错误状态：0.**

## 卸载命令
并非这些部署所需的所有安装命令都支持卸载命令。 你可以卸载 AD RMS 客户端和共享应用程序，也可以卸载 Office 加载项。 请使用以下命令卸载这些元素。

### 卸载 AD RMS 客户端和 RMS 共享应用程序

-   使用以下命令：

    -   对于 64 位 Windows：

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   对于 32 位 Windows：

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### 卸载 Office 加载项

-   使用以下命令：

    -   对于 64 位版本的 Office：

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   对于 32 位版本的 Office：

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## 禁止自动更新
默认情况下，当出现较新版本的 RMS 共享应用程序时，系统将通知用户并提示他们下载该应用程序。 你可以对注册表进行以下编辑来取消显示此通知：

1.  导航到 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC**，如果它尚不存在，请创建名为 **RmsSharingApp** 的新注册表项。

2.  选择 **RmsSharingApp**，创建一个新的 DWORD 值 **AllowUpdatePrompt**，并将该值设置为 **0**。

由于 WSUS 不支持 RMS 共享应用程序，你可以先使用以下技术测试所有新版本的 RMS 共享应用程序，然后再将其部署到所有用户：

1.  在所有用户的计算机上，运行一个脚本来禁止自动更新。 在管理员用于测试新版本的计算机上，请不要运行此脚本。

2.  当新版本可用时，管理员将下载它并对其进行测试。

3.  在测试完成且解决了所有问题之后，使用本指南中的自动部署说明将最新版本部署到所有用户。

## 仅限 Azure RMS：配置文档跟踪
如果你有[支持文档跟踪的订阅](https://technet.microsoft.com/dn858608)，则默认情况下，已经为你组织中的所有用户启用了文档跟踪站点。  文档跟踪会显示尝试访问用户共享的受保护文档的人员的电子邮件地址、其尝试访问这些文档的时间以及他们所在的位置。 如果你的组织出于隐私要求而要禁止显示此类信息，你可以使用 [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) cmdlet 来禁用对文档跟踪站点的访问。 你随时可以使用 [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) 来重新启用对该站点的访问，并可以使用 [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) 来查看当前是已启用还是已禁用这种访问。

若要运行这些 cmdlet，你必须安装至少 **2.3.0.0** 版的适用于 Windows PowerShell 的 Azure RMS 模块。  有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。

> [!TIP]
> 如果你以前已下载并安装过该模块，请通过运行以下命令检查版本号： `(Get-Module aadrm –ListAvailable).Version`

以下 URL 用于文档跟踪，必须允许使用它们（例如，如果你使用的是具有增强的安全性的 Internet Explorer，则将它们添加到你的受信任站点）：

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > 此 URL 用于 Bing 映射。

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## 仅限 AD RMS：在组织中支持多个电子邮件域
如果你使用 AD RMS 且你所在组织中的用户具有多个电子邮件域（可能由于组织的合并或收购而引起），则必须对注册表进行以下编辑：

1.  导航到 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC**，如果它尚不存在，请创建名为 **RmsSharingApp** 的新注册表项。

2.  选择 **RmsSharingApp**，创建一个名为 **FederatedDomains** 的新多字符串值，然后添加组织使用的域和所有子域。 不支持使用通配符。

    例如：Coho Vineyard &amp; Winery 公司拥有标准的电子邮件域 **cohovineyardandwinery.com**，但由于合并，它们也使用电子邮件域 **cohowinery.com**、**eastcoast.cohowinery.com** 和 **cohovineyard**。 对于 **FederatedDomains** 值数据，管理员可以输入：**cohowinery.com；eastcoast.cohowinery.com；cohovineyard**

如果未对该注册表进行更改，则用户可能无法使用由所在组织中的其他用户所保护的内容。 如果你使用 Azure RMS，则不需要编辑该注册表。


## 后续步骤
有关其他技术信息，包括保护级别（本机和通用）之间的区别、支持的文件类型和文件扩展名以及如何更改默认保护级别的相关说明，请参阅 [Rights Management 共享应用程序技术概述](sharing-app-admin-guide-technical.md)。




<!--HONumber=Jun16_HO4-->


