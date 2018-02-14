---
title: "安装和配置 Rights Management 连接器 - AIP"
description: "可以参考本文中的信息来安装和配置 Azure Rights Management (RMS) 连接器。 这些过程涉及到“部署 Azure Rights Management 连接器”中的步骤 1-4。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/03/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e4aabc3c571ca132327748935ab3aeafa002db0
ms.sourcegitcommit: e21fb3385de6f0e251167e5dc973e90f0e7f2bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="installing-and-configuring-the-azure-rights-management-connector"></a>安装和配置 Azure Rights Management 连接器

>*适用于：Azure 信息保护、Office 365*

可以参考以下信息来安装和配置 Azure Rights Management (RMS) 连接器。 这些过程涉及到[部署 Azure Rights Management 连接器](deploy-rms-connector.md)中的步骤 1-4。

在开始之前，请确保已查看并检查此部署的[先决条件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)。


## <a name="installing-the-rms-connector"></a>安装 RMS 连接器

1.  确定将要运行 RMS 连接器的计算机（最少两台）。 它们必须满足先决条件中列出的最低规格。

    > [!NOTE]
    > 备注为每个租户（Office 365 租户或 Azure AD 租户）安装单个 RMS 连接器（包含多个服务器以实现高可用性）。 与 Active Directory RMS 不同，无需在每个林中安装 RMS 连接器。

2.  从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkId=314106)下载 RMS 连接器的源文件。

    若要安装 RMS 连接器，请下载 RMSConnectorSetup.exe。

    此外：

    -   如果以后要从 32 位计算机配置连接器，请下载 RMSConnectorAdminToolSetup_x86.exe。

    -   若要使用 RMS 连接器的服务器配置工具以自动执行本地服务器上的注册表设置的配置，另请下载 GenConnectorConfig.ps1。

3.  在要安装 RMS 连接器的计算机上，以管理员权限运行 **RMSConnectorSetup.exe**。

4.  在 Microsoft Rights Management 连接器安装程序的欢迎页上，选择“在计算机上安装 Microsoft Rights Management 连接器”，然后单击“下一步”。

5.  阅读并同意 RMS 连接器许可条款，然后单击“下一步”。

若要继续，请输入帐户和密码以配置 RMS 连接器。

## <a name="entering-credentials"></a>输入凭据
在能够配置 RMS 连接器之前，必须输入具有足够 RMS 连接器配置权限的帐户的凭据。 例如，可以键入 **admin@contoso.com**，然后指定此帐户的密码。

此帐户不得要求进行多重身份验证 (MFA)，因为 Microsoft Rights Management 管理工具不支持对此帐户进行 MFA。 

