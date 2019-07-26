---
title: 适用于 Microsoft 信息保护的受保护的 PDF 阅读器
description: 了解已标记进行分类和保护的 PDF 文档，并了解其查看方式。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
search.appverid:
- MET150
ms.openlocfilehash: 9a1deef0cc63861560e528aa06cd44857ab86515
ms.sourcegitcommit: 47182b6a65bfae3561cb34be3d6a6852a1edccb9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68446857"
---
# <a name="supported-pdf-readers-for-microsoft-information-protection"></a>适用于 Microsoft 信息保护的受支持的 PDF 阅读器

使用以下信息以了解有关为分类和保护而标记的 PDF 文档，以及如何查看这些文档。

Microsoft 和 Adobe 之间的协作使得你在处理经过分类和受保护（可选）的 PDF 文档时获得更简化和更一致的体验。 此协作为 Adobe Acrobat 与 Microsoft 信息保护解决方案的原生集成提供支持，如 [Azure 信息保护](../what-is-information-protection.md)。 

此原生集成具有以下优点：

- 可查看由于包含敏感信息而受到保护的 PDF 文档。

- 可查看已应用于文档的组织标签的分类值。

- 对 PDF 加密的 ISO 标准的支持。
    
    如今，除非此功能被[管理员禁用](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)，否则 Azure 信息保护客户端的最新版本会默认为启用该受保护的 PDF 文件格式。

有关详细信息，请参阅以下博客文章：[自 10 月起，将 Adobe Acrobat Reader 用于受 Microsoft 信息保护保护的 PDF](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Starting-October-use-Adobe-Acrobat-Reader-for-PDFs-protected-by/ba-p/262738)

## <a name="supported-pdf-readers"></a>受支持的 PDF 阅读器

以下 PDF 阅读器可以打开遵循 PDF 加密的 ISO 标准的受保护的 PDF 文件：

|操作系统|受支持的阅读器和下载链接|
|----------------|-----------------------------------|
|Windows 10 及以前版本<br />通过 Windows 7 Service Pack 1|Adobe Acrobat Reader（首选）：<br />- 1. 阅读 [Adobe 一般使用条款](https://www.adobe.com/legal/terms.html) <br />- 2. 从[adobe 网站](https://www.adobe.com/)安装适用于 Windows 的 Adobe Reader<br />- 3. 安装适用于 Windows 的[Adobe 插件](https://go.microsoft.com/fwlink/?linkid=2050049) <br />- 4. 如果系统提示，请让管理员[对插件进行授权](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396) <br /><br /> Azure 信息保护查看器：[下载](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader：[下载](https://www.foxitsoftware.com/pdf-reader/)|
|macOS 版本 10.12-10.14 |Adobe Acrobat 读者:<br />- 1. 阅读 [Adobe 一般使用条款](https://www.adobe.com/legal/terms.html) <br />- 2. 从[adobe 网站](https://www.adobe.com/)安装适用于 Mac 的 adobe Reader<br />- 3. 安装适用于 Mac 的[Adobe 插件](https://go.microsoft.com/fwlink/?linkid=2050049) <br />- 4. 如果系统提示，请让管理员[对插件进行授权](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)|
|Android|Azure 信息保护应用：[下载](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|Azure 信息保护应用：[下载](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>支持以前的格式

下表中的 PDF 阅读器支持具有 .ppdf 文件扩展名的受保护的 PDF 文档和具有 .pdf 文件扩展名的旧格式。

目前，SharePoint Online 和本地 SharePoint 在受 IRM 保护的库中使用 PDF 文档的旧格式。


|操作系统|受支持的阅读器|
|----------------|-----------------------------------|
|Windows 10 及以前版本<br />通过 Windows 7 Service Pack 1|Azure 信息保护查看器<br /><br />Gaaiho 文档<br /><br />适用于 Adobe 的 GigaTrust 桌面 PDF 客户端<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF<br /><br />RMS 共享应用程序|
|Android|Azure 信息保护应用<br /><br />具有 RMS 的 Foxit MobilePDF<br /><br />适用于 Android 的 GigaTrust 应用|
|iOS|Azure 信息保护应用<br /><br />具有 RMS 的 Foxit MobilePDF<br /><br />TITUS 文档|
