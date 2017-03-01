---
title: "用户是否注册了个人 RMS - AIP"
description: "作为管理员，你如何知道用户是否注册了个人 RMS？ 你可能会分别或结合使用本文所述的任何方法。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: e696bf596255b5e28aa5589cfc18715f100c5b07
ms.lasthandoff: 02/24/2017


---


# <a name="how-to-find-out-if-your-users-have-signed-up-for-rms-for-individuals"></a>如何发现你的用户注册了个人 RMS？

>*适用于：Azure 信息保护*

作为管理员，你如何知道用户是否注册了个人 RMS？ 你可以使用以下任意一种方法，或者结合使用多种方法：

-   询问用户如何保护高度机密文件，特别是在与组织外部人员协作时。

-   如果你拥有组织的 Azure 订阅，请使用 [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) cmdlet 查看是否为用户分配了 **RIGHTSMANAGEMENT_ADHOC** 许可证。 此许可证来自授予该组织的个人 RMS 订阅，包含可供用户使用自助服务注册过程的活动单元池。

-   使用 System Center Configuration Manager 等系统管理解决方案来清点已安装软件和在用软件。 例如，查找 Azure 信息保护客户端使用的 **MSIP.App.exe **，以及 Rights Management 共享应用程序的 ** ipviewer.exe **。 可以免费下载并安装此客户端和应用程序，以确定随后用于软件清单的其他特征。

-   请注意 Azure 信息保护客户端或 Rights Management 共享应用程序创建的文件扩展名。 .pfile 和 .ppdf 文件扩展名是最明显的示例，但是也有一些其他文件在原本就受权限管理服务保护时会更改其文件扩展名。 有关详细信息，请参阅 Azure 信息保护客户端管理员指南中的[支持保护的文件类型](../rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
