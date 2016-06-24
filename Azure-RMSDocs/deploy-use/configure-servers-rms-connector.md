---
# required metadata

title: 为 Azure Rights Management 连接器配置服务器 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 为 Azure Rights Management 连接器配置服务器

*适用于：Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*


使用以下信息可帮助你配置将使用 Azure Rights Management (RMS) 连接器的本地服务器。 这些过程涉及[部署 Azure Rights Management 连接器](deploy-rms-connector.md)中的步骤 5。

在开始之前，请确保已安装并配置 RMS 连接器，并且已检查任何适用于将使用该连接器的服务器的[先决条件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)。


## 将服务器配置为使用 RMS 连接器
安装并配置 RMS 连接器之后，即可将本地服务器配置为使用 Rights Management 并通过连接器连接到 Azure RMS。 这意味着需要配置以下服务器：

-   **对于 Exchange 2016 和 Exchange 2013**：客户端访问服务器和邮箱服务器

-   **对于 Exchange 2010**：客户端访问服务器和中心传输服务器

-   **对于 SharePoint**：前端 SharePoint Web 服务器，包括托管中心管理服务器的 Web 服务器

-   **对于文件分类基础结构**：装有文件资源管理器的 Windows Server 计算机

这种配置需要注册表设置。 要执行此操作，你有两个选项：使用适用于 Microsoft RMS 连接器的服务器配置工具自动配置，或通过编辑注册表手动配置。

---

**使用适用于 Microsoft RMS 连接器的服务器配置工具自动配置：**

- 优点：

    - 不直接编辑注册表。 可以使用脚本进行自动编辑。

    - 无需运行 Windows PowerShell cmdlet 来获取你的 Microsoft RMS URL。

    - 如果你本地运行工具，则自动为你检查必备组件（但不自动进行补救）。

缺点：

- 当你运行工具时，必须连接到已在运行 RMS 连接器的服务器。

---

**通过编辑注册表进行手动配置**

- 优点：

    - 不需要连接到运行 RMS 连接器的服务器。

- 缺点：

    - 更多管理开销，容易发生错误。

    - 你必须获取 Microsoft RMS URL，这需要你运行 Windows PowerShell 命令。

    - 你必须始终自行进行所有必备组件检查。


---

> [!IMPORTANT]对于这两种情况，都必须手动安装所有必备组件，并将 Exchange、SharePoint 和文件分类基础结构配置为使用权限管理。

对于大多数组织，使用适用于 Microsoft RMS 连接器的服务器配置工具进行自动配置是更好的选择，因为它提供优于手动配置的效率和可靠性。

在这些服务器上进行配置更改之后，如果这些服务器正在运行 Exchange 或 SharePoint 并且以前配置为使用 AD RMS，则你必须重新启动它们。 在首次将它们配置为使用权限管理时，无需重新启动它们。 进行这些配置更改后，始终必须重新启动配置为使用文件分类基础结构的文件服务器。

### 如何使用适用于 Microsoft RMS 连接器的服务器配置工具

1.  如果你尚未下载适用于 Microsoft RMS 连接器的服务器配置工具的脚本 (GenConnectorConfig.ps1)，请从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkId=314106)下载。

2.  将 GenConnectorConfig.ps1 文件保存在你要运行工具的计算机上。 如果要在本地运行该工具，则此计算机必须是你想要配置为与 RMS 连接器通信的服务器。 否则，你可将文件保存在任何计算机上。

3.  确定如何运行工具：

    -   **本地**：可以从要将配置为与 RMS 连接器通信的服务器以交互方式运行该工具。 这对于一次性配置（例如测试环境）非常有用。

    -   **软件部署**：你可以运行工具以生成注册表文件，然后使用支持软件部署的系统管理应用程序（例如 System Center Configuration Manager），将这些注册表文件部署到一个或多个相关服务器。

    -   **组策略设置**：你可以运行工具以生成脚本，然后将脚本提供给管理员，管理员可为要配置的服务器创建组策略对象。 此脚本为要配置的每个服务器类型创建一个组策略对象，然后管理员能够将此对象分配给相关服务器。

    > [!NOTE]
    > 此工具可以配置将与 RMS 连接器通信并已在本部分开头列出的服务器。 不要在运行 RMS 连接器的服务器上运行此工具。

4.  使用“以管理员身份运行”选项启动 Windows PowerShell，然后使用 Get-help 命令阅读有关如何将工具用于你选择的配置方法的说明：

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

若要运行脚本，你必须输入组织的 RMS 连接器的 URL。 输入协议前缀（HTTP:// 或 HTTPS://），以及你在 DNS 中为连接器的负载平衡地址定义的连接器名称， 例如 https://connector.contoso.com。 然后，此工具会使用该 URL 来联系运行 RMS 连接器的服务器，并获取用于创建所需配置的其他参数。

> [!IMPORTANT]运行此工具时，请确保指定组织的负载平衡 RMS 连接器的名称，而不要指定运行 RMS 连接器服务的单个服务器的名称。

