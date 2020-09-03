---
title: 将 PowerShell 与 Azure 信息保护统一标签客户端配合使用
description: 管理员使用 PowerShell 管理 Azure 信息保护统一标签客户端的说明和信息。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a7705a284690094c3db2ac5fd3ac3e3eca1ed2e5
ms.sourcegitcommit: c133ada59dffcb9d8ee35688290d2b027bd63425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423122"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理员指南：将 PowerShell 与 Azure 信息保护统一客户端配合使用

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP For Windows And office 版本中的扩展支持](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。*
>
> *适用于以下内容的说明： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

当你安装 Azure 信息保护统一标签客户端时，将自动安装 PowerShell 命令。 这允许通过运行可放到脚本中实现自动执行的命令来管理客户端。

Cmdlet 随 PowerShell 模块 **AzureInformationProtection**一起安装，其中包含用于标记的 cmdlet。 例如：

|标记 cmdlet|用法示例|
|----------------|---------------|
|[Get AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|对于共享文件夹，请标识具有特定标签的所有文件。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|对于共享文件夹，检查文件内容，然后根据指定的条件自动标记未标记的文件。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|对于共享文件夹，将指定的标签应用于没有标签的所有文件。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|以非交互方式标记文件，例如使用按计划运行的脚本。|

> [!TIP]
> 若要使用路径长度超过 260 个字符的 cmdlet，请使用自 Windows 10 版本 1607 开始提供的以下[组策略设置](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)：<br /> **本地计算机策略**  > **计算机配置**  > **管理模板**  > **所有设置**  > **启用 Win32 长路径** 
> 
> 对于 Windows Server 2016，在安装 Windows 10 的最新管理模板 (.admx) 时，可以使用相同的组策略设置。
>
> 有关详细信息，请参阅 Windows 10 开发人员文档中的[最大路径长度限制](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)一节。

此模块安装在 **\ProgramFiles (x86)\Microsoft Azure Information Protection** 中，并将此文件夹添加到 **PSModulePath** 系统变量。 此模块的 .dll 命名为 **AIP.dll**。

> [!IMPORTANT]
> AzureInformationProtection 模块不支持配置标签或标签策略的高级设置。 对于这些设置，需要 Office 365 Security & 相容性中心 PowerShell。 有关详细信息，请参阅 [Azure 信息保护统一标签客户端的自定义配置](clientv2-admin-guide-customizations.md)。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>使用 AzureInformationProtection 模块的先决条件

除了安装 AzureInformationProtection 模块的先决条件之外，在使用 Azure 信息保护的标记 cmdlet 时还有其他先决条件：

1. 必须激活 Azure 权限管理服务。

2. 使用自己的帐户从他人的文件中删除保护： 

    - 必须为你的组织启用超级用户功能，而且必须将你的帐户配置为 Azure 权限管理的超级用户。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>先决条件 1：必须激活 Azure 权限管理服务

如果未激活 Azure 信息保护租户，请参阅 [[从 Azure 信息保护中激活保护服务中](../activate-service.md)的说明。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>先决条件 2：使用自己的帐户从他人的文件中删除保护

从他人的文件中删除保护的典型方案包括数据发现或数据恢复。 如果使用标签应用保护，则可以通过设置不应用保护的新标签或通过删除标签来删除保护。

用户必须具有从文件删除保护的权限管理使用权限或者成为超级用户。 对于数据发现或数据恢复，通常会使用超级用户功能。 若要启用此功能并将你的帐户配置为超级用户，请参阅 [为 Azure 信息保护和发现服务或数据恢复配置超级用户](../configure-super-users.md)。

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>如何以非交互方式为 Azure 信息保护标记文件

可以使用 Set-AIPAuthentication cmdlet，以非交互方式运行标记 cmdlet[](/powershell/module/azureinformationprotection/set-aipauthentication)。

默认情况下，运行 cmdlet 进行标记时，命令会在交互式 PowerShell 会话中你自己的用户上下文运行。 若要以无人参与模式运行，请使用可以交互方式登录的 Windows 帐户，并使用将用于委派访问的 Azure AD 中的帐户。 为了便于管理，请使用从 Active Directory 同步到 Azure AD 的单个帐户。

还需要请求 Azure AD 的访问令牌，该令牌将设置和存储委派用户的凭据，以向 Azure 信息保护进行身份验证。

运行 Set-aipauthentication cmdlet 的计算机将使用您的标签管理中心（如 Office 365 Security & 相容性中心）下载标签策略，并将其分配给委派的用户帐户。

> [!NOTE]
> 如果对不同用户使用标签策略，可能需要创建新的标签策略，以发布所有标签，并将策略发布到仅此委派的用户帐户。

Azure AD 中的令牌过期时，必须再次运行该 cmdlet 才能获取新令牌。 你可以在 Azure AD 中将访问令牌配置为一年、两年或永不过期。 Set-aipauthentication 的参数在 Azure AD 中使用应用注册过程中的值，如下一节中所述。

对于委派的用户帐户：

- 请确保已为此帐户分配了标签策略，并且该策略包含要使用的已发布标签。

- 如果此帐户需要解密内容，例如，要重新保护文件并检查其他人保护的文件，请使其成为 Azure 信息保护的 [超级用户](../configure-super-users.md) ，并确保已启用超级用户功能。

- 如果已为分阶段部署实现了 [载入控件](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) ，请确保此帐户包含在已配置的载入控件中。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>为 Set-AIPAuthentication 创建和配置 Azure AD 应用程序的具体步骤

> [!IMPORTANT]
> 这些说明适用于统一标签客户端的当前通用版本，也适用于此客户端的扫描仪的通用版本。

Set-aipauthentication 要求对 *AppId* 和 *AppSecret* 参数进行应用注册。 如果从客户端的以前版本升级并为以前的 *WebAppId* 和 *NativeAppId* 参数创建了应用注册，则它们将不能用于统一的标签客户端。 你必须创建一个新的应用注册，如下所示：

1. 在新的浏览器窗口中，登录 [Azure 门户](https://portal.azure.com/)。

2. 对于与 Azure 信息保护配合使用的 Azure AD 租户，请导航到**Azure Active Directory**  >  **管理**  >  **应用注册**"。 

3. 选择 " **+ 新注册**"。 在 " **注册应用程序** " 窗格上，指定以下值，然后单击 " **注册**"：

   - **名称**：`AIP-DelegatedUser`
        
        如果愿意的话，请指定其他名称。 该名称对于每个租户必须是唯一的。
    
    - **受支持的帐户类型**： **仅限此组织目录中的帐户**
    
    - **重定向 URI (可选) **： **Web** 和 `https://localhost`

4. 在 " **AIP-DelegatedUser** " 窗格上，复制 " **应用程序 (客户端) ID**" 的值。 值类似于下面的示例： `77c3c1c3-abf9-404e-8b2b-4652836c8c66` 。 运行 Set-aipauthentication cmdlet 时，此值用于 *AppId* 参数。 粘贴并保存该值供以后参考。

5. 从侧栏中，选择 "**管理**  >  **证书" & 密码**。

6. 在 " **AIP-DelegatedUser-证书 & 密码** " 窗格的 " **客户端密码** " 部分中，选择 " **+ 新建客户端密钥**"。

7. 对于 " **添加客户端密钥**"，请指定以下各项，然后选择 " **添加**"：
    
    - **说明**： `Azure Information Protection unified labeling client`
    - **过期**：指定所选持续时间 (1 年、2年或永不过期) 

8. 返回到 " **AIP-DelegatedUser-证书 & 机密** " 窗格的 " **客户端密码** " 部分中，复制 **值**的字符串。 此字符串类似于以下示例： `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4` 。 若要确保复制所有字符，请选择要 **复制到剪贴板**的图标。 
    
    请务必保存此字符串，因为它不会再次显示，并且无法检索。 对于所使用的任何敏感信息，请安全地存储保存的值并限制对它的访问。

9. 从边栏中选择 "**管理**  >  **API 权限**"。

10. 在 " **AIP-DelegatedUser-API 权限** " 窗格上，选择 " **+ 添加权限**"。

11. 在 " **请求 API 权限** " 窗格上，确保位于 " **Microsoft api** " 选项卡上，然后选择 " **Azure Rights Management 服务**"。 当系统提示你提供应用程序所需的权限类型时，请选择 " **应用程序权限**"。

12. 对于 " **选择权限**"，展开 " **内容** " 并选择以下各项：
    
    -  **DelegatedReader** 
    -  **DelegatedWriter**

13. 选择“添加权限”。

14. 返回到 **AIP-DelegatedUser-API 权限** 窗格，选择 " **+ 再次添加权限** "。

15. 在 " **请求 AIP 权限** " 窗格上，选择 **"我的组织使用的 api**"，并搜索 " **Microsoft 信息保护同步服务**"。

16. 在 " **请求 API 权限** " 窗格上，选择 " **应用程序权限**"。

17. 对于 " **选择权限**"，展开 " **UnifiedPolicy** "，然后选择以下内容：
    
    -  **UnifiedPolicy。读取**

18. 选择“添加权限”。

19. 返回到 " **AIP-DelegatedUser-API 权限**" 窗格，选择 "**授予管理员 \<*your tenant name*> 同意**"，并在确认提示时选择 **"是"** 。
    
    你的 API 权限应该如下所示：
    
    ![Azure AD 中已注册应用程序的 API 权限](../media/api-permissions-app.png)

现在，你已使用机密完成了此应用的注册，接下来可以使用参数*AppId*和*AppSecret*运行[set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 。 此外，还需要租户 ID。 

> [!TIP]
>你可以使用 Azure 门户**Azure Active Directory**  >  **管理**  >  **属性**  >  **目录 ID**快速复制你的租户 ID。

1. 通过 "以 **管理员身份运行" 选项**打开 Windows PowerShell。 

2. 在 PowerShell 会话中，创建一个变量以存储将以非交互方式运行的 Windows 用户帐户的凭据。 例如，如果为扫描程序创建了服务帐户：

    ```ps
    $pscreds = Get-Credential "CONTOSO\srv-scanner"
    ```

    系统将提示你输入此帐户的密码。

2. 运行 Set-aipauthentication cmdlet 和 *OnBeHalfOf* 参数，并将其值指定为刚创建的变量。 同时，在 Azure AD 中指定应用注册值、租户 ID 和委托用户帐户的名称。 例如：
    
    ```ps
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
    ```

> [!NOTE]
> 如果计算机无法访问 internet，则无需在 Azure AD 中创建应用程序并运行 Set-aipauthentication。 相反，请按照 [断开连接的计算机](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)的说明进行操作。  

## <a name="next-steps"></a>后续步骤
对于 PowerShell 会话中的 cmdlet 帮助，请键入 `Get-Help <cmdlet name> -online` 。 例如： 

```ps
Get-Help Set-AIPFileLabel -online
```

有关支持 Azure 信息保护客户端可能需要的其他信息，请参阅以下内容：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [支持的文件类型](clientv2-admin-guide-file-types.md)
