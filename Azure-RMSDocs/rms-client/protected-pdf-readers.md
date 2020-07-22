---
title: 适用于 Microsoft 信息保护的受保护的 PDF 阅读器
description: 为标记为分类和保护的 PDF 文档安装读取器
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: dd8a895c0fb6fb94311d7e028265bf9bbdbfe668
ms.sourcegitcommit: 16d2c7477b96c5e8f6e4328a61fe1dc3d12c878d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86927690"
---
# <a name="which-pdf-readers-are-supported-for-protected-pdfs"></a>受保护的 Pdf 支持哪些 PDF 读取器？

用于分类和/或受保护 Pdf 的 PDF 读者使你可以打开包含敏感信息的加密 Pdf。

通过[Azure 信息保护（AIP）](../what-is-information-protection.md)加密 pdf 可确保未经授权的人员无法读取文件的内容，甚至已获授权的人员也无法共享显示内容的屏幕或屏幕截图。

支持 Azure 信息保护的受保护的 PDF 读者验证你是否已获得打开文档的权限，还会解密你的内容。

例如，下图显示在 Adobe Acrobat Reader 中打开的加密文档。 顶部的栏表示文档受 Microsoft 信息保护解决方案保护。

:::image type="content" source="../media/protected-pdf-in-adobe-reader.png" alt-text="在 Adobe Acrobat Reader 中打开受保护的 PDF":::

有关说明，请参阅以下部分：

