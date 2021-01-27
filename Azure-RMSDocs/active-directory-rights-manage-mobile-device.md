---
title: 适用于 AIP 的 Active Directory rights management services 移动设备扩展
description: 了解 Active Directory 适用于 AIP 的移动设备扩展
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3fca14f82db5cd78727b14cc417517921baa0f7b
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98808588"
---
# <a name="active-directory-rights-management-services-mobile-device-extension"></a>Active Directory Rights Management Services 移动设备扩展

>***适用于**： Windows Server 2019、2016、2012 R2 和 2012 *
>
>相关内容：*[AIP 统一标记客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

你可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=43738) 下载 Active Directory Rights Management Services (AD RMS) 移动设备扩展，并在现有 AD RMS 部署之上安装此扩展。 这允许用户在其设备支持最新的启用应用时保护和使用敏感数据。 例如，用户可以执行以下操作：
- 使用 Azure 信息保护应用以不同格式使用受保护的文本文件， (包括 .txt、.csv 和 .xml) 。
- 使用 Azure 信息保护应用来使用受保护的图像文件 (包括 .jpg、.gif 和 .tif) 。
- 使用 Azure 信息保护应用打开已 ( 的常规保护文件) 。
- 使用 Azure 信息保护应用打开 (Word、Excel、PowerPoint) 的 Office 文件，该文件是 ( .pdf 和格式) 的 PDF 副本。
- 使用 Azure 信息保护应用在 Microsoft SharePoint 上打开受保护的电子邮件 ( .rpmsg) 和受保护的 PDF 文件。
- 使用 AIP-启用 PDF 查看器进行跨平台查看，或打开使用任何 AIP 启用应用程序保护的 PDF 文件。
- 使用使用 [MIP SDK](/information-protection/develop/)编写的内部开发的 AIP 启用应用。

> [!NOTE]
> 你可以从 Microsoft 网站的 [microsoft Rights Management](https://go.microsoft.com/fwlink/?linkid=303970) 页面下载 Azure 信息保护应用。 有关移动设备扩展支持的其他应用的信息，请参阅本文档中的 [应用程序](./requirements-applications.md) 页中的表。 有关 RMS 支持的不同文件类型的详细信息，请参阅 Rights Management 共享应用程序管理员指南 "中的 [支持的文件类型和文件扩展名](/rights-management/rms-client/sharing-app-admin-guide-technical#supported-file-types-and-file-name-extensions) 部分。

> [!IMPORTANT]
> 在安装移动设备扩展之前，请务必阅读并配置先决条件。

有关其他信息，请从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=40333)下载 "Microsoft Azure 信息保护" 白皮书和随附的脚本。

## <a name="prerequisites-for-ad-rms-mobile-device-extension"></a>AD RMS 移动设备扩展的先决条件

安装 AD RMS 移动设备扩展之前，请确保已准备好以下依赖项。


