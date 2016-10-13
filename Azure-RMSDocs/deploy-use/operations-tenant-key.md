---
title: "你的 Azure Rights Management 租户密钥的操作 | Azure 信息保护"
description: "确定对 Azure 信息保护租户密钥具有的不同级别控制权和责任。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d5b6a1fc3fa0a19f3a6b65aa7b8815eda7432cd7
ms.openlocfilehash: 780c4db3e791dd427828550e428ec4ea18d55fd5


---

# Azure 信息保护租户密钥的操作

>*适用于：Azure 信息保护、Office 365*

实现 Azure 信息保护租户密钥之后，你可对该密钥进行不同级别的控制并承担相应责任，具体取决于你的租户密钥拓扑（由 Microsoft 管理或由客户管理）。

这种在 Azure 密钥保管库中自行管理租户密钥的方式通常称为“自带密钥”(BYOK)。 有关此方案以及如何在两种租户密钥拓扑之间进行选择的详细信息，请参阅[计划和实现你的 Azure Rights Management 租户密钥](../plan-design/plan-implement-tenant-key.md)。

下表介绍了你可以执行的操作，具体取决于你为 Azure 信息保护租户密钥选择的拓扑。

|生命周期操作|由 Microsoft 管理（默认）|由客户管理 (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|撤消你的租户密钥|否（自动）|是|
|更新你的租户密钥|是|是|
|备份和恢复你的租户密钥|否|是|
|导出你的租户密钥|是|否|
|对违规行为做出响应|是|是|

确定实施了哪一种拓扑之后，请选择以下任一部分，获取有关 Azure 信息保护租户密钥的这些操作的详细信息：


- [Microsoft 托管的租户密钥](operations-microsoft-managed-tenant-key.md)
- [客户托管的租户密钥](operations-customer-managed-tenant-key.md)







<!--HONumber=Sep16_HO4-->


