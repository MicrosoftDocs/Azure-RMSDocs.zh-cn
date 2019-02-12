---
title: 通过 AIP 中的 Azure RMS 将客户端配置为使用 Office 应用
description: 面向管理员提供的有关配置 Office 应用以使用 Azure 信息保护中的 Azure Rights Management 服务的信息和说明。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/01/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7896e1c8a342ce8a430d9133950a2fe47a7de602
ms.sourcegitcommit: 8558af7116f62414054feffa346aba197a1250d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2019
ms.locfileid: "55559761"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office 应用：配置客户端，以使用 Azure 权限管理服务

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)


使用此信息确定需要执行的操作，使 Office 应用可与 Azure 信息保护中的 Azure 权限保护服务配合使用。

## <a name="office2016-and-office-2013"></a>Office 2016 和 Office 2013
由于 Office 的这些更高版本以本机方式支持 Azure 权限管理服务，因此无需客户端计算机配置即可支持各个应用程序（例如 Word、Excel、PowerPoint、Outlook 和 Outlook 网页版）的信息权限管理 (IRM) 功能。 所有用户都必须使用其 Office 365 凭据登录其 Office 应用程序。 然后，他们才能保护文件和电子邮件，以及使用受其他人保护的文件和电子邮件。

但是，我们建议你使用 Azure 信息保护客户端，为这些应用程序提供补充，使得用户能够发挥 Office 外接程序的优势。 有关详细信息，请参阅 [Azure 信息保护客户端：客户端安装和配置](configure-client.md)。

## <a name="office2010"></a>Office 2010
对于要将 Azure Rights Management 服务与 Office 2010 结合使用的客户端计算机，它们必须具有 Azure 信息保护客户端。 用户必须使用其 Office 365 凭据登录，然后才能保护文件并使用受其他用户保护的文件，此外不再需要更多配置。

有关 Azure 信息保护客户端的详细信息，请参阅 [Azure 信息保护客户端：客户端安装和配置](configure-client.md)。

