---
# required metadata

title: 如何&#58;获取 Azure 应用程序 ID | Azure RMS
description: 使用 Microsoft Rights Management SDK 4.2 创建启用 RMS 的应用需要与 RMS 团队创建协议。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0fe9dc-bc91-4018-b28d-2db293a3eaa2
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 如何：获取 Azure 应用程序 ID

使用 Microsoft Rights Management SDK 4.2 创建启用 RMS 的应用需要与 RMS 团队创建协议。

## 概述

使用 MS RMS SDK 4.2 创建和发布启用 RMS 的应用需要也与 RMS 团队创建服务使用协议。 此协议（也称为权限管理许可协议 (RMLA)）可指导你履行代表用户和/或内容所有者对你应用的行为（遵循业务规则）所赞成的内容保护协定。 作为启用 RMS 的应用的创建者，你与 RMS 团队之间的协定会通过“Azure 应用程序 ID”的存在来强制实施，该 ID 代表此协议，使你的应用可以连接到 Azure AD 身份验证服务。

## 处理

使用以下步骤可创建应用 Id 并与 RMS 团队签署使用协议。

-   请按照主题 [如何在 Azure 上创建应用 ID](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx) 中的指导创建应用 Id。
-   向 RMS 团队写信以启动 RMLA 过程，将“应用 ID”发送到 <askipteam@microsoft.com>.
-   签署 RMLA 并将它返回给 RMS 团队。
-   现在已签署了 RMLA，你应在调用身份验证库时通过 *clientID* 参数传递应用程序 ID。

    身份验证调用在 [iOS/OS X 代码示例](ios-os-x-code-examples.md) 主题中如下所示。


    // 使用 ADAL 检索令牌
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



**注意**  如果 RMS 团队未在 60 天内收到你签署的 RMLA，则会阻止你的应用向 Azure 身份验证系统进行身份验证。

 

 

 


<!--HONumber=Apr16_HO4-->


