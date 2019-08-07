---
title: 如何部署应用 - AIP
description: 本文介绍如何将服务应用程序部署到租户中，该租户不同于最初开发时使用的租户。
keywords: ''
author: kkanakas
ms.author: kartikka
manager: barbkess
ms.date: 02/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 34dc6d6f-cfe4-4848-9b11-8d90c4b38ef7
audience: developer
ms.reviewer: kartikka
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 5150c9f3339f442f7898f273d2275cd267e8d6b8
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68791158"
---
# <a name="deploying-a-service-application-into-a-different-tenant"></a>将服务应用程序部署到不同租户

本文介绍部署服务应用程序的过程。 这种情形中，将使用初始开发 AD 租户注册应用程序转换为使用不同公司的生产 AD 租户注册应用程序。

> [!Note]
> 仅在服务应用程序使用对称密钥身份验证时才涉及此情形。

## <a name="scenario"></a>应用场景
公司 CoolApp 使用 Azure 信息保护 (AIP) 开发了一个服务应用程序，该应用程序会在用户从业务应用程序（如 Dynamics、SAP 或 Salesforce）导出文档时，对文档进行加密、标记和保护。 在此方案中，大型企业 ABC 购买 CoolApp 的新应用程序，因此 CoolApp 团队需将他们的解决方案部署到 ABC 的环境中。 

![在不同的租户中创建对称密钥的示例流程](../media/develop/service-app-provision.jpg)

## <a name="flow-1-coolapp-provides-a-ui-dialog-to-abc-to-implement-the-deployment"></a>流程 1：CoolApp 向 ABC 提供 UI 对话框以实现部署

ABC 购买 CoolApp 的解决方案后，ABC 的 IT 管理员必须创建 CoolApp 服务主体，并将该应用程序注册到 ABC 的 Azure AD 租户。 

[部署应用程序](developing-your-application.md)的**创建服务主体**部分概述了这些步骤。

![IT 管理员对应用程序进行输入的 UI 示例](../media/develop/how-to-deploy-app-UI.png)

> [!Note]
> 需要租户管理员权限才可在租户中创建服务主体

然后，ABC IT 管理员将启动 CoolApp 的应用程序作为其环境中的服务，并嵌入要使用的 CoolApp 应用程序的详细信息，如应用程序 ID、租户 ID 和对称密钥。

如果不需向 ABC 的 IT 管理员提供 UI 对话框的服务主体信息，则请遵循**流程 2** 的方法。

## <a name="flow-2-abc-it-administrator-provides-the-key-to-the-coolapp-team"></a>流程 2：ABC IT 管理员向 CoolApp 团队提供密钥

ABC IT 管理员创建服务主体后（如**图 1** 所示），ABC 向 CoolApp 团队提供信息。 然后 CoolApp 团队继续在 CoolApp 应用程序中嵌入信息，以供 ABC 的租户使用。
