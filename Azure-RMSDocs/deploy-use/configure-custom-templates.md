---
# required metadata

title: 为 Azure Rights Management 配置自定义模板 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 为 Azure Rights Management 配置自定义模板
在你[激活 Azure Rights Management](activate-service.md) (Azure RMS) 之后，用户就能够自动使用两个默认模板，这些模板让他们能够轻松地将策略应用于在组织中限制访问授权用户的敏感文件。 这两个模板具有以下权限策略限制：

-   受保护内容的只读查看

    -   显示名称：**&lt;organization name&gt; - 机密，仅供查阅**

    -   特定权限：查看内容

-   受保护内容的读取或修改权限

    -   显示名称：**&lt;organization name&gt; - 机密**

    -   特定权限：查看内容、保存文件、编辑内容、查看分配的权限、允许宏、转发、答复、全部答复

此外，[RMS 共享应用程序](../rms-client/sharing-app-windows.md)让用户能够定义他们自己的一组权限。 对于 Outlook 客户端和 Outlook Web Access，用户可为电子邮件选择“不要转发”选项 **** 。

对于很多组织，默认模板可能足以满足他们的需求。 但如果你希望创建自己的自定义权限策略模板，也可以这样做。 创建自定义模板有以下原因：

-   你希望模板仅向组织内的一部分用户授权，而不是向所有用户授权。

-   你希望只有用户的子集能够在应用程序中查看和选择模板（部门模板），而不是组织中的所有用户都可以查看和选择模板。

-   你希望为模板定义一种自定义权限，例如查看和编辑，而不是复制和打印。

-   你希望在模板中配置更多选项，包括过期日期，以及是否能够在没有 Internet 连接的情况下访问内容。

要让用户能够选择包含此类设置的自定义模板，你必须首先创建一个自定义模板，对其进行配置，然后发布该模板。 尽管你可能只需要几个模板，但在 Azure 中可最多保存 500 个自定义模板。 

使用以下信息可帮助你配置和使用自定义模板：

-   [如何创建、配置和发布自定义模板](create-template.md)

-   [如何复制模板](copy-template.md)

-   [如何删除（存档）模板](remove-template.md)

-   [如何为用户刷新模板](refresh-templates.md)

-   [使用 PowerShell 管理模板](configure-templates-with-powershell.md)




<!--HONumber=Apr16_HO3-->