使用以下部分获取每个服务类型的特定信息：

-   [将 Exchange 服务器配置为使用连接器](#configuring-an-exchange-server-to-use-the-connector)

-   [将 SharePoint 服务器配置为使用连接器](#configuring-a-sharepoint-server-to-use-the-connector)

-   [将文件分类基础结构的文件服务器配置为使用连接器](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> 在将这些服务器配置为使用连接器之后，本地安装在这些服务器上的客户端应用程序可能无法使用 RMS。 发生这种情况的原因是应用程序试图使用连接器而不是直接使用 RMS，但这种方式不受支持。
>
> 此外，如果 Office 2010 本地安装在 Exchange 服务器上，则在将服务器配置为使用连接器之后，客户端应用的 IRM 功能可能从该计算机运行，但这种方式不受支持。
>
> 在上述两种情况下，你必须在没有配置为使用连接器的单独计算机上安装客户端应用程序。 然后它们即可正确地直接使用 RMS。

## 将 Exchange 服务器配置为使用连接器
以下 Exchange 角色将与 RMS 连接器通信：

-   对于 Exchange 2016 和 Exchange 2013：客户端访问服务器和邮箱服务器

-   对于 Exchange 2010：客户端访问服务器和中心传输服务器

若要使用 RMS 连接器，这些运行 Exchange 的服务器必须运行以下软件版本之一：

-   Exchange Server 2016

-   Exchange Server 2013，附带 Exchange 2013 累积更新 3

-   Exchange Server 2010，附带 Exchange 2010 Service Pack 3 汇总更新 6

你还需要在服务器上安装能够支持 RMS 加密模式 2 的 RMS 客户端版本。 Windows Server 2008 支持的最低版本包括在修补程序中，你可从 [在 Windows Server 2008 R2 和 Windows Server 2008 中，AD RMS 的 RSA 密钥长度增加到 2048 位](http://support.microsoft.com/kb/2627272)下载该修补程序。 适用于 Windows Server 2008 R2 的最低版本可从 [在 Windows 7 或 Windows Server 2008 R2 中，AD RMS 的 RSA 密钥长度增加到 2048 位](http://support.microsoft.com/kb/2627273)下载。 Windows Server 2012 和 Windows Server 2012 R2 以本机方式支持加密模式 2。

> [!IMPORTANT]
> 如果没有安装这些版本或更高版本的 Exchange 和 RMS 客户端，你就无法将 Exchange 配置为使用连接器。 继续之前，请确认已安装这些版本。

### 将 Exchange 服务器配置为使用连接器

1. 通过使用 RMS 连接器管理工具和[授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)部分的信息，确保 Exchange 服务器有权使用 RMS 连接器。 需要此配置，以便 Exchange 可以使用 RMS 连接器。

2.  在与 RMS 连接器通信的 Exchange 服务器角色上执行以下任一操作：

    -   运行适用于 Microsoft RMS 连接器的服务器配置工具。 有关详细信息，请参阅[如何使用适用于 Microsoft RMS 连接器的服务器配置工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，若要在本地运行该工具以配置运行 Exchange 2016 或 Exchange 2013 的服务器，请执行以下操作：

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
        ```

    -   使用 [RMS 连接器的注册表设置](rms-connector-registry-settings.md)中的信息，在服务器上手动添加注册表设置，进行手动注册表编辑。 

3.  在 Exchange 中启用 IRM 功能。 有关详细信息，请参阅 Exchange 库中的[信息权限管理过程](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx)。

    > [!NOTE]
    > 默认情况下，运行 **Set-IRMConfiguration -InternalLicensingEnabled $true** 后，出为邮箱启用 IRM 外，还将为 Outlook Web 应用和移动设备自动启用 IRM。 但管理员可以在不同级别禁用 IRM，例如，针对客户端访问服务器、Outlook Web App 虚拟目录或 Outlook Web App 邮箱策略，以及移动设备邮箱策略禁用。 如果用户在 Outlook Web App 中（等待一天后）或在移动设备上无法看到任何 Azure RMS 模板，而在 Outlook 客户端中能够看到这些模板，请检查相关设置，确保未禁用 IRM。 有关详细信息，请参阅 Exchange 文档中的 [Enable or Disable Information Rights Management on Client Access Servers](https://technet.microsoft.com/library/dd876938(v=exchg.150).aspx)（在客户端访问服务器上启用或禁用信息权限管理）。 


## 将 SharePoint 服务器配置为使用连接器
以下 SharePoint 角色将与 RMS 连接器通信：

-   前端 SharePoint Web 服务器，包括托管中心管理服务器的 Web 服务器

若要使用 RMS 连接器，这些运行 SharePoint 的服务器必须运行以下软件版本之一：

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

运行 SharePoint 2016 或 SharePoint 2013 的服务器也必须运行 RMS 连接器支持的 MSIPC 客户端 2.1 版。 若要确保使用受支持的版本，请从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=38396)下载最新的客户端。

> [!WARNING] MSIPC 2.1 客户端有多个版本，因此请确保安装版本 1.0.2004.0 或更高版本。
>
> 你可以通过检查 MSIPC.dll 的版本号来验证客户端版本，该文件位于 **\Program Files\Active Directory Rights Management Services Client 2.1**。 属性对话框将显示 MSIPC 2.1 客户端的版本号。

运行 SharePoint 2010 的服务器必须安装了能够支持 RMS 加密模式 2 的 MSDRM 客户端版本。 Windows Server 2008 支持的最低版本包括在修补程序中，你可从 [在 Windows Server 2008 R2 和 Windows Server 2008 中，AD RMS 的 RSA 密钥长度增加到 2048 位](http://support.microsoft.com/kb/2627272)下载该修补程序。适用于 Windows Server 2008 R2 的最低版本可从 [在 Windows 7 或 Windows Server 2008 R2 中，AD RMS 的 RSA 密钥长度增加到 2048 位](http://support.microsoft.com/kb/2627273)下载。 Windows Server 2012 和 Windows Server 2012 R2 以本机方式支持加密模式 2。

### 将 SharePoint 服务器配置为使用连接器

1. 通过使用 RMS 连接器管理工具和[授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)部分的信息，确保 SharePoint 服务器有权使用 RMS 连接器。 需要此配置，以便 Exchange 可以使用 RMS 连接器。

2.  在与 RMS 连接器通信的 SharePoint 服务器上执行以下任一操作：

    -   运行适用于 Microsoft RMS 连接器的服务器配置工具。 有关详细信息，请参阅[如何使用适用于 Microsoft RMS 连接器的服务器配置工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，若要在本地运行该工具以配置运行 SharePoint 2016 或 SharePoint 2013 的服务器，请执行以下操作：

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   如果你正在使用 SharePoint 2016 或 SharePoint 2013，请使用 [RMS 连接器的注册表设置](rms-connector-registry-settings.md)中的信息在服务器上手动添加注册表设置，进行手动注册表编辑。 

3.  在 SharePoint 中启用 IRM。 有关详细信息，请参阅 SharePoint 库中的[配置信息权限管理 (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx)。

    当你按照这些说明操作时，必须通过指定**使用此 RMS 服务器**，将 SharePoint 配置为使用连接器，然后输入你配置的负载平衡连接器 URL。 输入协议前缀（HTTP:// 或 HTTPS://），以及你在 DNS 中为连接器的负载平衡地址定义的连接器名称， 例如，如果你的连接器名称为 https://connector.contoso.com，则配置将如下图所示：

    ![为 RMS 连接器配置 SharePoint Server](../media/AzRMS_SharePointConnector.png)

    在 SharePoint 场上启用 IRM 之后，你可以使用每个库的 **“库设置”** 页上的 **“信息权限管理”** 选项，在各个库上启用 IRM。


## 将文件分类基础结构的文件服务器配置为使用连接器
若要使用 RMS 连接器和文件分类基础结构来保护 Office 文档，文件服务器必须运行以下操作系统之一：

-   Windows Server 2012 R2

-   Windows Server 2012

### 将文件服务器配置为使用连接器

1.  通过使用 RMS 连接器管理工具和[授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)部分的信息，确保文件服务器有权使用 RMS 连接器。 需要此配置，以便 Exchange 可以使用 RMS 连接器。

2.  在为文件分类基础结构配置的、将与 RMS 连接器通信的文件服务器上执行以下任一操作：

    -   运行适用于 Microsoft RMS 连接器的服务器配置工具。 有关详细信息，请参阅[如何使用适用于 Microsoft RMS 连接器的服务器配置工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，若要在本地运行该工具以配置运行 FCI 的文件服务器，请执行以下操作：

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - 使用 [RMS 连接器的注册表设置](rms-connector-registry-settings.md)中的信息，在服务器上手动添加注册表设置，进行手动注册表编辑。 

3.  创建分类规则和文件管理任务，才能使用 RMS 加密保护文档，然后指定一个用于自动将 RMS 策略的应用的 RMS 模板。 有关详细信息，请参阅 Windows Server 文档库中的 [文件服务器资源管理器概述](http://technet.microsoft.com/library/hh831701.aspx) 。

## 后续步骤
现已安装并配置了 RMS 连接器，并且你的服务器已配置为使用该连接器，IT 管理员和用户就可以使用 Azure RMS 保护和使用电子邮件与文档了。 若要让用户轻松使用此功能，请部署 RMS 共享应用程序，它会安装 Office 的外接程序并在文件资源管理器中添加新的右键单击选项。 有关详细信息，请参阅 [Rights Management 共享应用程序管理员指南](../rms-client/sharing-app-admin-guide.md)。

可以使用 [Azure Rights Management 部署路线图](../plan-design/deployment-roadmap.md)，检查向用户和管理员推出 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 之前是否还需要执行其他配置步骤。

若要监视 RMS 连接器，请参阅[监视 Azure Rights Management 连接器](monitor-rms-connector.md)。 


<!--HONumber=Jun16_HO2-->