连接器对于此密码还有一些字符限制。 不可使用具有下列任一字符的密码：& 号 (**&**)、左方括号 (**[**)、右方括号 (**]**)、直引号 (**"**) 和撇号 (**'**)。 如果密码包含上述任一字符，尽管在其他方案中可以使用此帐户和密码成功登录，但针对 RMS 连接器的身份验证也会失败，并且会显示“该用户名和密码组合不正确”的错误消息。 如果方案适用于密码，请使用密码不包含上述任一特殊字符的其他帐户，或者重置密码使其不包含上述任一特殊字符。

此外，如果实施了[加入控制机制](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)，请确保指定的帐户能够保护内容。 例如，如果限制为只有“IT 部门”组可以保护内容，那么在此处指定的帐户必须是该组成员。 若未实现，会显示以下错误消息：“发现管理服务和组织位置的尝试失败。请确保为组织启用 Microsoft Rights Management 服务。”

可以使用具有以下某一种权限的帐户：

-   **租户的全局管理员**：作为 Office 365 租户或 Azure AD 租户全局管理员的帐户。

-   **Azure Rights Management 全局管理员**：Azure Active Directory 中已分配为 Azure RMS 全局管理员角色的帐户。

-   **Azure Rights Management 连接器管理员**：Azure Active Directory 中已被授权为组织安装和管理 RMS 连接器的帐户。

    > [!NOTE]
    > 通过使用 Azure RMS [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) cmdlet，向帐户分配 Azure Rights Management 全局管理员角色和 Azure Rights Management 连接器管理员角色。
    > 
    > 若要使用最小特权运行 RMS 连接器，请为此创建一个专用帐户，然后通过执行以下操作为帐户分配 Azure RMS 连接器管理员角色：
    >
    > 1.  下载并安装适用于 Rights Management 的 Windows PowerShell（如果尚未这样做）。 有关详细信息，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](install-powershell.md)。
    >
    >     使用“以管理员身份运行”命令启动 Windows PowerShell，并使用 [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice) 命令连接到 Azure RMS 服务：
    >
    >     ```
    >     Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  然后运行 [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) 命令，仅使用以下参数之一：
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     例如，键入 **Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role "ConnectorAdministrator"**
    >
    >     尽管这些命令会分配连接器管理员角色，但也可以在此处使用 GlobalAdministrator 角色。

在 RMS 连接器安装过程中，将会验证和安装所有必备软件。如果还没有 Internet Information Services (IIS)，则会安装该服务。另外还要安装并配置连接器软件。 此外，还会创建以下各项，做好配置 Azure RMS 的准备：

-   一个空表，用于列出被授权使用连接器与 Azure RMS 通信的服务器。 以后可将服务器添加至此表。

-   一组连接器安全令牌，授权对 Azure RMS 所进行的操作。 可从 Azure RMS 下载这些令牌，并安装在注册表中的本地计算机上。 它们通过使用数据保护应用程序编程接口 (DPAPI) 和本地系统帐户凭据得到保护。

在向导的最后一页上执行以下操作，然后单击“完成”：

-   如果这是安装的第一个连接器，此时请不要选择“启动连接器管理员控制台对服务器授权”。 在安装第二个（或最后一个）RMS 连接器之后，再选择此选项。 请在至少一台其他计算机上再次运行向导。 必须安装至少两个连接器。

-   如果已安装第二个（或最后一个）连接器，请选择“启动连接器管理员控制台对服务器授权”。

> [!TIP]
> 现在，可以执行一项验证测试，以测试 RMS 连接器的 Web 服务是否可以运行：
>
> -   从 Web 浏览器连接到 **http://&lt;connectoraddress&gt;/_wmcs/certification/servercertification.asmx**（请将 *&lt;connectoraddress&gt;* 替换为安装 RMS 连接器的服务器地址或名称）。 如果成功连接，则将显示 **ServerCertificationWebService** 页。

如果需要卸载 RMS 连接器，请再次运行向导并选择卸载选项。

如果在安装过程中遇到任何问题，请检查安装日志：**%LocalAppData%\Temp\Microsoft Rights Management connector_\<date and time>.log** 

例如，安装日志可能类似于 C:\Users\Administrator\AppData\Local\Temp\Microsoft Rights Management connector_20170803110352.log

## <a name="authorizing-servers-to-use-the-rms-connector"></a>授权服务器使用 RMS 连接器
在至少两台计算机上安装 RMS 连接器之后，即可为你希望其使用 RMS 连接器的服务器和服务授权。 例如运行 Exchange Server 2013 或 SharePoint Server 2013 的服务器。

若要定义这些服务器，请运行 RMS 连接器管理工具，然后向允许服务器列表添加条目。 如果在 Microsoft Rights Management 连接器设置向导结束时选择了“启动连接器管理员控制台对服务器授权”，则可运行此工具，也可从向导单独运行此工具。

向这些服务器授权时，请注意以下事项：

- 添加的服务器会被授予特殊权限。 在连接器配置中为 Exchange Server 角色指定的所有帐户在 Azure RMS 中授予[超级用户角色](configure-super-users.md)，这会给予他们访问此 RMS 租户的所有内容的权限。 如有必要，超级用户功能将在此时自动启用。 为了避免权限提升带来的安全风险，请注意仅指定组织的 Exchange 服务器使用的帐户。 配置为 SharePoint 服务器的所有服务器或使用 FCI 的文件服务器会被授予常规用户权限。

- 可以通过指定 Active Directory 安全或分发组，或由多台服务器使用的服务帐户，添加多个服务器作为单个条目。 使用此配置时，服务器组共享相同的 RMS 证书，并且被视为其中任何一个服务器保护的内容的所有者。 为了最大程度地减少管理开销，我们建议使用这种单组配置，而不是使用单独服务器的配置，为组织的 Exchange 服务器或 SharePoint 服务器场授权。

在“被允许使用连接器的服务器”页上，单击“添加”。

> [!NOTE]
> 备注在 Azure RMS 中授权服务器等效于 AD RMS 配置，都可将 NTFS 权限手动应用到服务或服务器计算机帐户的 ServerCertification.asmx 中，并可向用户手动授予到 Exchange 帐户的超级权限。 此连接器上无需将 NTFS 权限应用到 ServerCertification.asmx。


### <a name="add-a-server-to-the-list-of-allowed-servers"></a>将服务器添加到允许服务器列表
在“允许服务器使用连接器”页上，输入对象的名称，或进行浏览以确定要授权的对象。

必须为正确的对象授权，这一点非常重要。 若要让服务器使用连接器，必须选择运行本地服务（例如 Exchange 或 SharePoint）的帐户来进行授权。 例如，如果服务作为配置的服务帐户运行，请将该服务帐户的名称添加到列表。 如果服务作为本地系统运行，请添加该计算机对象的名称（例如 SERVERNAME$）。 最佳做法是创建一个包含这些帐户的组并指定该组，而不是指定单独的服务器名称。

有关不同服务器角色的详细信息：

-   对于运行 Exchange 的服务器：必须指定一个安全组，并可使用 Exchange 自动创建和维护的包含林中所有 Exchange 服务器的默认组（“Exchange 服务器”）。

-   对于运行 SharePoint 的服务器：

    -   如果 SharePoint 2010 服务器配置为作为本地系统（它不使用服务帐户）运行，请在 Active Directory 域服务中手动创建安全组，并将此配置中的服务器的计算机名称对象添加到此组。

    -   如果 SharePoint 服务器配置为使用服务帐户（SharePoint 2010 的建议做法，并且是 SharePoint 2016 和 SharePoint 2013 的唯一选项），请执行以下操作：

        1.  添加运行 SharePoint 管理中心服务的服务帐户，以便从管理员控制台配置 SharePoint。

        2.  添加为 SharePoint 应用池配置的帐户。

        > [!TIP]
        > 提示如果上述两个帐户是不同的，可考虑创建包含这两个帐户的单个组，以最大程度地降低管理开销。

-   对于使用文件分类基础结构的文件服务器，相关服务作为本地系统帐户运行，因此必须为文件服务器（例如 SERVERNAME$）的计算机帐户或包含这些计算机帐户的组授权。

在将服务器添加至列表之后，请单击“关闭”。

如果尚未配置负载均衡，则现在必须为安装了 RMS 连接器的服务器配置负载均衡，并考虑是否使用 HTTPS 在这些服务器和刚才授权的服务器之间进行连接。

## <a name="configuring-load-balancing-and-high-availability"></a>配置负载均衡和高可用性
安装 RMS 连接器的第二个或最后一个实例之后，请定义连接器 URL 服务器名称并配置负载均衡系统。

连接器 URL 服务器名称可以是控制的命名空间中的任何名称。 例如，可在 DNS 系统中为 **rmsconnector.contoso.com** 创建一个条目，并将此条目配置为使用负载均衡系统中的 IP 地址。 此名称没有任何特殊要求，也无需在连接器服务器本身上进行配置。 除非 Exchange 和 SharePoint 服务器要通过 Internet 与连接器通信，否则此名称无需在 Internet 上解析。

> [!IMPORTANT]
> 在将 Exchange 或 SharePoint 服务器配置为使用连接器之后，我们建议不要更改该名称，因为随后必须清除这些服务器的所有 IRM 配置，然后重新进行配置。

在 DNS 中创建名称并配置 IP 地址之后，请配置该地址的负载均衡，将流量定向到连接器服务器。 可以使用任何基于 IP 的负载均衡器来达到此目的，该负载均衡器应包括 Windows Server 中的网络负载均衡 (NLB) 功能。 有关详细信息，请参阅[负载均衡部署指南](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx)。

使用以下设置来配置 NLB 群集：

-   端口：80（对于 HTTP）或 443（对于 HTTPS）

    有关如何使用 HTTP 或 HTTPS 的详细信息，请参阅下一部分。

-   关联：无

-   分发方法：等于

为负载均衡的系统（为运行 RMS 连接器服务的服务器）定义的此名称是稍后将本地服务器配置为使用 Azure RMS 时要使用的组织 RMS 连接器名称。

## <a name="configuring-the-rms-connector-to-use-https"></a>将 RMS 连接器配置为使用 HTTPS
> [!NOTE]
> 此配置步骤是可选的，但我们建议执行此步骤以提高安全性。

虽然使用 TLS 或 SSL 对于 RMS 连接器是可选的，但我们建议将其用于任何基于 HTTP 的安全敏感服务。 在此配置中，运行连接器的服务器向使用连接器的 Exchange 和 SharePoint 服务器进行身份验证。 此外，从这些服务器向连接器发送的所有数据都进行了加密。

若要让 RMS 连接器能够使用 TLS，请在运行 RMS 连接器的每个服务器上安装服务器身份验证证书，其中包含用于连接器的名称。 例如，如果在 DNS 中定义的 RMS 连接器名称为 **rmsconnector.contoso.com**，请部署一个服务器身份验证证书，其中的证书使用者包含 **rmsconnector.contoso.com** 作为通用名称。 也可在证书备选名称中指定 **rmsconnector.contoso.com** 作为 DNS 值。 证书不一定必须包括服务器的名称。 然后在 IIS 中，将此证书绑定到默认网站。

如果使用 HTTPS 选项，请确保运行连接器的所有服务器都具有有效的服务器身份验证证书，该证书链接到 Exchange 和 SharePoint 服务器信任的根 CA。 此外，如果为连接器服务器颁发证书的证书颁发机构 (CA) 发布了证书吊销列表 (CRL)，则 Exchange 和 SharePoint 服务器必须能够下载此 CRL。

> [!TIP]
> 可使用以下信息和资源，帮助请求和安装服务器身份验证证书，并将此证书绑定到 IIS 中的默认网站：
>
> -   如果使用 Active Directory 证书服务 (AD CS) 和企业证书颁发机构 (CA) 来部署这些服务器身份验证证书，则可以复制和使用 Web 服务器证书模板。 此证书模板使用“在请求中提供”作为证书使用者名称，这意味着在请求证书时，可以提供 RMS 连接器名称的 FQDN 作为证书使用者名称或使用者备选名称。
> -   如果使用独立 CA 或从其他公司购买此证书，请参阅 TechNet 上 [Web 服务器 (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) 文档库中的[配置 Internet 服务器证书 (IIS 7)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx)。
> -   若要将 IIS 配置为使用证书，请参阅 TechNet 上 [Web 服务器 (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) 文档库中的[添加网站绑定 (IIS 7)](http://technet.microsoft.com/library/cc731692.aspx)。

## <a name="configuring-the-rms-connector-for-a-web-proxy-server"></a>为 Web 代理服务器配置 RMS 连接器
如果连接器服务器安装在没有直接 Internet 连接的网络中，需要手动配置出站 Internet 访问的 Web 代理服务器，则必须在 RMS 连接器的这些服务器上配置注册表。

#### <a name="to-configure-the-rms-connector-to-use-a-web-proxy-server"></a>将 RMS 连接器配置为使用 Web 代理服务器

1.  在运行 RMS 连接器的每台服务器上，打开注册表编辑器，例如 Regedit。

2.  导航到 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  添加 **ProxyAddress** 的字符串值，然后将此值的数据设置为 **http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**

    例如：**http://proxyserver.contoso.com:8080**

4.  关闭注册表编辑器，然后重启服务器，或者执行 IISReset 命令以重启 IIS。

## <a name="installing-the-rms-connector-administration-tool-on-administrative-computers"></a>在管理计算机上安装 RMS 连接器管理工具
可以在未安装 RMS 连接器的计算机上运行 RMS 连接器管理工具，前提是该计算机符合以下要求：

-   运行 Windows Server 2012 或 Windows Server 2012 R2（所有版本）、Windows Server 2008 R2 或 Windows Server 2008 R2 Service Pack 1（所有版本）、Windows 8.1、Windows 8 或 Windows 7 的物理或虚拟计算机。

-   至少 1 GB 的 RAM。

-   至少 64 GB 的磁盘空间。

-   至少一个网络接口。

-   通过防火墙（或 Web 代理）访问 Internet。

若要安装 RMS 连接器管理工具，请运行以下文件：

-   对于 32 位计算机：运行 RMSConnectorAdminToolSetup_x86.exe

-   对于 64 位计算机：运行 RMSConnectorSetup.exe

如果尚未下载这些文件，可从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkId=314106)下载。


## <a name="next-steps"></a>后续步骤
安装并配置 RMS 连接器后，可将本地服务器配置为使用此连接器。 参阅[为 Azure Rights Management 连接器配置服务器](configure-servers-rms-connector.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
