---
title: 将 Azure 信息保护标签迁移到 Office 365 安全与合规中心
description: 为支持统一标签的客户端将 Azure 信息保护标签迁移到 Office 365 安全与合规中心。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/28/2018
ms.topic: article
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 64063af186f01a5829b7aa668260928e3b13656d
ms.sourcegitcommit: 304702a3f2f2ab2b32493c4aedeb5ee8424b925c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2018
ms.locfileid: "47415003"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>如何将 Azure 信息保护标签迁移到 Office 365 安全与合规中心

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

> [!IMPORTANT]
> 此功能处于预览状态，并且将租户迁移到新平台也处于预览状态。 迁移不可撤消。 新平台支持统一标签，以便你创建和管理的标签可由多个客户端和服务使用。

如果希望能够在 Office 365 安全与合规中心使用，则迁移标签，可以在其中发布标签，然后由[支持统一标签的客户端](#clients-that-support-unified-labeling)下载。 Azure 信息保护客户端将继续从 Azure 门户下载带有其 Azure 信息保护策略的标签。 

在迁移标签后，然后可以在 Azure 门户或 Office 365 安全与合规中心对其进行更改，相应的客户端将下载同一更改。

## <a name="considerations-for-unified-labels"></a>统一标签注意事项

在迁移标签之前，请确保了解以下更改和注意事项：

- 并非所有客户端目前都支持统一标签。 请确保你拥有[支持的客户端](#clients-that-support-unified-labeling)并准备好在 Azure 门户（适用于不支持统一标签的客户端）和安全与合规中心（适用于支持统一标签的客户端）进行管理。

- 如果你正在定义和配置你想要使用的标签，建议使用 Azure 门户来完成此过程，然后迁移标签。 此策略可以避免在迁移过程中重复标签，然后需要在安全与合规中心进行编辑。

- 不会迁移策略，包括策略设置和谁有权访问策略（作用域内策略）以及所有高级客户端设置。 对于这些不会迁移的更改，需要在迁移标签后在安全与合规中心配置相关选项。
    
    为了获得更一致的用户体验，建议在安全与合规中心的相同范围内发布相同标签。

- 安全与合规中心并不支持已迁移标签中的所有设置。 使用[安全与合规中心不支持的标签设置](#label-settings-that-are-not-supported-in-the-security--compliance-center)部分中的表，以帮助识别这些设置以及是否应在安全与合规中心从发布中排除已迁移的标签。

- 保护模板：
    
    - 使用基于云的密钥和为标签配置的一部分模板也随标签一同迁移。 不迁移其他保护模板。 
    
    - 迁移具有基于云保护设置的标签之后，生成的保护模板范围是在 Azure 门户中定义的范围（或通过使用 ADDRM PowerShell 模块），以及在安全与合规中心定义的范围。 

- 迁移标签时，将看到迁移结果显示标签是否创建、更新，或因重复而重命名：

    - 创建标签时，必须在安全与合规中心发布，以将其提供给应用程序和服务。
    
    - 当重命名标签，必须对其进行编辑，可以在安全与合规中心或 Azure 门户执行此操作。 

- 对于每个标签，Azure 门户仅显示可编辑的标签显示名称。 安全与合规中心显示标签的显示名称和标签名称。 标签名称是在首次创建标签时指定的初始名称，此属性由后端服务用于标识目的。

- 不迁移标签的任何本地化字符串。 必须在安全与合规中心为迁移的标签定义新的本地化字符串。

- 迁移之后，当你在 Azure 门户中编辑标签时，相同的更改将自动反应在安全与合规中心。 但是，当在安全与合规中心编辑已迁移的标签，必须更新 Azure 门户中的标签，以便标签选取更改。 例如，编辑“标签”边栏选项卡上的“添加备注以供管理员使用”框。 

- 仍向租户推出统一标签。 如果尚不支持你的租户，迁移将不会成功，并适当地撤消任何更改。 在支持所有租户之前，必须使用特殊的链接来访问用于迁移租户和标签的选项。 在后面的说明中提供了此链接。

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>安全与合规中心不支持的标签设置

使用下表来标识哪些已迁移标签的配置设置不支持使用这些标签的客户端，以及是否应在安全与合规中心编辑和发布迁移的标签。 如果发布标识为要从发布中排除的标签，则没有标签显示支持统一标签的客户端。

Azure 信息保护客户端可以使用这些标签设置，而不会出现任何问题，因为它们继续从 Azure 门户下载标签。

|标签配置|在安全与合规中心中受支持|不包括安全与合规中心的编辑和发布|
|-------------------|---------------------------------------------|-------------------------|
|启用或禁用状态<br /><br />说明：不会同步到安全与合规中心 |“不适用”|“不适用”|
|标签颜色：从列表中选择或使用 RGB 代码指定<br /><br />说明：安全与合规中心不支持标签颜色 |“不适用”|“不适用”|
|使用预定义模板的基于云的保护或基于 HYOK 的保护 |否|是|
|使用 Word、Excel 和 PowerPoint 中用户定义的权限的基于云的保护 |否|是|
|使用 Outlook for Do Not Forward 中用户定义的权限的基于 HYOK 的保护 |否|是|
|删除保护 |否|是|
|视觉标记（页眉、页脚、水印）：依据 RGB 代码的自定义字体和自定义字体颜色|否|如果使用变量则建议<br /><br />- 在客户端，变量显示为文本而不是显示动态值|
|每个应用的视觉标记|否|如果使用变量则建议<br /><br />- 在客户端，变量显示为文本而不是显示动态值|
|条件和关联设置 <br /><br />说明：包括自动和建议标签及其工具提示|“不适用”|否|


## <a name="to-migrate-azure-information-protection-labels"></a>若要迁移 Azure 信息保护标签

> [!IMPORTANT]
> 在确认可以在 Office 365 安全与合规中心编辑和发布敏感度标签之前，请勿迁移标签。 敏感度标签开始向 Office 365 租户推出，但尚不可供所有租户使用。
> 
> 若要检查：从 Office 365 安全与合规中心，转到“分类” > “标签”，并查看是否有“敏感度”选项卡。如果没有看到此选项卡，则租户尚且没有准备好使用敏感度标签，此时不应迁移 Azure 信息保护标签。

如果已确认租户支持安全与合规中心的敏感度标签，则使用以下说明迁移租户和 Azure 信息保护标签。

1. 通过使用以下链接，打开新的浏览器窗口并登录到 Azure 门户： https://portal.azure.com/?ActivateMigration=true#blade/Microsoft_Azure_InformationProtection/DataClassGroupEditBlade/migrationActivationBlade 

2. 在“Azure 信息保护 - 统一标签”边栏选项卡上，选择“激活”并按照联机说明进行操作。

对于成功迁移的标签，当这些标签在安全与合规中心发布时，它们现在可由[支持统一标签的客户端](#clients-that-support-unified-labeling)使用。


### <a name="clients-that-support-unified-labeling"></a>支持统一标签的客户端

当前支持统一标签的客户端包括：

- 来自 Office 预览体验计划的应用程序。 有关详细信息，请参阅 Office 文档中的[目前功能支持的区域？](https://support.office.com/article/2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US#bkmk_whereavailable)部分。
    
- 来自软件供应商和使用 [MIP SDK](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference) 的开发人员的客户端。


## <a name="next-steps"></a>后续步骤

有关 Office 365 安全与合规中心配置迁移标签的详细信息，请参阅博客文章，[宣布在安全与合规中心推出统一标签管理](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)。