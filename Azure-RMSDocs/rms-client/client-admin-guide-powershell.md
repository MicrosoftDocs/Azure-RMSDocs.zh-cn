---
title: "将 PowerShell 与 Azure 信息保护客户端配合使用"
description: "管理员通过使用 PowerShell 管理 Azure 信息保护客户端的说明和信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 2f8ad221d1193f5a6f40cc773548b9342ffd6659
ms.sourcegitcommit: 0fd2e63822280ec96ab957e22868c63de9ef3d47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2017
---
# <a name="using-powershell-with-the-azure-information-protection-client"></a>将 PowerShell 与 Azure 信息保护客户端配合使用

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

安装 Azure 信息保护客户端时，将自动安装 PowerShell 命令，从而通过运行可放入自动化脚本的命令来管理客户端。

cmdlet 是使用 PowerShell 模块 AzureInformationProtection 进行安装。 此模块替换随 RMS 保护工具一起安装的 RMSProtection 模块。 如果在安装 Azure 信息保护客户端时安装了 RMSProtection 工具，则会自动卸载 RMSProtection 模块。

AzureInformationProtection 模块包括 RMS 保护工具的所有 Rights Management cmdlet 和使用 Azure 信息保护 (AIP) 服务进行标记的三个新 cmdlet：

|标记 cmdlet|示例用法|
|----------------|---------------|
|[Get AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|对于共享文件夹，请标识具有特定标签的所有文件。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|对于共享文件夹，检查文件内容，然后根据指定的条件自动标记未标记的文件。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|对于共享文件夹，将指定的标签应用于没有标签的所有文件。|

有关所有 cmdlet 及其相应帮助的列表，请参阅 [AzureInformationProtection 模块](/powershell/module/azureinformationprotection)。 在 PowerShell 会话中，键入 `Get-Help <cmdlet name> -online` 以查看最新帮助以及除英语之外的其他受支持语言。  

此模块安装在 **\ProgramFiles (x86)\Microsoft Azure Information Protection** 中，并将此文件夹添加到 **PSModulePath** 系统变量。 此模块的 .dll 命名为 **AIP.dll**。

与 RMSProtection 模块一样，AzureInformationProtection 模块的当前版本具有以下限制：

- 可以取消保护 Outlook 个人文件夹（.pst 文件），但当前无法使用 PowerShell 模块本机保护这些文件或其他容器文件。

- 可以取消保护位于 Outlook 个人文件夹 (.pst) 中的 Outlook 受保护电子邮件（.rpmsg 文件），但不能取消保护个人文件夹外的 .rpmsg 文件。

在开始使用这些 cmdlet 之前，请参阅与你的部署对应的其他先决条件和说明：

- [Azure 信息保护服务和 Azure 权限管理服务](#azure-information-protection-service-and-azure-rights-management-service)

    - 将仅分类或分类用于 Rights Management 保护时适用：具有包含 Azure 信息保护的订阅（例如，企业移动性 + 安全性）。
    - 将仅保护用于 Azure 权限管理服务时适用：具有包含 Azure 权限管理服务的订阅（例如，Office 365 E3 和 Office 365 E5）。

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - 将仅保护用于 Azure 权限管理的本地版本时适用；Active Directory Rights Management Services (AD RMS)。


## <a name="azure-information-protection-service-and-azure-rights-management-service"></a>Azure 信息保护服务和 Azure 权限管理服务

如果组织使用 Azure 信息保护和 Azure Rights Management 数据保护服务，或仅使用 Azure Rights Management 服务，请先阅读本部分，再开始使用 PowerShell 命令。


### <a name="prerequisites"></a>先决条件

除了安装 AzureInformationProtection 模块这一先决条件之外，Azure 信息保护服务和 Azure Rights Management 数据保护服务还有其他先决条件：

1. 必须激活 Azure 权限管理服务。

2. 使用自己的帐户从他人的文件中删除保护： 
    
    - 必须为你的组织启用超级用户功能，而且必须将你的帐户配置为 Azure 权限管理的超级用户。

3. 在无用户交互的情况下直接保护或取消保护文件： 
    
    - 创建服务主体帐户，运行 Set-RMSServerAuthentication，并考虑将此服务主体作为 Azure 权限管理的超级用户。

4. 北美以外的区域： 
    
    - 编辑注册表，以便对服务进行身份验证。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>先决条件 1：必须激活 Azure 权限管理服务

无论是通过使用标签还是直接连接到 Azure 权限管理服务来应用数据保护，此先决条件都适用。

如果未激活 Azure 信息保护租户，请参阅[激活 Azure 权限管理](../deploy-use/activate-service.md)的说明。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>先决条件 2：使用自己的帐户从他人的文件中删除保护

从他人的文件中删除保护的典型方案包括数据发现或数据恢复。 如果使用标签应用保护，则可以通过设置不应用保护的新标签或通过删除标签来删除保护。 但是，你更有可能通过直接连接到 Azure 权限管理服务来删除保护。

用户必须具有从文件删除保护的权限管理使用权限或者成为超级用户。 对于数据发现或数据恢复，通常会使用超级用户功能。 若要启用此功能并将你的帐户配置为超级用户，请参阅[为 Azure 管理权限和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>先决条件 3：在无用户交互的情况下保护或取消保护文件

目前，不能以非交互方式应用标签，但可通过非交互方式直接连接到 Azure 权限管理服务以保护或取消保护文件。

用户必须使用服务主体以非交互方式连接到 Azure 权限管理服务，通过使用 `Set-RMSServerAuthentication` cmdlet 可完成此操作。 必须对运行直接连接到 Azure 权限管理服务的 cmdlet 的每个 Windows PowerShell 会话执行此操作。 运行此 cmdlet 之前，请确保具有以下三个标识符：

- BposTenantId

- AppPrincipalId

- 对称密钥

以下部分将介绍如何获取这些标识符。

##### <a name="to-get-the-bpostenantid"></a>获取 BposTenantId

从 Azure RMS Windows PowerShell 模块运行 Get-AadrmConfiguration cmdlet：

1. 如果计算机上尚未安装此模块，请参阅[安装适用于 Azure 权限管理的 Windows PowerShell](../deploy-use/install-powershell.md)。

2. 使用“以管理员身份运行”选项启动 Windows PowerShell。

3. 使用 `Connect-AadrmService` cmdlet 连接到 Azure 权限管理服务：
    
        Connect-AadrmService
    
    出现提示时，输入 Azure 信息保护租户管理员凭据（通常使用 Azure Active Directory 或 Office 365 全局管理员帐户）。
    
4. 运行 `Get-AadrmConfiguration` 并创建 BPOSId 值的副本。
    
    以下是 Get-AadrmConfiguration 的输出示例：
    
            BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
            RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
            LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
            CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification

5. 从服务断开连接：
    
        Disconnect-AadrmService

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>获取 AppPrincipalId 和对称密钥

通过从 Azure Active Directory 的 MSOnline PowerShell 模块运行 `New-MsolServicePrincipal` cmdlet 来创建新的服务主体，然后使用以下说明。 

> [!IMPORTANT]
> 请勿使用较新的 Azure AD PowerShell cmdlet（即 New-AzureADServicePrincipal）来创建此服务主体。 Azure Rights Management 服务不支持 New-AzureADServicePrincipal。 

1. 如果计算机上尚未安装 MSOnline 模块，请运行 `Install-Module MSOnline`。

2. 使用“以管理员身份运行”选项启动 Windows PowerShell。

3. 使用 **Connect-MsolService** cmdlet 连接到 Azure AD：
    
        Connect-MsolService
    
    出现提示时，输入 Azure AD 租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。

4. 运行 New-MsolServicePrincipal cmdlet 以创建新的服务主体：
    
        New-MsolServicePrincipal
    
    出现提示时，输入为此服务主体选择的显示名称，这样有助于确定之后将它用作连接到 Azure Rights Management 服务的帐户，以便可以保护和取消保护文件。
    
    New-MsolServicePrincipal 的输出示例：
    
        Supply values for the following parameters:
        
        DisplayName: AzureRMSProtectionServicePrincipal
        The following symmetric key was created as one was not supplied
        zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=
        
        Display Name: AzureRMSProtectionServicePrincipal
        ServicePrincipalNames: (b5e3f7g1-b5c2-4c96-a594-a0807f65bba4)
        ObjectId: 23720996-593c-4122-bfc7-1abb5a0b5109
        AppPrincialId: b5e3f76a-b5c2-4c96-a594-a0807f65bba4
        TrustedForDelegation: False
        AccountEnabled: True
        Addresses: ()
        KeyType: Symmetric
        KeyId: 8ef61651-ca11-48ea-a350-25834a1ba17c
        StartDate: 3/7/2014 4:43:59 AM
        EndDate: 3/7/2014 4:43:59 AM
        Usage: Verify

5. 在此输出中，记下对称密钥和 AppPrincialId。

    请务必创建对称密钥的副本，因为之后无法完整检索，所以如果不知道，下次需要向 Azure Rights Management 服务进行身份验证时，必须新建服务主体。

通过这些说明和示例可知，运行 Set-RMSServerAuthentication 需要 3 个标识符：

- 租户 ID：**23976bc6-dcd4-4173-9d96-dad1f48efd42**

- 对称密钥：**zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA =**

- AppPrincipalId：**b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

我们的示例命令将如下所示：

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

如上一个命令所示，可以使用单个命令提供值，也可以键入 Set-RMSServerAuthentication，并在出现提示时逐个提供值。 命令完成后，将看到“**RmsServerAuthentication 已设置为启用**”，这意味着客户端现在以“服务器模式”运行。 此消息不能确认通过使用你提供的值成功完成身份验证，但可以确认已成功切换到服务器模式。

考虑使此服务主体成为超级用户：要确保此服务主体始终可以取消保护其他人的文件，可以将其配置为超级用户。 通过与将标准用户帐户配置为超级用户相同的方式，使用相同的 Azure RMS cmdlet ([Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md))，但使用 AppPrincipalId 值指定 **-ServicePrincipalId** 参数。

有关超级用户的详细信息，请参阅[为 Azure 权限管理和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

> [!NOTE]
> 若要使用自己的帐户对 Azure 权限管理服务进行身份验证，则无需在保护或取消保护文件或获取模板之前运行 Set-RMSServerAuthentication。

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>先决条件 4：北美以外的区域

对于 Azure 北美地区以外的身份验证，必须按如下所示编辑注册表。 如果 Azure 信息保护租户位于北美，则不要执行此步骤：

1. 再次运行 Get-AadrmConfiguration cmdlet，并记下 **CertificationExtranetDistributionPointUrl** 和 **LicensingExtranetDistributionPointUrl** 的值。

2. 在运行 AzureInformationProtection cmdlet 的每台计算机上，打开注册表编辑器，并转到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC`

3. 如果没有看到 **ServiceLocation** 项，请创建一个，然后注册表路径将显示 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation**

4. 对于 **ServiceLocation** 项，创建两个项（若不存在），并分别命名为 **EnterpriseCertification** 和 **EnterprisePublishing**。 
    
    创建这些 REG_SZ 项时，不要更改“（默认）”的名称，但对其进行编辑以设置值数据：

    - 对于 **EnterpriseCertification**，粘贴 CertificationExtranetDistributionPointUrl 值。
    
    - 对于 **EnterprisePublishing**，粘贴 LicensingExtranetDistributionPointUrl 值。

5. 关闭注册表编辑器。 无需重启计算机。 但是，如果使用服务主体帐户而不是自己的用户帐户，则必须在此注册表编辑后运行 Set-RMSServerAuthentication 命令。

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>将 cmdlet 用于 Azure 信息保护和 Azure 权限管理服务的示例方案

使用标签来分类和保护文件更有效率，因为只需要两个 cmdlet，且它们可以单独或一起运行，这两个 cmdlet 为：[Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus) 和 [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel)。 请使用这两个 cmdlet 的帮助了解详细信息和示例。

但是，若要通过直接连接到 Azure 权限管理服务来保护或取消保护文件，一般必须运行一系列 cmdlet，如下所述。

首先，如果需要使用服务主体而不是自己的帐户对 Azure 权限管理进行身份验证，请在 Powershell 会话中键入：

    Set-RMSServerAuthentication

出现提示时，输入[先决条件 3：在无用户交互的情况下保护或取消保护文件](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction)中所述的三个标识符。

另外，还必须将 Rights Management 模板下载到计算机，并确定要使用的模板及其相应的 ID 号，然后才可以保护文件。 然后可从输出复制模板 ID：

    Get-RMSTemplate
    
输出可能与以下内容类似：

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

请注意，如果未运行 Set-RMSServerAuthentication 命令，将使用自己的用户帐户向 Azure Rights Management 服务进行身份验证。 如果是已加入域的计算机，将始终自动使用当前凭据。 如果是工作组计算机，将看到登录 Azure 的提示，这些凭据会进行缓存，以供用于后续命令。 在这种情况下，如果以后需要以其他用户身份登录，请使用 `Clear-RMSAuthentication` cmdlet。

知道模板 ID 后，可以用它和 `Protect-RMSFile` cmdlet 保护单个文件或文件夹中的所有文件。 例如，如果想要通过使用“Contoso, Ltd - Confidential”模板仅保护单个文件并覆盖原始文件：

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

输出可能与以下内容类似：

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx

若要保护文件夹中的所有文件，请使用带有驱动器号和路径或 UNC 路径的 **-Folder** 参数。 例如：

    Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

输出可能与以下内容类似：

    InputFile                          EncryptedFile
    ---------                          -------------
    \Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
    \Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
    \Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
    \Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx

如果应用保护后文件扩展名不更改，则以后可以始终使用 `Get-RMSFileStatus` cmdlet 来检查文件是否受保护。 例如：

    Get-RMSFileStatus -File \Server1\Documents\Test1.docx

输出可能与以下内容类似：

    FileName                              Status
    --------                              ------
    \Server1\Documents\Test1.docx         Protected

若要取消保护文件，则必须从文件受保护起具有“所有者”或“提取”权限，或者必须以超级用户身份运行 cmdlet。 然后使用 Unprotect cmdlet。 例如：

    Unprotect-RMSFile C:\test.docx -InPlace

输出可能与以下内容类似：

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

请注意，如果更改了 Rights Management 模板，则必须使用 `Get-RMSTemplate -force` 再次下载这些模板。 

## <a name="active-directory-rights-management-services"></a>Active Directory 权限管理服务

当你的组织仅使用 Active Directory Rights Management Services 时，请阅读本节，然后才开始使用 PowerShell 命令来保护或取消保护文件。


### <a name="prerequisites"></a>先决条件

除了安装 AzureInformationProtection 模块的先决条件之外，你的帐户必须具有读取和执行权限才能访问 ServerCertification.asmx：

1. 登录到 AD RMS 服务器。

2. 单击“开始”，然后单击“计算机”。

3. 在文件资源管理器中，导航到 %systemdrive%\Initpub\wwwroot\_wmsc\Certification。

4. 右键单击“ServerCertification.asmx”，然后单击“属性”。

5. 在“ServerCertification.asmx 属性”对话框中，单击“安全”选项卡。 

6. 单击“继续”按钮或“编辑”按钮。 

7. 在“ServerCertification.asmx 的权限”对话框中，单击“添加”。 

8. 添加你的帐户名称。 如果其他 AD RMS 管理员也将使用这些 cmdlet 保护和取消保护文件，也请添加其名称。

9. 在“允许”列中，请确保选中“读取和执行”和“读取”复选框。

10.单击“确定”两次。

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>使用适用于 Active Directory Rights Management Services 的 cmdlet 的示例方案

这些 cmdlet 的典型方案是通过使用权限策略模板保护文件夹中的所有文件或取消保护文件。 

首先，如果有多个 AD RMS 部署，需要获取 AD RMS 服务器名称。为此，请运行 Get-RMSServer cmdlet，显示可用服务器列表：

    Get-RMSServer

输出可能与以下内容类似：

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

在可以保护文件之前，需要获取 RMS 模板的列表，以确定要使用的模板及其相应的 ID 号。 仅当有多个 AD RMS 部署时，才需要同时指定 RMS 服务器。 

然后可从输出复制模板 ID：

    Get-RMSTemplate -RMSServer RmsContoso

输出可能与以下内容类似：

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

知道模板 ID 后，可以用它和 Protect-RMSFile cmdlet 保护单个文件或文件夹中的所有文件。 例如，如果想要通过使用“Contoso, Ltd - Confidential”模板仅保护单个文件并替换原始文件：

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

输出可能与以下内容类似：

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx   

若要保护文件夹中的所有文件，请使用带有驱动器号和路径或 UNC 路径的 -Folder 参数。 例如：

    Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

输出可能与以下内容类似：

    InputFile                          EncryptedFile
    ---------                          -------------
    \\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
    \\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
    \\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
    \\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   

如果应用 RMS 保护后文件扩展名不更改，则以后可以始终使用 Get-RMSFileStatus cmdlet 来检查文件是否受保护。 例如： 

    Get-RMSFileStatus -File \\Server1\Documents\Test1.docx

输出可能与以下内容类似：

    FileName                              Status
    --------                              ------
    \\Server1\Documents\Test1.docx        Protected

若要取消保护文件，则必须从文件受保护起具有“所有者”或“提取”权限，或者是 AD RMS 的超级用户。 然后使用 Unprotect cmdlet。 例如：

    Unprotect-RMSFile C:\test.docx -InPlace

输出可能与以下内容类似：

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>如何以非交互方式为 Azure 信息保护标记文件

自 1.8.41.0 版 Azure 信息保护客户端（当前处于预览阶段）起，可以使用 Set-AIPAuthentication cmdlet，以非交互方式运行标记 cmdlet。

默认情况下，运行 cmdlet 进行标记时，命令会在交互式 PowerShell 会话中你自己的用户上下文运行。 若要在无人参与的情况下运行这些命令，请为此新建一个 Azure AD 用户帐户。 然后，在相应用户的上下文中，运行 Set-AIPAuthentication cmdlet，以使用 Azure AD 中的访问令牌设置并存储凭据。 此用户帐户会进行身份验证，并启动以供 Azure Rights Management 服务使用。 此帐户下载 Azure 信息保护策略，以及标签使用的任何 Rights Management 模板。

首次运行此 cmdlet 时，会看到登录提示，以便使用 Azure 信息保护。 指定为无人参与用户帐户创建的用户帐户名称和密码。 在这之后，此帐户可以在身份验证令牌过期前，以非交互方式运行标记 cmdlet。 令牌过期后，再次运行此 cmdlet，以获取新令牌：

如果在运行此 cmdlet 时没有使用参数，用户帐户将获取有效期为 90 天或与密码有效期一样的访问令牌。  

若要控制访问令牌的过期时间，请在运行此 cmdlet 时使用参数。 这样一来，可以配置有效期为一年、两年或永不过期的访问令牌。 若要执行此配置，必须拥有在 Azure Active Directory 中注册的两个应用程序：Web/API 应用程序和本机应用程序。 此 cmdlet 的参数使用这些应用程序提供的值。

运行此 cmdlet 后，可以在创建的用户帐户上下文中运行标记 cmdlet。 若要使用多个帐户，那么每个帐户都必须有自己的 Azure AD 注册应用程序，因此必须对每个帐户运行此 cmdlet。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>为 Set-AIPAuthentication 创建和配置 Azure AD 应用程序的具体步骤

1. 在新的浏览器窗口中，登录 [Azure 门户](https://portal.azure.com/)。

2. 对于与 Azure 信息保护结合使用的 Azure AD 租户，依次转到“Azure Active Directory” > “应用程序注册”。 

3. 选择“新应用程序注册”，以创建 Web/API 应用程序。 在“创建”标签上，指定以下值，再单击“创建”：
    
    - 名称：AIPOnBehalfOf
    
    - 应用程序类型：Web/API 应用程序
    
    - 登录 URL：http://localhost
    
4. 选择刚刚创建的应用程序 AIPOnBehalfOf，再选择“设置”边栏选项卡中的“属性”。 在“属性”边栏选项卡中，复制“应用程序 ID”值，再关闭此边栏选项卡。 
    
    运行 Set-AIPAuthentication cmdlet 时，此值用于 `WebAppId` 参数。

5. 在“设置”边栏选项卡中，选择“密钥”。 指定说明和选定的持续时间（1 年、2 年或永不过期），添加新密钥。 然后，选择“保存”，并复制显示的“值”字符串。 请务必保存此字符串，因为它不会再次显示，并且无法检索。
    
    运行 Set-AIPAuthentication cmdlet 时，此值用于 `WebAppKey` 参数。

6. 回到“应用程序注册”边栏选项卡，选择“新应用程序注册”，创建本机应用程序。 在“创建”标签上，指定以下值，再单击“创建”：
    
    - 名称：AIPClient
    
    - 应用程序类型：本机
    
    - 登录 URL：http://localhost

7. 选择刚刚创建的应用程序 AIPClient，再选择“设置”边栏选项卡中的“属性”。 在“属性”边栏选项卡中，复制“应用程序 ID”值，再关闭此边栏选项卡。
    
    运行 Set-AIPAuthentication cmdlet 时，此值用于 `NativeAppId` 参数。

8. 在“设置”边栏选项卡中，选择“必需权限”。 

9. 在“必需权限”边栏选项卡中，依次单击“添加”和“选择 API”。 在搜索框中，键入“AIPOnBehalfOf”。 在列表框中选择此值，再单击“选择”。

10. 在“启用访问”边栏选项卡中，选择“AIPOnBehalfOf”，再依次单击“选择”和“完成”。
    
    至此，已配置完两个应用程序，并获取了使用参数运行 [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) 所需的值。


## <a name="next-steps"></a>后续步骤
若要在 PowerShell 会话中获取 cmdlet 帮助，请键入“`Get-Help <cmdlet name> cmdlet`”，并使用联机参数读取最新信息。 例如： 

    Get-Help Get-RMSTemplate -online

有关支持 Azure 信息保护客户端可能需要的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
