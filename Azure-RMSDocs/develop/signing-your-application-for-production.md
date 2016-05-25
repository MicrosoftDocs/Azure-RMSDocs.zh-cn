---
# required metadata

title: 为生产对应用程序进行签名 | Azure RMS
description: 本主题将指导你完成为生产模式对应用程序进行签名的过程。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 09BA148C-7D1E-43C8-92EA-24BBB6EFDB19
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 为生产对应用程序进行签名

本主题将指导你完成为生产模式对应用程序进行签名的过程。

## 对启用权限的应用程序进行签名

这些步骤假定你已为预生产层次结构对应用程序进行签名。 如果尚未执行此操作，请完成[测试启用权限的应用程序](running-your-first-application.md)中所述的过程。

从 Microsoft 收到生产证书后，你将立即获得以下文件：

-   YourPrivateKey.dat
-   YourPublicKey.dat
-   ProductionCertificate.xml

将其置于 *GenManifest.exe* 和你的应用程序二进制文件 (.exe) 所在的同一目录中。

-   以下过程将指导你使用生产证书创建新的 MCF 文件：

    -   创建新目录，并将文件置于该新目录中。 使用 Notepad.exe 为你的应用程序创建 MCF 文件。 该文件应具有以下内容。

        ``` syntax
        AUTO-GUID
        .\\YourPrivateKey.dat
        modulelist
        req     .\\<yourappname>.exe
        POLICYLIST
        INCLUSION
        PUBLICKEY .\\YourPublicKey.dat
        EXCLUSION
        ```

    -   运行以下命令来对你的应用程序进行签名：

        **genmanifest.exe -chain ProductionCertificate.xml** *YourAppName***.mcf** *YourAppName***.exe.man**

        如果 Genmanifest 成功，你将仅看到以下文本：

        如果 Genmanifest 失败，你将看到一条错误消息。

    -   你的 *YourAppName*.exe.man 应始终放置在与 *YourAppName*.exe 相同的目录中。

## 相关主题

* [使用方法](how-to-use-msipc.md)
* [测试启用权限的应用程序](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO4-->


