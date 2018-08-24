---
title: 如何设置 API 安全模式 | Azure RMS
description: 选择你的文件 API 应用程序运行的安全模式。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c6e7d29ac65e9f8494e6aaba8d5e3e2564bd3305
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42808406"
---
# <a name="how-to-set-the-api-security-mode"></a>操作说明：设置 API 安全模式

通过使用 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 函数，可选择文件 API 应用程序在哪种安全模式下运行。

若要初始化应用程序以在服务器模式下运行，请调用 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 函数并将安全模式设置为 [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx)。 默认情况下，你的应用程序将在*客户端模式* **IPC\_API\_MODE\_CLIENT** 下运行。

有关*服务器模式*的详细信息，请参阅[应用程序类型](application-types.md)。

**重要说明**  应该在调用任何其他 Rights Management Services SDK 2.1 函数前设置安全模式。 设置安全模式后，不能为当前的进程更改该模式。

## <a name="related-topics"></a>相关主题

* [应用程序类型](application-types.md)
* [API mode values](https://msdn.microsoft.com/library/hh535236.aspx)（API 模式值）
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
