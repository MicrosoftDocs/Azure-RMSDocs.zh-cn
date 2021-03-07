---
title: Microsoft 信息保护的受保护 PDF 查看器
description: 了解如何打开和查看标签为分类和保护的 Pdf。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: c982293c4b6544e0bc093caef5a94596660bfcb5
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415375"
---
# <a name="which-pdf-readers-are-supported-for-protected-pdfs"></a>受保护的 Pdf 支持哪些 PDF 读取器？

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>相关内容：*[AIP 统一标记客户端和经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

本文介绍 Azure 信息保护 (AIP) 支持的受保护 PDF 读取器。 受保护的 PDF 读者使用户能够打开这些加密的 Pdf 并查看包含的敏感信息。

用 AIP 加密 Pdf 可确保未经授权的人员无法读取文件的内容。 支持 AIP 的受保护的 PDF 读者验证你是否已被授权打开文档，还会解密你的内容。

例如，下图显示在 Adobe Acrobat Reader 中打开的加密文档。 顶部的栏表示文档受 Microsoft 信息保护解决方案保护。

:::image type="content" source="../media/protected-pdf-in-adobe-reader.png" alt-text="在 Adobe Acrobat Reader 中打开受保护的 PDF":::

有关说明，请参阅以下部分：

- [在 Windows 或 Mac 上的 Microsoft Edge 中查看受保护的 Pdf](#viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac)

- [安装适用于 Windows 或 Mac 的受保护的 PDF 读取器](#installing-a-protected-pdf-reader-for-windows-or-mac)

- [为 mobile (iOS/Android) 安装受保护的 PDF 阅读器 ](#installing-a-protected-pdf-reader-for-mobile-iosandroid)

> [!TIP]
> 如果在安装建议的读者后文档未打开，则文档可能会以较旧的格式进行保护。 
>
> 在这种情况下，请尝试将某个读取器列为先前格式的支持。 有关详细信息，请参阅 [以前的格式支持](#support-for-previous-formats)。
> 
### <a name="iso-standards-for-pdf-encryption"></a>PDF 加密的 ISO 标准

在此页上引用的 PDF 读者可以所有打开受保护的文档，这些文档符合 PDF 加密的 ISO 标准。 

默认情况下，AIP 客户端使用此标准。

> [!NOTE]
> **仅限经典客户端**：如果有 AIP 经典客户端，则管理员可能已将其 [禁用](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)。
> 

### <a name="viewing-protected-pdfs-in-adobe-acrobat-reader"></a>在 Adobe Acrobat Reader 中查看受保护的 Pdf

Adobe Acrobat Reader 与 Microsoft 信息保护解决方案（例如 Azure 信息保护）集成，为用户提供针对分类和/或受保护的 Pdf 的简化一致的体验。

[Windows](#installing-a-protected-pdf-reader-for-windows-or-mac)和[MacOS](#installing-a-protected-pdf-reader-for-windows-or-mac)支持 Adobe Acrobat Reader with Microsoft 信息保护集成。

有关详细信息，请参阅以下博客文章： 

- [Adobe Acrobat Reader 与 Microsoft 信息保护集成的公开上市](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Adobe reader 和 Microsoft 信息保护集成常见问题解答](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac"></a>在 Windows 或 Mac 上的 Microsoft Edge 中查看受保护的 Pdf

Microsoft Edge 为查看已分类和受保护的 PDF 文件提供内置支持。 使用 Microsoft Edge 确保用户可以无缝地打开受保护的 PDF 文件，而无需安装或配置任何额外的设置或软件。

受支持的版本包括：

- **Windows**： windows 10 和以前版本通过 windows 8。 
    
    有关早期版本的详细信息，请参阅 [对先前格式的支持](#support-for-previous-formats)。

- **Mac**： macOS 版本10.12 及更高版本 


**说明**： 

1. 检查系统上安装的 [Microsoft Edge 版本](https://support.microsoft.com/help/4027011/microsoft-edge-find-out-which-version-you-have) 。 
1. 如果 Microsoft Edge 版本为83.0.478.37 或更高版本，则可以直接在 Edge 浏览器中打开受保护的文件。 

1. 若要在 SharePoint 中打开 PDF 文件，**请单击 "**  >  **在浏览器中打开打开**"。 

    :::image type="content" source="../media/edge_open_browser.png" alt-text="使用 &quot;在浏览器中打开&quot; 选项，从浏览器使用 Microsoft Edge 打开受保护的 PDF":::
 
## <a name="installing-a-protected-pdf-reader-for-windows-or-mac"></a>安装适用于 Windows 或 Mac 的受保护的 PDF 读取器

若要在台式计算机上打开受保护的 PDF 文档，建议为你的操作系统安装适用于 Acrobat 的相关 [Microsoft 信息保护 (MIP) 插件](https://go.microsoft.com/fwlink/?linkid=2050049) 。

**说明**：

1. 如果尚未安装，请从 [adobe 网站](https://www.adobe.com/)安装 adobe Reader。

    请确保已阅读并同意 [Adobe 一般使用条款](https://www.adobe.com/legal/terms.html)。

1. 为你的操作系统安装 [适用于 acrobat 和 Acrobat 读取器的 MIP 插件](https://go.microsoft.com/fwlink/?linkid=2050049) 。  

    受支持的版本包括：

    - **Windows**： windows 10 和以前版本通过 windows 8。 
    
        有关早期版本的详细信息，请参阅 [对先前格式的支持](#support-for-previous-formats)。

    - **Mac**： macOS 版本 10.12-10.14 

1. 如果系统提示进行管理员批准，请要求管理员授权该插件。

    例如：
    
    :::image type="content" source="../media/admin-approval-for-mip-in-adobe-reader.png" alt-text="安装适用于 Acrobat 和 Acrobat 读取器的 MIP 插件所需的管理员批准":::
    
> [!NOTE]
> 有关详细信息，请参阅 [Microsoft 信息保护和 Adobe release 公告](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)。
> 

### <a name="alternative-protected-pdf-readers-for-windows"></a>适用于 Windows 的备用受保护 PDF 读者

或者，使用适用于适用于 PDF 加密 ISO 标准的 Windows 的下列 PDF 读者之一：

- [Azure 信息保护查看器](https://go.microsoft.com/fwlink/?linkid=838993) 

- [Foxit Reader](https://www.foxitsoftware.com/pdf-reader/)

## <a name="installing-a-protected-pdf-reader-for-mobile-iosandroid"></a>为 mobile (iOS/Android) 安装受保护的 PDF 阅读器

若要在 iOS 或 Android 设备上打开受保护的 PDF，请下载并安装适用于你的操作系统的应用：

|(OS)  |链接  |
|---------|---------|
|**iTunes**     | [![从 iTunes 安装。](../media/small/ios-icon-small.png)](https://apps.apple.com/app/microsoft-rights-management/id689516635)        |
|**Google Play**     |[![从 Google Play 安装。](../media/small/android-icon-small.png)](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)         |
| | |

有关详细信息，请参阅 [适用于 Azure 信息保护的移动查看器应用 (iOS 和 Android) ](mobile-app-faq.md)。

## <a name="support-for-previous-formats"></a>支持以前的格式

以下 PDF 读者支持扩展名为 **ppdf** 的受保护 pdf 和扩展名为 **.pdf** 的旧格式。

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
- [适用于 Azure 信息保护 (iOS 和 Android) 的移动查看器应用 ](mobile-app-faq.md)