---
title: "通过使用 RMS 共享应用删除保护 - AIP"
description: "有关删除之前使用 RMS 共享应用程序保护的文件保护（即取消文件保护）的说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 370b19894efb53604c798b38be02dda3f8804b8b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="remove-protection-from-a-file-by-using-the-rights-management-sharing-application"></a>使用 Rights Management 共享应用程序移除对文件的保护

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、具有 SP1 的 Windows 7、Windows 8、Windows 8.1*

若要移除之前使用 RMS 共享应用程序保护的文件保护（即取消文件保护），请从文件资源管理器中使用“移除保护”选项  。

> [!IMPORTANT]
> 你必须是文件所有者才能移除保护。

## <a name="to-remove-protection-from-a-file"></a>移除对文件的保护

1.  在文件资源管理器中，右键单击文件（例如 Sample.ptxt），选择“使用 RMS 保护”，单击“就地保护”，然后单击“移除保护”：

    ![删除 RMS 共享应用程序的保护菜单选项](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    系统可能会提示你输入凭据。

注意：如果看不到这些选项，则很可能你的计算机上未安装 RMS 共享应用程序、未安装最新版本，或必须重启计算机才能完成安装。 有关如何安装共享应用程序的详细信息，请参阅[下载和安装 Rights Management 共享应用程序](install-sharing-app.md)。

原始的受保护文件（例如 Sample.ptxt）将会删除，并替换为一个同名但文件扩展名不受保护的文件（例如 Sample.txt）。

## <a name="examples-and-other-instructions"></a>示例和其他说明
有关如何使用 Rights Management 共享应用程序以及操作说明的示例，请参阅以下 Rights Management 共享应用程序用户指南部分：

-   [使用 RMS 共享应用程序的示例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [要执行什么操作？](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>另请参阅
[权限管理共享应用程序用户指南](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]