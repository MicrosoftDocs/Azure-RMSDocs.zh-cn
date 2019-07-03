---
title: Microsoft 托管 - AIP 租户密钥生命周期操作
description: 当 Microsoft 管理 Azure 信息保护租户密钥（默认）时生命周期操作的相关信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: bd7701e9b90f2ebd681dad4516c17d74c000f611
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521920"
---
# <a name="microsoft-managed-tenant-key-life-cycle-operations"></a>Microsoft 托管：租户密钥生命周期操作

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

如果由 Microsoft 管理 Azure 信息保护的租户密钥（默认），请阅读以下部分，获取与此拓扑相关的生命周期操作的详细信息。

## <a name="revoke-your-tenant-key"></a>撤消你的租户密钥
取消 Azure 信息保护订阅时，Azure 信息保护会停止使用租户密钥，用户无需执行任何操作。

## <a name="rekey-your-tenant-key"></a>重新生成租户密钥
重新生成密钥也称为滚动密钥。 执行此操作时，Azure 信息保护会停止使用现有租户密钥保护文档和电子邮件，而开始使用其他密钥。 策略和模板将立即进行重新签名，但对于使用 Azure 信息保护的现有客户端和服务，此转换将逐渐完成。 因此在一段时间内，有些新内容继续使用旧租户密钥进行保护。

要重新生成密钥，必须配置租户密钥对象并指定要使用的备用密钥。 然后，以前使用的密钥将自动为 Azure 信息保护 标记为“已存档”。 此配置可确保通过使用此密钥进行保护的内容仍可访问。

可能需要重新生成 Azure 信息保护密钥的情况示例：

- 使用加密模式 1 密钥从 Active Directory Rights Management Services (AD RMS) 迁移。 迁移完成后，想要改为使用加密模式 2 密钥。

- 你的公司拆分为两家或更多公司。 在重新生成租户密钥时，新公司将无法访问员工发布的新内容。 如果有旧租户密钥的副本，他们可以访问旧内容。

- 想从一个密钥管理拓扑移动到另一个拓扑。

- 你认为租户密钥的主控副本已泄露。

要重新生成密钥，可选择其他 Microsoft 托管密钥作为租户密钥，但不能创建新的 Microsoft 托管密钥。 要创新新密钥，必须将密钥拓扑更改为客户托管 (BYOK)。

如果从 Active Directory Rights Management Services (AD RMS) 进行迁移，并且为 Azure 信息保护选择 Microsoft 托管密钥拓扑，那么将具有多个 Microsoft 托管密钥。 在此方案中，租户具有至少 2 个 Microsoft 托管密钥。 这一个密钥或多个密钥是从 AD RMS 导出的密钥。 还将拥有为 Azure 信息保护租户自动创建的默认密钥。