- [在 Windows 或 Mac 上的 Microsoft Edge 中查看受保护的 Pdf](#viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac)

- [安装适用于 Windows 或 Mac 的受保护的 PDF 读取器](#installing-a-protected-pdf-reader-for-windows-or-mac)

- [安装适用于移动设备的受保护的 PDF 阅读器（iOS/Android）](#installing-a-protected-pdf-reader-for-mobile-iosandroid)

> [!TIP]
> 如果在安装建议的读者后文档未打开，则文档可能会以较旧的格式进行保护。 
>
> 在这种情况下，请尝试将某个读取器列为先前格式的支持。 有关详细信息，请参阅[以前的格式支持](#support-for-previous-formats)。
> 
### <a name="iso-standards-for-pdf-encryption"></a>PDF 加密的 ISO 标准

在此页上引用的 PDF 读者可以所有打开受保护的文档，这些文档符合 PDF 加密的 ISO 标准。 

默认情况下，AIP 经典和统一标签客户端使用此标准，除非管理员已将其[禁用](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)。

### <a name="viewing-protected-pdfs-in-adobe-acrobat-reader"></a>在 Adobe Acrobat Reader 中查看受保护的 Pdf

Adobe Acrobat Reader 与 Microsoft 信息保护解决方案（例如[Azure 信息保护](../what-is-information-protection.md)）集成，为用户提供针对分类和/或受保护的 pdf 的简化一致的体验。

[Windows](protected-pdf-readers-windows.md)和[MacOS](protected-pdf-readers-mac.md)支持 Adobe Acrobat Reader with Microsoft 信息保护集成。

有关详细信息，请参阅以下博客文章： 

- [Adobe Acrobat Reader 与 Microsoft 信息保护集成的公开上市](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Adobe reader 和 Microsoft 信息保护集成常见问题解答](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac"></a>在 Windows 或 Mac 上的 Microsoft Edge 中查看受保护的 Pdf

Microsoft Edge 提供对查看已分类和受保护的 PDF 文件的本机支持。 使用 Microsoft Edge 可以确保用户无需安装或配置任何其他设置或软件即可无缝打开受保护的 PDF 文件。

受支持的版本包括：

- **Windows：** Windows 10 和以前版本通过 Windows 8。 
    
    有关早期版本的详细信息，请参阅[对先前格式的支持](#support-for-previous-formats)。

- **Mac：** macOS 版本10.12 及更高版本 



<!--
With Microsoft Edge, when a user encounters a locally saved protected PDF file, they can view the file directly in the browser. If the file is available on SharePoint, the user only needs to click **Open** > **Open in browser** from Microsoft Edge, to view the file. 
-->

**说明** 

1. 检查系统上安装的[Microsoft Edge 版本](https://support.microsoft.com/help/4027011/microsoft-edge-find-out-which-version-you-have)。 
1. 如果 Microsoft Edge 版本为83.0.478.37 或更高版本，则可以直接在 Edge 浏览器中打开受保护的文件。 

1. 若要在 SharePoint 中打开 PDF 文件，**请单击 "**  >  **在浏览器中打开打开**"。 

    :::image type="content" source="../media/edge_open_browser.png" alt-text="使用 "在浏览器中打开" 选项，从浏览器使用 Microsoft Edge 打开受保护的 PDF":::
 
## <a name="installing-a-protected-pdf-reader-for-windows-or-mac"></a>安装适用于 Windows 或 Mac 的受保护的 PDF 读取器

若要在台式计算机上打开受保护的 PDF 文档，建议为你的操作系统安装适用于[acrobat 和 Acrobat 读者的相关 Microsoft 信息保护（MIP）插件](https://go.microsoft.com/fwlink/?linkid=2050049)。

**说明**

1. 如果尚未安装，请从[adobe 网站](https://www.adobe.com/)安装 adobe Reader。

    请确保已阅读并同意[Adobe 一般使用条款](https://www.adobe.com/legal/terms.html)。

1. 为你的操作系统安装[适用于 acrobat 和 Acrobat 读取器的 MIP 插件](https://go.microsoft.com/fwlink/?linkid=2050049)。  

    下载： [![下载](../media/download.png "下载适用于 Acrobat 和 Acrobat 读者的 MIP 插件")](https://go.microsoft.com/fwlink/?linkid=2050049)

    受支持的版本包括：

    - **Windows：** Windows 10 和以前版本通过 Windows 8。 
    
        有关早期版本的详细信息，请参阅[对先前格式的支持](#support-for-previous-formats)。

    - **Mac：** macOS 版本 10.12-10.14 

1. 如果系统提示进行管理员批准，请要求管理员授权该插件。

    例如：
    
    :::image type="content" source="../media/admin-approval-for-mip-in-adobe-reader.png" alt-text="安装适用于 Acrobat 和 Acrobat 读取器的 MIP 插件所需的管理员批准":::
    
> [!NOTE]
> 有关详细信息，请参阅[Microsoft 信息保护和 Adobe release 公告](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)。
> 

### <a name="alternative-protected-pdf-readers-for-windows"></a>适用于 Windows 的备用受保护 PDF 读者

或者，使用适用于适用于 PDF 加密 ISO 标准的 Windows 的下列 PDF 读者之一：

- Azure 信息保护查看器[![下载](../media/download.png "下载 AIP 查看器")](https://go.microsoft.com/fwlink/?linkid=838993) 

- Foxit 读者[![下载](../media/download.png "下载 Foxit Reader 查看器")](https://www.foxitsoftware.com/pdf-reader/)

## <a name="installing-a-protected-pdf-reader-for-mobile-iosandroid"></a>安装适用于移动设备的受保护的 PDF 阅读器（iOS/Android）

若要在 iOS 或 Android 设备上打开受保护的 PDF，请下载并安装适用于你的操作系统的应用：

- 适用于 iOS 的 Azure 信息保护应用[![下载](../media/download.png "适用于 iOS 的 Azure 信息保护应用")  ](https://go.microsoft.com/fwlink/?LinkId=325338)

- 适用于 Android 的 Azure 信息保护应用[![下载](../media/download.png "适用于 Android 的 Azure 信息保护应用")](https://go.microsoft.com/fwlink/?LinkId=325340)

有关详细信息，请参阅[什么是适用于 iOS 或 Android 的 Azure 信息保护应用？](mobile-app-faq.md)。

## <a name="support-for-previous-formats"></a>支持以前的格式

以下 PDF 读取器支持带有扩展名**ppdf**的受保护 pdf，以及扩展名为 **.pdf**的旧格式。

如果无法使用推荐的读者打开受保护的 PDF，则文档可能会使用以前的格式进行保护。 例如，Microsoft SharePoint 当前对受 IRM 保护的库中的 PDF 文档使用较旧格式。

- **Windows 10/以前版本通过 Windows 7 Service Pack 1**

    - [Azure 信息保护查看器](https://go.microsoft.com/fwlink/?linkid=838993)
    - Gaaiho 文档
    - 适用于 Adobe 的 GigaTrust 桌面 PDF 客户端
    - Foxit Reader
    - Nitro PDF Reader
    - Nuance Power PDF
    - 边缘 Chromium

- **Android**：

    - [Azure 信息保护应用](mobile-app-faq.md)
    - 具有 RMS 的 Foxit MobilePDF
    - 适用于 Android 的 GigaTrust 应用

- **iOS**：

    - [Azure 信息保护应用](mobile-app-faq.md)
    - 具有 RMS 的 Foxit MobilePDF
    - TITUS 文档

- **MacOS Catalina**： Edge Chromium

## <a name="next-steps"></a>后续步骤

如果在安装后需要更多帮助，请使用每个读取器的说明和文档。 例如，请参阅以下文章：

- [用户指南：通过 Azure 信息保护统一标签客户端查看受保护的文件](clientv2-view-use-files.md)
- [什么是适用于 iOS 或 Android 的 Azure 信息保护应用？](mobile-app-faq.md)