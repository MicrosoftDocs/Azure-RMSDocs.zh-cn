---
title: 将 PowerShell 与 Azure 信息保护统一标签客户端配合使用
description: 管理员使用 PowerShell 管理 Azure 信息保护统一标签客户端的说明和信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ee514720cf13e819f3d64e77635ae96a26e4d0ed
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793216"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理员指南：将 PowerShell 与 Azure 信息保护统一客户端配合使用

>适用对象： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> 说明： *[适用于 Windows 的 Azure 信息保护统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

当你安装 Azure 信息保护统一标签客户端时, 将自动安装 PowerShell 命令。 这允许通过运行可放到脚本中实现自动执行的命令来管理客户端。

Cmdlet 随 PowerShell 模块**AzureInformationProtection**一起安装, 其中包含用于标记的 cmdlet。 例如：

|标记 cmdlet|示例用法|
|----------------|---------------|
|[Get AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|对于共享文件夹，请标识具有特定标签的所有文件。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|对于共享文件夹，检查文件内容，然后根据指定的条件自动标记未标记的文件。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|对于共享文件夹，将指定的标签应用于没有标签的所有文件。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|使用不同的用户帐户以交互方式标记文件。|

> [!TIP]
> 若要使用路径长度超过 260 个字符的 cmdlet，请使用自 Windows 10 版本 1607 开始提供的以下[组策略设置](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)：<br /> **本地计算机策略** > **计算机配置** > **管理模板** **所有设置都**启用**Win32 长路径** >  >  
> 
> 对于 Windows Server 2016，在安装 Windows 10 的最新管理模板 (.admx) 时，可以使用相同的组策略设置。
>
> 有关详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

此模块安装在 **\ProgramFiles (x86)\Microsoft Azure Information Protection** 中，并将此文件夹添加到 **PSModulePath** 系统变量。 此模块的 .dll 命名为 **AIP.dll**。

> [!IMPORTANT]
> AzureInformationProtection 模块不支持配置标签或标签策略的高级设置。 对于这些设置, 需要 Office 365 安全与合规中心 PowerShell。 有关详细信息, 请参阅[Azure 信息保护统一标签客户端的自定义配置](clientv2-admin-guide-customizations.md)。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>使用 AzureInformationProtection 模块的先决条件

除了安装 AzureInformationProtection 模块的先决条件之外, 在使用 Azure 信息保护的标记 cmdlet 时还有其他先决条件:

1. 必须激活 Azure 权限管理服务。

2. 使用自己的帐户从他人的文件中删除保护： 

    - 必须为你的组织启用超级用户功能，而且必须将你的帐户配置为 Azure 权限管理的超级用户。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>先决条件 1：必须激活 Azure Rights Management 服务

如果未激活 Azure 信息保护租户来应用保护, 请参阅[激活 azure Rights Management](../activate-service.md)的说明。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>先决条件 2：使用自己的帐户从他人的文件中删除保护

从他人的文件中删除保护的典型方案包括数据发现或数据恢复。 如果使用标签应用保护，则可以通过设置不应用保护的新标签或通过删除标签来删除保护。

用户必须具有从文件删除保护的权限管理使用权限或者成为超级用户。 对于数据发现或数据恢复，通常会使用超级用户功能。 若要启用此功能并将你的帐户配置为超级用户，请参阅[为 Azure 管理权限和发现服务或数据恢复配置超级用户](../configure-super-users.md)。

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>如何以非交互方式为 Azure 信息保护标记文件

可以使用 Set-AIPAuthentication cmdlet，以非交互方式运行标记 cmdlet。

默认情况下，运行 cmdlet 进行标记时，命令会在交互式 PowerShell 会话中你自己的用户上下文运行。 若要在无人参与的情况下运行这些命令，请为此新建一个 Azure AD 用户帐户。 然后，在相应用户的上下文中，运行 Set-AIPAuthentication cmdlet，以使用 Azure AD 中的访问令牌设置并存储凭据。 然后, 将对此用户帐户进行身份验证, 并引导 Azure 信息保护中的保护服务。 帐户下载 Azure 信息保护策略和标签使用的任何保护模板。

> [!NOTE]
> 如果使用[作用域内策略](../configure-policy-scope.md)，请记住，你可能需要将此帐户添加到作用域内策略中。

首次运行此 cmdlet 时，会看到登录提示，以便使用 Azure 信息保护。 指定为无人参与帐户创建的用户帐户名和密码。 之后, 此帐户可在 Azure AD 中的身份验证令牌过期之前, 以非交互方式运行标记 cmdlet。 

为了使用户帐户能够在第一次进行交互登录, 该帐户必须具有 "**本地登录**" 用户权限分配。 此权限是用户帐户的标准配置，但是你的公司策略可能为服务帐户禁用了此配置。 如果是这种情况, 则可以运行具有*OnBehalfOf*参数的 set-aipauthentication, 以便在不登录提示的情况下完成身份验证。

Azure AD 中的令牌过期时, 请再次运行 cmdlet 以获取新令牌。

如果在运行此 cmdlet 时没有使用参数，用户帐户将获取有效期为 90 天或与密码有效期一样的访问令牌。  

若要控制访问令牌的过期时间，请在运行此 cmdlet 时使用参数。 此配置允许你将 Azure AD 的访问令牌配置为一年、两年或永不过期。 需要在 Azure Active Directory 中注册两个应用程序:一个 Web 应用/API 应用程序和一个本机应用程序。 Set-aipauthentication 的参数使用这些应用程序中的值。

运行此 cmdlet 后, 可以在创建的服务帐户的上下文中运行标记 cmdlet。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>为 Set-AIPAuthentication 创建和配置 Azure AD 应用程序的具体步骤

1. 在新的浏览器窗口中，登录 [Azure 门户](https://portal.azure.com/)。

2. 对于与 Azure 信息保护配合使用的 Azure AD 租户, 请导航到**Azure Active Directory** > **管理** > **应用注册**"。 

3. 选择 " **+ 新建注册**", 创建 Web 应用/API 应用程序。 在 "**注册应用程序**" 边栏选项卡上, 指定以下值, 然后单击 "**注册**":

   - **名称**:`AIPOnBehalfOf`
        
        如果愿意的话，请指定其他名称。 该名称对于每个租户必须是唯一的。
    
    - **支持的帐户类型**:**仅限此组织目录中的帐户**
    
    - **重定向 URI (可选)** :**Web**和`http://localhost`

4. 在 " **AIPOnBehalfOf** " 边栏选项卡上, 复制 "**应用程序 (客户端) ID**" 的值。 值类似于下面的示例: `57c3c1c3-abf9-404e-8b2b-4652836c8c66`。 在运行 Set-aipauthentication cmdlet 时, 此值用于*WebAppId*参数。 粘贴并保存该值供以后参考。

5. 仍在 " **AIPOnBehalfOf** " 边栏选项卡上的 "**管理**" 菜单中, 选择 "**身份验证**"。

6. 在 " **AIPOnBehalfOf-身份验证**" 边栏选项卡上的 "**高级设置**" 部分中, 选择 " **ID 令牌**" 复选框, 然后选择 "**保存**"。

7. 仍在 " **AIPOnBehalfOf-身份验证**" 边栏选项卡上的 "**管理**" 菜单中, 选择 "**证书" & 机密**"。

8. 在 " **AIPOnBehalfOf & 机密**" 边栏选项卡上的 "**客户端密码**" 部分中, 选择 " **+ 新建客户端密钥**"。 

9. 对于 "**添加客户端密钥**", 请指定以下各项, 然后选择 "**添加**":
    
    - **说明**:`Azure Information Protection client`
    - **过期**时间:指定选择的持续时间 (1 年、2年或永不过期)

9. 返回到 " **AIPOnBehalfOf-证书 & 机密**" 边栏选项卡上的 "**客户端密码**" 部分中, 复制**值**的字符串。 此字符串类似于以下示例: `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`。 若要确保复制所有字符, 请选择要**复制到剪贴板**的图标。 
    
    请务必保存此字符串，因为它不会再次显示，并且无法检索。 对于所使用的任何敏感信息, 请安全地存储保存的值并限制对它的访问。

10. 仍在 " **AIPOnBehalfOf-证书 & 机密**" 边栏选项卡上的 "**管理**" 菜单中, 选择 "**公开 API**"。

11. 在 " **AIPOnBehalfOf-公开 API** " 边栏选项卡上, 选择 "**设置** **应用程序 id uri** " 选项, 然后在 "**应用程序 id uri** " 值中, 将**API**更改为**http**。 此字符串类似于以下示例: `http://d244e75e-870b-4491-b70d-65534953099e`。 
    
    选择**保存**。

12. 返回 " **AIPOnBehalfOf-公开 API** " 边栏选项卡, 选择 " **+ 添加作用域**"。

13. 在 "**添加作用域**" 边栏选项卡上, 指定以下内容, 并使用建议的字符串作为示例, 然后选择 "**添加作用域**":
    - **作用域名称**:`user-impersonation`
    - **谁可以获得许可？** :**管理员和用户**
    - **管理员许可显示名称**:`Access Azure Information Protection scanner`
    - **管理员同意说明**:`Allow the application to access the scanner for the signed-in user`
    - **用户同意显示名称**:`Access Azure Information Protection scanner`
    - **用户同意说明**:`Allow the application to access the scanner for the signed-in user`
    - **状态**:**已启用**(默认值)

14. 返回 " **AIPOnBehalfOf-公开 API** " 边栏选项卡。

15. 在 "**应用注册**" 边栏选项卡上, 选择 " **+ 新建应用程序注册**", 立即创建本机应用程序。

16. 在 "**注册应用程序**" 边栏选项卡上, 指定以下设置, 然后选择 "**注册**":
    - **名称**:`AIPClient`
    - **支持的帐户类型**:**仅限此组织目录中的帐户**
    - **重定向 URI (可选)** :**公共客户端 (移动 & 桌面)** 和`http://localhost`

17. 在 " **AIPClient** " 边栏选项卡上, 复制 "**应用程序 (客户端) ID**" 的值。 值类似于下面的示例: `8ef1c873-9869-4bb1-9c11-8313f9d7f76f`。 
    
    在运行 Set-aipauthentication cmdlet 时, 此值用于 NativeAppId 参数。 粘贴并保存该值供以后参考。

18. 仍在 " **AIPClient** " 边栏选项卡上的 "**管理**" 菜单中, 选择 "**身份验证**"。

19. 在 " **AIPClient-身份验证**" 边栏选项卡上, 指定以下内容, 然后选择 "**保存**":
    - 在 "**高级设置**" 部分中, 选择 " **ID 令牌**"。
    - 在 "**默认客户端类型**" 部分中, 选择 **"是"** 。

20. 仍在 " **AIPClient-身份验证**" 边栏选项卡上的 "**管理**" 菜单中, 选择 " **API 权限**"。

21. 在 " **AIPClient** " 边栏选项卡上, 选择 " **+ 添加权限**"。

22. 在 "**请求 api 权限**" 边栏选项卡上, 选择 **"我的 api**"。

23. 在 "**选择 API** " 部分中, 选择 " **APIOnBehalfOf**", 然后选中 "**用户模拟**" 复选框作为权限。 选择 "**添加权限**"。 

24. 返回 " **API 权限**" 边栏选项卡, 在 "**授予许可**" 部分中, 选择 "  **\<授予*租户名称*>管理员同意**", 并在确认提示中选择 **"是"** 。

至此，你已配置完两个应用，并获得了使用参数 *WebAppId*、*WebAppKey* 和 *NativeAppId* 运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 所需的值。 在我们的示例中:

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

请在将以非交互模式对文档进行标记和保护的帐户的上下文中运行此命令。 例如，你的 PowerShell 脚本的用户帐户或用于运行 Azure 信息保护扫描程序的服务帐户。

首次运行此命令时，会提示你进行登录，这将在 %localappdata%\Microsoft\MSIP 中创建并安全地存储你的帐户的访问令牌。 在此初次登录后，可以在计算机上以非交互方式对文件进行标记和保护。 但是, 如果使用服务帐户来标记和保护文件, 并且此服务帐户无法以交互方式登录, 请使用 Set-aipauthentication 的*OnBehalfOf*参数:

1. 创建一个变量, 用于存储被授予用户权限分配以交互方式登录的 Active Directory 帐户的凭据。 例如：
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. 运行 Set-aipauthentication cmdlet 和*OnBeHalfOf*参数, 并将其值指定为刚创建的变量。 例如：
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds

## <a name="next-steps"></a>后续步骤
对于 PowerShell 会话中的 cmdlet 帮助, 请键入`Get-Help <cmdlet name> -online`。 例如： 

    Get-Help Set-AIPFileLabel -online

有关支持 Azure 信息保护客户端可能需要的其他信息，请参阅以下内容：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)