|要求|更多信息|
|---------------|------------------------|
|Windows Server 2019、2016、2012 R2 或2012上的现有 AD RMS 部署，包括以下各项：<br /><br /> -您的 AD RMS 群集必须可从 Internet 访问。 <br /><br /> -AD RMS 必须在单独的服务器上使用完全基于 Microsoft SQL Server 的数据库，而不是通常用于在同一服务器上测试的 Windows 内部数据库。 <br /><br />-用于安装移动设备扩展的帐户必须对用于 AD RMS 的 SQL Server 实例具有 sysadmin 权限。 <br /><br />-必须将 AD RMS 服务器配置为使用 SSL/TLS，其中包含移动设备客户端信任的有效 x.509 证书。<br /><br /> -如果 AD RMS 服务器位于防火墙后面或使用反向代理发布，则除了将 **/_wmcs** 文件夹发布到 Internet 外，还必须发布/my 文件夹 (例如： **_https： \/ \/ RMSserver.contoso.com/my**) 。|有关 AD RMS 先决条件和部署信息的详细信息，请参阅本文的先决条件部分。|
|Windows Server 上部署的 AD FS：<br /><br /> -必须能够从 Internet 访问你的 AD FS 服务器场 (你已) 部署了联合服务器代理。 <br /><br />-不支持基于窗体的身份验证;必须使用 Windows 集成身份验证 <br /><br /> **重要说明**： AD FS 必须在运行 AD RMS 的计算机和移动设备扩展上运行不同的计算机。|有关 AD FS 的文档，请参阅 Windows Server 库中的 [Windows server AD FS 部署指南](/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on) 。<br /><br /> 必须为移动设备扩展配置 AD FS。 有关说明，请参阅本主题中的 **配置 AD RMS 移动设备扩展的 AD FS** 部分。|
|移动设备必须信任 RMS 服务器 (或服务器上的 PKI 证书) |从公共 CA （如 VeriSign 或 Comodo）购买服务器证书时，移动设备可能已信任这些证书的根 CA，因此这些设备将信任服务器证书，而无需进行配置。<br /><br /> 但是，如果使用自己的内部 CA 为 RMS 部署服务器证书，则必须执行其他步骤以在移动设备上安装根 CA 证书。 如果不这样做，移动设备将无法与 RMS 服务器建立成功的连接。|
|DNS 中的 SRV 记录|在一个或多个公司域中创建一条或多条 SRV 记录：<br /><br />1：为用户将使用的每个电子邮件域后缀创建一条记录 <br /><br />2：为你的 RMS 群集用于保护内容的每个 FQDN 创建一条记录，而不包括群集名称 <br /><br />这些记录必须可从连接的移动设备使用的任何网络（包括 intranet，如果移动设备通过 intranet 连接）进行解析。<br /><br /> 当用户从其移动设备提供电子邮件地址时，将使用域后缀来确定是否应使用 AD RMS 基础结构或 Azure AIP。 找到 SRV 记录后，客户端将重定向到对应于该 URL 的 AD RMS 服务器。<br /><br /> 如果用户使用移动设备使用受保护的内容，则客户端应用程序将在 DNS 中查找与保护内容的群集 URL 中的 FQDN 相匹配的记录，而不会将 (的群集名称) 。 然后，设备定向到在 DNS 记录中指定的 AD RMS 群集并获取许可证以打开该内容。 在大多数情况下，RMS 群集将会是用于保护内容的同一 RMS 群集。<br /><br /> 有关如何指定 SRV 记录的信息，请参阅本主题中的为 **AD RMS 移动设备扩展指定 DNS SRV 记录** 部分。|
|支持的客户端使用通过使用适用于此平台的 MIP SDK 开发的应用程序。 |使用 [Microsoft Azure 信息保护](https://www.microsoft.com/download/details.aspx?id=40333) 下载 "页上的链接下载所用设备支持的应用。|

### <a name="configuring-ad-fs-for-the-ad-rms-mobile-device-extension"></a>为 AD RMS 移动设备扩展配置 AD FS

必须先配置 AD FS，然后为要使用的设备授权 AIP 应用。

#### <a name="step-1-to-configure-ad-fs"></a>步骤1：配置 AD FS

- 可以运行 Windows PowerShell 脚本自动配置 AD FS 以支持 AD RMS 移动设备扩展，也可以手动指定配置选项和值：
    - 若要为 AD RMS 移动设备扩展自动配置 AD FS，请将以下内容复制并粘贴到 Windows PowerShell 脚本文件中，然后运行该脚本：

```powershell
# This Script Configures the Microsoft Rights Management Mobile Device Extension and Claims used in the ADFS Server

# Check if Microsoft Rights Management Mobile Device Extension is configured on the Server
$CheckifConfigured = Get-AdfsRelyingPartyTrust -Identifier "api.rms.rest.com"
if ($CheckifConfigured)
{
Write-Host "api.rms.rest.com Identifer used for Microsoft Rights Management Mobile Device Extension is already configured on this Server"
Write-Host $CheckifConfigured
}
else
{
Write-Host "Configuring  Microsoft Rights Management Mobile Device Extension "

# TransformaRules used by Microsoft Rights Management Mobile Device Extension
# Claims: E-mail, UPN and ProxyAddresses
$TransformRules = @"
@RuleTemplate = "LdapClaims"
@RuleName = "Jwt Token"
c:[Type ==
"http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname",
Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types =
("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn",
"http://schemas.xmlsoap.org/claims/ProxyAddresses"), query =
";mail,userPrincipalName,proxyAddresses;{0}", param = c.Value);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through Proxy addresses"
c:[Type == "http://schemas.xmlsoap.org/claims/ProxyAddresses"]
 => issue(claim = c);
"@

# AuthorizationRules used by Microsoft Rights Management Mobile Device Extension
# Allow All users
$AuthorizationRules = @"
@RuleTemplate = "AllowAllAuthzRule"
 => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit",
Value = "true");
"@

# Add a Relying Part Truest with Name -"Microsoft Rights Management Mobile Device Extension" Identifier "api.rms.rest.com"
Add-ADFSRelyingPartyTrust -Name "Microsoft Rights Management Mobile Device Extension" -Identifier "api.rms.rest.com" -IssuanceTransformRules $TransformRules -IssuanceAuthorizationRules  $AuthorizationRules

Write-Host "Microsoft Rights Management Mobile Device Extension Configured"
}
```

- 若要为 AD RMS 移动设备扩展手动配置 AD FS，请使用以下设置：

|**配置**|**值**|
|-----|-----|
|**信赖方信任**|_api。|
|**声明规则**|**属性存储**： Active Directory <br /><br />**电子邮件地址**：电子邮件地址<br /><br>**用户-名称**： UPN<br /><br /> **代理地址**： _https： \/ \/schemas.xmlsoap.org/claims/ProxyAddresses|

> [!TIP]
> 有关使用 AD FS AD RMS 部署示例的分步说明，请参阅 [使用 Active Directory 联合身份验证服务部署 Active Directory Rights Management Services](/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on)。

#### <a name="step-2-authorize-apps-for-your-devices"></a>步骤2：为你的设备授权应用

- 在替换变量以添加对 **Azure 信息保护** 应用的支持后，运行以下 Windows PowerShell 命令。 请确保按显示的顺序运行这两个命令：


```powershell
Add-AdfsClient -Name "R<your application name> " -ClientId "<YOUR CLIENT ID >" -RedirectUri @("<YOUR REDIRECT URI >")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '<YOUR CLIENT ID>' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

**Powershell 示例**
```powershell
Add-AdfsClient -Name "Fabrikam application for MIP" -ClientId "96731E97-2204-4D74-BEA5-75DCA53566C3" -RedirectUri @("com.fabrikam.MIPAPP://authorize")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '96731E97-2204-4D74-BEA5-75DCA53566C3' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

- 对于 **Azure 信息保护统一标签客户端**，请运行以下 Windows PowerShell 命令，以在你的设备上添加对 Azure 信息保护客户端的支持：

```powershell
Add-AdfsClient -Name "Azure Information Protection Client" -ClientId "c00e9d32-3c8d-4a7d-832b-029040e7db99" -RedirectUri @("com.microsoft.azip://authorize")
Grant-AdfsApplicationPermission -ClientRoleIdentifier "c00e9d32-3c8d-4a7d-832b-029040e7db99" -ServerRoleIdentifier api.rms.rest.com -ScopeName "openid"
```
- 若要 **在 Windows 2016 和2019上支持 ADFS** ，并为第三方产品支持 **ADRMS MDE** ，请运行以下 Windows PowerShell 命令：

```powershell
Add-AdfsClient -Name "YOUR APP" -ClientId 'YOUR CLIENT ID' -RedirectUri @("YOUR REDIRECT") 
Grant-AdfsApplicationPermission -ClientRoleIdentifier 'YOUR CLIENT ID' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

若要在 **windows、** **Mac**、mobile 和 **Office mobile** 上配置 AIP 客户端，以便在 **windows Server 2012 R2 和更高版本上使用 AD FS****或 AD RMS 受保护的内容**，请使用以下内容： 

- 对于使用 RMS 共享应用)  (Mac 设备，请确保按显示的顺序运行这两个命令：

```powershell
Add-AdfsClient -Name "RMS Sharing App for macOS" -ClientId "96731E97-2204-4D74-BEA5-75DCA53566C3" -RedirectUri @("com.microsoft.rms-sharing-for-osx://authorize")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '96731E97-2204-4D74-BEA5-75DCA53566C3' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

- 对于使用 Azure 信息保护应用)  (的 iOS 设备，请确保按显示的顺序运行这两个命令：
```powershell
Add-AdfsClient -Name "Azure Information Protection app for iOS" -ClientId "9D7590FB-9536-4D87-B5AA-FAA863DCC3AB" -RedirectUri @("com.microsoft.rms-sharing-for-ios://authorize")
```

```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '9D7590FB-9536-4D87-B5AA-FAA863DCC3AB' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

- 对于使用 Azure 信息保护应用)  (Android 设备，请确保按显示的顺序运行这两个命令：
```powershell
Add-AdfsClient -Name "Azure Information Protection app for Android" -ClientId "ECAD3080-3AE9-4782-B763-2DF1B1373B3A" -RedirectUri @("com.microsoft.rms-sharing-for-android://authorize")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier 'ECAD3080-3AE9-4782-B763-2DF1B1373B3A' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

运行以下 PowerShell 命令，添加对设备上 Microsoft Office 应用的支持：
- 对于 Mac、iOS、Android 设备 (确保按) 显示的顺序运行这两个命令：

```powershell
Add-AdfsClient –Name "Office for Mac and Office Mobile" –ClientId "d3590ed6-52b3-4102-aeff-aad2292ab01c" –RedirectUri @("urn:ietf:wg:oauth:2.0:oob")
```

```powershell
Set-AdfsClient -TargetClientId d3590ed6-52b3-4102-aeff-aad2292ab01c -RedirectUri "urn:ietf:wg:oauth:2.0:oob","launch-word://com.microsoft.Office.Word","launch-excel://com.microsoft.Office.Excel","launch-ppt://com.microsoft.Office.Powerpoint"
```

### <a name="specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension"></a>为 AD RMS 移动设备扩展指定 DNS SRV 记录

必须为你的用户所使用的每个电子邮件域创建 DNS SRV 记录。 如果你的所有用户都使用来自单个父域的子域，并且此连续命名空间中的所有用户都使用相同的 RMS 群集，则可以在父域中仅使用一条 SRV 记录，而 RMS 将会找到相应的 DNS 记录。
SRV 记录采用以下格式： _rmsdisco. _http. _tcp。 \<emailsuffix>\<portnumber>\<RMSClusterFQDN>

> [!NOTE]
> 为指定 443 \<portnumber> 。 尽管可以在 DNS 中指定不同的端口号，但使用移动设备扩展的设备将始终使用443。

例如，如果你的组织具有使用以下电子邮件地址的用户：
  - _user@contoso.com
  - _user@sales.contoso.com
  - _user@fabrikam.com 如果 _contoso .com 的其他子域与名为 _rmsserver 的 RMS 群集不同，请创建两个具有以下值的 DNS SRV 记录：
- _rmsdisco _rmsdisco._http _rmsdisco._http._tcp .com 443 _rmsserver
- _rmsdisco _rmsdisco._http 443 _rmsdisco._http._tcp _rmsserver .com

如果使用 Windows Server 上的 DNS 服务器角色，请在 DNS 管理器控制台中使用以下表格作为 SRV 记录属性的指南：

|字段|值|
|------|------|
|域|_tcp contoso .com
|服务|_rmsdisco
|协议|_http
|优先级|0
|重量|0
|端口号|443
|提供此服务的主机|_rmsserver contoso .com

|字段|值|
|------|------|
|域|_tcp fabrikam
|服务|_rmsdisco
|协议|_http
|优先级|0
|重量|0
|端口号|443
|提供此服务的主机|_rmsserver contoso .com|
| | |

除了你的电子邮件域的这些 DNS SRV 记录外，还必须在 RMS 群集域中创建另一个 DNS SRV 记录。 此记录必须指定用于保护内容的 RMS 群集的 Fqdn。 RMS 所保护的每个文件都包含指向保护该文件的群集的 URL。 移动设备使用 DNS SRV 记录和记录中指定的 URL FQDN 查找可支持移动设备的相应 RMS 群集。

例如，如果你的 RMS 群集为 **_rmsserver**，则创建一个具有以下值的 DNS SRV 记录： **_rmsdisco 443 _rmsserver. _http.** .com

如果使用 Windows Server 上的 DNS 服务器角色，请使用下表作为 DNS 管理器控制台中的 SRV 记录属性的指南：

|字段|值|
|------|------|
|域|_tcp contoso .com
|服务|_rmsdisco
|协议|_http
|优先级|0
|重量|0
|端口号|443
|提供此服务的主机|_rmsserver contoso .com|
| | |

## <a name="deploying-the-ad-rms-mobile-device-extension"></a>部署 AD RMS 移动设备扩展

安装 AD RMS 移动设备扩展之前，请确保之前部分中的先决条件已准备就绪，并且你知道 AD FS 服务器的 URL。 然后执行以下操作：

1. 从 Microsoft 下载中心 ( # A0) 下载 AD RMS 移动设备扩展。
1. 运行 **ADRMS.MobileDeviceExtension.exe** 以启动 Active Directory Rights Management Services 移动设备扩展安装向导。
出现提示时，输入之前配置的 AD FS 服务器的 URL。
1. 完成向导。

在 RMS 群集中的所有节点上运行此向导。

如果 AD RMS 群集与 AD FS 服务器之间有代理服务器，则默认情况下，AD RMS 群集将无法联系联合服务。 发生这种情况时，AD RMS 将无法验证从移动客户端收到的令牌，并将拒绝该请求。 如果你的代理服务器阻止此通信，则必须从 AD RMS 移动设备扩展网站更新 web.config 文件，以便 AD RMS 在需要与 AD FS 服务器联系时可以绕过代理服务器。

#### <a name="updating-proxy-settings-for-the-ad-rms-mobile-device-extension"></a>正在更新 AD RMS 移动设备扩展的代理设置

1. 打开位于 **\Program Files\Active Directory Rights Management Services 移动设备 Extension\Web 服务** 中的 web.config 文件。

1. 将以下节点添加到文件：

    ```PowerShell
       <system.net>
        <defaultProxy>
            <proxy  proxyaddress="http://<proxy server>:<port>"
                    bypassonlocal="true"
            />
            <bypasslist>
                <add address="<AD FS URL>" />
            </bypasslist>
        </defaultProxy>
    <system.net>
    ```
1. 进行以下更改，并保存该文件：
    - \<proxy-server>将替换为代理服务器的名称或地址。
    - 替换 \<port> 为将代理服务器配置为使用的端口号。
    - 替换 \<AD FS URL> 为联合身份验证服务的 URL。 不要包含 HTTP 前缀。

    > [!NOTE]
    > 若要了解有关替代代理设置的详细信息，请参阅 [代理配置](/dotnet/framework/network-programming/proxy-configuration) 文档。

1. 重置 IIS，例如，通过在命令提示符下以管理员身份运行 **iisreset** 。

在 RMS 群集中的所有节点上重复此过程。


## <a name="see-also"></a>另请参阅

了解有关 Azure 信息保护的详细信息，与其他 AIP 客户联系，并使用 [API yammer 组](https://www.yammer.com/askipteam/)与 AIP 产品经理联系。 