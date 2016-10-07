---
title: "Windows 应用商店安装程序 | Azure RMS"
description: "Windows 应用商店应用程序可以使用 Microsoft Rights Management SDK 4.2 在其应用程序中启用集成信息保护。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 763e99e40bbe329305e97757e87d10b048cc62e9


---

# Windows 应用商店安装程序

Windows 应用商店应用程序可以使用 Microsoft Rights Management SDK 4.2 在其应用程序中启用集成信息保护（通过使用 Azure Active Directory Rights Management (AAD RM)）。

本主题将指导你完成环境设置过程，以创建自己的新应用。

-   [先决条件](#prerequisites)
-   [可选](#optional)
-   [配置开发环境](#configuring-your-development-environment)
-   [另请参阅](#see-also)

## 先决条件


开发系统上必须安装以下软件：

-   [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet) 操作系统
-   [适用于 Windows 8.1 的 Windows SDK](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) 或更高版本，或 Visual Studio Express 2012，后者包含在适用于 Windows 8.0/8.1 的 Windows SDK中。
-   适用于 Windows 应用商店应用程序的 MS RMS SDK 4.2 包。 有关详细信息，请参阅[入门](get-started.md)。
-   身份验证库：我们建议使用 [Azure AD 身份验证库](https://msdn.microsoft.com/en-us/library/jj573266.aspx)和其他可用的身份验证库。

有关 API 更新、设备和环境信息、发行说明和常见问题 (FAQ) 的信息，请阅读[新增功能](release-notes.md)主题。

## 可选

针对不想创建其自己的自定义 UI 的开发人员，我们的 UI 库为其提供了可重复使用的 UI，以进行使用和保护操作 - [适用于 Windows 应用商店应用的 UI 库](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore)。 我们还提供 Windows 应用商店应用程序示例应用程序 - [RMS 示例 Windows 应用商店的应用程序](https://github.com/AzureADSamples/rms-samples-for-windowsstore)。

## 配置开发环境


-   打开 Visual Studio。
-   依次单击“文件”、“新建”和“项目”。
-   在“新建项目”对话框中，单击“Visual C”**\#，选择“空白应用(Windows)”****，然后单击“确定”**。

    ![新建项目](../media/winrtsetup-newproj.png)

-   在“解决方案资源管理器”，右键单击你的项目，然后选择“添加引用”以打开“添加引用”对话框。

    ![添加引用](../media/winrtsetup-addref.png)

-   在“添加引用”对话框中，单击“浏览”，然后选择位于要将 SDK 包解压到其中的文件夹中的 *Microsoft.RightsManagement.dll* 文件。
-   **托管应用** - 要生成托管应用程序，将需要添加此引用；选择 **Windows 8.1** -&gt;**扩展**，并选中**适用于 Windows 的 Windows Visual C++ 运行时包**的复选框

    ![添加扩展](../media/winrtsetup-refmngr.png)

-   **添加功能** - 你的应用程序将需要“Internet（客户端和服务器）”功能来使用 SDK。 若要将此功能添加到你的应用程序中，请打开项目中的 *Package.appxmanifest* 文件，并导航到“功能”选项卡已进行添加。

你现在已准备就绪，可创建新 Windows 应用商店应用。

### 另请参阅

[入门](get-started.md)

[新增功能](release-notes.md)

[开发人员术语和概念](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows API 参考](/information-protection/sdk/4.2/api/winrt/Microsoft.RightsManagement)



<!--HONumber=Oct16_HO1-->


