---
title: "准备 Rights Management 保护 - AIP"
description: "检查是否已具备使用 Rights Management 服务的条件，以便组织可以保护文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4b074f9a9a3d72b4d1ab5810b69e92b4792b0711
ms.sourcegitcommit: 16fec44713c7064959ebb520b9f0857744fecce9
translationtype: HT
---
# <a name="preparing-for-azure-information-protection"></a>准备 Azure 信息保护

>*适用于：Azure 信息保护、Office 365*

为组织部署 Azure 信息保护之前，请确保已准备好以下项：

-   在云中手动或自动创建的已从 Active Directory 域服务 (AD DS) 同步的用户帐户和组。

    当你同步本地帐户和组时，并非所有属性都需要同步。 有关必须为 Azure 信息保护使用的 Azure Rights Management 服务同步的属性列表，请参阅 Azure Active Directory 文档中的 [Azure RMS 部分](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)。 为了便于部署，我们建议你使用 [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) 将本地目录连接到 Azure Active Directory，但你可以使用任何目录同步方法实现相同的结果。

-   云中支持邮件的组，将用于 Azure 信息保护。 这些组可以是内置组或手动创建的组，其中包含使用受保护文档和电子邮件的用户。

    如果你有 Exchange Online，则可以使用 Exchange 管理中心创建和使用支持邮件的组。 如果你有 AD DS 并要同步到 Azure AD，则可以创建和使用支持邮件的组（安全组或通讯组）。

### <a name="group-membership-caching"></a>组成员身份缓存

出于性能原因，组成员身份由 Azure 权限管理服务缓存。 这意味着，对组成员身份所做的任何更改最多需要 3 小时才会生效，并且此时间段可能有变。 在 Azure 权限管理服务的配置中使用组时（如配置[自定义模板](../deploy-use/configure-custom-templates.md)）或使用[超级用户功能](../deploy-use/configure-super-users.md)的组时，对所做的任何更改或测试，都请考虑到此延迟。 

### <a name="considerations-if-email-addresses-change"></a>电子邮件地址已更改情况下的注意事项

在配置用户或组的使用权限并按其显示名称进行选择时，你的选择将保存并使用该对象的电子邮件地址。 如果稍后更改电子邮件地址，你所选的用户将不会成功获得授权。

如果更改了电子邮件地址，我们建议将旧的电子邮件地址作为代理电子邮件地址（也称为别名或备用电子邮件地址）添加到用户或组，以便保留以前分配的使用权限。 如果无法执行此操作，则必须从配置中删除用户或组，并再次选择它以保存已更新的电子邮件地址，以使新的受保护的内容使用新电子邮件地址。

自定义 Rights Management 模板是一个示例，你可以在其中按显示名称选择用户或组来分配用户权限。 此外，当用户使用 Azure 信息保护客户端配置自定义权限时，他们可以按显示名称选择用户和组。

## <a name="activate-the-rights-management-service-for-data-protection"></a>激活数据保护的 Rights Management 服务
保护文档和电子邮件的工作准备就绪后，请激活 Rights Management 服务来实现这一技术。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


