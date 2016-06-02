---
# required metadata

title: 亲自生成和传送你的租户密钥 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3281e45e-cf69-4dc5-946b-3029851d3152

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 亲自生成和传送你的租户密钥

*适用于：Azure Rights Management、Office 365*


如果你决定 [管理自己的租户密钥](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) 并且不希望通过 Internet 传送它，请使用以下过程亲自传送你的租户密钥。

## 生成你的租户密钥
若要生成你自己的租户密钥，请执行以下 3 个步骤：

-   [步骤 1：准备运行 Thales HSM 的工作站](#step-1-prepare-a-workstation-with-thales-hsm)

-   [步骤 2：创建安全体系](#step-2-create-a-security-world)

-   [步骤 3：创建新密钥](#step-3-create-a-new-key)

### 步骤 1：准备运行 Thales HSM 的工作站
在 Windows 计算机上安装 nCipher (Thales) 支持软件。 将 Thales HSM 连接到该计算机。 确保 Thales 工具在你的路径中。 有关详细信息，请参阅 Thales HSM 附带的用户指南，或者访问 Thales 的 Azure RMS 网站，地址为 [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### 步骤 2：创建安全体系
启动命令提示符，并运行 Thales new-world 程序。

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
此程序可在 %NFAST_KMDATA%\local\world（与 C:\ProgramData\nCipher\Key Management Data\local 文件夹对应）下创建一个**安全体系**文件。 你可以使用不同值进行仲裁，但在我们的示例中，系统提示你输入三个空白卡，以及每个卡的 Pin。 因此，其中任意二个卡将提供对安全体系的完全访问权限。  这些卡变成新安全体系的 **管理员卡集** 。

然后执行下列操作：

1.  按照 Thales 文档中的说明，安装 Thales CNG 提供程序，并将其配置为使用新安全体系。

2.  备份体系文件。 保护体系文件、管理员卡及其 PIN，确保没有任何用户能够访问多个卡。

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
cngimport --import –M --key=contosokey --appname=simple contosokey
```
当你运行此命令时，请使用以下说明：

-   将 *contosokey* 替换为你在步骤 1 中指定的同一值。

-   请使用 **-M** 选项，使得密钥适合此方案。 在不使用此选项的情况下，生成的密钥将是当前用户的用户特定密钥。

此命令可在你的 %NFAST_KMDATA%\local 文件夹中创建一个标记化密钥文件，其名称以 **key_caping`_`** 开头，后跟 SID。 例如：**key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**。 此文件包含加密密钥。

在安全位置备份这个标记化密钥文件。

> [!IMPORTANT]
> 当你以后将密钥传送到 Azure RMS 时，Microsoft 将拥有你的密钥的不可恢复副本。 这意味着 Microsoft 的任何人都无法从 HSM 检索你的密钥。 这使你能够保持对租户密钥的独有控制。 因此，你必须安全地备份密钥和安全体系，这一点极为重要。 请联系 Thales 以获得备份密钥的指导和最佳实践。

你现在可将租户密钥传送到 Azure RMS。

## 将你的租户密钥传送到 Azure RMS
在你生成自己的密钥之后，在使用之前，必须将其传送到 Azure RMS。 为了达到最高级别的安全性，这种传送采用人工过程，要求你亲自前往位于美国华盛顿州 Redmond 市的 Microsoft 办事处。 若要完成此过程，请执行以下 3 个步骤：

-   [步骤 1：将你的密钥提供给 Microsoft](#step-1-bring-your-key-to-microsoft)

-   [步骤 2：将你的密钥传送到 Azure RMS 安全体系](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [步骤 3：完成过程](#step-3-closing-procedures)

### 步骤 1：将你的密钥提供给 Microsoft

-   联系 Microsoft 客户支持服务 (CSS)，安排 Azure RMS 的密钥传送预约。 向位于 Redmond 市的 Microsoft 设施提交以下项目：

    -   管理卡的仲裁。 如果你遵循了前面[步骤 2：创建安全体系](#step-2-create-a-security-world)中的说明，则它们是三个卡中的任意两个卡。

    -   被授权携带你的管理卡和 PIN 的员工，通常有两位（一人一卡）。

    -   你的安全体系文件 (%NFAST_KMDATA%\local\world)，保存在 USB 驱动器上。

    -   你的标记化密钥文件，保存在 USB 驱动器上。

### 步骤 2：将你的密钥传送到 Azure RMS 安全体系

1.  当你亲自前往 Microsoft 传送你的密钥时，会发生以下情况：

    -   Microsoft 为你提供连接 Thales HSM 的脱机工作站，它安装了 Thales 软件，并将 Azure RMS 安全体系文件预先加载到文件夹 C:\Temp\Destination。

    -   在此工作站上，你将 USB 驱动器上的安全体系文件和标记化密钥文件加载到 C:\Temp\Source 文件夹中。

    -   Azure RMS 操作人员使用 Thales 实用工具，将你的密钥安全传送到 Azure RMS 安全体系。

    这个过程与以下过程类似，本例中的最后一个参数 key-xfer-im 替换为你的标记化密钥文件名称：

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  Mk-reprogram 将请求你和 Azure RMS 操作人员插入相应的管理员卡和 PIN。 这些命令在包含受 Azure RMS 安全体系保护的密钥的 C:\Temp\Destination 目录中输出一个标记化密钥文件。

### 步骤 3：完成过程

-   当你在场的情况下，Azure RMS 操作人员执行以下操作：

    -   运行 Microsoft 和 Thales 协作开发的一种工具，用于删除两种权限：恢复密钥的权限、更改权限的权限。 完成此操作后，你的这个密钥副本将会锁定到 Azure RMS 安全体系。 Thales HSM 将不允许拥有管理员卡的 Azure RM 操作人员恢复密钥明文副本。

    -   将生成的密钥文件复制到 USB 驱动器，以便以后上载到 Azure RMS 服务。

    -   对 HSM 进行出厂重置，将工作站擦除干净。

你现在已经完成了自带密钥所需的说明，可以返回到组织执行规划和实现租户密钥的后续步骤。

> [!div class="button"]
[后续步骤 >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Apr16_HO4-->


