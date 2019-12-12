---
title: 如何调试启用权限的应用程序 | Azure RMS
description: 下面的主题演示如何调试应用程序和使用 Windows 事件日志。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: c0b53c0f749427f785bf12afa6b3f8cda461947e
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "68792549"
---
# <a name="how-to-debug-a-rights-enabled-application"></a>操作说明：调试启用权限的应用程序

下面的主题演示如何调试应用程序和使用 Windows 事件日志。

## <a name="debugging-your-application"></a>调试应用程序

Rights Management Services SDK 2.1 中禁用了运行时的开发人员版本的反调试检查。

你可以使用以下注册表项启用调试跟踪。 （若要关闭调试跟踪，请将值更改为0。）在此版本中进行调试时，无需执行任何其他操作。


```
HKEY_LOCAL_MACHINE
   SOFTWARE
      Microsoft
         MSIPC
            "Trace" = 00000001
            Data type
            dword
```

### <a name="application-logging-by-using-the-windows-event-log"></a>使用 Windows 事件日志的应用程序日志记录

事件日志的名称为“Microsoft-RMS-MSIPC/Debug”。 这意味着，在 Windows 事件查看器中，你的日志会显示为“Application and Services Logs\\Microsoft\\RMS\\MSIPC\\Debug”。

请注意  默认情况下，此日志处于启用状态，其详细程度级别设置为 3。

 

若要更改日志记录功能的设置，可以使用 Windows 事件查看器的 UI或者 Wevtutil（一种Windows 中内置的命令行工具）。

通过 Wevtutil 接口可以控制日志的详细程度。

目前，我们支持 3 种级别的日志记录：

-   级别 2- 错误
-   级别 3 - 警告
-   级别 4 - 信息

例如，下面的命令将启用 MSIPC 事件日志并将详细程度级别设置为信息。

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

请注意：在 Windows 事件查看器的“视图”菜单中，选择“显示分析和调试日志”可使 MSIPC 调试日志可见  。
