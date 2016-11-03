---
title: "如何设置 API 安全模式 | Azure RMS"
description: "选择你的文件 API 应用程序运行的安全模式。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 77e2dfe7f2afb1e70de658850f83f86e9224aea6
ms.openlocfilehash: 9235fa1c194162689b854493ea31e76c08c40ce7


---

# 操作说明：设置 API 安全模式

通过使用 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 函数，可选择文件 API 应用程序在哪种安全模式下运行。

若要初始化应用程序以在服务器模式下运行，请调用 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 函数并将安全模式设置为 [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx)。 默认情况下，你的应用程序将在*客户端模式* **IPC\_API\_MODE\_CLIENT** 下运行。

有关*服务器模式*的详细信息，请参阅[应用程序类型](application-types.md)。

**重要说明**  应该在调用任何其他 Rights Management Services SDK 2.1 函数前设置安全模式。 设置安全模式后，不能为当前的进程更改该模式。

## 相关主题

* [应用程序类型](application-types.md)
* [API 模式值](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
 

 



<!--HONumber=Oct16_HO3-->


