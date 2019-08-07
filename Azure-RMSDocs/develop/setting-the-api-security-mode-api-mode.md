---
title: 如何设置 API 安全模式 | Azure RMS
description: 选择你的文件 API 应用程序运行的安全模式。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 2a71fcddecbe688f38360c42cf83946f82269013
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68790801"
---
# <a name="how-to-set-the-api-security-mode"></a>操作说明：设置 API 安全模式

通过使用 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 函数，可选择文件 API 应用程序在哪种安全模式下运行。

若要初始化应用程序以在服务器模式下运行，请调用 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 函数并将安全模式设置为 [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx)。 默认情况下，你的应用程序将在*客户端模式* **IPC\_API\_MODE\_CLIENT** 下运行。

有关*服务器模式*的详细信息，请参阅[应用程序类型](application-types.md)。

重要说明  应该在调用任何其他 Rights Management Services SDK 2.1 函数前设置安全模式。 设置安全模式后，不能为当前的进程更改该模式。

## <a name="related-topics"></a>相关主题

* [应用程序类型](application-types.md)
* [API mode values](https://msdn.microsoft.com/library/hh535236.aspx)（API 模式值）
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
