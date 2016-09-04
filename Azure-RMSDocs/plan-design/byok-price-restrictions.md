---
title: "BYOK 定价和限制 | Azure RMS"
description: "具有订阅（包含 Azure 权限管理）的组织可以在 Azure 密钥保管库中使用客户托管的密钥 (BYOK)，并记录其使用情况，无需额外付费。 但是，若要使用 Azure 密钥保管库，必须具有支持含 HSM 保护密钥的密钥保管库的 Azure 订阅。 在 Azure 密钥保管库中使用密钥会按月产生费用。 有关详细信息，请参阅 Azure 密钥保管库定价页。"
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 8505032a2a12f84c245e834e71d0b7b0d12e894f


---

# BYOK 定价和限制

>*适用于：Azure Rights Management、Office 365*


具有订阅（包含 Azure 权限管理）的组织可以在 Azure 密钥保管库中使用客户托管的密钥 (BYOK)，并记录其使用情况，无需额外付费。 但是，若要使用 Azure 密钥保管库，必须具有支持含 HSM 保护密钥的密钥保管库的 Azure 订阅。 在 Azure 密钥保管库中使用密钥会按月产生费用。 有关详细信息，请参阅 [Azure 密钥保管库定价页](https://azure.microsoft.com/en-us/pricing/details/key-vault/)。

如果有用户通过使用个人 RMS 免费注册帐户，则不能使用 BYOK 和使用日志记录，因为此配置没有租户管理员来配置这些功能。


> [!NOTE]
> 有关个人 RMS 的详细信息，请参阅[个人 RMS 和 Azure Rights Management](../understand-explore/rms-for-individuals.md)。

![BYOK 不支持 Exchange Online](../media/RMS_BYOK_noExchange.png)

BYOK 和使用日志记录可以无缝应用程序于任何与 Azure RMS 集成的应用程序。 其中包括 SharePoint Online 等云服务、运行 Exchange 和 SharePoint 的本地服务器（它们通过使用 RMS 连接器来运行 Azure RMS）、Office 2016 和 Office 2013 等客户端应用程序。 无论哪个应用程序请求 Azure RMS，你都将获得密钥使用日志。

但有一个例外：目前， **Azure RMS BYOK 不兼容 Exchange Online**。 如果你使用 Exchange Online，我们建议你暂时以默认密钥管理模式部署 Azure RMS，由 Microsoft 生成和管理你的密钥。 例如，以后你可以在 Exchange Online 不支持 Azure RMS BYOK 时，选择改用 BYOK。 但是，如果你不能等待，则目前可以采用另一种做法，那就是使用 BYOK 部署 Azure RMS，在这种情况下，Exchange 的 RMS 功能将会下降（未受保护的电子邮件和未受保护的附件将保持完全正常运行）：

-   无法显示 Outlook Web Access 中受保护的电子邮件或受保护的附件。

-   无法显示使用 Exchange ActiveSync IRM 的移动设备上的受保护电子邮件。

-   无法进行传输解密（例如，扫描恶意软件）和日记解密，因此将跳过受保护的电子邮件和受保护的附件。

-   无法执行会强制 IRM 策略的传输保护规则和数据丢失预防 (DLP)，因此，无法使用这些方法应用 RMS 保护。

-   基于服务器的受保护的电子邮件，因此将跳过受保护的电子邮件搜索。

当你对 Exchange Online 使用 RMS 功能缩减的 Azure RMS BYOK 时，RMS 将适用于 Windows 和 Mac 上 Outlook 中的电子邮件客户端，以及在不使用 Exchange ActiveSync IRM 的其他电子邮件客户端。

如果你正在从 AD RMS 迁移到 Azure RMS，你可能已导入你的密钥作为可信发布域 (TPD) 到 Exchange Online（在 Exchange 术语中也称为 BYOK，这不同于 Azure 密钥保管库 BYOK）。 在此情况下，你必须从 Exchange Online 中删除 TPD，以避免模板和策略冲突。 有关详细信息，请参阅 Exchange Online cmdlet 库中的 [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx)。

有时，Exchange Online 的 Azure RMS BYOK 异常实际上并不是问题。 例如，需要 BYOK 和日志记录功能的组织在本地运行他们的数据应用程序（Exchange、SharePoint、Office），并使用 Azure RMS 提供使用本地 AD RMS 不易实现的功能（例如，与其他公司协作，从移动客户端进行访问）。 BYOK 和日志记录功能在这种方案中使用效果非常好，让组织能够完全控制他们的 Azure RMS 订阅。

## 后续步骤

如果你已决定管理自己的密钥，转至[实现你的 Azure Rights Management 租户密钥](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key)。

如果你已决定保留默认配置，让 Microsoft 管理你的租户密钥，请参阅“计划和实现你的 Azure Rights Management 租户密钥”文章中的[后续步骤](plan-implement-tenant-key.md#next-steps)。




<!--HONumber=Aug16_HO4-->


