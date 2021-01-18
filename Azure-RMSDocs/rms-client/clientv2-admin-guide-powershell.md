---
title: 将 PowerShell 与 Azure 信息保护统一标签客户端配合使用
description: 管理员使用 PowerShell 管理 Azure 信息保护统一标签客户端的说明和信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/14/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 60f9493601d40b17c42354dae2d3978b8cb5972b
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560061"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理员指南：将 PowerShell 与 Azure 信息保护统一客户端配合使用

>***适用于**： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，Windows 8，Windows Server 2019，Windows Server 2016，windows Server 2012 R2，windows server 2012 *
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP 和旧版 Windows 和 office 版本](../known-issues.md#aip-and-legacy-windows-and-office-versions)。*
>
>*适用 **于**： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [经典客户端管理员指南](client-admin-guide-powershell.md)。 *

安装 Azure 信息保护统一标签客户端时，会自动将 PowerShell 命令作为 [AzureInformationProtection](/powershell/module/azureinformationprotection) 模块的一部分进行安装，其中包含用于标记的 cmdlet。 

使用 **AzureInformationProtection** 模块，可以通过运行自动化脚本的命令来管理客户端。

例如：

- [Get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus)：获取指定文件的 Azure 信息保护标签和保护信息。
- [Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification)：扫描文件，根据策略中配置的条件，自动设置文件的 Azure 信息保护标签。
- [Set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)：设置或删除文件的 Azure 信息保护标签，并根据标签配置或自定义权限设置或取消保护。
- [Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)：设置 Azure 信息保护客户端的身份验证凭据。

**AzureInformationProtection** 模块安装在 **\ProgramFiles (X86) \Microsoft Azure 信息保护** 文件夹中，然后将此文件夹添加到 **PSModulePath** 系统变量。 此模块的 .dll 命名为 **AIP.dll**。

> [!IMPORTANT]
> **AzureInformationProtection** 模块不支持配置标签或标签策略的高级设置。 
>
>对于这些设置，需要 Office 365 Security & 相容性中心 PowerShell。 有关详细信息，请参阅 [Azure 信息保护统一标签客户端的自定义配置](clientv2-admin-guide-customizations.md)。

> [!TIP]
> 若要使用路径长度超过 260 个字符的 cmdlet，请使用自 Windows 10 版本 1607 开始提供的以下[组策略设置](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)：<br /> **本地计算机策略**  > **计算机配置**  > **管理模板**  > **所有设置**  > **启用 Win32 长路径** 
> 
> 对于 Windows Server 2016，在安装 Windows 10 的最新管理模板 (.admx) 时，可以使用相同的组策略设置。
>
> 有关详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

## <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>使用 AzureInformationProtection 模块的先决条件

除了安装 **AzureInformationProtection** 模块的先决条件之外，在使用 Azure 信息保护的标记 cmdlet 时还有额外的先决条件：

- **必须激活 Azure Rights Management 服务**。

    如果未激活 Azure 信息保护租户，请参阅 [从 Azure 信息保护中激活保护服务](../activate-service.md)的说明。

- **使用自己的帐户从其他人的文件中删除保护**：

    - 必须为你的组织启用 [超级用户](../configure-super-users.md) 功能。
    - 你的帐户必须配置为 Azure Rights Management 的超级用户。

    例如，你可能想要删除对其他人的保护，以便发现或恢复数据。 如果使用标签来应用保护，则可以通过设置不应用保护的新标签来删除该保护，也可以删除标签。

    若要删除保护，请将 [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel) Cmdlet 与 *RemoveProtection* 参数一起使用。 默认情况下，删除保护功能处于禁用状态，必须先使用 [LabelPolicy](/powershell/module/azureinformationprotection/set-labelpolicy) cmdlet 启用该功能。

## <a name="rms-to-unified-labeling-cmdlet-mapping"></a>RMS 到统一标签 cmdlet 的映射

如果已从 Azure RMS 迁移，请注意，与 RMS 相关的 cmdlet 已弃用，可用于统一标签。 

某些旧 cmdlet 已替换为用于统一标签的新 cmdlet。 例如，如果你将 **RMSProtectionLicense** 与 RMS 保护一起使用，并已迁移到统一标签，请改用 **AIPCustomPermissions** 。

下表映射了与 RMS 相关的 cmdlet，其中包含用于统一标记的更新 cmdlet：

|RMS cmdlet  |统一标签 cmdlet  |
|---------|---------|
|[Get-rmsfilestatus](/powershell/module/azureinformationprotection/get-rmsfilestatus)     |  [Get AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)        |
|[RMSServer](/powershell/module/azureinformationprotection/get-rmsserver)     |  与统一标签无关。      |
|[Set-rmsserverauthentication](/powershell/module/azureinformationprotection/get-rmsserverauthentication)      |   [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[RMSAuthentication](/powershell/module/azureinformationprotection/clear-rmsauthentication)     | [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication)     |  [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)      |
|[Get-rmstemplate](/powershell/module/azureinformationprotection/get-rmstemplate)     |       与统一标签无关  |
|[新-RMSProtectionLicense](/powershell/module/azureinformationprotection/new-rmsprotectionlicense)     |  带有 **CustomPermissions** 参数的 [AIPCustomPermissions](/powershell/module/azureinformationprotection/new-aipcustompermissions)和 [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)      |
|[保护-Protect-rmsfile](/powershell/module/azureinformationprotection/protect-rmsfile) |[Set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)，具有 **RemoveProtection** 参数 |
| | |


## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>如何以非交互方式为 Azure 信息保护标记文件

默认情况下，运行 cmdlet 进行标记时，命令会在交互式 PowerShell 会话中你自己的用户上下文运行。

有关详细信息，请参见:

- [以无人参与方式运行 AIP 标签 cmdlet 的先决条件](#prerequisites-for-running-aip-labeling-cmdlets-unattended)
- [为 Set-aipauthentication 创建和配置 Azure AD 应用程序](#create-and-configure-azure-ad-applications-for-set-aipauthentication)
- [运行 Set-AIPAuthentication cmdlet](#running-the-set-aipauthentication-cmdlet)

> [!NOTE]
> 如果计算机无法访问 internet，则无需在 Azure AD 中创建应用程序并运行 **set-aipauthentication** cmdlet。 相反，请按照 [断开连接的计算机](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)的说明进行操作。  

### <a name="prerequisites-for-running-aip-labeling-cmdlets-unattended"></a>以无人参与方式运行 AIP 标签 cmdlet 的先决条件

若要以无人参与方式运行 Azure 信息保护标记 cmdlet，请使用以下访问详细信息：

- 可以交互方式登录的 **Windows 帐户**。

- 用于委派访问权限的 **Azure AD 帐户**。 为了便于管理，请使用从 Active Directory 同步到 Azure AD 的单个帐户。

    对于委派的用户帐户：

    |要求  |详细信息  |
    |---------|---------|
    |**标签策略**     |  请确保已为此帐户分配了标签策略，并且该策略包含要使用的已发布标签。   <br><br>如果对不同用户使用标签策略，可能需要创建新的标签策略，以发布所有标签，并将策略发布到仅此委派的用户帐户。    |
    |**解密内容**     |    如果此帐户需要解密内容，例如，要重新保护文件并检查其他人保护的文件，请使其成为 Azure 信息保护的 [超级用户](../configure-super-users.md) ，并确保已启用超级用户功能。     |
    |**载入控件**     |    如果已为分阶段部署实现了 [载入控件](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) ，请确保此帐户包含在已配置的载入控件中。     |
    |     |         |

- **Azure AD 访问令牌**，用于设置和存储委派用户的凭据，以向 Azure 信息保护进行身份验证。 Azure AD 中的令牌过期时，必须再次运行该 cmdlet 才能获取新令牌。 

    **Set-aipauthentication** 的参数使用 Azure AD 中的应用注册过程中的值。 有关详细信息，请参阅 [创建和配置 set-aipauthentication 的 Azure AD 应用程序](#create-and-configure-azure-ad-applications-for-set-aipauthentication)。

首先运行 [set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication) cmdlet，以非交互方式运行标记 cmdlet。

运行 **set-aipauthentication** cmdlet 的计算机会将分配给你的已委派用户帐户的标记策略下载到你的标记管理中心，如 Microsoft 365 安全 & 相容性中心。

### <a name="create-and-configure-azure-ad-applications-for-set-aipauthentication"></a>为 Set-AIPAuthentication 创建和配置 Azure AD 应用程序

**Set-aipauthentication** cmdlet 要求对 *AppId* 和 *AppSecret* 参数进行应用注册。 

对于最近从经典客户端迁移并为以前的 *WebAppID* 和 *NativeAppId* 参数创建了应用注册的用户，你将需要为统一标签客户端创建新的应用注册。

**若要为统一标签客户端创建新应用注册 Set-AIPAuthentication cmdlet**：

1. 在新的浏览器窗口中，登录到与 Azure 信息保护配合使用的 Azure AD 租户 [Azure 门户](https://portal.azure.com/) 。

1. 导航到 **Azure Active Directory**  >  **管理**  >  **应用注册**，然后选择 "**新注册**"。 

1. 在 " **注册应用程序** " 窗格上，指定以下值，然后单击 " **注册**"：

    |选项  |值  |
    |---------|---------|
    |**名称**     |  `AIP-DelegatedUser` <br>根据需要指定其他名称。 每个租户的名称必须是唯一的。       |
    |**支持的帐户类型**     |   选择“仅此组织目录中的帐户”。      |
    |**重定向 URI（可选）**     |     选择 " **Web**"，然后输入 `https://localhost` 。    |
    |     |         |

1. 在 " **AIP-DelegatedUser** " 窗格上，复制 " **应用程序 (客户端) ID**" 的值。 

    值类似于下面的示例： `77c3c1c3-abf9-404e-8b2b-4652836c8c66` 。 

    运行 **set-aipauthentication cmdlet** 时，此值用于 *AppId* 参数。 粘贴并保存该值供以后参考。

1. 从侧栏中，选择 "**管理**  >  **证书" & 密码**。

    然后，在 " **AIP-DelegatedUser-证书 & 密码** " 窗格的 " **客户端密码** " 部分中，选择 " **新建客户端密码**"。

1. 对于 " **添加客户端密钥**"，请指定以下各项，然后选择 " **添加**"：

    |字段  |值  |
    |---------|---------|
    |**说明**     |  `Azure Information Protection unified labeling client`       |
    |**完**     |   指定选择持续时间 (1 年、2年或永不过期)      |
    |     |         |

1. 返回到 " **AIP-DelegatedUser-证书 & 机密** " 窗格的 " **客户端密码** " 部分中，复制 **值** 的字符串。 

    此字符串类似于以下示例： `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4` 。 

    若要确保复制所有字符，请选择要 **复制到剪贴板** 的图标。 
    
    > [!IMPORTANT]
    > 请务必保存此字符串，因为它不会再次显示，并且无法检索。 对于所使用的任何敏感信息，请安全地存储保存的值并限制对它的访问。
    > 

1. 从边栏中选择 "**管理**  >  **API 权限**"。

    在 " **AIP-DelegatedUser-API 权限** " 窗格上，选择 " **添加权限**"。

1. 在 " **请求 API 权限** " 窗格上，确保位于 " **Microsoft api** " 选项卡上，然后选择 " **Azure Rights Management 服务**"。 

    当系统提示你提供应用程序所需的权限类型时，请选择 " **应用程序权限**"。

1. 对于 " **选择权限**"，展开 " **内容** " 并选择以下各项，然后选择 " **添加权限**"。
    
    -  **DelegatedReader** 
    -  **DelegatedWriter**

1. 返回到 **AIP-DelegatedUser-API 权限** 窗格，再次选择 " **添加权限** "。

    在 " **请求 AIP 权限** " 窗格上，选择 **"我的组织使用的 api**"，并搜索 " **Microsoft 信息保护同步服务**"。

1. 在 " **请求 API 权限** " 窗格上，选择 " **应用程序权限**"。
    
    对于 " **选择权限**"，展开 " **UnifiedPolicy**"，选择 " **UnifiedPolicy**"，然后选择 " **添加权限**"。

1. 返回到 " **AIP-DelegatedUser-API 权限**" 窗格，选择 "**授予管理员 \<*your tenant name*> 同意**"，并在确认提示时选择 **"是"** 。
    
    你的 API 权限应该如下图所示：

    :::image type="content" source="../media/api-permissions-app.png" alt-text="Azure AD 中已注册应用程序的 API 权限":::

现在，你已使用机密完成了此应用的注册，接下来可以使用参数 *AppId* 和 *AppSecret* 运行 [set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 。 此外，还需要租户 ID。 

> [!TIP]
>你可以使用 Azure 门户 **Azure Active Directory**  >  **管理**  >  **属性**  >  **目录 ID** 快速复制你的租户 ID。

### <a name="running-the-set-aipauthentication-cmdlet"></a>运行 Set-AIPAuthentication cmdlet

1. 通过 "以 **管理员身份运行" 选项** 打开 Windows PowerShell。 

1. 在 PowerShell 会话中，创建一个变量以存储将以非交互方式运行的 Windows 用户帐户的凭据。 例如，如果为扫描程序创建了服务帐户：

    ```PowerShell
    $pscreds = Get-Credential "CONTOSO\srv-scanner"
    ```

    系统将提示你输入此帐户的密码。

1. 运行 **set-aipauthentication** Cmdlet 和 *OnBeHalfOf* 参数，并将所创建的变量指定为其值。 

    同时，在 Azure AD 中指定应用注册值、租户 ID 和委托用户帐户的名称。 例如：
    
    ```PowerShell
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
    ```
## <a name="next-steps"></a>后续步骤

对于 PowerShell 会话中的 cmdlet 帮助，请键入 `Get-Help <cmdlet name> -online` 。 例如： 

```PowerShell
Get-Help Set-AIPFileLabel -online
```

有关详细信息，请参阅：

- [统一标签客户端自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)