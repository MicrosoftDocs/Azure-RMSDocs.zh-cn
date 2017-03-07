---
title: "将 PowerShell 与 Azure 信息保护客户端配合使用"
description: "管理员通过使用 PowerShell 管理 Azure 信息保护客户端的说明和信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 17824b007444e9539ffc0374bf39f0984efa494c
ms.openlocfilehash: d180b0ff4390df45a61b7d50913c267fb3cf35e1
ms.lasthandoff: 02/28/2017


---


# <a name="using-powershell-with-the-azure-information-protection-client"></a>将 PowerShell 与 Azure 信息保护客户端配合使用

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

安装 Azure 信息保护客户端时，将自动安装 PowerShell 命令，从而通过运行可放入自动化脚本的命令来管理客户端。

cmdlet 随 PowerShell 模块 **AzureInformationProtection** 一起安装，该模块将替代随 RMS 保护工具一起安装的 RMSProtection 模块。 如果在安装 Azure 信息保护客户端时安装了 RMSProtection 工具，则会自动卸载 RMSProtection 模块。

AzureInformationProtection 模块包括 RMS 保护工具的所有 Rights Management cmdlet 和使用 Azure 信息保护 (AIP) 服务进行标记的两个新 cmdlet：

|标记 cmdlet|示例用法|
|----------------|---------------|
|[Get AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus)|对于共享文件夹，请标识具有特定标签的所有文件。|
|[Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel)|对于共享文件夹，将指定的标签应用于没有标签的所有文件。|

有关所有 cmdlet 及其相应帮助的列表，请参阅 [AzureInformationProtection 模块](/powershell/azureinformationprotection/vlatest/aip)。

此模块安装在 **\ProgramFiles (x86)\Microsoft Azure Information Protection** 中，并将此文件夹添加到 **PSModulePath** 系统变量。 此模块的 .dll 命名为 **AIP.dll**。

与 RMSProtection 模块一样，AzureInformationProtection 模块的当前版本具有以下限制：

- 可以取消保护 Outlook 个人文件夹（.pst 文件），但当前无法使用 PowerShell 模块本机保护这些文件或其他容器文件。

- 当 Outlook 保护的电子邮件（.rpmsg 文件）位于 Outlook 个人文件夹 (.pst) 时，可以取消保护这些文件，但不能取消保护个人文件夹外的 .rpmsg 文件。

在开始使用这些 cmdlet 之前，请参阅与你的部署对应的其他先决条件和说明：