若要选择不同的密钥为 Azure 信息保护的活动租户密钥，请使用[集 AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) AIPService 模块中的 cmdlet。 若要帮助你确定要使用哪个密钥，请使用[Get AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) cmdlet。 通过运行以下命令，可以确定为 Azure 信息保护租户自动创建的默认密钥：

    (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1

要将密钥拓扑更改为客户托管 (BYOK)，请参阅[为 Azure 信息保护租户密钥实现 BYOK](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)。

## <a name="backup-and-recover-your-tenant-key"></a>备份和恢复你的租户密钥
Microsoft 负责备份你的租户密钥，无需你进行任何操作。

## <a name="export-your-tenant-key"></a>导出你的租户密钥
可以按照以下 3 个步骤的说明，导出 Azure 信息保护配置和租户密钥：

### <a name="step-1-initiate-export"></a>步骤 1：启动导出

- 请[与 Microsoft 支持部门联系](information-support.md#to-contact-microsoft-support)，以打开**带有 Azure 信息保护密钥导出请求的 Azure 信息保护支持案例**。 必须证明你是 Azure 信息保护租户的管理员，并且了解需要几天时间才能确认此过程。 收取标准支持费用；导出租户密钥并不是免费支持服务。

### <a name="step-2-wait-for-verification"></a>步骤 2：等待验证

- Microsoft 将验证发放 Azure 信息保护租户密钥的请求是否合法。 此过程最多可能需要三周时间。

### <a name="step-3-receive-key-instructions-from-css"></a>步骤 3：接收来自 CSS 的密钥说明

- Microsoft 客户支持服务 (CSS) 将 Azure 信息保护配置和在一个受密码保护的文件中加密的租户密钥发送给用户。 此文件的文件扩展名为 .tpd  。 执行此操作时，CSS 首先通过电子邮件向你（即启动导出的人员）发送一个工具。 你必须从命令提示符处运行该工具，如下所示：

    ```
    AadrmTpd.exe -createkey
    ```
    这样可以生成 RSA 密钥对，并将公有部分和私有部分保存为当前文件夹中的文件。 例如：PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt 和 PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt   。

    回复来自 CSS 的电子邮件，附加名称以 **PublicKey** 开头的文件。 CSS 随后向你发送一个作为 .xml 文件的 TPD 文件，该文件使用你的 RSA 密钥进行加密。 将此文件复制到与你最初运行 AadrmTpd 工具时的相同文件夹，并使用以 **PrivateKey** 开头的文件和来自 CSS 的文件再次运行该工具。 例如：

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    此命令的输出应为两个文件：一个文件包含受密码保护的 TPD 的纯文本密码，另一个文件则是受密码保护的 TPD 本身。 这些文件具有新的 GUID，例如：
     
  - Password-5E4C2018-8C8C-4548-8705-E3218AA1544E.txt

  - ExportedTPD-5E4C2018-8C8C-4548-8705-E3218AA1544E.xml

    备份这些文件并将其安全存储，以确保用户能够继续解密使用此租户密钥保护的内容。 此外，如果你要迁移到 AD RMS，则可将此 TPD 文件（以 **ExportedTDP** 开头的文件）导入到 AD RMS 服务器。

### <a name="step-4-ongoing-protect-your-tenant-key"></a>步骤 4:正在进行：保护你的租户密钥

在收到你的租户密钥后，对其进行良好的保护，因为如果有人得到了它，他们将可以解密由该密钥保护的所有文档。

如果导出租户密钥的原因是不再需要使用 Azure 信息保护，最佳做法是立即从 Azure 信息保护租户中停用 Azure Rights Management 服务。 不要拖延到收到租户密钥后再执行此操作，因为此预防措施可以帮助用户将不该得到租户密钥的人得到它后导致的后果降至最低。 相关说明请参阅[解除 Azure Rights Management 授权和停用 Azure Rights Management](decommission-deactivate.md)。

## <a name="respond-to-a-breach"></a>对违规行为做出响应
如果没有违规响应流程，无论如何强大的安全系统都是不完整的。 你的租户密钥可能泄漏或失窃。 即便它得到了很好的保护，在当前这代密钥技术或当前的密钥长度和算法方面也可以找到一些漏洞。

Microsoft 拥有一个专业团队，负责响应其产品和服务中的安全事件。 当收到某个事件的可信报告时，该团队将参与调查事件的范围、根本原因和缓解办法。 如果该事件影响到资产，Microsoft 则将使用在订阅时提供的电子邮件地址，通过电子邮件通知 Azure 信息保护租户管理员。

如果你发现了安全违规行为，则你或 Microsoft 能够采取的最佳行动取决于安全违规的范围；Microsoft 将与你共同完成这个过程。 下表显示了一些典型情况以及可能的响应，但具体的响应要取决于在调查过程中揭示的所有信息。

|事件描述|可能的响应|
|------------------------|-------------------|
|你的租户密钥泄露。|重新生成租户密钥。 请参阅本文中的[重新生成租户密钥](#rekey-your-tenant-key)部分。|
|未经授权的个人或恶意软件获取了使用你的租户密钥的权限，但密钥本身并未泄露。|重新生成租户密钥在这种情况下并不奏效，需要进行根源分析。 如果进程或软件 Bug 是导致未经授权的个人获得访问权限的原因，则必须解决这一问题。|
|在 RSA 算法、密钥长度或暴力攻击方面发现的漏洞可能被利用。|Microsoft 必须更新 Azure 信息保护以支持新的算法和具有弹性的更长密钥长度，并指示所有客户重新生成他们的租户密钥。|


