---
# required metadata

title: 如何设置 API 安全模式 | Azure RMS
description: 选择你的文件 API 应用程序运行的安全模式。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 操作说明：设置 API 安全模式

通过使用 [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函数，你可以选择文件 API 应用程序在哪种安全模式下运行。

若要初始化你的应用程序以在*服务器模式*下运行，请调用 [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函数并将安全模式设置为 [**IPC\_API\_MODE\_SERVER**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)。 默认情况下，你的应用程序将在*客户端模式* **IPC\_API\_MODE\_CLIENT** 下运行。

有关*服务器模式*的详细信息，请参阅[应用程序类型](application-types.md)。

**重要说明**  应该在调用任何其他 Rights Management Services SDK 2.1 函数前设置安全模式。 设置安全模式后，不能为当前的进程更改该模式。

## 相关主题

* [应用程序类型](application-types.md)
* [**API 模式值**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 


<!--HONumber=Jun16_HO2-->


