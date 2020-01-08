---
title: 适用于 Microsoft 信息保护的受保护的 PDF 阅读器
description: 为标记为分类和保护的 PDF 文档安装读取器
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: 6d9dc21d2541ab9aeb6d6fc6772781e1c23c1f2e
ms.sourcegitcommit: 40693000ce86110e14ffce3b553e42149d6b7dc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2019
ms.locfileid: "75326354"
---
# <a name="pdf-readers-that-support-microsoft-information-protection"></a>支持 Microsoft 信息保护的 PDF 读者

如果需要打开受 Microsoft 信息保护保护的 PDF 文档，请使用以下链接和信息。

受保护的 PDF 文档可能包含敏感信息。 为了增加安全性，会对文档进行加密，使未经授权的用户无法阅读该文档。 若要打开此文档，你需要一个读取器（有时称为查看器），该读者验证你是否已被授权打开文档，然后对其进行解密。

## <a name="install-pdf-readers-for-your-device"></a>为设备安装 PDF 读取器

选择用来安装 PDF 读取器的设备，该设备可以打开受保护的 PDF 文档。 所有这些读者都可以打开受保护的文档，这些文档符合 PDF 加密的 ISO 标准：

- **计算机**： [Windows](protected-pdf-readers-windows.md) | [MacOS](protected-pdf-readers-mac.md)

- **移动设备**： [Android](protected-pdf-readers-android.md) | [iOS](protected-pdf-readers-ios.md)

### <a name="support-for-previous-formats"></a>支持以前的格式

下表中的 PDF 读者支持文件扩展名为 ppdf 的受保护的 PDF 文档和具有 .pdf 文件扩展名的旧格式。 

目前，SharePoint Online 和本地 SharePoint 在受 IRM 保护的库中使用 PDF 文档的旧格式。


|操作系统|受支持的阅读器|
|----------------|-----------------------------------|
|Windows 10 及以前版本<br />通过 Windows 7 Service Pack 1|Azure 信息保护查看器<br /><br />Gaaiho 文档<br /><br />适用于 Adobe 的 GigaTrust 桌面 PDF 客户端<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF|
|Android|Azure 信息保护应用<br /><br />具有 RMS 的 Foxit MobilePDF<br /><br />适用于 Android 的 GigaTrust 应用|
|iOS|Azure 信息保护应用<br /><br />具有 RMS 的 Foxit MobilePDF<br /><br />TITUS 文档|

## <a name="using-adobe-acrobat-reader-with-the-adobe-plug-in"></a>将 Adobe Acrobat Reader 与 Adobe 插件配合使用

Microsoft 与 Adobe 之间的协作为你提供了更简单、更一致的 PDF 文档体验，并可选择进行保护。 此协作为 Adobe Acrobat 与 Microsoft 信息保护解决方案的原生集成提供支持，如 [Azure 信息保护](../what-is-information-protection.md)。 

此原生集成具有以下优点：

- 可查看由于包含敏感信息而受到保护的 PDF 文档。

- 可查看已应用于文档的组织标签的分类值。

- 对 PDF 加密的 ISO 标准的支持。
    
    除非[管理员禁用](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)了此功能，否则，默认情况下会为 Azure 信息保护客户端（经典）启用此受保护的 PDF 文件格式，并始终使用 Azure 信息保护统一标签客户端。

可以将 Adobe 插件用于[Windows](protected-pdf-readers-windows.md)和[MacOS](protected-pdf-readers-mac.md)。

有关详细信息，请参阅以下博客文章： 

- [Adobe Acrobat Reader 与 Microsoft 信息保护集成的公开上市](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Adobe reader 和 Microsoft 信息保护集成常见问题解答](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="next-steps"></a>后续步骤

使用此页中的链接安装 PDF 读取器，以便您可以打开受保护的 PDF 文档。

如果在安装读者之后需要帮助，请使用该读者随附的说明和文档。 例如，对于适用于 Windows 的 Azure 信息保护查看器，请参阅[用户指南：通过 Azure 信息保护统一标签客户端查看受保护的文件](clientv2-view-use-files.md)。
