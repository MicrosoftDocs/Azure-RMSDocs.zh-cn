---
title: "通过 AIP 中的 Azure RMS 将客户端配置为使用 Office 应用"
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
ms.openlocfilehash: 52b3942d7918ada46cbdd7b45ed3925817e75f45
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2017
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office 应用：配置客户端，以使用 Azure 权限管理服务

>*适用于：Azure 信息保护、Office 365*


使用此信息确定需要执行的操作，使 Office 应用可与 Azure 信息保护中的 Azure 权限保护服务配合使用。

## <a name="office-2016-and-office-2013"></a>Office 2016 和 Office 2013
由于 Office 的这些更高版本以本机方式支持 Azure 权限管理服务，因此无需客户端计算机配置即可支持各个应用程序（例如 Word、Excel、PowerPoint、Outlook 和 Outlook 网页版）的信息权限管理 (IRM) 功能。 用户需要做的只是使用其 [!INCLUDE[o365_1](../includes/o365_1_md.md)] 凭据登录到 Office 应用程序。 然后，他们才能保护文件和电子邮件，以及使用受其他人保护的文件和电子邮件。

但是，我们建议你使用 Azure 信息保护客户端，为这些应用程序提供补充，使得用户能够发挥 Office 外接程序的优势。 有关详细信息，请参阅 [Azure 信息保护客户端：安装和配置客户端](configure-client.md)。

## <a name="office-2010"></a>Office 2010
对于要将 Azure 权限管理服务用于 Office 2010 的客户端计算机，它们必须具有 Azure 信息保护客户端或适用于 Windows 的 Rights Management 共享应用程序。 用户必须使用他们的 [!INCLUDE[o365_1](../includes/o365_1_md.md)] 凭据登录才能保护文件并使用其他用户保护的文件，此外不再需要更多配置。

有关 Azure 信息保护客户端的详细信息，请参阅 [Azure 信息保护客户端：安装和配置客户端](configure-client.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
