---
title: 为 Rights Management 连接器配置服务器 - AIP
description: 此信息可帮助你配置将使用 Azure Rights Management (RMS) 连接器的本地服务器。 这些过程涉及部署 Azure Rights Management 连接器中的步骤 5。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e07d4f634d774be91df03c279705f52e9bee6c8c
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809678"
---
# <a name="configuring-servers-for-the-azure-rights-management-connector"></a>为 Azure Rights Management 连接器配置服务器

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>相关内容：*[AIP 统一标记客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

使用以下信息可帮助你配置将使用 Azure Rights Management (RMS) 连接器的本地服务器。 这些过程涉及 [部署 Azure Rights Management 连接器](deploy-rms-connector.md)中的步骤5。

**先决条件**：在开始之前，请确保具备以下条件：
    - 已安装并配置 RMS 连接器
    - 检查与将使用连接器的服务器相关的任何 [先决条件](deploy-rms-connector.md#prerequisites-for-the-rms-connector) 。

## <a name="configuring-servers-to-use-the-rms-connector"></a>将服务器配置为使用 RMS 连接器
安装并配置 RMS 连接器后，便可以配置将连接到 Azure Rights Management 服务的本地服务器，并通过连接器使用此保护技术。 

这意味着需要配置以下服务器：

|环境  |要配置的服务器  |
|---------|---------|
|**Exchange 2016 和 Exchange 2013**     |  客户端访问服务器和邮箱服务器       |
|**Exchange 2019**     |   客户端访问服务器和中心传输服务器      |
|**SharePoint**     |    前端 SharePoint Web 服务器，包括托管中心管理服务器的 Web 服务器     |
|**文件分类基础结构**     |   装有文件资源管理器的 Windows Server 计算机      |
| | |

此配置需要注册表设置，具有以下选项：

- [自动编辑注册表设置](#edit-registry-settings-automatically---advantages-and-disadvantages)
- [手动编辑注册表设置](#edit-registry-settings-manually---advantages-and-disadvantages)

> [!IMPORTANT]
> 对于这两种情况，都必须手动安装所有必备组件，并将 Exchange、SharePoint 和文件分类基础结构配置为使用权限管理。

> [!NOTE]
> 对于大多数组织，使用适用于 Microsoft RMS 连接器的服务器配置工具进行自动配置是更好的选择，因为它提供优于手动配置的效率和可靠性。
> 

在这些服务器上进行配置更改之后，如果这些服务器正在运行 Exchange 或 SharePoint 并且以前配置为使用 AD RMS，则必须重新启动它们。 在首次将它们配置为使用权限管理时，无需重新启动它们。 

进行这些配置更改后，始终必须重新启动配置为使用文件分类基础结构的文件服务器。
### <a name="edit-registry-settings-automatically---advantages-and-disadvantages"></a>自动编辑注册表设置-优点和缺点

使用适用于 Microsoft RMS 连接器的服务器配置工具自动编辑你的注册表设置。

**优点包括**：

- 不直接编辑注册表。 可以使用脚本进行自动编辑。

- 无需运行 Windows PowerShell cmdlet 来获取你的 Microsoft RMS URL。

- 如果你本地运行工具，则自动为你检查必备组件（但不自动进行补救）。

**缺点包括**：运行该工具时，必须连接到已在运行 RMS 连接器的服务器。

有关详细信息，请参阅 [如何使用适用于 MICROSOFT RMS 连接器的服务器配置工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。
### <a name="edit-registry-settings-manually---advantages-and-disadvantages"></a>手动编辑注册表设置-优点和缺点

**优点包括**：不需要连接到运行 RMS 连接器的服务器。

**缺点包括**：

- 更多管理开销，容易发生错误。

- 你必须获取 Microsoft RMS URL，这需要你运行 Windows PowerShell 命令。

- 你必须始终自行进行所有必备组件检查。

### <a name="how-to-use-the-server-configuration-tool-for-microsoft-rms-connector"></a>如何使用适用于 Microsoft RMS 连接器的服务器配置工具

1.  如果尚未下载适用于 Microsoft RMS 连接器的服务器配置工具的脚本 **( # A0)**，请从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkId=314106)下载它。

2.  将 **GenConnectorConfig.ps1** 文件保存在运行该工具的计算机上。 

    如果要在本地运行该工具，则此计算机必须是你想要配置为与 RMS 连接器通信的服务器。 否则，你可将文件保存在任何计算机上。

3.  确定如何运行工具：
    
    |方法  |说明  |
    |---------|---------|
    |**就地**     |  从要配置为与 RMS 连接器通信的服务器以交互方式运行该工具。 <br><br>**提示**：这对于一次性配置（例如测试环境）非常有用。       |
    |**软件部署**     |  运行该工具以生成注册表文件，然后将其部署到一个或多个相关服务器。 <br><br>使用支持软件部署的系统管理应用程序（如 System Center Configuration Manager）部署注册表文件。       |
    |**组策略**     | 运行该工具以生成一个脚本，该脚本可为管理员创建要配置的服务器的组策略对象。 <br><br>此脚本为要配置的每个服务器类型创建一个组策略对象，然后管理员能够将此对象分配给相关服务器。        |
    | | |

    > [!NOTE]
    > 此工具可以配置将与 RMS 连接器通信并已在本部分开头列出的服务器。 不要在运行 RMS 连接器的服务器上运行此工具。

4.  使用 " **以管理员身份运行** " 选项启动 Windows PowerShell，并使用 **get-help** 命令阅读有关如何将工具用于你选择的配置方法的说明：

    ```PowerShell
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

若要运行脚本，你必须输入组织的 RMS 连接器的 URL。 

输入协议前缀（HTTP:// 或 HTTPS://），以及你在 DNS 中为连接器的负载平衡地址定义的连接器名称， 例如，`https:\//connector.contoso.com`。 

然后，此工具会使用该 URL 来联系运行 RMS 连接器的服务器，并获取用于创建所需配置的其他参数。

> [!IMPORTANT]
> 当你运行此工具时，请确保指定组织的负载平衡 RMS 连接器的名称，而不要指定运行 RMS 连接器服务的单个服务器的名称。

使用以下部分获取每个服务类型的特定信息：

-   [将 Exchange 服务器配置为使用连接器](#configuring-an-exchange-server-to-use-the-connector)

-   [将 SharePoint 服务器配置为使用连接器](#configuring-a-sharepoint-server-to-use-the-connector)

-   [将文件分类基础结构的文件服务器配置为使用连接器](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

**何时在未配置为使用连接器的单独计算机上安装客户端应用程序**

在将这些服务器配置为使用连接器之后，本地安装在这些服务器上的客户端应用程序可能无法使用 RMS。 发生这种情况的原因是应用程序试图使用连接器而不是直接使用 RMS，但这种方式不受支持。

此外，如果在 Exchange 服务器上本地安装 Office 2010，则在将服务器配置为使用连接器之后，客户端应用的 IRM 功能可能从该计算机运行，但这不受支持。 

在上述两种情况下，你必须在没有配置为使用连接器的单独计算机上安装客户端应用程序。 然后它们即可正确地直接使用 RMS。

> [!IMPORTANT]
> Office 2010 外延支持已于 2020 年 10 月 13 日结束。 有关详细信息，请参阅 [AIP 和旧版 Windows 和 Office 版本](known-issues.md#aip-and-legacy-windows-and-office-versions)。
> 
## <a name="configuring-an-exchange-server-to-use-the-connector"></a>将 Exchange 服务器配置为使用连接器
以下 Exchange 角色将与 RMS 连接器通信：

-   对于 Exchange 2016 和 Exchange 2013：客户端访问服务器和邮箱服务器

-   对于 Exchange 2019：客户端访问服务器和集线器传输服务器

若要使用 RMS 连接器，这些运行 Exchange 的服务器必须运行以下软件版本之一：

-   Exchange Server 2016

-   Exchange Server 2013，附带 Exchange 2013 累积更新 3

-   Exchange Server 2019

你还需要在服务器上安装能够支持 RMS 加密模式 2 的 RMS 客户端版本 1，也称为 MSDRM。 所有 Windows 操作系统都包括 MSDRM 客户端，但早期版本的客户端不支持加密模式 2。 如果 Exchange 服务器至少运行 Windows Server 2012，则无需进一步的操作，因为使用这些操作系统安装的 RMS 客户端可本机支持加密模式 2。 


> [!IMPORTANT]
> 如果没有安装这些版本或更高版本的 Exchange 和 MSDRM 客户端，就无法将 Exchange 配置为使用连接器。 继续之前，请确认已安装这些版本。

### <a name="to-configure-exchange-servers-to-use-the-connector"></a>将 Exchange 服务器配置为使用连接器

1. 通过使用 RMS 连接器管理工具和[授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)部分的信息，确保 Exchange 服务器有权使用 RMS 连接器。 

    需要此配置，以便 Exchange 可以使用 RMS 连接器。

2. 在与 RMS 连接器通信的 Exchange 服务器角色上执行以下任一操作：

   -   **运行适用于 MICROSOFT RMS 连接器的服务器配置工具**。 

       有关详细信息，请参阅 [如何使用适用于 MICROSOFT RMS 连接器的服务器配置工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，若要在本地运行该工具以配置运行 Exchange 2016 或 Exchange 2013 的服务器，请执行以下操作：

       ```PowerShell
       .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
       ```

    
   -   **进行手动注册表编辑**。 有关详细信息，请参阅 [RMS 连接器的注册表设置](rms-connector-registry-settings.md)。 

3. 使用 Exchange PowerShell cmdlet [set-irmconfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration)启用适用于 EXCHANGE 的 IRM 功能。 设置 `InternalLicensingEnabled $true` 和 `ClientAccessServerEnabled $true`。


## <a name="configuring-a-sharepoint-server-to-use-the-connector"></a>将 SharePoint 服务器配置为使用连接器

前端 SharePoint webservers，包括托管管理中心服务器的服务器，与 RMS 连接器通信。

若要使用 RMS 连接器，这些运行 SharePoint 的服务器必须运行以下软件版本之一：

-   SharePoint Server 2019

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

运行 SharePoint 2019、2016或 SharePoint 2013 的服务器还必须运行 RMS 连接器支持的 MSIPC 客户端2.1 版本。 

若要确保使用受支持的版本，请从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=38396)下载最新的客户端。

> [!WARNING]
> MSIPC 2.1 客户端有多个版本，因此请确保安装版本 1.0.2004.0 或更高版本。
>
> 你可以通过检查 MSIPC.dll 的版本号来验证客户端版本，该文件位于 **\Program Files\Active Directory Rights Management Services Client 2.1**。 属性对话框将显示 MSIPC 2.1 客户端的版本号。

运行 SharePoint 2010 的服务器必须安装了能够支持 RMS 加密模式 2 的 MSDRM 客户端版本。 Windows Server 2012 和 Windows Server 2012 R2 以本机方式支持加密模式 2。

### <a name="to-configure-sharepoint-servers-to-use-the-connector"></a>将 SharePoint 服务器配置为使用连接器

1. 通过使用 RMS 连接器管理工具和[授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)部分的信息，确保 SharePoint 服务器有权使用 RMS 连接器。 

    需要此配置，以便 SharePoint 客户端可使用 RMS 连接器。

2.  在与 RMS 连接器通信的 SharePoint 服务器上执行以下任一操作：

    -   **运行适用于 Microsoft RMS 连接器的服务器配置工具** 

        有关详细信息，请参阅 [如何使用适用于 MICROSOFT RMS 连接器的服务器配置工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，若要在本地运行该工具以配置运行 SharePoint 2019、2016或 SharePoint 2013 的服务器，请执行以下操作：

        ```PowerShell
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   **如果你使用的是 sharepoint 2019、2016或 sharepoint 2013，** 请使用 [RMS 连接器的注册表设置](rms-connector-registry-settings.md) 中的信息，在服务器上手动添加注册表设置，进行手动注册表编辑。 

3.  在 SharePoint 中启用 IRM。 有关详细信息，请参阅 SharePoint 库中的[配置信息权限管理 (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/hh545607(v=office.14))。

    当你按照这些说明操作时，必须通过指定 **“使用此 RMS 服务器”**，将 SharePoint 配置为使用连接器，然后输入你配置的负载平衡连接器 URL。 

    输入协议前缀（HTTP:// 或 HTTPS://），以及你在 DNS 中为连接器的负载平衡地址定义的连接器名称， 

    例如，如果你的连接器名称为 `https:\//connector.contoso.com`，则配置将如下图所示：

    ![为 RMS 连接器配置 SharePoint Server](./media/AzRMS_SharePointConnector.png)

    在 SharePoint 场上启用 IRM 之后，你可以使用每个库的 **“库设置”** 页上的 **“信息权限管理”** 选项，在各个库上启用 IRM。

## <a name="configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector"></a>将文件分类基础结构的文件服务器配置为使用连接器

若要使用 RMS 连接器和文件分类基础结构来保护 Office 文档，文件服务器必须运行以下操作系统之一：

- Windows Server 2016

- Windows Server 2012 R2

- Windows Server 2012

### <a name="to-configure-file-servers-to-use-the-connector"></a>将文件服务器配置为使用连接器

1. 通过使用 RMS 连接器管理工具和[授权服务器使用 RMS 连接器](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)部分的信息，确保文件服务器有权使用 RMS 连接器。 

    需要此配置，以便文件客户端可使用 RMS 连接器。

2. 在为文件分类基础结构配置的、将与 RMS 连接器通信的文件服务器上执行以下任一操作：

    -   **运行适用于 Microsoft RMS 连接器的服务器配置工具** 
    
        有关详细信息，请参阅 [如何使用适用于 MICROSOFT RMS 连接器的服务器配置工具](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)。

        例如，若要在本地运行该工具以配置运行 FCI 的文件服务器，请执行以下操作：

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - 通过使用 [RMS 连接器的注册表设置](rms-connector-registry-settings.md)中的信息在服务器上手动添加注册表设置，**进行手动注册表编辑**。 

3. 创建分类规则和文件管理任务，才能使用 RMS 加密保护文档，然后指定一个用于自动将 RMS 策略的应用的 RMS 模板。 

    有关详细信息，请参阅 Windows Server 文档库中的 [文件服务器资源管理器概述](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11)) 。

## <a name="next-steps"></a>后续步骤
由于已安装并配置 RMS 连接器，并且服务器已配置为使用该连接器，IT 管理员和用户可以使用 Azure Rights Management Services 保护和使用电子邮件与文档。 

若要让用户轻松使用此功能，请部署 Azure 信息保护客户端，它会安装 Office 的外接程序并在文件资源管理器中添加新的右键单击选项。 

有关详细信息，请参阅 [Azure 信息保护客户端管理员指南](./rms-client/client-admin-guide.md)。

请注意，若要配置用于 Exchange 传输规则或 Windows Server FCI 的部门模板，范围配置必须包含应用程序兼容性选项，以选中“如果应用程序不支持用户标识，则向所有用户显示此模板”复选框。

可以使用 [Azure 信息保护部署路线图](deployment-roadmap-classify-label-protect.md)，检查向用户和管理员推出 Azure Rights Management 之前是否还需要执行其他配置步骤。

若要监视 RMS 连接器，请参阅[监视 Azure Rights Management 连接器](monitor-rms-connector.md)。