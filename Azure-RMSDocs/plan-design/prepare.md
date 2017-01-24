---
title: "准备 Azure Rights Management 保护 |Azure 信息保护"
description: "检查是否已具备使用 Rights Management 服务的条件，以便组织可以保护文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: b0c5596feec3f61ad25fe47416a1383f453bdc6b


---

# <a name="preparing-for-azure-information-protection"></a>准备 Azure 信息保护

>*适用于：Azure 信息保护、Office 365*

为组织部署 Azure 信息保护之前，请确保已准备好以下项：

-   在云中手动或自动创建的已从 Active Directory 域服务 (AD DS) 同步的用户帐户和组。

    当你同步本地帐户和组时，并非所有属性都需要同步。 有关必须为 Azure 信息保护使用的 Azure Rights Management 服务同步的属性列表，请参阅 Azure Active Directory 文档中的 [Azure RMS 部分](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)。 为了便于部署，我们建议你使用 [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) 将本地目录连接到 Azure Active Directory，但你可以使用任何目录同步方法实现相同的结果。

-   云中支持邮件的组，将用于 Azure 信息保护。 这些组可以是内置组或手动创建的组，其中包含使用受保护文档和电子邮件的用户。

    如果你有 Exchange Online，则可以使用 Exchange 管理中心创建和使用支持邮件的组。 如果你有 AD DS 并要同步到 Azure AD，则可以创建和使用支持邮件的组（安全组或通讯组）。

## <a name="activate-the-rights-management-service-for-data-protection"></a>激活数据保护的 Rights Management 服务
保护文档和电子邮件的工作准备就绪后，请激活 Rights Management 服务来实现这一技术。 有关详细信息，请参阅[激活 Azure Rights Management](../deploy-use/activate-service.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


