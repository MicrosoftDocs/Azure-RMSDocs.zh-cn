---
# required metadata

title: 了解使用限制 | Azure RMS
description: 所有启用 RMS 的应用程序都必须强制实施使用限制。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 此 SDK 内容不是最新的。 在短时间内，请在 MSDN 上找到[最新版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)的文档。 **
# 了解使用限制

所有启用 RMS 的应用程序都必须强制实施使用限制。 使用限制是在用户尝试执行操作时产生的结果（例如 打印文档），但该文档的 RMS 策略未授予他们执行该操作的权限（例如 打印权限）。

可以使用 [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck) 函数查询某个文档的用户权限。

## 了解使用限制

-   熟悉标准 RMS 权限

    有关应用程序可能会强制实施的完整 RMS 权限集，请参阅[使用限制参考](usage-restriction-reference.md)。

    请注意，应用程序已定义了特定于你的情况的权限，且可能会创建超出标准 RMS 权限的权限。

-   确定使用限制强制点

    *使用限制强制点*是应用程序的控制流中的一个位置，此处需要强制实施使用限制。 [使用限制参考](usage-restriction-reference.md)主题提供了几个常见强制点的示例。

    评估你自己的应用程序以确定应用哪些使用限制强制点。

    你的应用程序可能不需要[使用限制参考](usage-restriction-reference.md)中所述的所有强制点。 例如，如果你的应用程序不允许用户打印内容，则不需要检查 **IPC\_GENERIC\_PRINT** 权限。

-   更新代码以在每个强制点执行访问检查

    有关如何强制实施特定权限的指南，请参阅[使用限制参考](usage-restriction-reference.md)。

## 相关主题

* [开发人员概念](ad-rms-concepts-nav.md)
* [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck)
* [使用限制参考](usage-restriction-reference.md)
 

 





<!--HONumber=Jun16_HO1-->


