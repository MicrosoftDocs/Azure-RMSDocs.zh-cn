---
# required metadata

title: 测试启用权限的应用程序 | Azure RMS
description: 描述测试 RMS SDK 2.1 启用权限的应用程序所需完成的步骤。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 834B7242-31D3-4275-A892-CFE95A61E29E
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
# 测试启用权限的应用程序

本主题描述测试 Rights Management Services SDK 2.1 启用权限的应用程序所需完成的步骤。

要发布和使用受保护的内容，Rights Management Services (RMS) 应用程序将利用多种证书和许可证，每一种包括最终回溯到 Microsoft 证书颁发机构的证书链。 Microsoft 提供以下层次结构：

-   预生产层次结构可用于开发和测试应用程序。
-   生产层次结构必须由发布的应用程序使用。

我们建议在开发应用程序时使用预生产层次结构。 从而可在不与 Microsoft 签订生产许可证协议的情况下进行使用。

> [!IMPORTANT]
> 推荐的最佳做法是首先通过针对 RMS 服务器的 RMS 预生产环境测试 RMS SDK 2.1 应用程序。 然后，如果你希望客户能通过 Azure RMS 服务使用你的应用程序，可在此环境中测试。 有关详细信息，请参阅[使服务应用程序可与基于云的 RMS 一起使用](how-to-use-file-api-with-aadrm-cloud.md)。

 

### 先决条件

-   RMS SDK 2.1 开发环境设置。 有关详细信息，请参阅[设置预生产开发环境](how-to-set-up-the-pre-production-development-environment.md)。
-   有关示例应用程序，请参阅 [IPCHelloWorld - 一个示例应用程序](how-to-build-your-first-application.md)。

说明

### 步骤 1：

创建和生成启用权限的应用程序。 请参阅以上“先决条件”部分了解选项。

### 第 2 步：生成使用预生产证书链的应用程序清单

运行前，必须生成应用程序的清单。

**注意** 如果你的应用程序使用服务器 API 模式 (**IPC\_API\_MODE\_SERVER**)，则无需使用应用程序清单。 你可以针对生产 AD RMS 服务器测试应用程序，并且在切换到生产环境时无需获取生产许可证。 有关服务器模式应用程序的详细信息，请参阅[应用程序类型](application-types.md)。

 

此过程也被称为对应用程序进行签名。 可以使用随 SDK 一起安装的生产证书链或预生产证书链来生成清单。 我们建议在开发过程中使用预生产证书链。

关于密钥和证书链的详细信息，请参阅[了解证书链](understanding-certificate-chains.md)。

有关如何使用生产证书链对应用程序进行签名的信息，请参阅[切换到生产环境](switching-to-the-production-environment.md)。

要使用预生产证书链生成应用程序清单，请在开发计算机上执行以下步骤：

1.  将以下文件从其安装目录复制到与你的应用程序相同的文件夹。

    %MSIPCSdkDir%\\Tools\\Genmanifest.exe

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningprivkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningpubkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsignsdk\_client.xml

    %MSIPCSdkDir%\\bin\\YourAppName.isv.mcf

2.  在应用程序文件夹中，将清单配置文件 YourAppName.isv.mcf 重命名为你的应用程序的名称，最后附加上文件扩展名 .mcf。 例如，如果你的应用程序名为 MyApp.exe，则将 YourAppName.isv.mcf 重命名为 MyApp.exe.mcf。

3.  使用文本编辑器将你的应用程序添加到清单配置文件。 为此，将 .mcf 文件内模块列表中的 &lt;YourAppName&gt;.exe 占位符文本替换为你的应用程序名称；例如 MyApp.exe。

    如果 .mcf 文件在未经修改的情况下使用，则签名过程将生成错误。

4.  运行 Genmanifest.exe 生成应用程序清单。 这也被称为对应用程序进行签名。 此操作的输出应为 .man 文件。 例如，如果你的应用程序名为 MyApp.exe，且清单配置文件名为 MyApp.exe.mcf，则运行以下命令：

    **genmanifest.exe -chain isvtier5appsignsdk\_client.xml MyApp.exe.mcf MyApp.exe.man**

### 步骤 3：运行应用程序

你可以从任何目录运行你的应用程序，但应用程序清单 (MyApp.exe.man) 必须与可执行文件 (MyApp.exe) 位于同一目录。

-   **使用 RMS 1 框环境**

    如果使用 RMS 单框环境来测试应用程序，则将应用程序可执行文件和应用程序清单复制到单框环境中的任何目录，然后运行应用程序。

    有关 RMS 单框环境的信息，请参阅[设置测试环境](how-to-set-up-your-test-environment.md)。

-   **使用预生产服务器配置**

    如果要针对为预生产配置的 RMS 服务器测试应用程序，请确保已在该应用程序要在其上运行的计算机上配置了 Active Directory Rights Management Services Client 2.1；例如，在你的开发计算机上。 然后确保应用程序可执行文件和应用程序清单位于该计算机中的相同目录，然后运行应用程序。

    有关如何在计算机上配置客户端的信息，请参阅[配置客户端](how-to-configure-the-ad-rms-client-2-0.md)。 有关安装 RMS 服务器的信息，请参阅 [安装和配置服务器](how-to-install-and-configure-an-rms-server.md)。

## 相关主题

* [使用方法](how-to-use-msipc.md)
* [配置客户端](how-to-configure-the-ad-rms-client-2-0.md)
* [安装并配置服务器](how-to-install-and-configure-an-rms-server.md)
* [IPCHelloWorld - 一个示例应用程序](how-to-build-your-first-application.md)
* [设置预生产开发环境](how-to-set-up-the-pre-production-development-environment.md)
* [切换到生产环境](switching-to-the-production-environment.md)
* [设置测试环境](how-to-set-up-your-test-environment.md)
* [了解证书链](understanding-certificate-chains.md)
 

 





<!--HONumber=Jun16_HO1-->


