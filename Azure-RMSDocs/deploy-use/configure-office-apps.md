---
title: "Office 应用；客户端配置 | Azure 信息保护"
description: "面向管理员提供的有关配置 Office 应用以使用 Azure 信息保护中的 Azure Rights Management 服务的信息和说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4cdac14d3a77ea7bcce23b914bc3be0a1f46d2b5
ms.openlocfilehash: f69fd9629afaafbf6f78b52f65b3bb69eaf19c9e


---

# <a name="office-apps-configuration-for-clients"></a>Office 应用；客户端配置

>*适用于：Azure 信息保护、Office 365*


使用此信息确定需要执行的操作，以便你的最终用户使用的 Office 应用可与 Azure 信息保护中的 Azure Rights Management 服务一同使用。

## <a name="office-2016-and-office-2013"></a>Office 2016 和 Office 2013
由于 Office 的这些更高版本以本机方式支持 Azure Rights Management 服务，因此无需客户端计算机配置即可支持各个应用程序（例如 Word、Excel、PowerPoint、Outlook 和 Outlook Web App）的信息权限管理 (IRM) 功能。 用户只需使用他们的 [!INCLUDE[o365_1](../includes/o365_1_md.md)] 凭据登录 Office 应用程序，即可保护文件和电子邮件，并可使用其他人保护的文件和电子邮件。

但是，我们建议你使用 Azure 信息保护客户端，为这些应用程序提供补充，使得用户能够发挥 Office 外接程序的优势。 有关详细信息，请参阅 [Azure 信息保护客户端：安装和配置客户端](configure-client.md)。

## <a name="office-2010"></a>Office 2010
对于要将 Azure 权限管理服务用于 Office 2010 的客户端计算机，它们必须安装 Azure 信息保护客户端或适用于 Windows 的 Rights Management 共享应用程序。 用户必须使用他们的 [!INCLUDE[o365_1](../includes/o365_1_md.md)] 凭据登录才能保护文件并使用其他用户保护的文件，此外不再需要更多配置。

有关 Azure 信息保护客户端的详细信息，请参阅 [Azure 信息保护客户端：安装和配置客户端](configure-client.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


