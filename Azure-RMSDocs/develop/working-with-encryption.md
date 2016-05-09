---
# required metadata

title: 使用加密 | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 088c98f9-f06e-4aae-8fac-bc7605e545f5

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# 使用加密

本主题将针对加密包，并显示其使用的一些代码段。

## 新的默认 AES 256 的支持

假设针对 RMS SDK 2.1 2015 年 3 月的更新版本或更高版本进行构建，则无需其他代码即可使用基于的 *AES 256* 的加密，因为它是新的默认值。 应该认真考虑使用 *AES 256* 此版本的其他安全优势来更新你的应用程序。

> [!IMPORTANT]
> 对 *AES 256* 受保护的文件的使用支持自 [2014 年 10 月的版本](release-notes-rtm.md)起已存在。 如果正在运行使用 2014 年 10 月之前的 SDK 版本构建的应用程序，此更新将中断该应用程序。 请确保正在构建的应用程序的客户使用更新后的 SDK，或愿意立即更新该应用程序的最新版本。

 
## API 加密支持

从 [2015 年 3 月更新](release-notes-rtm.md)开始，我们已经将下列三个标记合并到我们的 API 及其关联的加密包中：

-   IPC_ENCRYPTION_PACKAGE_AES256_CBC4K
-   IPC_ENCRYPTION_PACKAGE _AES128_CBC4K
-   IPC_ENCRYPTION_PACKAGE _AES128_ECB（也是不推荐使用的算法）

加密包标记（请参阅[**首选加密**](/rights-management/sdk/2.1/api/win/constants#msipc_preferred_encryption)）可与我们的新许可证标记 **IPC_LI_PREFERRED_ENCRYPTION_PACKAGE** 结合使用。

以下是一些简单的代码段，用于演示如何使用新的许可证属性。

## 不推荐使用的算法

我们不再公开 API 中的 **IPC_LI_DEPRECATED_ENCRYPTION_ALGORITHMS** 标记。 这意味着，如果以后的应用程序引用此标记，则这些应用程序将无法再编译，但已使用它构建的应用程序可以继续工作，因为我们遵循 API 代码中的专用标记。

只需通过更改一个标记便可利用旧的不推荐使用的加密算法标记的益处。 请参阅下面的代码段示例。

## 使用 AES 256 CBC4K 保护文件

不需要代码中的更改，*AES 256* CBC4K 是默认值。

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    

## 使用 AES-128 CBC4K 保护文件

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    
    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K; 
    
    hr = IpcSetLicenseProperty(pLicenseHandle, 
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);
    

## 使用 AES-128 ECB（不推荐使用的算法）保护文件

此示例还演示支持*不推荐使用的算法*的新方法。

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    
    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;
    
    hr = IpcSetLicenseProperty(pLicenseHandle, 
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE, 
                           &amp;dwEncryptionMode);
    
 

 





<!--HONumber=Apr16_HO3-->

