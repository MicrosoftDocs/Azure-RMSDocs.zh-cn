---
title: 通过 AIP 中的 Azure RMS 将客户端配置为使用 Office 应用
description: 面向管理员提供的有关配置 Office 应用以使用 Azure 信息保护中的 Azure Rights Management 服务的信息和说明。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ea6b8afa02b9555924bcd1df5dfae1b7b37a217a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383527"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office 应用：配置客户端，以使用 Azure 权限管理服务

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***相关** 内容： [AIP 统一标签客户端和经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


使用此信息确定需要执行的操作，使 Office 应用可与 Azure 信息保护中的 Azure 权限保护服务配合使用。

## <a name="office-365-apps-office-2019-office-2016-and-office-2013"></a>Office 365 应用、Office 2019、Office 2016 和 Office 2013

由于 Office 的这些更高版本提供了对 Azure Rights Management 服务的内置支持，因此无需客户端计算机配置即可支持适用于应用程序（例如 Word、Excel、PowerPoint、Outlook 和 Outlook 网页版）的信息权限管理 (IRM) 功能。 

所有用户都必须在 Windows 上对这些应用执行操作，使用其 Microsoft 365 凭据登录到 Office 应用程序。 然后，他们才能保护文件和电子邮件，以及使用受其他人保护的文件和电子邮件。

### <a name="user-instructions-for-office-for-mac"></a>Office for Mac 的用户说明

具有 Office for Mac 的用户必须先验证其凭据，然后才能保护内容。 例如：

1. 打开 Outlook 并使用您 Microsoft 365 的工作或学校帐户创建配置文件。 

2. 创建新消息，在 " **选项** " 选项卡上选择 " **权限**"，然后选择 " **验证凭据**"。 出现提示时，再次指定 Microsoft 365 的工作或学校帐户详细信息，然后选择 " **登录**"。
    
    此操作将下载 Azure Rights Management 模板，并 **验证凭据** 现在已替换为不包含 **任何限制**、不 **转发** 以及为租户发布的任何 Azure Rights Management 模板的选项。 

3. 现在可以取消此新邮件。

4. 保护电子邮件或文档：在 " **选项** " 选项卡上，选择 " **权限** "，然后选择用于保护电子邮件或文档的选项或模板。

## <a name="office-2010"></a>Office 2010

对于要将 Azure Rights Management 服务与 Office 2010 结合使用的客户端计算机，它们必须具有 Azure 信息保护客户端。 无需进一步的配置，用户必须使用其 Microsoft 365 凭据登录，然后才能保护文件并使用受他人保护的文件。

有关详细信息，请参阅 [Azure 信息保护客户端：安装和配置客户端](configure-client.md)。