- [Azure 信息保护服务和 Azure 权限管理服务](#azure-information-protection-service-and-azure-rights-management-service)

    - 将仅分类或分类用于 Rights Management 保护时适用：具有包含 Azure 信息保护的订阅（例如，企业移动性 + 安全性）。
    - 将仅保护用于 Azure 权限管理服务时适用：具有包含 Azure 权限管理服务的订阅（例如，Office 365 E3 和 Office 365 E5）。

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - 将仅保护用于 Azure 权限管理的本地版本时适用；Active Directory Rights Management Services (AD RMS)。


## <a name="azure-information-protection-service-and-azure-rights-management-service"></a>Azure 信息保护服务和 Azure 权限管理服务

当你的组织在使用 Azure 信息保护和 Azure 权限管理数据保护服务或仅使用 Azure 权限管理服务时，请阅读本节，然后才开始使用 PowerShell 命令。


### <a name="prerequisites-for-aip-and-azure-rms"></a>AIP 和 Azure RMS 的先决条件

除了安装 AzureInformationProtection 模块的先决条件之外，Azure 信息保护服务和 Azure 权限管理数据保护服务还有其他先决条件：

1. 必须激活 Azure 权限管理服务。

2. 若要使用自己的帐户从他人的文件中删除保护：必须为你的组织启用超级用户功能，而且必须将你的帐户配置为 Azure 权限管理的超级用户。

3. 若要在无用户交互的情况下直接保护或取消保护文件：创建服务主体帐户，运行 Set-RMSServerAuthentication，并考虑将此服务主体作为 Azure 权限管理的超级用户。

4. 对于北美以外的地区：编辑注册表，以便对服务进行身份验证。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>先决条件 1：必须激活 Azure 权限管理服务

无论是通过使用标签还是直接连接到 Azure 权限管理服务来应用数据保护，此先决条件都适用。 配置为应用数据保护。

如果未激活 Azure 信息保护租户，请参阅[激活 Azure 权限管理](../deploy-use/activate-service.md)的说明。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>先决条件 2：使用自己的帐户从他人的文件中删除保护

从他人的文件中删除保护的典型方案包括数据发现或数据恢复。 如果使用标签应用保护，则可以通过设置不应用保护的新标签或通过删除标签来删除保护。 但是，你更有可能通过直接连接到 Azure 权限管理服务来删除保护。

用户必须具有从文件删除保护的 Rights Management 权限或者成为超级用户。 对于数据发现或数据恢复，通常会使用超级用户功能。 若要启用此功能并将你的帐户配置为超级用户，请参阅[为 Azure 管理权限和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

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
    
    出现提示时，输入 Azure 信息保护租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。
    
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

通过从 Azure Active Directory 的 MSOnline PowerShell 模块运行 `New-MsolServicePrincipal` cmdlet 或从较新的 Azure Active Directory 版本 2 PowerShell 模块运行 `New-AzureADServicePrincipal` 来创建新的服务主体。 

以下说明适用于 Azure Active Directory 的 MSOnline PowerShell 模块中的 New-MsolServicePrincipal：

1. 如果计算机上尚未安装此模块，请参阅[安装 Azure AD 模块](/powershell/azuread/#install-the-azure-ad-module)。

2. 使用“以管理员身份运行”选项启动 Windows PowerShell。

3. 使用 **Connect-MsolService** cmdlet 连接到 Azure AD：
    
        Connect-MsolService
    
    出现提示时，输入 Azure AD 租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。

4. 运行 New-MsolServicePrincipal cmdlet 以创建新的服务主体：
    
        New-MsolServicePrincipal
    
    出现提示时，请输入为此服务主体选择的显示名称，以帮助你确定其用途是以后作为你连接到 Azure 权限管理服务的帐户，从而可以保护和取消保护文件。
    
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

    请务必创建对称密钥的副本，因为在以后无法完整地检索它，所以如果你不知道，在下次需要对 Azure 权限管理服务进行身份验证时，需要创建新的服务主体。

通过这些说明和示例可知，运行 Set-RMSServerAuthentication 需要&3; 个标识符：

- 租户 ID：**23976bc6-dcd4-4173-9d96-dad1f48efd42**

- 对称密钥：**zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA =**

- AppPrincipalId：**b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

我们的示例命令将如下所示：

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

如上一个命令所示，可以使用单个命令提供值，也可以键入 Set-RMSServerAuthentication，并在出现提示时逐个提供值。 命令完成后，你将看到“RmsServerAuthentication 设置为启用”，这意味着现在可以通过使用服务主体来保护和取消保护文件。

考虑使此服务主体成为超级用户：要确保此服务主体始终可以取消保护其他人的文件，可以将其配置为超级用户。 通过与将标准用户帐户配置为超级用户相同的方式，使用相同的 Azure RMS cmdlet ([Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md))，但使用 AppPrincipalId 值指定 **-ServicePrincipalId** 参数。

有关超级用户的详细信息，请参阅[为 Azure 权限管理和发现服务或数据恢复配置超级用户](../deploy-use/configure-super-users.md)。

> [!NOTE]
> 若要使用自己的帐户对 Azure 权限管理服务进行身份验证，则无需在保护或取消保护文件或获取模板之前运行 Set-RMSServerAuthentication。

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>先决条件 4：北美以外的区域

对于 Azure 北美地区以外的身份验证，必须按如下所示编辑注册表。 如果 Azure 信息保护租户位于北美，则不要执行此步骤：

1. 再次运行 Get-AadrmConfiguration cmdlet，并记下 **CertificationExtranetDistributionPointUrl** 和 **LicensingExtranetDistributionPointUrl** 的值。

2. 在将运行 AzureInformationProtection cmdlet 的每台计算机上，打开注册表编辑器并导航到：`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC`

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

另外，还需要获取 Rights Management 模板的列表以确定要使用的模板及其相应的 ID 号，然后才可以保护文件。 然后可从输出复制模板 ID：

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

请注意，如果你未运行 Set-RMSServerAuthentication 命令，将使用自己的用户帐户对 Azure 权限管理服务进行身份验证。 如果在已加入域的计算机上，将始终自动使用你的当前凭据。 如果在工作组计算机上，系统将提示你登录到 Azure，然后缓存这些凭据以用于后续命令。 在这种情况下，如果以后需要以其他用户身份登录，请使用 `Clear-RMSAuthentication` cmdlet。

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


## <a name="active-directory-rights-management-services"></a>Active Directory 权限管理服务

当你的组织仅使用 Active Directory Rights Management Services 时，请阅读本节，然后才开始使用 PowerShell 命令来保护或取消保护文件。


### <a name="prerequisites-for-ad-rms"></a>AD RMS 的先决条件

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

首先，如果有多个 AD RMS 部署，则需要 AD RMS 服务器的名称，通过使用 Get-RMSServer cmdlet 来显示可用服务器的列表可以完成此操作：

    Get-RMSServer

输出可能与以下内容类似：

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

在可以保护文件之前，需要获取 RMS 模板的列表，以确定要使用的模板及其相应的 ID 号。 仅当具有多个 AD RMS 部署时，才需要同时指定 RMS 服务器。 

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


## <a name="next-steps"></a>后续步骤
对于在 PowerShell 会话中时所需的 cmdlet帮助，请使用 Get-Help <cmdlet name> cmdlet，其中 <cmdlet name> 是要研究的 cmdlet 的名称。 例如： 

    Get-Help Get-RMSTemplate

有关支持 Azure 信息保护客户端可能需要的其他信息，请参阅以下内容：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

