---
title: "生成和传送租户密钥 – 通过 Internet | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1bff9b06-8c5a-4b1d-9962-6668219210e6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 20cfa722f7008c52f4fbc219a4de04c50ee3548d


---


# 生成和传送租户密钥 – 通过 Internet

*适用于：Azure Rights Management、Office 365*

如果你决定 [管理自己的租户密钥](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) 并且希望通过 Internet 传送它，而不是亲自前往 Microsoft 设施来传送密钥，请使用以下过程：


## 准备你的连接 Internet 的工作站
为了准备连接 Internet 的工作站，请按照以下 3 个步骤操作：

-   [步骤 1：安装适用于 Azure 权限管理的 Windows PowerShell](#step-1-install-windows-powershell-for-azure-rights-management)

-   [步骤 2：获取你的 Azure Active Directory 租户 ID](#step-2-get-your-azure-active-directory-tenant-id)

-   [步骤 3：下载 BYOK 工具集](#step-3-download-the-byok-toolset)

### 步骤 1：安装适用于 Azure 权限管理的 Windows PowerShell
在连接 Internet 的工作站上下载和安装适用于 Azure Rights Management 的 Windows PowerShell 模块。

> [!NOTE]
> 如果你之前已下载了此 Windows PowerShell 模块，请运行以下命令来检查你的版本号是否至少为 2.1.0.0： `(Get-Module aadrm -ListAvailable).Version`

有关安装说明，请参阅[安装适用于 Azure Rights Management 的 Windows PowerShell](../deploy-use/install-powershell.md)。

### 步骤 2：获取你的 Azure Active Directory 租户 ID
使用 **“以管理员身份运行”** 选项启动 Windows PowerShell，然后运行以下命令：

-   使用 [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) cmdlet 连接到 Azure RMS 服务：

    ```
    Connect-AadrmService
    ```
    出现提示时，输入 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租户管理员凭据（通常，将使用作为 Azure Active Directory 或 Office 365 的全局管理员的帐户）。

-   使用 [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) cmdlet 显示你的租户的配置：

    ```
    Get-AadrmConfiguration
    ```
    保存输出的第一行中的 GUID (BPOSId)。 这是你的 Azure Active Directory 租户 ID，以后你在准备要上载的租户密钥时需要使用它。

-   使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) cmdlet 断开与 Azure RMS 服务的连接，直至你为上载密钥做好准备：

    ```
    Disconnect-AadrmService
    ```

不要关闭 Windows PowerShell 窗口。

### 步骤 3：下载 BYOK 工具集
转至 Microsoft 下载中心并 [下载适用于你所在区域的 BYOK 工具集](http://go.microsoft.com/fwlink/?LinkId=335781) ：

|区域|包名称|
|----------|----------------|
|北美|AzureRMS-BYOK-tools-UnitedStates.zip|
|欧洲|AzureRMS-BYOK-tools-Europe.zip|
|亚洲|AzureRMS-BYOK-tools-AsiaPacific.zip|
工具集包括以下部分：

-   “密钥交换密钥”(KEK) 软件包，名称以 **BYOK-KEK-pkg-** 开头。

-   安全体系包，名称以 **BYOK-SecurityWorld-pkg-** 开头。

-   名为 **verifykeypackage.py**的 Python 脚本。

-   一个名为 **KeyTransferRemote.exe** 的命令行可执行文件、一个名为 **KeyTransferRemote.exe.config** 的元数据文件以及关联的 DLL。

-   名为 **vcredist_x64.exe** 的 Visual C++ 可再分发包。

将包复制到 USB 驱动器或其他便携式存储设备。

## 准备你的未连接工作站
为了准备未连接到网络（Internet 或内部网络）的工作站，请按照以下 2 个步骤操作：

-   [步骤 1：准备要运行 Thales HSM 的未连接工作站](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [步骤 2：在未连接工作站上安装 BYOK 工具集](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### 步骤 1：准备要运行 Thales HSM 的未连接工作站
在未连接工作站的 Windows 计算机上安装 nCipher (Thales) 支持软件，然后将 Thales HSM 连接到该计算机。

确保 Thales 工具在你的路径（**%nfast_home%\bin** 和 **%nfast_home%\python\bin**）中。 例如，键入以下命令：

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
有关详细信息，请参阅 Thales HSM 附带的用户指南，或者访问 Thales 的 Azure RMS 网站，地址为 [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud)。

### 步骤 2：在未连接工作站上安装 BYOK 工具集
从 USB 驱动器或其他便携式存储设备复制 BYOK 工具集包，然后执行以下操作：

1.  将文件从下载包解压到任意文件夹。

2.  在该文件夹下运行 vcredist_x64.exe。

3.  按照以下说明安装 Visual Studio 2012 的 Visual C++ 运行时组件。

## 生成你的租户密钥
在未连接工作站上，按照以下 3 个步骤，生成你自己的租户密钥：

-   [步骤 1：创建安全体系](#step-1-create-a-security-world)

-   [步骤 2：验证下载的包](#step-2-validate-the-downloaded-package)

-   [步骤 3：创建新密钥](#step-3-create-a-new-key)

### 步骤 1：创建安全体系
启动命令提示符，并运行 Thales new-world 程序。

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
此程序可在 %NFAST_KMDATA%\local\world（与 C:\ProgramData\nCipher\Key Management Data\local 文件夹对应）下创建一个**安全体系**文件。 你可以使用不同值进行仲裁，但在我们的示例中，系统提示你输入三个空白卡，以及每个卡的 Pin。 然后，将要求任意两个卡对安全体系（你的指定仲裁）具有管理访问权限。  这些卡变成新安全体系的 **管理员卡集** 。 在此阶段，你可以为每个 ACS 卡指定密码或 PIN，也可以在以后使用命令添加它。

> [!TIP]
> 你可以使用 `nkminfo` 命令验证 HSM 的当前配置状态。

然后执行下列操作：

1.  按照 Thales 文档中的说明，安装 Thales CNG 提供程序，并将其配置为使用新安全体系。

2.  备份 **%nfast_kmdata%\local** 中的体系文件。 保护体系文件、管理员卡及其 PIN，确保没有任何用户能够访问多个卡。

### 步骤 2：验证下载的包
此步骤是可选的，但我们建议执行此步骤，以便能够进行以下验证：

-   工具集包括的“密钥交换密钥”是从真品 Thales HSM 生成的。

-   工具集包括的 Azure RMS 安全体系的哈希是在真品 Thales HSM 中生成的。

-   “密钥交换密钥”是无法导出的。

> [!NOTE]
> 若要验证下载的包，HSM 必须处于连接状态且接通电源，其上必须有安全体系（例如你刚才创建的那一个）。

#### 验证下载的包

1.  根据你所在的地区，键入以下命令之一，以运行 verifykeypackage.py 脚本：

    -   适用于北美：

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   适用于欧洲：

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   适用于亚洲：

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > Thales 软件包括了一个 Python 解释器（位于 %NFAST_HOME%\python\bin 中）

2.  确认你看到以下结果，它表示验证成功： **结果：SUCCESS**

此脚本验证签名人链，一直到 Thales 根密钥。 此根密钥的哈希嵌入到脚本中，其值应为 **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**。 你也可以通过访问 [Thales 网站](http://www.thalesesec.com/)，单独确认该值。

你现在可以创建一个新密钥，作为你的 RMS 租户密钥。

### 步骤 3：创建新密钥
使用 Thales **generatekey** 和 **cngimport** 程序，创建一个 CNG 密钥。

运行以下命令以生成密钥：

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
当你运行此命令时，请使用以下说明：

-   必须将 **protect** 参数设置为值 **module**，如上所示。 这将创建一个受模块保护的密钥。 BYOK 工具集不支持受 OCS 保护的密钥。

-   对于密钥大小，我们建议为 2048 位，但也支持现有 AD RMS 客户拥有 1024 位 RSA 密钥，这些客户使用此类密钥向 Azure RMS 迁移。

-   将 *ident* 和 **plainname** 的 **contosokey** 值替换为任何字符串值。 为了最大程度地减少管理开销和降低错误风险，我们建议两者使用相同的值，并且全部使用小写字符。

-   在本例中，pubexp 保留空白（默认值），但你可以指定特定值。 有关详细信息，请参阅 Thales 文档。

然后运行以下命令，将密钥导入 CNG：

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
当你运行此命令时，请使用以下说明：

-   将 *contosokey* 替换为*在生成你的租户密钥*部分的[步骤 1：创建安全体系](#step-1-create-a-security-world)中指定的同一值。

-   请使用 **-M** 选项，使得密钥适合此方案。 在不使用此选项的情况下，生成的密钥将是当前用户的用户特定密钥。

-   **appname** 选项是密钥文件中报告的应用名称。 如果你使用这些说明创建新密钥，则我们使用与命令中所示一样简单的值。 但是，如果你要迁移现有受 HSM 保护的密钥以便从 AD RMS 迁移到 Azure RMS，请在此命令以及随后的命令（当它们也使用 appname 选项时）中指定现有名称。

此命令可在你的 %NFAST_KMDATA%\local 文件夹中创建一个标记化密钥文件，其名称以 **key_caping`_`** 开头，后跟 SID。 例如：**key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**。 此文件包含加密密钥。

> [!TIP]
> 你可以使用 `nkminfo –k` 命令查看密钥的当前配置状态。

在安全位置备份这个标记化密钥文件。

> [!IMPORTANT]
> 当你以后将密钥传送到 Azure RMS 时，Microsoft 无法再将此密钥导出给你，因此你必须安全地备份密钥和安全体系，这一点极为重要。 请联系 Thales 以获得备份密钥的指导和最佳实践。

你现在可将租户密钥传送到 Azure RMS。

## 准备要传送的租户密钥
在未连接工作站上，按照以下 4 个步骤，准备你自己的租户密钥：

-   [步骤 1：创建你的密钥副本，该副本具有降低的权限](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [步骤 2：检测新的密钥副本](#step-2-inspect-the-new-copy-of-the-key)

-   [步骤 3：使用 Microsoft 的“密钥交换密钥”加密你的密钥](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [步骤 4：将你的密钥传送包复制到连接 Internet 的工作站](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### 步骤 1：创建你的密钥副本，该副本具有降低的权限
若要降低你的租户密钥的权限，请执行以下操作：

-   根据你所在的地区，从命令提示符处运行以下命令之一：

    -   适用于北美：

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   适用于欧洲：

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   适用于亚洲：

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

运行此命令时，请将 *contosokey* 替换为*生成你的租户密钥*部分的[步骤 1：创建安全体系](#step-1-create-a-security-world)中指定的同一值。

可能会要求你插入安全体系 ACS 卡，并且如果指定了其密码或 PIN，还会要求提供它们。

命令完成时，你将看到 **Result: SUCCESS**，并且具有降低的权限的租户密钥副本将位于名为 key_xferacId_*&lt;contosokey&gt;* 的文件中。

### 步骤 2：检测新的密钥副本
或者，运行 Thales 实用工具以确认新租户密钥的最低权限：

-   aclprint.py：

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe：

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

运行此命令时，请将 *contosokey* 替换为*生成你的租户密钥*部分的[步骤 1：创建安全体系](#step-1-create-a-security-world)中指定的同一值。

### 步骤 3：使用 Microsoft 的“密钥交换密钥”加密你的密钥
根据你所在的地区，运行以下命令之一：

-   适用于北美：

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   适用于欧洲：

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   适用于亚洲：

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

当你运行此命令时，请使用以下说明：

-   将 *contosokey* 替换为*生成你的租户密钥*部分的[步骤 1：创建安全体系](#step-1-create-a-security-world)中用于生成密钥的标识符。

-   将 *GUID* 替换为你在*准备你的连接 Internet 的工作站*部分的[步骤 2：获取你的 Azure Active Directory 租户 ID](#step-2-get-your-azure-active-directory-tenant-id) 中检索的 Azure Active Directory 租户 ID。

-   将 *ContosoFirstKey* 替换为将用作输出文件名称的标签。

成功完成后，它将显示 **Result: SUCCESS**，当前文件夹中将有一个新文件，名称如下：TransferPackage-*ContosoFirstkey*.byok

### 步骤 4：将你的密钥传送包复制到连接 Internet 的工作站
使用 USB 驱动器或其他便携式存储设备，将前一步骤中的输出文件 (KeyTransferPackage-*ContosoFirstkey*.byok) 复制到连接 Internet 的工作站。

> [!NOTE]
> 运用安全实践来保护该文件，因为其中包含你的私钥。

## 将你的租户密钥传送到 Azure RMS
在连接 Internet 的工作站上，按照以下 3 个步骤，将你的新租户密钥传送到 Azure RMS：

-   [步骤 1：连接到 Azure RMS](#step-1-connect-to-azure-rms)

-   [步骤 2：上载密钥包](#step-2-upload-the-key-package)

-   [步骤 3：根据需要枚举你的租户密钥](#step-3-enumerate-your-tenant-keys-as-needed)

### 步骤 1：连接到 Azure RMS
返回到 Windows PowerShell 窗口并键入以下命令：

1.  重新连接到 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]服务：

    ```
    Connect-AadrmService
    ```

2.  使用 [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) cmdlet 查看你的当前租户密钥配置：

    ```
    Get-AadrmKeys
    ```

### 步骤 2：上载密钥包
使用 [Add-AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) cmdlet 上载你从未连接工作站复制的密钥传送包：

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> 系统将提示你确认此操作。 必须知道此操作是无法撤销的，这一点非常重要。 当你上载租户文件时，它自动成为你组织的首选租户密钥，用户将在保护文档和文件时开始使用此租户密钥。

如果上载成功，你将看到以下消息： **权限管理服务已成功添加密钥。**

当更改传播到所有 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]数据中心时，将会出现复制延迟。

### 步骤 3：根据需要枚举你的租户密钥
每当你希望查看租户密钥列表以及查看租户密钥的更改时，可再次使用 Get-AadrmKeys cmdlet。 显示的租户密钥包括 Microsoft 为你生成的初始租户密钥，以及你添加的任何租户密钥：

```
Get-AadrmKeys
```
标记为 **“活动”** 的租户密钥是你的组织当前用于保护文档和文件的密钥。

你现在已经完成了通过 Internet 自带密钥所需的全部步骤，接下来可以执行规划和实现租户密钥的后续步骤。


> [!div class="button"]
[后续步骤 >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Jun16_HO4-->


