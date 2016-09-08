---
title: "Android 安装程序 |Azure RMS"
description: "Android 应用程序可以使用 Microsoft Rights Management SDK 4.2 在其应用程序中启用集成信息保护。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 986f6932-159b-4791-bd1a-7640a83ee792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 72196edd630a1934f2c0b6e755771039fceaa795


---

# Android 安装程序

Android 应用程序可以通过使用 Azure Active Directory Rights Management (AAD RM)，利用 Microsoft Rights Management SDK 4.2 在其应用中启用集成信息保护。

本主题将指导你完成环境设置过程，以创建自己的新应用。

-   [先决条件](#prerequisites)
-   [可选](#optional)
-   [配置开发环境](#configuring-your-development-environment_)
-   [另请参阅](#see-also)

## 先决条件

我们建议在开发系统上安装以下软件：

-   Windows 或 OS X 操作系统，用于运行 [Eclipse](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 开发环境。
-   本指南假定你在使用从 Eclipse Juno 4.2 开始的 Eclipse SDK 并使用默认安装。
-   从 Java 1.6 开始的 Java。
-   [Android 开发人员工具 (ADT) 插件](http://developer.android.com/sdk/installing/index.html)。 注意 - 可能会请你重新启动 Eclipse 以完成安装。

     

-   Android 的 MS RMS SDK 4.2 包。 有关详细信息，请参阅[入门](get-started.md)。

    此 SDK 可以用于为 Android 4.0.3（API 级别 15）及更高版本进行开发。

-   身份验证库：建议使用 [Azure AD 身份验证库 (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx)。 但是也可使用其他支持 OAuth 2.0 的身份验证库。

    有关详细信息，请参阅 [ADAL for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

    **注意**  如果应用程序未使用 ADAL 库作为 OAuth 2.0 身份验证库，则你应该查看本 Android 指南 [一些 SecureRandom 想法](http://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html)。

     

有关 API 更新、发行说明和常见问题解答 (FAQ) 的信息，请阅读[新增功能](release-notes.md)主题。

## 可选

我们的 UI 库可为不想创建自己的自定义 UI 的开发人员提供用于使用和保护操作的可重用 UI - [适用于 Android 的 UI 库和示例](https://github.com/AzureAD/rms-sdk-ui-for-android)。

## 配置开发环境

**注意**  MS RMS SDK 4.2 预览版本中：在此预览版本中，屏幕截图尚未更新为可显示路径名称从 com/microsoft/protection 到 com/microsoft/rightsmanagment 的更改。 不过文本已进行了更新。

 
-   打开 Eclipse 开发环境。
-   若要创建新 Android 应用程序项目，请在 **“文件”** 菜单上，单击 **“新建”**，单击 **“项目”**，然后选择 **“Android 应用程序项目”**。

    ![创建新的 Android 应用程序](../media/Android-setup-01c.png)

-   输入应用程序名称。 项目名称和包名称根据应用程序名称进行填充。
-   单击 **“下一步”**，然后选择要用于创建工作区的位置。

    ![输入应用程序名称](../media/Android-setup-02a.jpg)

-   单击 **“下一步”**，然后为应用选择图标。

    ![为应用选择图标](../media/Android-setup-03.png)

-   单击 **“下一步”**，然后选择 **“空白活动”** 以创建活动。

    ![创建活动](../media/Android-setup-04.png)

-   单击 **“下一步”** 并提供活动的名称。 可以将 *MainActivity* 保留为默认名称，并且布局名称为 *activity\_main*。

    ![提供活动的名称](../media/Android-setup-05a.jpg)

-   单击 **“完成”**。

    ![完成创建](../media/Android-setup-06.jpg)

-   项目以及主活动类 *MainActivity.java* 已创建。

**引用 SDK**

-   导航到在其中提取 *adrms\_android\_sdk.zip* 的文件夹。 在“SDK > com > microsoft > rightsmanagement”文件夹中，确保文件 *.classpath*、*.project* 和 *project.properties* 未标记为只读。
-   若要引用 SDK，必须将它导入工作区中。

    在 Eclipse 中，单击 **“文件”**。 在 **“文件”** 菜单上，单击 **“导入”**。 在 **“导入”** 对话框中，选择 **“Android/现有 Android 代码到工作区”**。

    ![将其导入到工作区](../media/Android-setup-07.png)

-   单击“下一步” 。 导航以选择在其中提取 *adrms\_android\_sdk.zip* 的文件夹。 SDK 应作为 **com.microsoft.rightsmanagement** 显示在列表中。

    ![导航到“选择文件夹”](../media/Android-setup-08c.jpg)

-   单击 **“完成”** 时，SDK 项目显示为以前创建的应用程序的同级。

    ![该 SDK 项目将显示为应用程序的同级](../media/Android-setup-09.jpg)

-   右键单击 **“项目”** 图标并查看项目的属性。
-   导航到 **“Android”** 选项卡。
-   单击 **“添加”**，然后从工作区中选择 *com.microsoft.rightsmanagement* 库。

    ![添加库](../media/Android-setup-10b.jpg)

-   单击" **确定**"。

    因为 MS RMS SDK 4.2 与 AAD RM 相连接，所以必须向应用程序授予 **INTERNET** 和 **ACCESS\_NETWORK\_STATE** 权限。 为此，请在项目的根目录中打开 *AndroidManifest.xml* 文件。

    若要添加权限，请单击 **“添加”**，然后选择 **“使用权限”**。

    ![添加权限](../media/Android-setup-11d.jpg)

-   可以通过在文本编辑器视图中查看清单来验证清单步骤。 确保显示以下行：


    <uses-sdk      android:minSdkVersion="15"      android:targetSdkVersion="19"/> <uses-permission android:name="android.permission.INTERNET"/> <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> <uses-permission/>


**注意**  SDK 使用 *android.support.v4*

-   你现在已准备就绪，可创建新 Android 应用。

### 另請參閱

[入门](get-started.md)

[新增功能](release-notes.md)

[开发人员术语和概念](core-concepts.md)

[Android API 参考](android-namespaces.md)

 

 



<!--HONumber=Aug16_HO4-->


