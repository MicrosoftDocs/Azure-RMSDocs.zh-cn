---
title: Azure 信息保护租户密钥的操作
description: 确定对 Azure 信息保护租户密钥具有的不同级别控制权和责任。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 1c36013c007b3e670af2a13de891cbdffccd3117
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39489910"
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Azure 信息保护租户密钥的操作

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

根据你的租户密钥拓扑，可以对 Azure 信息保护租户密钥进行不同级别的控制并承担相应责任。 两种密钥拓扑分别由 Microsoft 托管和客户托管。

这种在 Azure 密钥保管库中自行管理租户密钥的方式通常称为“自带密钥”(BYOK)。 有关此方案以及如何在这两种租户密钥拓扑之间进行选择的详细信息，请参阅[计划和实现你的 Azure 信息保护租户密钥](plan-implement-tenant-key.md)。

下表介绍了你可以执行的操作，具体取决于你为 Azure 信息保护租户密钥所选择的拓扑。

|生命周期操作|由 Microsoft 管理（默认）|由客户管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|撤消你的租户密钥|否（自动）|是|
|重新生成租户密钥|是|是|
|备份和恢复你的租户密钥|否|是|
|导出你的租户密钥|是|否|
|对违规行为做出响应|是|是|

确定实施了哪种拓扑之后，请选择以下的某个链接，获取这些针对 Azure 信息保护租户密钥的操作的相关详细信息：

- [Microsoft 托管的租户密钥](operations-microsoft-managed-tenant-key.md)
- [客户托管的租户密钥](operations-customer-managed-tenant-key.md)

但是，如果要通过从 Active Directory Rights Management Services 导入受信任的发布域 (TPD) 来创建 Azure 信息保护租户密钥，则执行此导入操作作为[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)的一部分。  

