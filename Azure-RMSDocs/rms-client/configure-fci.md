---
title: 使用 Windows Server FCI 的 Azure RMS 保护 - AIP
description: 有关将 Rights Management (RMS) 客户端与 Azure 信息保护客户端配合使用，以配置文件服务器资源管理器和文件分类基础结构 (FCI) 的说明。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d3afd356ee64d337bf171488e8be6aa65049d7ee
ms.sourcegitcommit: 479b3aaea7011750ff85a217298e5ae9185c1dd1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82224727"
---
# <a name="rms-protection-with-windows-server-file-classification-infrastructure-fci"></a>使用 Windows Server 文件分类基础结构 (FCI) 的 RMS 保护

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012、Windows Server 2012 R2**
>
> *适用于[Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

通过本文获取相关说明和脚本以使用 Azure 信息保护客户端和 PowerShell 配置文件服务器资源管理器和文件分类基础结构 (FCI)。

此解决方案允许你自动保护运行 Windows Server 的文件服务器上的文件夹中的所有文件或自动保护符合特定条件的文件。 例如，已分类为包含机密或敏感信息的文件。 此解决方案直接连接 Azure 信息保护中的 Azure 权限管理服务来保护文件，因此必须为你的组织部署此服务。

> [!NOTE]
> 尽管 Azure 信息保护包括支持文件分类基础结构的[连接器](../deploy-rms-connector.md)，但该解决方案仅支持本机保护（例如，Office 文件）。
> 
> 若要支持使用 Windows Server 文件分类基础结构的多个文件类型，必须使用 PowerShell **AzureInformationProtection** 模块，如本文中所述。 Azure 信息保护 cmdlet（如 Azure 信息保护客户端）支持常规保护和本机保护，这意味着可以保护 Office 文档以外的文件类型。 有关详细信息，请参阅 Azure 信息保护客户端管理员指南中的 [Azure 信息保护客户端支持的文件类型](client-admin-guide-file-types.md)。

接下来的说明适用于 Windows Server 2012 R2 或 Windows Server 2012。 如果你运行其他受支持的 Windows 版本，则可能需要调整某些步骤，以适应你的操作系统版本与本文所述的操作系统版本之间的差异。

## <a name="prerequisites-for-azure-rights-management-protection-with-windows-server-fci"></a>使用 Windows Server FCI 的 Azure Rights Management 保护的先决条件
这些说明的先决条件：

- 在你将运行使用文件分类基础结构的文件资源管理器的每个文件服务器上：
    
  - 你已安装文件服务器资源管理器作为文件服务角色的角色服务之一。
    
  - 已标识包含要使用 Rights Management 保护的文件的本地文件夹。 例如，C:\FileShare。
    
  - 你已安装 AzureInfAormationProtection PowerShell 模块并已为此模块配置先决条件以连接到 Azure 权限管理服务。
    
    Azure 信息保护客户端附带 AzureInformationProtection PowerShell 模块。 有关安装说明，请参阅 Azure 信息保护管理员指南中的[为用户安装 Azure 信息保护客户端](client-admin-guide-install.md)。 如有需要，可以使用 `PowerShellOnly=true` 参数仅安装 PowerShell 模块。
    
    如果你的租户在北美以外的地区，则[使用此 PowerShell 模块的先决条件](client-admin-guide-powershell.md#azure-information-protection-and-azure-rights-management-service)包括激活 Azure 权限管理服务、创建服务主体，以及编辑注册表。 在按照本文说明开始操作之前，请确保你具有 BposTenantId****、AppPrincipalId**** 以及对称密钥**** 的值，如先决条件中所述。 
    
  - 如果要更改特定文件扩展名保护（本机或常规）的默认级别，需已编辑注册表，如管理员指南中的[更改文件的默认保护级别](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)部分所述。
    
  - 你具有 internet 连接，并且已配置了计算机设置（如果代理服务器需要这些设置）。 例如：`netsh winhttp import proxy source=ie`
    
- 你已将本地 Active Directory 用户帐户（包括其电子邮件地址）与 Azure Active Directory 或 Office 365 同步。 对于所有需要访问受 FCI 和 Azure Rights Management 服务保护的文件的用户来说，这都是必需的。 如果你未执行此步骤（例如，在测试环境中），可能会阻止用户访问这些文件。 如果你需要有关此要求的详细信息，请参阅 [准备用户和组以便使用 Azure 信息保护](../prepare.md)。
    
- 此方案不支持部门模板，因此你必须使用未配置为作用域的模板，或者使用[AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) Cmdlet 和*EnableInLegacyApps*参数。

## <a name="instructions-to-configure-file-server-resource-manager-fci-for-azure-rights-management-protection"></a>为 Azure 权限管理保护配置文件服务器资源管理器 FCI 的说明
按照这些说明通过使用 PowerShell 脚本作为自定义任务自动保护一个文件夹中的所有文件。 按此顺序执行这些过程：

1. 保存 PowerShell 脚本

2. 为 Rights Management (RMS) 创建分类属性

3. 创建分类规则 (Classify for RMS)

4. 配置分类计划

5. 创建自定义文件管理任务（使用 RMS 保护文件）

6. 通过手动运行规则和任务来测试配置

在这些说明结束时，所选文件夹中的所有文件都将使用 RMS 的自定义属性进行分类，然后这些文件将受 Rights Management 保护。 对于更复杂的配置（如有选择性地保护某些文件，而不保护其他文件），你可以然后创建或使用不同的分类属性和规则，用于仅保护这些文件的文件管理任务。

请注意，如果对用于 FCI 的 Rights Management 模板进行更改，运行脚本以保护文件的计算机帐户不会自动获得更新的模板。 为此，在脚本中，找到被注释掉的 `Get-RMSTemplate -Force` 命令，并删除 `#` 注释字符。 当下载更新模板（该脚本至少运行一次），可以注释掉此附加命令，以便不会每次不必要地下载模板。 如果通过对模板的更改就足以重新保护文件服务器上的文件，则可以通过运行 Protect-RMSFile cmdlet 与对文件具有“导出”或“完全控制”使用权限的帐户以交互方式执行此操作。 如果发布了想要用于 FCI 的新模板，则还必须运行 `Get-RMSTemplate -Force`。

### <a name="save-the-windows-powershell-script"></a>保存 Windows PowerShell 脚本

1.  使用文件服务器资源管理器，复制用于 Azure RMS 保护的 [Windows PowerShell 脚本](fci-script.md)的内容。 粘贴该脚本的内容，并在你自己的计算机上将该文件命名为 **RMS-Protect-FCI.ps1**。

2.  查看脚本，然后进行以下更改：
    
    - 搜索以下字符串并将其替换为自己的 AppPrincipalId，将在 [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) cmdlet 中使用此 AppPrincipalId 连接到 Azure 权限管理服务：

        ```
        <enter your AppPrincipalId here>
        ```
        例如，脚本可能如下所示：

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   搜索以下字符串并将其替换为你自己的对称密钥，你将在 [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) cmdlet 中使用此对称密钥连接到 Azure Rights Management 服务：

        ```
        <enter your key here>
        ```
        例如，脚本可能如下所示：

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   搜索以下字符串并将其替换为你自己的 BposTenantId（租户 ID），你将在 [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) cmdlet 中使用此对称密钥连接到 Azure Rights Management 服务：

        ```
        <enter your BposTenantId here>
        ```
        例如，脚本可能如下所示：

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

3.  为脚本签名。 如果未为脚本签名（更安全），则必须在运行该脚本的服务器上配置 Windows PowerShell。 例如，使用“以管理员身份运行”**** 选项运行 Windows PowerShell 会话，然后键入：“Set-ExecutionPolicy RemoteSigned”****。 但是，当未签名的脚本被存储在此服务器上时，此配置将允许所有未签名的脚本运行（不太安全）。

    有关为 Windows PowerShell 脚本签名的详细信息，请参阅 PowerShell 文档库中的 [about_Signing](https://technet.microsoft.com/library/hh847874.aspx)。

4.  将文件本地保存到运行使用文件分类基础结构的文件资源管理器的每个文件服务器上。 例如，将文件保存到 **C:\RMS-Protection** 中。 如果你使用不同的路径或文件夹名称，则选择不含空格的路径和文件夹。 使用 NTFS 权限保护此文件，使未经授权的用户不能修改它。

现在，你可以开始配置文件服务器资源管理器。

### <a name="create-a-classification-property-for-rights-management-rms"></a>为 Rights Management (RMS) 创建分类属性

-   在文件服务器资源管理器中，为“分类管理”创建新的本地属性：

    -   **名称**：键入 **RMS**

    -   **说明**： 键入“Rights Management 保护” ****

    -   **属性类型**：选择“是/否”****

    -   **值**：选择“是” ****

我们现在可以创建使用此属性的分类规则。

### <a name="create-a-classification-rule-classify-for-rms"></a>创建分类规则 (Classify for RMS)

-   创建新的分类规则：

    -   在“常规”选项卡上****：

        -   **名称**：键入 **Classify for RMS**

        -   **已启用**：保留默认设置，即选中此复选框。

        -   **说明**：键入“对&lt;文件夹名称&gt;中的所有文件进行分类以便使用 Rights Management”****。

            将* &lt;文件夹名称&gt; *替换为所选的文件夹名称。 例如，“为 Rights Management 的 C:\FileShare 文件夹中的所有文件分类”****

        -   **范围**：添加所选的文件夹。 例如，**C:\FileShare**。

            请勿选择复选框。

    -   在“分类”选项卡上****：

    -   **分类方法**：选择“文件夹分类器” ****

    -   **属性** 名称：选择 **RMS**

    -   属性 **值**：选择“是” ****

虽然可以手动运行分类规则，但是对于正在进行的操作，需要按计划运行此规则，使新文件使用 RMS 属性进行分类。

### <a name="configure-the-classification-schedule"></a>配置分类计划

-   在“自动分类”选项卡上****：

    -   **启用固定日程安排**：选中此复选框。

    -   配置所有要运行的分类规则的日程安排，其中包括要使用 RMS 属性为文件分类的新规则。

    -   允许对新文件进行连续分类：选中此复选框以便将新文件进行分类****。

    -   可选：进行任何其他所需的更改，例如，为报告和通知配置选项。

现在你已完成分类配置，已可以配置管理任务，以将 RMS 保护应用于这些文件。

### <a name="create-a-custom-file-management-task-protect-files-with-rms"></a>创建自定义文件管理任务（使用 RMS 保护文件）

-   在“文件管理任务”中，创建新的文件管理任务****：

    -   在“常规”选项卡上****：

        -   **任务名称**：键入 **Protect files with RMS**

        -   保留选中“启用”**** 复选框。

        -   **说明**：键入**使用 Windows PowerShell 脚本通过 Rights Management 和模板保护&lt;文件夹名称&gt;中的文件。**

            将* &lt;文件夹名称&gt; *替换为所选的文件夹名称。 例如，“使用 Windows PowerShell 脚本通过 Rights Management 和模板保护 C:\FileShare 中的文件”****

        -   **范围**：选择所选的文件夹。 例如，**C:\FileShare**。

            请勿选择复选框。

    -   在“操作”选项卡上****：

        -   **类型**：选择“自定义” ****

        -   **可执行文件**：指定以下项：

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            如果 Windows 不在 C: 驱动器上，请修改此路径或浏览到此文件。

        -   **参数**：指定下列各项，为&lt;路径&gt;和&lt;模板 ID&gt;提供自己的值：

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail '[Source File Owner Email]'"
            ```
            例如，如果你将该脚本复制到 C:\RMS-Protection 并且从必备组件找到的模板 ID 是 e6ee2481-26b9-45e5-b34a-f744eacd53b0，请指定以下项：

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail '[Source File Owner Email]'"`

            在此命令中，[Source File Path] 和 [Source File Owner Email] 都是特定于 FCI 的变量，因此键入这些项时要与出现在之前的命令中的内容完全一致********。 第一个变量由 FCI 用于自动指定文件夹中标识的文件，第二个变量供 FCI 用于自动检索所标识文件的命名所有者的电子邮件地址。 对文件夹中的每个文件重复执行此命令，在我们的示例中为 C:\FileShare 文件夹中还使用 RMS 作为文件分类属性的每个文件。

            > [!NOTE]
            > **-OwnerMail [Source File Owner Email]** 参数和值可确保在文件受保护之后，向文件的原始所有者授予文件的 Rights Management 所有者的权限。 此配置可确保原始文件所有者对其自己的文件具有所有 Rights Management 权限。 当域用户创建文件时，将自动使用文件 Owner 属性中的用户帐户名称从 Active Directory 中检索电子邮件地址。 要做到这一点，文件服务器必须与用户在同一个域或受信任的域中。
            > 
            > 尽可能将原始所有者分配给受保护的文档，以确保这些用户继续对他们创建的文件具有完全控制权。 但是，如果按之前的命令中所示使用 [Source File Owner Email] 变量并且文件没有将域用户定义为所有者（例如，使用本地帐户创建的该文件，因此所有者显示 SYSTEM），则脚本会失败。
            > 
            > 对于未使用域用户作为所有者的文件，你可以作为域用户自行复制并保存这些文件，使你只是成为这些文件的所有者。 或者，如果你有权限，你可以手动更改所有者。  或者，你也可以提供特定电子邮件地址（例如，你自己的电子邮件地址或 IT 部门的组地址）而不使用 [Source File Owner Email] 变量，这意味着你通过使用此脚本保护的所有文件都将使用此电子邮件地址来定义新的所有者。

    -   **运行命令的访问权限**：选择“本地系统” ****

    -   在“条件”选项卡上****：

        -   **属性**：选择“是/否” **RMS**

        -   **运营商**：选择“等于”****

        -   **值**：选择“是” ****

    -   在“计划”**** 选项卡上：

        -   **运行时间**：配置你的首选计划。

            安排足够的的时间让脚本可以完成。 尽管此解决方案保护文件夹中的所有文件，但该脚本每次对于每个文件只运行一次。 尽管这比同时保护所有文件（Azure 信息保护客户端支持此方式）要费时，但 FCI 的此逐个文件配置更功能强大。 例如，使用 [Source File Owner Email] 变量时，受保护的文件可以具有不同的所有者（保留原始所有者），并且如果稍后更改配置以有选择性地保护文件（而不是文件夹中的所有文件），则需要此逐个文件操作。

        -   **连续对新文件运行**：选中此复选框。

### <a name="test-the-configuration-by-manually-running-the-rule-and-task"></a>通过手动运行规则和任务来测试配置

1.  运行分类规则：

    1.  单击“分类规则”**>“立即使用所有规则运行分类”** &gt; ****

    2.  单击“等待分类完成”，然后单击“确定”********。

2.  等待“运行分类”对话框关闭，然后在自动显示的报告中查看结果****。 你应该会在“属性”字段中看到“1”，并可以看到你的文件夹中的文件数********。 通过使用文件资源管理器检查所选文件夹中的文件的属性来进行确认。 在“分类”选项卡上，你应该会看到 **RMS** 为属性名称，“是”为其**值**********。

3.  运行文件管理任务：

    1.  单击“文件管理任务”**>“使用 RMS 保护文件”** &gt; **>“立即运行文件管理任务”** &gt; ****

    2.  单击“等待任务完成”，然后单击“确定”********。

4.  等待“运行文件管理任务”对话框关闭，然后在自动显示的报告中查看结果****。 你应在“文件”字段中看到所选文件夹中的文件数****。 确认所选文件夹中的文件现已受权限管理保护。 例如，如果所选文件夹是 C:\FileShare，则在 Windows PowerShell 会话中键入以下命令并确认没有文件处于“未保护”**** 状态：

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > 一些故障排除技巧：
    > 
    > -   如果你在报告中看到“0”****（而不是你的文件夹中的文件数），则此输出指示脚本未运行。 首先，通过在 Windows PowerShell ISE 中加载脚本以验证脚本内容来检查脚本本身，然后尝试在相同的 PowerShell 会话中运行脚本一次，查看是否显示任何错误。 如果未指定任何参数，该脚本会尝试连接到 Azure 权限管理服务并向其进行身份验证。
    > 
    >     -   如果该脚本报告无法连接到 Azure 权限管理服务 (Azure RMS)，请检查它为服务主体帐户显示的值，该帐户在脚本中指定。 有关如何创建此服务主体帐户的详细信息，请参阅 Azure 信息保护客户端管理员指南中的[先决条件 3：在不交互的情况下保护或取消保护文件](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction)。
    >     -   如果该脚本报告可连接到 Azure RMS，接下来通过直接运行服务器上 Windows PowerShell 的 [Get-RMSTemplate](/powershell/azureinformationprotection/vlatest/get-rmstemplate) 检查是否可找到指定的模板。 你应该会看到你所指定的模板返回到结果中。
    > -   如果该脚本单独在 Windows PowerShell ISE 中运行时未出现错误，请尝试从 PowerShell 会话中按以下方式运行它：指定要保护的文件名，并且不带 -OwnerEmail 参数：
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   如果该脚本在此 Windows PowerShell 会话中成功运行，请在文件管理任务操作中检查 **Executive** 和 **Argument** 的条目。  如果已指定 **-OwnerEmail [Source File Owner Email]**，请尝试删除此参数。
    > 
    >         如果文件管理任务在没有 **-OwnerEmail [Source File Owner Email]** 的情况下成功运行，请检查未受保护的文件是否有域用户（而不是 **SYSTEM**）列出为文件所有者。  若要执行此检查，请使用文件的属性的“安全”**** 选项卡，然后单击“高级”****。 **所有者**值将紧接着显示在文件**名称**之后。 另外，请验证文件服务器是否位于同一域或受信任的域中，以便从 Active Directory 域服务中查找该用户的电子邮件地址。
    > -   如果你在报告中看到正确的文件数，但文件未受保护，请尝试使用 [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile) cmdlet 手动保护文件以查看是否显示任何错误。

在确认这些任务成功运行之后，可以关闭文件资源管理器。 计划的任务运行时，会自动对新文件进行分类并给予保护。 

## <a name="action-required-if-you-make-changes-to-the-rights-management-template"></a>对 Rights Management 模板进行更改所需的操作

如果对脚本引用的 Rights Management 模板进行更改，运行脚本以保护文件的计算机帐户不会自动获得更新的模板。 在脚本中，查找出 Set-RMSConnection 函数中注释掉的 `Get-RMSTemplate -Force` 命令，并删除行开头的注释字符。 下次该脚本运行时，会下载更新的模板。 若要优化性能，以便不会不必要地下载模板，则可以再次注释掉此行。 

如果通过对模板的更改就足以重新保护文件服务器上的文件，则可以通过运行 Protect-RMSFile cmdlet 与对文件具有“导出”或“完全控制”使用权限的帐户以交互方式执行此操作。 

此外，如果发布了想要用于 FCI 的新模板，并且在自定义文件管理任务的参数行中更改模板 ID，请在脚本中运行该行。

## <a name="modifying-the-instructions-to-selectively-protect-files"></a>修改说明可有选择性地保护文件
如果按前面的说明正常操作，则可轻松修改它们以实现更复杂的配置。 例如，使用同一个脚本保护文件，但只针对包含个人身份信息的文件，然后可能选择具有更多限制权限的模板。

若要进行此修改，请使用内置分类属性之一（例如“个人身份信息”****）或创建你自己的新属性。 然后创建一个使用此属性的新规则。 例如，可能会选择“内容分类器”，为“个人身份信息”属性选择值“高”，并配置字符串或表达式模式（如字符串“出生日期”）以标识要为此属性配置的文件****************。

现在你需要做的只是创建新的文件管理任务（该任务使用同一脚本但可能使用不同模板），并为刚配置的分类属性配置条件。 例如，不是我们前面配置的条件（**RMS** 属性**等于**“是”），而是选择“运算符”值设为“等于”且“值”为“高”的“个人身份信息”属性************************。

## <a name="next-steps"></a>后续步骤

你可能想知道：[Windows Server FCI 和 Azure 信息保护扫描程序有何区别？](../faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner) 

