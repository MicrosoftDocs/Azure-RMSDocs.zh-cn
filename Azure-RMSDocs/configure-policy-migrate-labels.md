---
title: 将 Azure 信息保护标签迁移到 Office 365 安全与合规中心 - AIP
description: 为支持统一标签的客户端将 Azure 信息保护标签迁移到 Office 365 安全与合规中心。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/17/20198
ms.topic: article
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 221b503fa3621e51c4822a6ad5a6d08fae4f1bad
ms.sourcegitcommit: 8dec864bf25c7da62b9e0f628f1bf673c81c15ae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2019
ms.locfileid: "54356005"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>如何将 Azure 信息保护标签迁移到 Office 365 安全与合规中心

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

> [!IMPORTANT]
> 此功能处于预览状态，并且将租户迁移到新平台也处于预览状态。 迁移不可撤消。 新平台支持统一标签，以便你创建和管理的标签可由多个客户端和服务使用。

如果希望能够在 Office 365 安全与合规中心使用，则迁移标签，可以在其中发布标签，然后由[支持统一标签的客户端](#clients-that-support-unified-labeling)下载。 Azure 信息保护客户端将继续从 Azure 门户下载带有其 Azure 信息保护策略的标签。 

在迁移标签后，然后可以在 Azure 门户或 Office 365 安全与合规中心对其进行更改，相应的客户端将下载同一更改。

### <a name="important-information-about-administrative-roles"></a>有关管理角色的重要信息

统一标记平台不支持安全管理员和信息保护管理员的 [Azure AD 角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)。 如果在组织中使用了这些管理角色，则在迁移标记之前，请将具有这些角色的用户添加到 Office 365 安全与合规中心的合规性管理员或组织管理角色组。 或者，可以为这些用户创建新角色组并将保留管理或组织配置角色添加到此组。 有关说明，请参阅[向用户授予对 Office 365 安全与合规中心的访问权限](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center)。

如果未使用其中一个配置向这些用户授予对安全与合规中心的访问权限，则在迁移标记后将无法访问 Azure 门户中的标记和策略。

迁移标记后，租户的全局管理员可以继续管理 Azure 门户和安全与合规中心中的标记和策略。


## <a name="considerations-for-unified-labels"></a>统一标签注意事项

在迁移标签之前，请确保了解以下更改和注意事项：

- 并非所有客户端目前都支持统一标签。 请确保你拥有[支持的客户端](#clients-that-support-unified-labeling)并准备好在 Azure 门户（适用于不支持统一标签的客户端）和安全与合规中心（适用于支持统一标签的客户端）进行管理。

- 如果你正在定义和配置你想要使用的标签，建议使用 Azure 门户来完成此过程，然后迁移标签。 此策略可以避免在迁移过程中重复标签，然后需要在安全与合规中心进行编辑。

- 不会迁移策略，包括策略设置和谁有权访问策略（作用域内策略）以及所有高级客户端设置。 对于这些不会迁移的更改，需要在迁移标签后在安全与合规中心配置相关选项。
    
    为了获得更一致的用户体验，建议在安全与合规中心的相同范围内发布相同标签。

- 安全与合规中心并不支持已迁移标签中的所有设置。 使用[安全与合规中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-security--compliance-center)部分中的表，来帮助识别安全与合规中心不支持的设置。

- 保护模板：
    
    - 使用基于云的密钥和为标签配置的一部分模板也随标签一同迁移。 不迁移其他保护模板。 
    
    - 迁移具有基于云保护设置的标记之后，生成的保护模板范围是在 Azure 门户中定义的范围（或通过使用 AADRM PowerShell 模块），以及在安全与合规中心定义的范围。 

- 迁移标签时，将看到迁移结果显示标签是否创建、更新，或因重复而重命名：

    - 创建标签时，必须在安全与合规中心发布，以将其提供给应用程序和服务。
    
    - 当重命名标签，必须对其进行编辑，可以在安全与合规中心或 Azure 门户执行此操作。 

- 对于每个标签，Azure 门户仅显示可编辑的标签显示名称。 安全与合规中心显示标签的显示名称和标签名称。 标签名称是在首次创建标签时指定的初始名称，此属性由后端服务用于标识目的。

- 不迁移标签的任何本地化字符串。 必须在安全与合规中心为迁移的标签定义新的本地化字符串。

- 迁移之后，当你在 Azure 门户中编辑标签时，相同的更改将自动反应在安全与合规中心。 但是，当在安全与合规中心编辑已迁移的标签，必须返回到 Azure 门户的“Azure 信息保护 - 统一标记”边栏选项卡，并选择“发布”。 Azure 信息保护客户端需要通过此附加操作来获取标签更改。

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>安全与合规中心不支持的标签设置

使用下表来识别迁移的标签的哪些配置设置不受统一标记客户端的支持，或受到有限的支持。 为避免混淆，建议不要配置对统一标记客户端无效的设置。

Azure 信息保护客户端可以使用这些标签设置，而不会出现任何问题，因为它们继续从 Azure 门户下载标签。

|标签配置|受统一标记客户端的支持|不包括安全与合规中心的编辑|
|-------------------|---------------------------------------------|-------------------------|
|启用或禁用状态<br /><br />注意：不会同步到安全与合规中心 |“不适用”|“不适用”|
|标签颜色：从列表中选择或使用 RGB 代码指定<br /><br />注意：安全与合规中心不支持标签颜色 |“不适用”|“不适用”|
|使用预定义模板的基于云的保护或基于 HYOK 的保护 |否|是|
|使用 Word、Excel 和 PowerPoint 中用户定义的权限的基于云的保护 |否|是|
|使用 Outlook for Do Not Forward 中用户定义的权限的基于 HYOK 的保护 |否|是|
|删除保护 |否|是|
|视觉标记（页眉、页脚、水印）：由 RGB 代码指定的自定义字体和字体颜色|否|如果使用变量则建议<br /><br />- 在客户端，变量显示为文本而不是显示动态值|
|每个应用的视觉标记|否|如果使用变量则建议<br /><br />- 在客户端，变量显示为文本而不是显示动态值|
|条件和关联设置 <br /><br />注意：包括自动和建议标签及其工具提示|“不适用”|否|


## <a name="to-migrate-azure-information-protection-labels"></a>若要迁移 Azure 信息保护标签

请使用以下说明迁移租户和 Azure 信息保护标签，来使用新的统一标记存储。

你必须是全局管理员才能迁移标记。

1. 如果尚未执行此操作，请打开新的浏览器窗口，并[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)。 然后导航到“Azure 信息保护”边栏选项卡。
    
    例如，在中心菜单上单击“所有服务”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

2. 从“管理”菜单选项，选择“统一标记(预览)”。

3. 在“Azure 信息保护 - 统一标签”边栏选项卡上，选择“激活”并按照联机说明进行操作。

成功迁移的标签现在可被[支持统一标签的客户端](#clients-that-support-unified-labeling)使用。 但必须先在安全与合规中心发布这些标签。

> [!IMPORTANT]
> 在 Azure 信息保护客户端的 Azure 门户外部编辑标签时，请返回该“Azure 信息保护 - 统一标记”边栏选项卡，并选择“发布”。

### <a name="clients-that-support-unified-labeling"></a>支持统一标签的客户端

当前支持统一标签的客户端包括：

- [适用于 Windows 的 Azure 信息保护统一标记客户端](./rms-client/unifiedlabelingclient-version-release-history.md) - 预览版

- 来自 Office 预览体验计划的应用程序。 有关详细信息，请参阅 Office 文档中的[目前功能支持的区域？](https://support.office.com/article/2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US#bkmk_whereavailable)部分。
    
- 来自软件供应商和使用 [MIP SDK](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference) 的开发人员的客户端。


## <a name="next-steps"></a>后续步骤

有关现可在 Office 365 安全与合规中心中配置和发布的已迁移标记的详细信息，请参阅[敏感度标记概述](/Office365/SecurityCompliance/sensitivity-labels)。

阅读博客通告文章：[宣布推出安全与合规中心的统一标记管理](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)。