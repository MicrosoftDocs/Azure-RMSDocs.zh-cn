---
title: 准备用户和组以便使用 Azure 信息保护
description: 查看你是否拥有可以开始对组织的文档和电子邮件进行分类、标记和保护所需的用户和组帐户。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e14844a5bd1b0ace4085eaaa9c15be6b3c814146
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39473740"
---
# <a name="preparing-users-and-groups-for-azure-information-protection"></a>准备用户和组以便使用 Azure 信息保护

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

在为组织部署 Azure 信息保护之前，请确保你的组织租户在 Azure AD 中具有用户和组帐户。

创建这些用户和组的帐户有多种方法，其中包括：

- 在 Office 365 管理中心创建用户，在 Exchange Online 管理中心创建组。

- 在 Azure 门户中创建用户和组。

- 使用 Azure AD PowerShell 和 Exchange Online cmdlet 创建用户和组。

- 在本地 Active Directory 中创建用户和组，并将其同步到 Azure AD。

- 在其他目录中创建用户和组，并将它们同步到 Azure AD。

当你使用此列表中的前三种方法创建用户和组时，它们将在 Azure AD 中自动创建，Azure 信息保护可以直接使用这些帐户。 然而，许多企业网络使用本地目录来创建和管理用户和组。 Azure 信息保护不能直接使用这些帐户；用户必须将它们同步到 Azure AD。

## <a name="how-users-and-groups-are-used-by-azure-information-protection"></a>Azure 信息保护如何使用用户和组

Azure 信息保护使用用户和组的方式有三种：

配置 Azure 信息保护策略时，**用于将标签分配给用户**，以便将标签应用于文档和电子邮件。 只有管理员可以选择这些用户和组：

- 默认的 Azure 信息保护策略将自动分配给租户的 Azure AD 中的所有用户。 但是，你也可以使用作用域策略为指定用户或组分配其他标签。     

在使用 Azure 权限管理服务保护文档和电子邮件时，**用于分配使用权限和访问控制权限**。 管理员和用户均可选择这些用户和组：

- 使用权限可决定用户是否能够打开文档或电子邮件以及如何使用它们。 例如，用户是只能阅读，可以阅读并打印，还是可以阅读并编辑。 

- 访问控制权限包括到期日期以及是否需要连接到 Internet 进行访问。 

**用于配置 Azure 权限管理服务**以支持特定方案，因此只有管理员可以选择这些组。 示例包括配置下列各项：

- 超级用户，以便指定的服务或人员可以打开加密的内容（如果电子数据展示或数据恢复需要）。

- Azure 权限管理服务的委派管理。

- 支持分阶段部署的加入控制。

## <a name="azure-information-protection-requirements-for-user-accounts"></a>用户帐户 Azure 信息保护要求

用于分配标签：

- Azure AD 中的所有用户帐户都可用于配置为用户分配其他标签的作用域策略。

用于分配使用权限和访问控制，以及配置 Azure 权限管理服务：

- 若要授权用户，请使用 Azure AD 中的两个属性：**proxyAddresses** 和 **userPrincipalName**。

