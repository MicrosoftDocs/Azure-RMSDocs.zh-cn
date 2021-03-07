---
title: 适用于 Azure 信息保护的移动查看器应用 (iOS 和 Android) -AIP
description: 了解如何使用 Azure 信息保护 (AIP) 查看器应用在 iOS 和 Android 设备上查看受保护的文件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/22/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 1f0e3de4a8548761cd58cc69216a7e80fe0128e5
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415328"
---
# <a name="mobile-viewer-apps-for-azure-information-protection-on-ios-and-android"></a>IOS 和 Android 上用于 Azure 信息保护的移动查看器应用

>***适用** 于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)*
>
>相关内容：*[AIP 统一标记客户端和经典客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

使用 Azure 信息保护 (AIP) 移动应用程序，可以查看受保护的电子邮件、Pdf、图像和文本文件，而不能使用这些文件类型的常规应用打开这些文件。 例如，如果受保护的电子邮件在你的电子邮件移动应用中显示为附件，你可能想要使用 AIP 移动应用来查看该电子邮件。

**Mobile Office 版本支持保护和敏感度标签**。 如果设备上安装了移动 Office 应用，我们建议使用 Office 应用查看受保护的文件。 有关详细信息，请参阅 [Word、Excel 和 PowerPoint 中的敏感度标签功能](/microsoft-365/compliance/sensitivity-labels-office-apps#sensitivity-label-capabilities-in-word-excel-and-powerpoint)。

**如果要在桌面上打开文件**，请使用 [AIP 查看器的桌面版本](clientv2-view-use-files.md)。 

> [!NOTE]
> AIP 移动应用仅适用于 *查看器，* 并且不允许你创建新的电子邮件或回复电子邮件，或者创建或编辑受保护的文件。 AIP 移动应用程序也无法打开受保护的 Pdf 或电子邮件的附件。
> 

## <a name="aip-mobile-viewer-app-requirements"></a>AIP 移动查看器应用要求

适用于 iOS 和 Android 的 AIP 移动查看器应用支持以下文件类型和环境：

|要求  |说明  |
|---------|---------|
|**支持的操作系统版本**     | 最小移动操作系统包括： </br>-iOS 11  </br>-Android 6。0 </br></br>**注意**： Intel cpu 不支持 AIP 移动查看器应用。  |
|**支持的登录凭据**     | 通过以下方式之一登录到 AIP 移动查看器应用： </br></br>**工作或学校凭据。** 尝试使用你的工作或学校凭据登录。 如果有疑问，请与管理员联系，了解你的组织是否已使用移动设备扩展在本地 AD RMS，或使用 Azure 信息保护。 </br></br>**一个 Microsoft 帐户。** 如果使用个人电子邮件地址来保护文件，请使用 [Microsoft 帐户](https://signup.live.com)登录。 如果需要申请 Microsoft 帐户，可以使用自己的 Hotmail、Gmail 或其他电子邮件地址来执行此操作。 </br></br>**注意**：并非所有应用程序都能打开使用 Microsoft 帐户保护的内容。 有关详细信息，请参阅 [打开受保护文档的支持方案](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)。|
|**支持的文件类型**     | 支持的文件类型包括受保护的电子邮件、PDF 文件、图像和文本文件。 </br></br>例如，这些文件包括以下扩展名： **.rpmsg**、 **.pdf**、 **. ppdf**、 **. .pjpg**、 **.pjpeg**、 **ptiff** **、.ppng** **、. .ptxt**、 **. .pxml** </br></br>有关支持的文件类型的完整列表，请参阅 [AIP 客户端管理员指南](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)。|
| | |

## <a name="download-and-install-the-aip-app-for-your-device"></a>下载并安装适用于设备的 AIP 应用

如果你没有可用于打开受保护文件的 [Office 应用](/microsoft-365/compliance/sensitivity-labels-office-apps#sensitivity-label-capabilities-in-word-excel-and-powerpoint) ，请下载并安装 AIP 移动查看器应用。

从以下位置下载并安装移动查看器应用：

|位置  |详细信息/链接  |
|---------|---------|
|**iTunes**     | [![从 iTunes 安装。](../media/small/ios-icon-small.png)](https://apps.apple.com/app/microsoft-rights-management/id689516635)        |
|**Google Play**     |[![从 Google Play 安装。](../media/small/android-icon-small.png)](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)         |
|**公司门户**     |  如果你的移动设备由 Microsoft Intune 管理，则你可以从公司门户下载 AIP 移动查看器应用。 <br><br>有关详细信息，请与系统管理员联系。        |
|     |         |

## <a name="ios-view-protected-files-on-your-device"></a>iOS：在设备上查看受保护的文件

[安装 AIP 移动应用](#download-and-install-the-aip-app-for-your-device)后，打开受保护的电子邮件或文件。 

1. 如果系统提示你选择一个应用以打开该文件，请点击 "共享" 按钮以共享该文件。

    选择 "**通过 ... 共享文件**..."，然后选择 "**复制到 AIP 查看器**"。

    例如：

    :::image type="content" source="../media/ios-share-to-aip-viewer.png" alt-text="在 iOS 中共享到 AIP 查看器" border="false":::

1. 登录，或在出现提示时选择证书。

    经过身份验证后，你的电子邮件或文件将在 AIP 查看器中打开。
 
## <a name="android-view-protected-files-on-your-device"></a>Android：在设备上查看受保护的文件

[安装 AIP 移动应用](#download-and-install-the-aip-app-for-your-device)后，打开受保护的电子邮件或文件。 

1. 当系统提示选择应用时，选择 "AIP 查看器"：

    :::image type="content" source="../media/select-aip-viewer.png" alt-text="选择 AIP 查看器移动应用":::

1. 登录，或在出现提示时选择证书。

    经过身份验证后，你的电子邮件或文件将在 AIP 查看器中打开。


## <a name="admins-testing-the-aip-mobile-viewer-apps"></a>管理员：测试 AIP 移动查看器应用

大多数用户通常会使用 AIP 移动应用来打开受保护的电子邮件或文件，该电子邮件或文件不能使用其常规移动应用打开。

如果你是一位系统管理员，想要为你的组织测试 AIP 移动查看器应用程序，或者只是想亲自尝试一下，请使用下面的说明来完成整个过程。

1. 确保你有权访问设备上的 AIP 移动应用支持的文件类型。 

    例如，向自己发送以下受权限保护的文件之一：

    |文件类型  |说明  |
    |---------|---------|
    |**电子邮件 ( .rpmsg)**     | 使用其他设备（如 Windows 计算机上的 Outlook）向自己发送受权限保护的电子邮件，可以从移动设备访问该邮件。  |
    |**PDF**     | 1. 从 Windows 计算机上，使用 AIP 客户端 [保护 PDF](clientv2-classify-protect.md) 文件。 </br>2. 向自己发送受保护的 PDF，或将其上传到 SharePoint 受保护的库，并将其共享到你自己的电子邮件地址。        |
    |**Image (。 .ptxt、.pjpg 或 .ppng)**     | 1. 从 Windows 计算机上，使用 AIP 客户端 [保护文本或图像文件](clientv2-classify-protect.md) 。 </br></br>2. 向自己发送受保护的文件，或将其上传到 SharePoint 受保护的库，并将其共享到你自己的电子邮件地址。   |
| | |

1. 使用发送给你自己的电子邮件附件或链接在你的移动设备上打开受保护的文件。

    例如，受保护的电子邮件将以附件形式显示在你的常规电子邮件移动应用中。 

1. 当系统提示选择应用以打开受保护的电子邮件或文件时，请选择 " **AIP 查看器** " 应用。

1. 根据提示登录或选择证书。 

    经过身份验证后，AIP 查看器应用会显示电子邮件或文件。

> [!NOTE]
> 始终打开受保护的内容，以打开 AIP 应用。 在出现提示时，请不要尝试登录到应用程序，或从 AIP 查看器应用程序中打开受保护的文件。
> 

## <a name="next-steps"></a>后续步骤

使用以下方法之一来提供有关 AIP 移动查看器应用的反馈：

- 中转到 "**设置**" "  >  **发送反馈**"
- 在我们的[Yammer 网站](https://www.yammer.com/AskIPTeam)上发布你的问题

有关应用程序中支持的保护功能的详细信息，请参阅 [支持 Azure Rights Management 数据保护的应用程序](../requirements-applications.md)。
