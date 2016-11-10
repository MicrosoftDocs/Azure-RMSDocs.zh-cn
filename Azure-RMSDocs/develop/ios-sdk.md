---
title: "iOS 和 OS X 安装程序 | Azure RMS"
description: "通过 AAD RM，iOS 和 OS X 应用程序可使用 RMS SDK 4.2 在其应用程序中启用集成信息保护。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b31e5b72-e65e-450a-b1b8-d46e81e9fb34
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7c0b885c35dcac0237788a69486d8f736c97c0c4
ms.openlocfilehash: 96b71d26461559aa8e53960e7e8f3f748b7ebb1d


---

# <a name="ios-and-os-x-setup"></a>iOS 和 OS X 安装程序

借助 Azure Rights Management (Azure RMS)，iOS 和 OS X 应用程序可使用 Microsoft Rights Management SDK 4.2 在其应用程序中启用集成信息保护。

本主题将指导你完成环境设置过程，以创建自己的新应用。

**注意** 此 SDK 不支持 iPod Touch。


-   [必备条件](#prerequisites)
-   [可选](#optional)
-   [配置开发环境](#configuring-your-development-environment)
-   [另请参阅](#see-also)

## <a name="prerequisites"></a>先决条件

我们建议在开发系统上安装以下软件：

-   OS X 是所有 iOS 开发所必需的。
-   Xcode 版本 6.0 及更高版本

    Xcode 可通过 [Mac 应用商店](https://developer.apple.com/technologies/mac/)获取。

-   适用于 iOS 和 OS X 的 MS RMS SDK 4.2 包。有关详细信息，请参阅[入门](get-started.md)。

    此 SDK 可用于为 iOS 7.0、OS X 10.8 及更高版本进行开发。

-   身份验证库：建议使用 [Azure AD 身份验证库 (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx)。 但是也可使用其他支持 OAuth 2.0 的身份验证库。

    有关详细信息，请参阅 [ADAL for iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) 或 [ADAL for OS X](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal)

有关 API 更新、发行说明和常见问题解答 (FAQ) 的信息，请阅读[新增功能](release-notes.md)主题。

## <a name="optional"></a>可选

针对不想自行创建自定义 UI 的开发人员，我们的 UI 库为其提供了可重复使用的 UI，以进行使用和保护操作 -[适用于 iOS 的 UI 库和示例应用](https://github.com/AzureAD/rms-sdk-ui-for-ios)。

## <a name="configuring-your-development-environment"></a>配置开发环境

-   若要创建新项目，请在“文件”上单击“新建”，然后单击“项目”。
-   选择“单视图应用程序”。

    ![创建新项目](../media/iOS-Project.png)

-   输入新项目的名称和标识符。

    ![为项目命名](../media/iOS-project-options.png)

-   单击“下一步”，然后选择项目的位置。
-   若要添加面向 iOS 框架的 **MSRightsManagement** 框架，请将 SDK 安装文件夹中的 .framework 文件夹拖入“项目导航器”的“框架”部分。

    ![设置位置](../media/ios-add-dependencies-01a.png)

-   选择“为添加的所有文件夹创建组”选项按钮，然后清除“将项目复制到目标组的文件夹(若必需)”复选框。

    此操作将保留对 SDK 安装文件夹的引用，而不是创建副本。

    ![设置对 SDK 安装文件夹的引用](../media/iOS-create-groups.png)

-   若要添加适用于资源包的 MS RMS SDK 4.2，请将 MSRightsManagement.framework/Resources 文件夹中的 MSRightsManagementResources.bundle 文件拖入“项目导航器”的“框架”部分。

    ![添加资源包](../media/iOS-add-resource-bundle-02a.png)

-   按复制框架时的方式一样，选择“为添加的所有文件夹创建组”选项按钮，然后清除“将项目复制到目标组的文件夹(若必需)”复选框。
-   SDK 依赖于其他框架，包括：**CoreData****MessageUI****SystemConfiguration****Libresolv** 和 **Security**。 若要添加这些框架，请导航至目标的“摘要”面板的“已链接框架和库”部分，然后展开此部分以添加框架。

    **UIKit** 和 **Foundation** 框架是必需的，且通常默认存在。

    ![添加资源](../media/iOS-add-libraries.png)

-   将 **-ObjC** 标记添加至目标“生成设置”的“其他链接器标记”中。

    ![添加生成设置](../media/iOS-linker-flags.png)

-   现在你的“项目导航器”看起来应类似此树。

    ![新建项目](../media/iOS-verify-setup-01a.png)

-   你现已准备就绪，可自行创建新的 iOS/OS X 应用。

### <a name="see-also"></a>另请参阅

* [入门](get-started.md)

* [新增功能](release-notes.md)

* [开发人员术语和概念](core-concepts.md)

* [iOS / OS X API 参考](https://msdn.microsoft.com/library/dn758306.aspx)

 

 



<!--HONumber=Nov16_HO1-->