- **Azure AD proxyAddresses** 属性存储帐户的所有电子邮件地址，并能以不同的方式填充。 例如，Office 365 中具有 Exchange Online 邮箱的用户自动具有存储在此属性中的电子邮件地址。 如果你为 Office 365 用户分配备用电子邮件地址，那么该地址也会保存在此属性中。 它也可以由从本地帐户同步的电子邮件地址填充。 
    
    如果已将域添加到你的租户（“已验证的域”），Azure 信息保护可以使用此 Azure AD proxyAddresses 属性中的任何值。 有关验证域的详细信息，请参阅：
    
    - 对于 Azure AD：[将自定义域名添加到 Azure Active Directory](/active-directory/active-directory-add-domain)

    - 对于 office 365：[将域和用户添加到 Office 365](https://go.microsoft.com/fwlinkid/?linkid=847121)

- 仅当租户中的帐户在 Azure AD proxyAddresses 属性中没有值时，才会使用 **Azure AD userPrincipalName** 属性。 例如，你可以在 Azure 门户中创建用户，或者创建没有邮箱的 Office 365 用户。

### <a name="assigning-usage-rights-and-access-controls-to-external-users"></a>向外部用户分配使用权限和访问控制权限

除了为你的租户中的用户使用 Azure AD proxyAddresses 和 Azure AD userPrincipalName 之外，Azure 信息保护还以同样的方式使用这些属性来授权其他租户的用户。

其他授权方法：

- 对于 Azure AD 中不存在的电子邮件地址，Azure 信息保护可以在使用 Microsoft 帐户对这些电子邮件地址进行 身份验证后对它们进行授权。 但是，并非所有应用程序都可以在使用 Microsoft 帐户进行身份验证时打开受保护的内容。 [详细信息](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

- 使用具有新功能的 Office 365 邮件加密向 Azure AD 中没有帐户的用户发送电子邮件时，会通过社交标识提供者使用联合身份验证或使用一次性密码对此用户进行身份验证。 然后使用受保护电子邮件中指定的电子邮件地址向此用户授权。

## <a name="azure-information-protection-requirements-for-group-accounts"></a>组帐户 Azure 信息保护要求

用于分配标签：

- 若要配置将其他标签分配给组成员的作用域策略，可以使用 Azure AD 中的任何类型的组，但需要具有包含用户租户的已验证域的电子邮件地址。 具有电子邮件地址的组通常称为启用邮件的组。
    
    例如，你可以使用启用邮件的安全组、通讯组（可以是静态或动态）和 Office 365 组。 不能使用安全组（动态或静态），因为该组类型没有电子邮件地址。

对于分配使用权限和访问控制权限：

- 可以使用 Azure AD 中的任何类型的组，但需要具有包含用户租户的已验证域的电子邮件地址。 具有电子邮件地址的组通常称为启用邮件的组。 

对于配置 Azure 权限管理服务：

- 可以使用 Azure AD 中的任何类型的组，其中包含租户中已验证域的电子邮件地址，但有一个例外。 即当你配置加入控制来使用某个组时，该组必须是租户的 Azure AD 中的一个安全组。

- 你可以从租户中的已验证域使用 Azure AD 中的任何组（无论是否具有电子邮件地址），以进行 Azure Rights Management 服务的委派管理。

### <a name="assigning-usage-rights-and-access-controls-to-external-groups"></a>向外部组分配使用权限和访问控制权限

除了为租户中的组使用 Azure AD proxyAddresses 之外，Azure 信息保护还以同样的方式使用此属性来授权其他租户的组。

## <a name="using-accounts-from-active-directory-on-premises-for-azure-information-protection"></a>将 Active Directory 本地帐户用于 Azure 信息保护

如果你希望将本地托管的帐户用于 Azure 信息保护，则必须将其同步到 Azure AD。 为方便部署，我们建议使用 [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect)。 但是，你可以使用可实现相同结果的任何目录同步方法。

同步帐户时，无需同步所有属性。 有关必须同步的属性列表，请参阅 Azure Active Directory 文档中的 [Azure RMS 部分](/azure/active-directory/connect/active-directory-aadconnectsync-attributes-synchronized#azure-rms)。

从 Azure 权限管理的属性列表中可以看到，对于用户而言，需要本地 AD属性 mail、proxyAddresses 和 userPrincipalName 进行同步。 **mail** 和 **proxyAddresses** 的值同步到 Azure AD proxyAddresses 属性。 有关详细信息，请参阅[如何在 Azure AD 中填充 proxyAddresses 属性](https://support.microsoft.com/help/3190357/how-the-proxyaddresses-attribute-is-populated-in-azure-ad)

## <a name="confirming-your-users-and-groups-are-prepared-for-azure-information-protection"></a>确认已准备好用户和组以使用 Azure 信息保护

可以使用 Azure AD PowerShell 确认用户和组可用于 Azure 信息保护。 此外，还可以使用 PowerShell 确认可用于向他们授权的值。 

例如，在 PowerShell 会话中使用 Azure Active Directory 的 V1 PowerShell 模块 [MSOnline](/powershell/module/msonline/?view=azureadps-1.0)，首先连接到服务并提供全局管理员凭据：

    Connect-MsolService


注意：如果此命令不起作用，可以运行 `Install-Module MSOnline` 安装 MSOnline 模块。

接下来，配置 PowerShell 会话，以便它不会截断该值：

    $Formatenumerationlimit =-1

### <a name="confirm-user-accounts-are-ready-for-azure-information-protection"></a>确认已准备好用户帐户用于 Azure 信息保护

若要确认用户帐户，请运行以下命令：

    Get-Msoluser | select DisplayName, UserPrincipalName, ProxyAddresses

首先查看并确保显示要用于 Azure 信息保护的用户。

然后查看是否填充了 **ProxyAddresses** 列。 如果是，可使用此列中的电子邮件值授权用户以使用 Azure 信息保护。

如果“ProxyAddresses”列未填充，则使用“UserPrincipalName”中的值授权用户以用于 Azure 权限管理服务。

例如：

|显示名称|UserPrincipalName|ProxyAddresses
|-------------------|-----------------|--------------------|
|Jagannath Reddy |jagannathreddy@contoso.com|{}|
|Ankur Roy|ankurroy@contoso.com|{SMTP:ankur.roy@contoso.com, smtp: ankur.roy@onmicrosoft.contoso.com}|

在此示例中：

- Jagannath Reddy 的用户帐户将通过 **jagannathreddy@contoso.com** 进行授权。

-  Ankur Roy 的用户帐户将使用 **ankur.roy@contoso.com** 和 **ankur.roy@onmicrosoft.contoso.com** 进行授权，而不是 **ankurroy@contoso.com**。

在大多数情况下，UserPrincipalName 的值匹配 ProxyAddresses 字段中的一个值。 这是推荐配置，但如果你无法更改 UPN 以匹配电子邮件地址，则必须执行以下步骤：

1. 如果 UPN 值中的域名是 Azure AD 租户的已验证域，请添加该 UPN 值作为 Azure AD 中的另一个电子邮件地址，以便现在可以使用 UPN 值授权用户帐户用于 Azure 信息保护。

    如果 UPN 值中的域名不是租户的已验证域，则不能用于 Azure 信息保护。 但是，当组电子邮件地址使用已验证域名时，用户仍然可以被授权为组成员。

2. 如果 UPN 不可路由（例如，**ankurroy@contoso.local** ），请为用户配置备用登录 ID，并指导他们使用此备用登录方式登录 Office。 还必须为 Office 设置注册表项。

    有关详细信息，请参阅[配置备用登录 ID](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) 和 [Office 应用程序定期提示输入 SharePoint Online、OneDrive 和 Lync Online 的凭据](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)。

> [!TIP]
> 你可以使用 Export-Csv cmdlet 将结果导出到电子表格，以便于进行管理，例如搜索和批量编辑以进行导入。
>
> 例如：`Get-MsolGroup | select DisplayName, ProxyAddresses | Export-Csv -Path UserAccounts.csv`

### <a name="confirm-group-accounts-are-ready-for-azure-information-protection"></a>确认已准备好组帐户用于 Azure 信息保护

若要确认组帐户，请使用以下命令：

    Get-MsolGroup | select DisplayName, ProxyAddresses

确保显示要用于 Azure 信息保护的组。 对于显示的组，可以使用 **ProxyAddresses** 列中的电子邮件地址授权组成员使用 Azure权限管理服务。

然后查看组是否包含要用于 Azure 信息保护的用户（或其他组）。 可以使用 PowerShell 来执行此操作（例如，[Get-MsolGroupMember](/powershell/module/msonline/Get-MsolGroupMember?view=azureadps-1.0)），或使用你的管理门户。

对于使用安全组的两个 Azure 权限管理服务配置方案，可以使用以下 PowerShell 命令查找对象 ID 并显示可用于标识这些组的名称。 你还可以使用 Azure 门户查找这些组，复制对象 ID 的值并显示名称：

    Get-MsolGroup | where {$_.GroupType -eq "Security"}

## <a name="considerations-for-azure-information-protection-if-email-addresses-change"></a>电子邮件地址更改情况下的 Azure 信息保护注意事项

如果更改用户或组的电子邮件地址，我们建议你向用户或组添加旧电子邮件地址作为第二个电子邮件地址（也称为代理地址、别名或备用电子邮件地址）。 执行此操作后，旧电子邮件地址将添加到 Azure AD proxyAddresses 属性。 此帐户管理功能可确保在使用旧电子邮件地址时保存的任何使用权限或其他配置的业务连续性。 

如果无法如此操作，则具有新电子邮件地址的用户或组可能无法访问先前受旧电子邮件地址保护的文档和电子邮件。 此情况下，必须重复保护配置以保护新的电子邮件地址。 例如，如果向用户或组授予了模板或标签的使用权限，则他们可使用与你向旧电子邮件地址授予的相同使用权限编辑这些模板或标签，还可按相同权限指定新的电子邮件地址。

请注意，一个组更改其电子邮件地址的情况很少见，如果你为某个组而不是单个用户分配使用权限，则用户的电子邮件地址是否更改无关紧要。 在这种情况下，使用权限分配给组电子邮件地址，而不是单个用户电子邮件地址。 这是管理员在配置可保护文档和电子邮件的使用权限时最有可能采用的方法，同时也是推荐的方法。 但是，用户通常更有可能为单个用户分配自定义权限。 由于你无法随时了解用户帐户或组是否已用于授予访问权限，因此，始终添加旧电子邮件地址作为第二个电子邮件地址是最安全的做法。

## <a name="group-membership-caching-by-azure-information-protection"></a>Azure 信息保护缓存组成员身份

出于性能原因，Azure 信息保护会缓存组成员身份。 这意味着，当 Azure 信息保护使用这些组时，对 Azure AD 中的组成员身份所做的任何更改将在三小时内生效，并且此时间段可能会有所变化。 

请注意，此延迟归因于将组用于授予使用权限或配置 Azure Rights Management 服务时，或者配置作用域策略时执行的任何更改或测试。


## <a name="next-steps"></a>后续步骤

在已确认可将 Azure 信息保护用于你的用户和组，并已准备好开始保护文档和电子邮件后，请检查是否需要激活 Azure Rights Management 服务。 必须首先激活此服务才能开始保护你组织的文档和电子邮件： 

- 从 2018 年 2 月开始：如果包含 Azure Rights Management 或 Azure 信息保护的订阅是在当月或之后获取的，将自动为你激活此服务。 

- 如果你的订阅是在 2018 年 2 月之前获取的：必须自己激活此服务。 

有关检查激活状态等详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。

