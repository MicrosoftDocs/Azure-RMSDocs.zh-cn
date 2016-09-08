---
title: "管理员如何控制为个人 RMS 创建的帐户 | Azure RMS"
description: "如果你不希望将组织的个人 RMS 订阅转换为付费订阅，你仍然可以通过下列方式，控制为组织创建的 Azure 目录中的用户帐户。"
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a83880d0-f0f9-4a32-9e00-2f6635d7cc8d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: a900622fcce4a0a1431f47647709584e404a7f8c


---



# 管理员如何才能控制为个人 RMS 创建的帐户

>*适用于：Azure Rights Management*


如果你不希望将组织的个人 RMS 订阅转换为付费订阅，你仍然可以通过下列方式，控制为组织创建的 Azure 目录中的用户帐户：

-   实现 Azure Active Directory 和 Active Directory 域服务基础结构的目录集成解决方案。 你可以同步帐户和密码，使得用户无需创建新帐户即可使用权限管理，你的本地密码策略将应用于新的 Azure 用户帐户。 你还可以同步密码，使得用户无需为了使用权限管理而记忆不同密码。

-   你可以阻止用户注册使用 Azure Rights Management 和个人 RMS 订阅。 大多数情况下，这种做法没有什么好处，因为用户在不受保护的情况下共享文件可能会让公司承担风险，用户还可能会使用其他文件保护机制，导致 IT 部门不能访问数据。 但是，如果你希望阻止用户注册使用个人 RMS，请在取得组织的 Azure 目录的所有权后执行以下操作之一：

    -   阻止所有用户注册包括个人 RMS 的自助订阅。  目前，你无法通过服务设置此内容；该设置适用于所有使用自助过程的 Azure 订阅。 为此，请使用 Azure Active Directory 的 Windows PowerShell 模块中的 [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet，将 **AllowAdHocSubscriptions** 参数设置为 false。 例如：**Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   阻止用户在 Azure 中创建新帐户，这意味着仅已经具有 Azure 帐户的用户可以注册包括个人 RMS 的自助订阅。  为此，请使用 Azure Active Directory 的 Windows PowerShell 模块中的 [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) cmdlet，将 **AllowEmailVerifiedUsers** 参数设置为 false。 例如：**Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   将 Active Directory 域服务基础结构与 Azure Active Directory 同步。 此操作可以在用户注册自助订阅（如个人 RMS）阻止创建新帐户，并且你还可以删除或禁用以前在 Azure 目录中创建的帐户。

若要控制 Azure 目录中的用户帐户，或者阻止用户注册个人 RMS，你必须具有 Azure 订阅并拥有该目录。 如果没有 Azure 订阅，你可以免费获取一个订阅。 如果在自助过程期间自动为你创建了目录，请获取用于创建该目录的域的所有权。 如果你在 Azure 中已经拥有目录，但用户指定了在组织中使用的新的域，请将该域合并到现有目录中。 有关详细信息，请参阅 [什么是 Azure 自助注册？](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)中的说明。


## 后续步骤

如果用户（而不是管理员）可以在个人 RMS 的 Azure Active Directory 中创建其帐户，则如何发现用户已进行了此操作？  请参阅[如何发现用户已注册了个人 RMS](rms-for-individuals-identify-sign-up.md)。



<!--HONumber=Aug16_HO4-->


