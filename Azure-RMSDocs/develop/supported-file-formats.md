---
# required metadata

title: 支持的文件格式 | Azure RMS
description: 当前版本的文件 API 支持对 MS Office 文件的本机保护、对所有其他文件格式的 PDF 和 PFile 保护。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: deb9a110-c098-4834-8319-05d5a28a0ccd

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 支持的文件格式

文件 API 支持本机和 Pfile 格式。

## 支持的文件格式

当前版本的文件 API 支持对 Microsoft Office 文件的本机保护、对所有其他文件格式的可移植文档文件 (PDF) 和 PFile 保护。 PDF 文件可根据需要应用 PFile 保护。

-   **本机保护**。 在本机保护下，文件基于其 MIME 类型（文件扩展名）加密为 AD RMS 文件格式。 使用文件 API 以本机方式保护的文件与支持 AD RMS 的使用本机保护的应用程序所需的格式一致；例如，Office 2013、Office 2010 和 FoxIt PDF 阅读器。 仅支持对 Office 文件、PDF 文件和某些其他类型的文件的本机保护。 有关本机保护支持的文件类型的详细信息，请参阅[文件 API 配置](file-api-configuration.md)。
-   **PFile 保护**。 在 PFile 保护中，使用 AD RMS 受保护文件 (PFile) 格式对文件进行加密。 该文件加密为具有扩展名 .pfile 的文件。 PFile 保护支持所有文件格式，除了 Office 文件。

管理员可以设置注册表项，以基于文件扩展名就文件是否应受保护以及如何进行保护进行配置。 有关如何在使用文件 API 时配置文件保护的详细信息，请参阅[文件 API 配置](file-api-configuration.md)。

### 相关主题

* [开发人员说明](developer-notes.md)
* [文件 API 配置](file-api-configuration.md)
 

 





<!--HONumber=Apr16_HO3-->

