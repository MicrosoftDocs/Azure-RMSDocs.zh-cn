---
title: 教程 - 从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端
description: 从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端的分步操作教程。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/19/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: f988ba63671164463a4ad1b566daab7df123e057
ms.sourcegitcommit: df6ee1aca02e089e3a72006ecf0747f14213979c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "94503632"
---
# <a name="tutorial-migrating-from-the-azure-information-protection-aip-classic-client-to-the-unified-labeling-client"></a>教程：从 Azure 信息保护 (AIP) 经典客户端迁移到统一标记客户端

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明： *[适用于 Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用。
> 
> 在此时间框架内，所有 Azure 信息保护经典客户端客户都可以使用 Microsoft 信息保护统一标记平台转换到 AIP 统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。
>

本教程介绍如何将组织的 Azure 信息保护部署从经典客户端迁移到统一标记客户端。

所需时间：完成迁移所需的时间取决于策略的复杂程度以及使用的 AIP 功能。 在后台迁移时，你可以继续使用经典客户端。

本教程提供了每个步骤的大致说明，然后引用 Microsoft 文档中其他位置的相关部分以了解更多详细信息。

在本教程中，你将：
> [!div class="checklist"]
> * 了解如何规划迁移
> * 将标签迁移到统一标记平台
> * 了解如何在新标记管理中心配置高级设置
> * 将策略复制到统一标记平台
> * 部署统一标记客户端

## <a name="why-migrate-to-the-unified-labeling-platform"></a>为什么要将策略复制到统一标记平台？

迁移到统一标记客户端，不仅能够应对[计划的经典客户端弃用](https://aka.ms/aipclassicsunset)，还能有效地保护整个数字资产中的敏感数据。 迁移后，可将 Microsoft 信息保护 (MIP) 用于 Microsoft 365 云服务、本地、第三方 SaaS 应用程序等。

MIP 支持许多基本信息保护功能的内置标记服务，使你能够仅为内置标记不支持的额外功能保留客户端使用。

- 通过减少部署和维护的额外软件来降低维护成本
- 提高 Office 性能，无需其他加载项
- 使用标记管理中心，在 AIP、Office 365 和 Windows 中简化标记和保护策略管理。 

    受支持的管理中心包括 Microsoft 365 合规中心、Microsoft 365 安全中心或 Microsoft 365 安全与合规中心。

有关详细信息，请参阅[了解统一标记迁移博客](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185)。

## <a name="planning-your-migration"></a>规划迁移

虽然 AIP 经典客户端可用的大多数功能也可用于统一标记客户端，但有些功能尚未完全可用，还有些在统一标记方面配置方式不同。

查看以下文章，了解使用统一标记客户端时使用的信息保护功能有何不同：

- [了解 Microsoft 365 中的内置标记功能](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)
- [比较经典和统一标记客户端的支持](rms-client/use-client.md#compare-the-labeling-clients-for-windows-computers)
- [了解如何管理统一标记管理中心中不支持开箱即用的标签设置](configure-policy-migrate-labels.md#label-settings-that-are-not-supported-in-the-admin-centers)

> [!TIP]
> 如果在影响最终用户行为的客户端之间记录了差异，我们建议你在部署统一标记客户端和发布新策略之前，有效地向用户传达这些更改。

计划迁移并了解将发生的更改后，请继续[将标记迁移到统一标记平台](#migrating-labels-to-the-unified-labeling-platform)。

## <a name="migrating-labels-to-the-unified-labeling-platform"></a>将标签迁移到统一标记平台

规划迁移并考虑如何处理客户端的差异后，即可激活统一标记并迁移标记。

迁移时，可以继续在 Azure 门户中使用 Azure 信息保护区域中的 AIP 经典客户端和策略。 两个客户端可以并行工作，而无需任何其他配置。

1. 以具有以下角色之一的管理员身份，登录到 [Azure 门户](https://portal.azure.com)：

    - **法规管理员**
    - **合规性数据管理员**
    - **安全管理员**
    - **全局管理员**
    

1. 在“Azure 信息保护”区域的左侧“管理”下，选择“统一标记” 。

    在页面顶部，选择 :::image type="icon" source="media/qs-tutor/activate.PNG" border="false":::“激活”以激活统一标记。

    标记将从 Azure 信息保护复制到统一标记平台，现在存储在两个系统中。

    打开标记管理中心，比较显示在此中心和 Azure 信息保护区域中的标记。 这两个列表应相同。 例如，与 Microsoft 365 安全与合规中心进行比较时：

    :::image type="content" source="media/qs-tutor/compare-migrated-labels-small.png" alt-text="比较 Azure 门户和安全与合规中心之间的迁移标签" lightbox="media/qs-tutor/compare-migrated-labels.png":::

    > [!NOTE]
    > 如果需要，请继续使用两个系统中的标签，直到完成迁移。 有关详细信息，请参阅[同步标记编辑](#synchronizing-labeling-edits)。

继续[将策略复制到统一标记平台](#copy-policies-to-the-unified-labeling-platform)。

### <a name="synchronizing-labeling-edits"></a>同步标记编辑

当你将标签迁移到标签管理中心（包括 Microsoft 365 安全中心、Microsoft 365 合规性中心或 Microsoft 365 安全与合规中心）后，继续在 Azure 门户中对迁移后的标签进行的任何编辑都会自动同步到管理中心内的相同标签，以实现统一标签。

但是，对管理中心中的已迁移标签所做的编辑不同步到 Azure 门户。 如果在管理中心进行编辑，并且需要在 Azure 门户中更新它们，请返回到门户以发布更新。

若要在 Azure 门户中发布更新的标签：

1. 在“Azure 信息保护”区域的左侧“管理”下，选择“统一标记” 。

1. 选择 :::image type="icon" source="media/i-publish.PNG" border="false":::“发布”。 

> [!NOTE]
> 仅当你在统一标记平台中对迁移的标记进行了编辑，并且需要这些编辑同步到 Azure 门户时，才需要执行此步骤。 

### <a name="migrating-labels-via-powershell"></a>通过 PowerShell 迁移标签

还可以使用 PowerShell 迁移现有标签，例如对于 GCC High 环境。

使用 [New-Label](/powershell/module/exchange/new-label) cmdlet 迁移现有敏感度标签。

例如，如果你的敏感度标签具有加密功能，你可以使用 New-Label cmdlet，如下所示：

```PowerShell
New-Label -Name 'aipscopetest' -Tooltip 'aipscopetest' -Comment 'admin notes' -DisplayName 'aipscopetest' -Identity 'b342447b-eab9-ea11-8360-001a7dda7113' -EncryptionEnabled $true -EncryptionProtectionType 'template' -EncryptionTemplateId 'a32027d7-ea77-4ba8-b2a9-7101a4e44d89' -EncryptionAipTemplateScopes "['allcompany@labelaction.onmicrosoft.com','admin@labelaction.onmicrosoft.com']"
```

有关在 GCC、GCC-High 和 DoD 环境中工作的详细信息，请参阅 [Azure 信息保护高级政府服务说明](/enterprise-mobility-security/solutions/ems-aip-premium-govt-service-description#label-migration)。 

## <a name="copy-policies-to-the-unified-labeling-platform"></a>将策略复制到统一标记平台

复制你存储在 Azure 门户中并希望在统一标记平台中启用的任何策略。

此功能目前处于预览状态。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。

> [!NOTE]
> 复制策略具有某些限制。 你还可以从头开始，在标记管理中心手动创建策略。 有关详细信息，请参阅 [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)。
> 

若要复制策略： 

1. 请考虑以下项目，并确认此时要复制策略：

    |注意事项  |说明  |
    |---------|---------|
    |复制策略会复制你的所有策略     |     复制策略不支持仅复制特定策略 - 现在要么复制所有策略，要么都不复制。   |
    |复制时会自动发布策略     |  将策略复制到统一标记客户端会自动将其发布到统一标记支持的所有客户端。 <br /><br />   **重要事项：** 如果不想发布策略，请不要复制它们。     |
    |复制时会覆盖具有相同名称的现有策略     |   如果你的管理中心中已有同名策略，则复制策略将覆盖该策略中定义的任何设置。   <br /><br />从 Azure 门户复制的所有策略都通过以下语法命名：`AIP_<policy name>`。    |
    |不会复制某些客户端设置     | 某些客户端设置不会复制到统一标记平台，迁移后必须手动配置。 <br /><br />有关详细信息，请参阅[配置高级标记设置](#configuring-advanced-labeling-settings)|
    | | |

1. 以具有以下角色之一的管理员身份，登录到 [Azure 门户](https://portal.azure.com)：

    - **法规管理员**
    - **合规性数据管理员**
    - **安全管理员**
    - **全局管理员**


1. 在“Azure 信息保护”区域的左侧“管理”下，选择“统一标记” 。

1. 选择 :::image type="icon" source="media/i-copy-policies.PNG" border="false":::“复制策略(预览版)”。 存储在 Azure 门户中的所有策略都会复制到管理中心。

    如果管理中心中已有具有相同名称的任何策略，则 Azure 门户中的设置将覆盖这些策略。

    > [!IMPORTANT]
    > 如果当前使用 Microsoft Cloud App Security 和 Azure 信息保护标签，请验证是否已将带有最小标签集的至少一个策略发布到标记管理中心，即使该策略的适用范围是单个用户。 
    >
    > Microsoft Cloud App Security 需要此策略来标识标记管理中心的所有标签，并在 Microsoft Cloud App Security 门户中显示它们。

现在，你已经迁移了标签和策略，请继续[配置高级标记设置](#configuring-advanced-labeling-settings)，以涵盖未迁移的任何高级配置。

## <a name="configuring-advanced-labeling-settings"></a>配置高级标记设置

如[规划阶段](#planning-your-migration)所述，某些高级标记设置不会自动迁移，必须为统一标记平台重新配置它们。

有关详情，请参阅：

- [在 PowerShell 中配置高级标记设置](#configure-advanced-labeling-settings-in-powershell)
- [在标记管理中心定义标签条件](#define-label-conditions-in-the-labeling-admin-center)

### <a name="configure-advanced-labeling-settings-in-powershell"></a>在 PowerShell 中配置高级标记设置

1. 连接到 Office 365 安全与合规中心 PowerShell 模块。 有关详细信息，请参阅[安全与合规中心 PowerShell 文档](https://docs.microsoft.com/powershell/exchange/connect-to-scc-powershell)。

1. 若要定义高级标签设置，请使用 Set-Label cmdlet，指定 AdvancedSettings 参数、要向其应用设置的标签，以及定义设置的键/值对 。
    
    使用以下语法：

    ```PowerShell
    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{<Key>="<value1>,<value2>"}
    ```

    其中：
    - `<LabelGUIDorName>` 使用标签名称或 GUID 标识标签
    - `<Key>` 是你希望部署到设备的高级设置的键或名称
    - `<Value>` 是要定义的设置值。 用引号括住值，用逗号分隔多个值。 不支持空格。

1. 由配置以下高级设置开始：

    - [指定标签的颜色](rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)
    - [为父标签指定默认子标签](rms-client/clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [将标签配置为在 Outlook 中应用 S/MIME 保护](rms-client/clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [使用自定义属性定义标签](rms-client/clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions) 
    - [定义标签翻译](https://docs.microsoft.com/powershell/module/exchange/set-label)。 

    有关可用高级配置的详细信息，请参阅[管理员指南：Azure 信息保护统一标记客户端的自定义配置](rms-client/clientv2-admin-guide-customizations.md)。

> [!NOTE]
> 若要利用为统一标记平台定义的设置，最终用户必须在其计算机上安装统一标记客户端。 
>
> 这些高级设置不适用于仅具有 Office 365 提供的内置标记的用户。
> 

### <a name="define-label-conditions-in-the-labeling-admin-center"></a>在标记管理中心定义标签条件

与 Azure 门户中创建的对应条件相比，统一标记条件提供了更多灵活性和更高的准确性。 

若要利用统一标记条件功能，请手动在标记管理中心创建标记条件，包括：

- Microsoft 365 合规中心
- Microsoft 365 安全中心
- Microsoft 365 安全与合规中心

有关详细信息，请参阅 Microsoft 365 文档中的[敏感度标签能执行的操作](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do)。

> [!TIP]
> 如果你有任何用于 Office 365 DLP 或 Microsoft Cloud App Security 的自定义敏感信息类型，请将它们按原样应用于统一标记。 有关详细信息，请参阅 [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)。
>  

## <a name="deploy-a-unified-labeling-client"></a>部署统一标记客户端

部署支持跨用户计算机的统一标记的客户端，以确保他们能够使用统一标记策略和标签。 

用户必须具有可连接到标记管理中心并拉取统一标记策略的受支持的客户端。 

有关详情，请参阅：
- [非 Windows 平台](#non-windows-platforms)
- [Windows 平台](#windows-platforms)
- [对经典客户端最终用户而言有哪些变化？](#what-changes-for-classic-client-end-users)

### <a name="non-windows-platforms"></a>非 Windows 平台

对于非 Windows 平台上的用户，统一标记功能直接集成到 Office 客户端中，并可直接使用你发布的任何标签。 

具有集成的统一标记功能的 Office 客户端包括： 

- 适用于 macOS 的 Office 客户端
- Office 网页版（预览版）
- Outlook Web App
- Outlook 移动版

有关这些平台中的统一标记的详细信息，请参阅 Microsoft 支持站点上的[将敏感度标签应用于 Office 中的文件和电子邮件](https://support.microsoft.com/office/apply-sensitivity-labels-to-your-files-and-email-in-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)。 

### <a name="windows-platforms"></a>Windows 平台

对于具有 Microsoft 365 企业应用版的 Windows 计算机，请使用 Office 版本 1910 及更高版本中提供的内置标记支持，或安装 Azure 信息保护统一标记客户端，以将 AIP 功能扩展到文件资源管理器或 PowerShell。

有关详情，请参阅： 

- [比较 Windows 计算机的标签客户端](rms-client/use-client.md#compare-the-labeling-clients-for-windows-computers)
- [快速入门：部署 Azure 信息保护 (AIP) 统一标记客户端](quickstart-deploy-client.md)

可以从 [Microsoft 下载中心](https://aka.ms/aipclient)下载 Azure 信息保护统一标记客户端。 

请确保使用 AzInfoProtection_UL 文件来部署客户端。 如果当前计算机上安装了经典客户端，则安装统一标记客户端将执行就地升级。

> [!NOTE]
> 在确定何时使用内置标记以及何时使用统一标记客户端时，请考虑组织当前所需的 AIP 功能。 
>> 

### <a name="what-changes-for-classic-client-end-users"></a>对经典客户端最终用户而言有哪些变化？

对使用 Azure 信息保护经典客户端的最终用户而言，主要、最明显的区别在于，Office 应用中的“保护”按钮已替换为“敏感度”按钮 。 

当你利用敏感度标签和统一标记支持的其他功能后，最终用户也将在 Office 应用中看到这些更改。

例如：

- Windows AIP 经典客户端

    :::image type="content" source="media/infoprotect-protectbutton-pulldown.png" alt-text="经典客户端中的保护按钮":::

- Windows AIP 统一标记客户端

    :::image type="content" source="media/qs-tutor/sample-aip-client-office.PNG" alt-text="Microsoft Office 中统一标记客户端的示例按钮":::

> [!TIP]
> 如果你已发布标签，并且具有内置支持的客户端未显示“敏感度”按钮，请根据需要查看相关故障排除指南。
>
 
## <a name="next-steps"></a>后续步骤

根据需要迁移标签、策略和已部署的客户端后，请继续[仅在标记管理中心（包括 Microsoft 365 合规性中心、Microsoft 365 安全中心或 Microsoft 365 安全与合规中心）中管理标签和标记策略](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)。

使用统一标记平台，你只需返回到 Azure 门户中的 Azure 信息保护区域，以：

- [使用 AIP 扫描程序](deploy-aip-scanner.md)
- [使用 AIP 分析监视标记活动](reports-aip.md)

我们建议最终用户利用适用于 Web、Mac、iOS 和 Android 的最新 Office 应用以及 Microsoft 365 企业应用版中的内置标记功能。 

若要使用内置标记不支持的其他 AIP 功能，建议使用适用于 Windows 的最新统一标记客户端。
