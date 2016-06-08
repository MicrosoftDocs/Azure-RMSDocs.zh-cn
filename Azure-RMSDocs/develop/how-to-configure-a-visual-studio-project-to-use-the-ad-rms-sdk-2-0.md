---
# required metadata

title: 配置 Visual Studio | Azure RMS
description: 有关如何配置 Visual Studio 项目以使用 RMS SDK 2.1 的说明。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 此 SDK 内容不是最新的。 在短时间内，请在 MSDN 上找到[最新版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)的文档。 **
# 配置 Visual Studio

本主题包含有关如何配置 Visual Studio 项目以使用 Rights Management Services SDK 2.1 的说明。

## 先决条件

-   [安装 SDK](create-your-first-rights-aware-application.md)

**说明**

### 步骤 1：配置 Visual Studio 项目以使用 RMS SDK 2.1

这些说明特定于 Microsoft Visual Studio 2010。 如果使用不同版本的 Microsoft Visual Studio，则设置对话框可能略有不同。

这些说明适用于构建本机 32 位应用程序。

1.  将 RMS SDK 2.1 包含目录添加到 Visual Studio 2010 项目。

    在**配置属性**下，选择 **VC++ 目录**，然后将 RMS SDK 2.1 包含目录 **$(MSIPCSDKDIR)\\inc** 添加到**包含目录**字段。

    ![配置属性包含目录字段](../media/include_directories.png)

2.  将 RMS SDK 2.1 库目录添加到 Visual Studio 2010 项目。

    在 **“配置属性”** 下，选择 **“VC++ 目录”**，然后针对你的平台将 RMS SDK 2.1 库目录添加到 **“库目录”** 字段。

    -   对于 Win32，使用 **$(MSIPCSDKDIR)\\lib**
    -   对于 x64，使用 **$(MSIPCSDKDIR)\\lib\\x64**

    ![配置属性库目录字段](../media/library_directories.png)

3.  将 RMS SDK 2.1 库文件添加为 Visual Studio 2010 依赖项。

    在**链接器**下，选择**输入**，然后将 RMS SDK 2.1 库文件 **Msipc.lib** 和 **Msipc\_s.lib** 添加到**附加依赖项**字段。

    ![链接器库依赖项字段](../media/additional_dependencies.png)

4.  将 RMS SDK 2.1 动态链接库 (DLL) 添加为延迟加载的 DLL。

    在 **“链接器”** 下，选择 **“输入”**，然后将 RMS SDK 2.1 DLL 文件 **Msipc.dll** 添加到 **“延迟加载的 DLL”** 字段。

    ![链接器延迟加载的库字段](../media/delay_loaded.png)

5.  为生成的二进制文件创建版本信息。

    在 **“解决方案资源管理器”** 下，选择 **“资源文件”**，然后将二进制文件名称添加到 **“OriginalFileName”** 字段。

    ![解决方案资源管理器资源文件字段](../media/original_file_name.png)

## 相关主题

* [使用方法](how-to-use-msipc.md)
* [安装 SDK](create-your-first-rights-aware-application.md)
 

 





<!--HONumber=Jun16_HO1-->


