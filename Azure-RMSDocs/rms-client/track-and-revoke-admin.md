---
title: 跟踪和撤销访问权限-Azure 信息保护
description: 介绍管理员如何跟踪受保护文档的文档访问，以及如何在需要时撤销访问权限。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/07/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 7b60438ad3d1e8a971c58a7f29b2f8b41dd84c91
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98163733"
---
# <a name="administrator-guide-track-and-revoke-document-access-with-azure-information-protection-public-preview"></a>管理员指南：使用 Azure 信息保护跟踪和撤消文档访问 (公开预览版) 

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***相关的**： [仅限 AIP 统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [管理员指南：配置和使用适用于 AIP 的文档跟踪使用经典客户端](client-admin-guide-document-tracking.md)。 *

如果已升级到 [版本 2.9.111.0](unifiedlabelingclient-version-release-history.md#version-291110) 或更高版本，则在下次通过 AIP 统一标签客户端打开时，将自动注册尚未注册跟踪的所有受保护文档。 支持跟踪和撤消受保护的文档，即使它们未标记。

为跟踪注册文档可使 [Microsoft 365 全局管理员](/microsoft-365/admin/add-users/about-admin-roles#commonly-used-microsoft-365-admin-center-roles) 跟踪访问详细信息，包括成功的访问事件和拒绝的尝试，并根据需要撤消访问权限。 

统一标签客户端的跟踪和撤销功能目前处于预览阶段。 [Azure 预览版补充条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)包含适用于 beta 版、预览版或其他尚未正式发布的 Azure 功能的其他法律条款。 

## <a name="track-document-access"></a>跟踪文档访问

全局管理员可以通过 PowerShell 使用在注册过程中为受保护文档生成的 **id 为** 跟踪受保护文档的访问权限。

**查看文档访问详细信息**：

使用以下 cmdlet 查找要跟踪的文档的详细信息：

1. 查找要跟踪的文档的 **id 为** 值。
    
    使用 [AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) ，以使用应用了保护的用户的文件名和/或电子邮件地址搜索文档。
    
    例如，
        
    ```PowerShell
    Get-AipServiceDocumentLog -ContentName "test.docx" -Owner “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```
 
    此命令返回为跟踪注册的所有匹配、受保护的文档的 **id 为** 。

    > [!NOTE]
    > 当在安装了统一标签客户端的计算机上首次打开受保护的文档时，这些文档将被注册以供跟踪。 如果此命令不返回受保护文件的 Id 为，请在安装了统一标签客户端的计算机上打开它以注册要跟踪的文档。

1. 将 [AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog) cmdlet 与文档的 **id 为** 一起使用，以返回跟踪数据。

    例如：
    
    ```PowerShell
    Get-AipServiceTrackingLog -ContentId c03bf90c-6e40-4f3f-9ba0-2bcd77524b87
    ```

    将返回跟踪数据，其中包括尝试访问的用户的电子邮件、是否授予或拒绝访问、尝试的时间和日期以及访问尝试产生的域和位置。

## <a name="revoke-document-access-from-powershell"></a>撤消 PowerShell 的文档访问

全局管理员可以使用 [AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) cmdlet 撤消对其本地内容共享中存储的任何受保护文档的访问权限。

1. 查找要撤消其访问权限的文档的 **id 为** 值。
    
    使用 [AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) ，以使用应用了保护的用户的文件名和/或电子邮件地址搜索文档。
    
    例如：
        
    ```PowerShell
    Get-AipServiceDocumentLog -ContentName "test.docx" -Owner “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```

    返回的数据包含文档的 Id 为值。

    > [!TIP]
    > 只有已受保护且已注册跟踪的文档具有 **id 为** 值。 
    >
    > 如果文档没有 **id 为**，请在安装了统一标签客户端的计算机上打开它以注册要跟踪的文件。

1. 将 [AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) 与文档的 id 为配合使用可撤销访问权限。

    例如：

    ```PowerShell
    Set-AipServiceDocumentRevoked -ContentId 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
    ```

> [!NOTE]
> 如果允许 [脱机访问](/microsoft-365/compliance/encryption-sensitivity-labels#assign-permissions-now) ，用户可以继续访问已撤消的文档，直到脱机策略期限过期。 
> 

> [!TIP]
> 用户还可以从其 Office 应用中的 " **敏感度** " 菜单直接对其应用保护的任何文档撤消访问权限。 有关详细信息，请参阅 [用户指南：撤消使用 Azure 信息保护的文档访问](revoke-access-user.md)

### <a name="un-revoke-access"></a>撤消访问权限

如果你意外地撤销了对特定文档的访问权限，请使用 **id 为** Cmdlet 和 [AipServiceDocumentRevoke](/powershell/module/aipservice/clear-aipservicedocumentrevoke) cmdlet 来取消对该访问的访问。 

例如：

```PowerShell
Clear-AipServiceDocumentRevoke -ContentId   0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
```

文档访问权限被授予在 **IssuerName** 参数中定义的用户。

## <a name="turn-off-track-and-revoke-features-for-your-tenant"></a>为租户禁用跟踪和撤消功能

如果需要为你的租户关闭 "跟踪" 和 "撤消" 功能，如组织或区域中的隐私要求，请执行以下两个步骤：

1. 运行 [AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) cmdlet。

1. 将 [EnableTrackAndRevoke](clientv2-admin-guide-customizations.md#turn-off-document-tracking-features-public-preview) advanced client 设置设置为 **false**。 

为租户禁用文档跟踪和撤消访问的选项：

- 打开包含 AIP 统一标签客户端的受保护文档时，不再注册要跟踪和撤消的文档。
- 打开已注册的受保护文档时，不会存储访问日志。 在关闭这些功能之前存储的访问日志仍可用。 
- 管理员将无法通过 PowerShell 跟踪或撤销访问权限，最终用户将不再在其 Office 应用程序中看到 " [**撤消**](revoke-access-user.md#revoke-access-from-microsoft-office-apps) " 菜单选项。

> [!NOTE]
> 若要启用跟踪和撤消，请将 [EnableTrackAndRevoke](clientv2-admin-guide-customizations.md#turn-off-document-tracking-features-public-preview) 设置为 **true**，并运行 [AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature) cmdlet。
>
## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅：

- [AIP 统一标签客户端用户指南](clientv2-user-guide.md)
- [AIP 统一标签客户端管理员指南](clientv2-admin-guide.md)
- [跟踪和撤销功能的已知问题](../known-issues.md#known-issues-for-track-and-revoke-features-public-preview)
