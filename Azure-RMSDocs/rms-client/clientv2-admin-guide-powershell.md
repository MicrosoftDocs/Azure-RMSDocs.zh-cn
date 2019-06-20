---
title: 使用 PowerShell 和 Azure 信息保护统一标记客户端
description: 说明和管理员可以使用 PowerShell 管理 Azure 信息保护统一标记客户端的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f90697e1e4df90ab8876843b45957b93c8ba8b07
ms.sourcegitcommit: a26e4e50165107efd51280b5c621dfe74be51a7a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67236883"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理员指南：使用 PowerShell 管理 Azure 信息保护统一客户端

>适用对象： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> 说明： *[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

在安装 Azure 信息保护统一标记客户端时，将自动安装 PowerShell 命令。 这允许通过运行可放到脚本中实现自动执行的命令来管理客户端。

Cmdlet 随 PowerShell 模块**AzureInformationProtection**，其中包含 cmdlet 进行标记。 例如：

|标记 cmdlet|示例用法|
|----------------|---------------|
|[Get AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|对于共享文件夹，请标识具有特定标签的所有文件。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|对于共享文件夹，检查文件内容，然后根据指定的条件自动标记未标记的文件。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|对于共享文件夹，将指定的标签应用于没有标签的所有文件。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|用标签标记文件以交互方式，通过使用不同的用户帐户添加到你自己。|

> [!TIP]
> 若要使用路径长度超过 260 个字符的 cmdlet，请使用自 Windows 10 版本 1607 开始提供的以下[组策略设置](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)：<br /> **本地计算机策略** > **计算机配置** > **管理模板** > **所有设置**  > **启用 Win32 长路径** 
> 
> 对于 Windows Server 2016，在安装 Windows 10 的最新管理模板 (.admx) 时，可以使用相同的组策略设置。
>
> 有关详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

此模块安装在 **\ProgramFiles (x86)\Microsoft Azure Information Protection** 中，并将此文件夹添加到 **PSModulePath** 系统变量。 此模块的 .dll 命名为 **AIP.dll**。

> [!IMPORTANT]
> AzureInformationProtection 模块不支持配置的标签或标签策略高级的设置。 对于这些设置，您需要 Office 365 安全与合规性中心 PowerShell。 有关详细信息，请参阅[自定义配置 Azure 信息保护统一标记的客户端](clientv2-admin-guide-customizations.md)。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>使用 AzureInformationProtection 模块的先决条件

除了安装 AzureInformationProtection 模块的先决条件，没有其他先决条件时标记 cmdlet 用于 Azure 信息保护：

1. 必须激活 Azure 权限管理服务。

2. 使用自己的帐户从他人的文件中删除保护： 

    - 必须为你的组织启用超级用户功能，而且必须将你的帐户配置为 Azure 权限管理的超级用户。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>先决条件 1：必须激活 Azure Rights Management 服务

如果未激活你的 Azure 信息保护租户以应用保护，请参阅的说明[激活 Azure Rights Management](../activate-service.md)。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>先决条件 2：使用自己的帐户从他人的文件中删除保护

从他人的文件中删除保护的典型方案包括数据发现或数据恢复。 如果使用标签应用保护，则可以通过设置不应用保护的新标签或通过删除标签来删除保护。

用户必须具有从文件删除保护的权限管理使用权限或者成为超级用户。 对于数据发现或数据恢复，通常会使用超级用户功能。 若要启用此功能并将你的帐户配置为超级用户，请参阅[为 Azure 管理权限和发现服务或数据恢复配置超级用户](../configure-super-users.md)。

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>如何以非交互方式为 Azure 信息保护标记文件

注意：在本部分中的信息适用于仅 Azure 信息保护统一标记客户端的预览版本。

可以使用 Set-AIPAuthentication cmdlet，以非交互方式运行标记 cmdlet  。

默认情况下，运行 cmdlet 进行标记时，命令会在交互式 PowerShell 会话中你自己的用户上下文运行。 若要在无人参与的情况下运行这些命令，请为此新建一个 Azure AD 用户帐户。 然后，在相应用户的上下文中，运行 Set-AIPAuthentication cmdlet，以使用 Azure AD 中的访问令牌设置并存储凭据。 然后，此用户帐户进行身份验证和 Azure 信息保护中保护服务的引导。 此帐户下载 Azure 信息保护策略和标签使用任何保护模板。

> [!NOTE]
> 如果使用[作用域内策略](../configure-policy-scope.md)，请记住，你可能需要将此帐户添加到作用域内策略中。

首次运行此 cmdlet 时，会看到登录提示，以便使用 Azure 信息保护。 指定用户帐户名称和创建无人参与的帐户的密码。 之后，此帐户可以运行标记 cmdlet 以非交互方式在 Azure AD 中的身份验证令牌过期之前。 

若要能够在以交互方式这第一次登录的用户帐户，帐户必须具有**在本地登录**的用户权限分配。 此权限是用户帐户的标准配置，但是你的公司策略可能为服务帐户禁用了此配置。 如果是这样，则可以运行使用 Set-aipauthentication *OnBehalfOf*参数以便在不登录提示的情况下完成身份验证。

在 Azure AD 令牌过期时，运行 cmdlet 后，再次以获取新令牌。

如果在运行此 cmdlet 时没有使用参数，用户帐户将获取有效期为 90 天或与密码有效期一样的访问令牌。  

若要控制访问令牌的过期时间，请在运行此 cmdlet 时使用参数。 此配置，可在一年，两年，Azure AD 中配置的访问令牌或永不过期。 需要在 Azure Active Directory 中注册的两个应用程序：一个 Web 应用/API 应用程序和一个本机应用程序   。 为 Set-aipauthentication 参数使用这些应用程序中的值。

运行此 cmdlet 后，您可以在您创建的服务帐户的上下文中运行标记 cmdlet。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>为 Set-AIPAuthentication 创建和配置 Azure AD 应用程序的具体步骤

1. 在新的浏览器窗口中，登录 [Azure 门户](https://portal.azure.com/)。

2. 用于 Azure 信息保护的 Azure AD 租户，导航到**Azure Active Directory** > **管理** > **应用注册**. 

3. 选择 **+ 新注册**、 创建 Web 应用 /API 应用程序。 上**注册应用程序**边栏选项卡中，指定以下值，然后单击**注册**:

   - **名称**: `AIPOnBehalfOf`
        
        如果愿意的话，请指定其他名称。 该名称对于每个租户必须是唯一的。
    
    - **支持的帐户类型**:**此组织目录中的帐户**
    
    - **重定向 URI （可选）** :**Web**和 `http://localhost`

4. 上**AIPOnBehalfOf**边栏选项卡上，复制的值**应用程序 （客户端） ID**。 值看起来类似于下面的示例： `57c3c1c3-abf9-404e-8b2b-4652836c8c66`。 此值用于*WebAppId*运行 Set-aipauthentication cmdlet 时的参数。 粘贴并保存以供日后参考的值。

5. 也可以在**AIPOnBehalfOf**边栏选项卡中，从**管理**菜单中，选择**身份验证**。

6. 上**AIPOnBehalfOf-身份验证**边栏选项卡，在**高级设置**部分中，选择**ID 令牌**复选框，然后选择**保存**.

7. 也可以在**AIPOnBehalfOf-身份验证**边栏选项卡中，从**管理**菜单中，选择**证书和机密**。

8. 上**AIPOnBehalfOf-证书和机密**边栏选项卡，在**客户端机密**部分中，选择 **+ 新客户端机密**。 

9. 有关**添加客户端密码**，指定以下内容，并选择**添加**:
    
    - **说明**: `Azure Information Protection client`
    - **过期**:指定你选择的持续时间 （1 年、 2 年或永不过期）

9. 重新**AIPOnBehalfOf-证书和机密**边栏选项卡，在**客户端机密**部分中，复制的字符串**值**。 此字符串看起来类似于下面的示例： `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`。 为了确保复制的所有字符，请选择的图标**都复制到剪贴板**。 
    
    请务必保存此字符串，因为它不会再次显示，并且无法检索。 与使用任何敏感信息，安全地存储保存的值，并限制对它的访问。

10. 也可以在**AIPOnBehalfOf-证书和机密**边栏选项卡中，从**管理**菜单中，选择**公开 API**。

11. 上**AIPOnBehalfOf-公开一个 API**边栏选项卡，选择**设置**有关**应用程序 ID URI**选项，然后在**应用程序 ID URI**值，更改**api**到**http**。 此字符串看起来类似于下面的示例： `http://d244e75e-870b-4491-b70d-65534953099e`。 
    
    选择“保存”。 

12. 重新**AIPOnBehalfOf-公开一个 API**边栏选项卡，选择 **+ 添加作用域**。

13. 上**添加一个作用域**边栏选项卡中，指定下列各项，例如，使用建议的字符串，然后选择**添加作用域**:
    - **作用域名称**: `user-impersonation`
    - **谁可以许可？** :**管理员和用户**
    - **管理员许可显示名称**: `Access Azure Information Protection scanner`
    - **管理员许可说明**: `Allow the application to access the scanner for the signed-in user`
    - **用户许可显示名称**: `Access Azure Information Protection scanner`
    - **用户许可说明**: `Allow the application to access the scanner for the signed-in user`
    - **状态**:**启用**（默认值）

14. 重新**AIPOnBehalfOf-公开 API**边栏选项卡中，关闭此边栏选项卡。

15. 上**应用注册**边栏选项卡，选择 **+ 新应用程序注册**现在创建本机应用程序。

16. 上**注册应用程序**边栏选项卡中，指定以下设置，并选择**注册**:
    - **名称**: `AIPClient`
    - **支持的帐户类型**:**此组织目录中的帐户**
    - **重定向 URI （可选）** :**公共客户端 （移动和桌面）** 和 `http://localhost`

17. 上**AIPClient**边栏选项卡上，复制的值**应用程序 （客户端） ID**。 值看起来类似于下面的示例： `8ef1c873-9869-4bb1-9c11-8313f9d7f76f`。 
    
    运行 Set-aipauthentication cmdlet 时，此值用于获得参数。 粘贴并保存以供日后参考的值。

18. 也可以在**AIPClient**边栏选项卡中，从**管理**菜单中，选择**身份验证**。

19. 上**AIPClient-身份验证**边栏选项卡中，指定以下内容，并选择**保存**:
    - 在中**高级设置**部分中，选择**ID 令牌**。
    - 在中**默认客户端类型**部分中，选择**是**。

20. 也可以在**AIPClient-身份验证**边栏选项卡中，从**管理**菜单中，选择**API 权限**。

21. 上**AIPClient-权限**边栏选项卡，选择 **+ 添加权限**。

22. 上**请求 API 的权限**边栏选项卡，选择**我的 Api**。

23. 在中**选择 API**部分中，选择**APIOnBehalfOf**，然后选中的复选框**用户模拟**，与权限。 选择**添加权限**。 

24. 重新**API 的权限**边栏选项卡，在**授予许可**部分中，选择**授予管理员的同意\<*你的租户名称*>** ，然后选择**是**的确认提示。

至此，你已配置完两个应用，并获得了使用参数 *WebAppId*、*WebAppKey* 和 *NativeAppId* 运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 所需的值。 从我们的示例：

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

请在将以非交互模式对文档进行标记和保护的帐户的上下文中运行此命令。 例如，你的 PowerShell 脚本的用户帐户或用于运行 Azure 信息保护扫描程序的服务帐户。

首次运行此命令时，会提示你进行登录，这将在 %localappdata%\Microsoft\MSIP 中创建并安全地存储你的帐户的访问令牌。 在此初次登录后，可以在计算机上以非交互方式对文件进行标记和保护。 但是，如果使用的服务帐户对标签和保护的文件，并且此服务帐户不能以交互方式登录，则使用*OnBehalfOf* Set-aipauthentication 参数：

1. 创建一个变量来存储授予权限的用户权限分配，以交互方式登录的 Active Directory 帐户的凭据。 例如：
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. 使用运行 Set-aipauthentication cmdlet *OnBeHalfOf*参数，指定其值为刚刚创建的变量。 例如：
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds

## <a name="next-steps"></a>后续步骤
有关 cmdlet 帮助信息时在 PowerShell 会话中，键入`Get-Help <cmdlet name> -online`。 例如： 

    Get-Help Set-AIPFileLabel -online

有关支持 Azure 信息保护客户端可能需要的其他信息，请参阅以下内容：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)
