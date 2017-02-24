---
title: "运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器 | Azure 信息保护"
description: "部署 RMS 连接器时如何将 Windows Server 文件分类基础结构与 Azure RMS 结合使用以自动保护 Office 文档。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4cdac14d3a77ea7bcce23b914bc3be0a1f46d2b5
ms.openlocfilehash: dd94145bc2a6f338bb8a8c0ac0712ed1c86517d4


---


# <a name="file-servers-that-run-windows-server-and-use-file-classification-infrastructure-fci"></a>运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器

>*适用于：Azure 信息保护、Office 365*


当你将 Windows Server 配置为使用文件分类基础结构时，此文件服务器资源管理器功能可以扫描本地文件，并确定它们是否包含敏感数据。 对于满足此条件的文件，可以使用管理员定义的分类属性，对其进行标记。 然后，文件分类基础结构可根据分类执行自动操作。 其中一种操作是使用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 来应用信息保护，并部署 Rights Management 连接器（也称为 RMS 连接器）。 然后，由 Azure RMS 自动保护 Office 文件。

若要保护所有文件类型，应不使用 RMS 连接器，而是改为运行 Windows PowerShell 脚本，该脚本使用 [Azure 信息保护模块](../rms-client/client-admin-guide-powershell.md)中提供的 cmdlet。

分类策略是完全可以配置的，并且具有高度的可扩展性，因此你可以防止未授权和已授权用户可能发生的数据泄漏。 它甚至有助于降低网络管理员的数据泄漏风险，因为你可以配置不要求这些管理员具有文件访问权限的策略。

有关为 Office 文件部署和配置 RMS 连接器的说明，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

有关针对所有文件类型使用 Windows PowerShell 脚本的说明，请参阅[使用 Windows Server 文件分类基础结构 &#40;FCI&#41; 的 RMS 保护](../rms-client/configure-fci.md)。



## <a name="next-steps"></a>后续步骤
现在你已经了解应用程序和服务如何支持 Azure RMS，你可能会希望将 Azure RMS 与Rights Management、Active Directory Rights Management Services (AD RMS) 的本地版本进行比较。 有关功能、要求和安全控制的比较，请参阅 [比较 Azure Rights Management 和 AD RMS](compare-azure-rms-ad-rms.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]




<!--HONumber=Feb17_HO2-->


