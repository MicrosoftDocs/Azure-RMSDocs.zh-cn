---
title: 适用于 Microsoft 信息保护的受保护的 PDF 阅读器
description: 为标记为分类和保护的 PDF 文档安装读取器
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
search.appverid:
- MET150
ms.openlocfilehash: fae4a3f0e95e0ee3cf548c59aee55fc6e1a39831
ms.sourcegitcommit: 0ff7941832bd8476d53810d2c849c56efa0303fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68701613"
---
# <a name="install-a-pdf-reader-that-supports-microsoft-information-protection"></a>安装支持 Microsoft 信息保护的 PDF 读取器

如果需要打开受 Microsoft 信息保护保护的 PDF 文档, 请使用以下链接和信息。

## <a name="choose-your-pdf-reader"></a>选择 PDF 读者

以下 PDF 读者可以打开受保护的 PDF 文档, 这些文档符合 PDF 加密的 ISO 标准:

|操作系统|受支持的阅读器和下载链接|
|----------------|-----------------------------------|
|Windows 10 及以前版本<br />通过 Windows 7 Service Pack 1|Adobe Acrobat Reader（首选）：<br /> 1.阅读 [Adobe 一般使用条款](https://www.adobe.com/legal/terms.html) <br /> 2.从[adobe 网站](https://www.adobe.com/)安装适用于 Windows 的 Adobe Reader<br /> 3.安装适用于 Windows 的[Adobe 插件](https://go.microsoft.com/fwlink/?linkid=2050049) <br /> 4.如果系统提示，请让管理员[对插件进行授权](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396) <br /><br /> Azure 信息保护查看器：[下载](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader：[下载](https://www.foxitsoftware.com/pdf-reader/)|
|MacOS 版本 10.12-10.14 |Adobe Acrobat 读者:<br /> 1.阅读 [Adobe 一般使用条款](https://www.adobe.com/legal/terms.html) <br /> 2.从[adobe 网站](https://www.adobe.com/)安装适用于 Mac 的 adobe Reader<br /> 3.安装适用于 Mac 的[Adobe 插件](https://go.microsoft.com/fwlink/?linkid=2050049) <br /> 4.如果系统提示，请让管理员[对插件进行授权](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)|
|Android|Azure 信息保护应用：[下载](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|Azure 信息保护应用：[下载](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>支持以前的格式

下表中的 PDF 读者支持文件扩展名为 ppdf 的受保护的 PDF 文档和具有 .pdf 文件扩展名的旧格式。

目前，SharePoint Online 和本地 SharePoint 在受 IRM 保护的库中使用 PDF 文档的旧格式。


|操作系统|受支持的阅读器|
|----------------|-----------------------------------|
|Windows 10 及以前版本<br />通过 Windows 7 Service Pack 1|Azure 信息保护查看器<br /><br />Gaaiho 文档<br /><br />适用于 Adobe 的 GigaTrust 桌面 PDF 客户端<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF<br /><br />RMS 共享应用程序|
|Android|Azure 信息保护应用<br /><br />具有 RMS 的 Foxit MobilePDF<br /><br />适用于 Android 的 GigaTrust 应用|
|iOS|Azure 信息保护应用<br /><br />具有 RMS 的 Foxit MobilePDF<br /><br />TITUS 文档|

## <a name="using-adobe-acrobat-reader-with-the-adobe-plug-in"></a>将 Adobe Acrobat Reader 与 Adobe 插件配合使用

Microsoft 与 Adobe 之间的协作为你提供了更简单、更一致的 PDF 文档体验, 并可选择进行保护。 此协作为 Adobe Acrobat 与 Microsoft 信息保护解决方案的原生集成提供支持，如 [Azure 信息保护](../what-is-information-protection.md)。 

此原生集成具有以下优点：

- 可查看由于包含敏感信息而受到保护的 PDF 文档。

- 可查看已应用于文档的组织标签的分类值。

- 对 PDF 加密的 ISO 标准的支持。
    
    除非[管理员禁用](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)了此功能, 否则, 默认情况下会为 Azure 信息保护客户端 (经典) 启用此受保护的 PDF 文件格式, 并始终使用 Azure 信息保护统一标签客户端。

有关详细信息, 请参阅以下博客文章: 

- [Adobe Acrobat Reader 与 Microsoft 信息保护集成的公开上市](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Adobe reader 和 Microsoft 信息保护集成常见问题解答](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)
