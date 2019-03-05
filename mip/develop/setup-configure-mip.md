---
title: Microsoft 信息保护 (MIP) SDK 的安装和配置
description: 提供安装和配置先决条件，以便使用 Microsoft 信息保护 SDK 构建应用程序。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/30/2019
ms.author: mbaldwin
ms.openlocfilehash: c61b2c08cf0cb0fc59942bad3b5bb3fdbc47832c
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331964"
---
# <a name="microsoft-information-protection-mip-sdk-setup-and-configuration"></a>Microsoft 信息保护 (MIP) SDK 的安装和配置 

快速入门和教程文章主要介绍使用 MIP SDK 库和 API 构建应用程序。 本文介绍如何安装和配置 Office 365 订阅和客户端工作站，为使用 SDK 做准备。

## <a name="prerequisites"></a>先决条件

在开始之前，请务必查看以下主题：

- [什么是 Office 365 安全与合规中心？](https://docs.microsoft.com/office365/securitycompliance/security-and-compliance)
- [什么是 Azure 信息保护？](/azure/information-protection/understand-explore/what-is-information-protection)
- [如何使用 Azure 信息保护进行保护？](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

> [!IMPORTANT]
> **为了尊重用户隐私，必须要求用户先同意才能启用自动日志记录。** 下面的示例是 Microsoft 用于日志记录通知的标准消息：
>
> *启用错误和性能日志记录即表示同意向 Microsoft 发送错误和性能数据。Microsoft 会通过 Internet 收集错误和性能数据（统称“数据”）。Microsoft 利用此数据来保证并改进 Microsoft 产品和服务的质量、安全性和完整性。例如，会分析性能和可靠性（如使用哪些功能、功能的响应速度、设备性能、用户界面交互和遇到的任何产品问题）。数据还包括当前运行的软件以及 IP 地址的配置信息。*

## <a name="sign-up-for-an-office-365-subscription"></a>注册 Office 365 订阅

许多 SDK 示例都需要访问 Office 365 订阅的权限。 如果尚未注册，请务必注册以下订阅类型之一：

| 名称 | 注册 |
|------|---------|
| Office 365 企业版 E3 试用版（30 天免费试用） | https://go.microsoft.com/fwlink/p/?LinkID=403802 |
| Office 365 企业版 E3 或 E5 | https://products.office.com/business/office-365-enterprise-e3-business-software |
| 企业移动性 + 安全性 E3 或 E5 | https://www.microsoft.com/cloud-platform/enterprise-mobility-security |
| Azure 信息保护高级版 P1 或 P2 | https://azure.microsoft.com/pricing/details/information-protection/ |
| Microsoft 365 E3、E5、或 F1 | https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans | 

## <a name="configure-sensitivity-labels"></a>配置敏感度标签

如果当前正在使用 Azure 信息保护，则必须迁移到 Office 365 安全与合规中心的标签。 有关该过程的详细信息，请参阅[如何将 Azure 信息保护标签迁移到 Office 365 安全与合规中心](/azure/information-protection/configure-policy-migrate-labels)。 

## <a name="configure-your-client-workstation"></a>配置客户端工作站

接下来，完成以下步骤以确保正确安装和配置客户端计算机。

1. 如果使用 Windows 10 工作站：

   - 请使用 Windows 更新，将计算机更新到 Windows 10 Fall Creators Update（版本 1709）或更高版本。 验证当前的版本：
     - 单击左下角的 Windows 图标。
     - 键入“关于电脑”并按 Enter。
     - 向下滚动到“Windows 规范”并查看“版本”。

   - 请确保工作站启用了“开发人员模式”：
     - 单击左下角的 Windows 图标。
     - 当看到“使用开发人员功能”项时，请键入“使用开发人员功能”并按 Enter。
     - 在“设置”对话框中，“针对开发人员”选项卡，在“使用开发人员功能”下，选择“开发人员模式”选项。
     - 关闭“设置”对话框。

2. 使用以下工作负载和可选组件安装 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)：
   - **通用 Windows 平台开发** Windows 工作负载及以下可选组件：
     - **C++ 通用 Windows 平台工具**
     - Windows 10 SDK 10.0.16299.0 SDK 或更高版本（如果未包含在内）
   - **C++ 桌面开发** Windows 工作负载及以下可选组件：
     - Windows 10 SDK 10.0.16299.0 SDK 或更高版本（如果未包含在内） 

     [![Visual Studio 设置](media/setup-mip-client/visual-studio-install.png)](media/setup-mip-client/visual-studio-install.png#lightbox)

3. 安装[ADAL.PS PowerShell 模块](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2): 

   - 由于安装模块需要管理员权限，因此首先需要：

     - 使用具有管理员权限的帐户登录到计算机。
     - 使用提升后的权限运行 Windows PowerShell 会话（以管理员身份运行）。

   - 然后运行 `install-module -name adal.ps` cmdlet：

     ```powershell
     PS C:\WINDOWS\system32> install-module -name adal.ps

     Untrusted repository
     You are installing the modules from an untrusted repository. If you trust this repository, change its
     InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
     'PSGallery'?
     [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A

     PS C:\WINDOWS\system32>
     ```

4. 下载 SDK 文件：

   MIP SDK 支持以下平台，使用单独的下载包的每个受支持的平台/语言：  

   [!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

   **Tar.gz/。Zip 下载**

   Tar.gz 和。Zip 下载包含其他压缩的文件，分别对应于每个 API。 压缩的文件命名，如下所示，其中\<API\> = `file`， `protection`，或`upe`，以及\<OS\> = 平台： `mip_sdk_<API>_<OS>_1.0.0.0.zip (or .tar.gz)`。 例如，将在 Debian 上保护 API 的二进制文件和标头文件： `mip_sdk_protection_debian9_1.0.0.0.tar.gz`。 每个包含的.tar.gz/.zip 拆分为三个目录：

   - **箱：** 编译二进制文件的每个平台体系结构中，在适用的情况。
   - **包括：** 标头文件 （c + +）。
   - **示例：** 示例应用程序的源代码。
    
   **NuGet 包**

   如果正在进行 Visual Studio 开发，也可以通过 NuGet 包管理器控制台安装 SDK：

    ```console
    Install-Package Microsoft.InformationProtection.File
    Install-Package Microsoft.InformationProtection.Policy
    Install-Package Microsoft.InformationProtection.Protection
    ```  

5. 如果不使用 NuGet 包，将 SDK 二进制文件的路径添加到 PATH 环境变量。 路径变量允许相关二进制文件 (Dll) 要查找在运行时，客户端应用程序 （可选）：

   如果使用 Windows 10 工作站：

   - 单击左下角的 Windows 图标。
   - 看到“编辑系统环境变量”项目时，键入“路径”并按 Enter。
   - 在“系统属性”对话框中，单击“环境变量”。
   - 在“环境变量”对话框中，单击\<用户\>“用户变量”下的“路径”变量行，然后单击“修改...”。
   - 在“编辑环境变量”对话框中，单击“新建”，创建一个新的可编辑行。 使用 `file\bins\debug\amd64`、`protection\bins\debug\amd64` 和 `upe\bins\debug\amd64` 子目录的完整路径，为每个子目录添加一个新行。 SDK 目录以 `<API>\bins\<target>\<platform>` 格式存储，其中：
     - \<API\> = `file`、`protection`、`upe`
     - \<目标\> = `debug`、`release`
     - \<平台\> =  `amd64` (x64)， `x86`，等等。
   
   - 完成更新“路径”变量后，单击“确定”。 然后在返回到“环境变量”对话框时单击“确定”。

6. 从 GitHub （可选） 下载 SDK 示例：

   - 如果还没有 GitHub，请先创建一个 [GitHub 配置文件](https://github.com/join)。
   - 然后安装最新版本的 [Software Freedom Conservancy Git 客户端工具 (Git Bash)](https://git-scm.com/download/)
   - 使用 Git Bash，下载感兴趣的示例：
     - 使用以下查询查看存储库： https://github.com/Azure-Samples?utf8=%E2%9C%93&q=MipSdk。 
     - 使用 Git Bash，使用 `git clone https://github.com/azure-samples/<repo-name>` 下载每个示例存储库。

## <a name="register-a-client-application-with-azure-active-directory"></a>向 Azure Active Directory 注册将客户端应用程序

作为 Office 365 订阅预配过程的一部分，创建一个关联的 Azure Active Directory (Azure AD) 租户。 Azure AD 租户为 Office 365 用户帐户和应用程序帐户提供标识和访问管理。 应用程序需要应用程序帐户才能访问受保护的 API（例如 MIP API）。

对于运行时的身份验证和授权，帐户由安全主体表示，该安全主体派生自帐户的标识信息。 表示应用程序帐户的安全主体称为[*服务主体*](/azure/active-directory/develop/developer-glossary#service-principal-object)。 

在 Azure AD 中注册应用程序帐户以用于快速入门和 MIP SDK 示例：

  > [!IMPORTANT] 
  > 要访问 Azure AD 租户管理以创建帐户，需要使用用户帐户登录 Azure 门户，该用户帐户应是[订阅上“所有者”角色](/azure/billing/billing-add-change-azure-subscription-administrator)的成员。 根据租户的配置，可能还需要成为“全局管理员”目录角色的成员才能[注册应用程序](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)。
  > 建议使用受限帐户进行测试。 请确保该帐户仅具有访问必要 SCC 终结点的权限。 日志记录系统可收集通过命令行传递的明文密码。

1. 按照中的步骤[与 Azure AD 注册应用，注册新的应用程序](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad#register-a-new-application-using-the-azure-portal)部分。 出于测试目的，在完成指导步骤时，请对给定属性使用以下值： 
    - **应用程序类型** - 选择“本机”，因为 SDK 演示的应用程序是本机安装的控制台应用程序。 OAuth2 将本机应用程序视为“公共”客户端，因为它们无法以安全的方式存储/使用应用程序凭据。 与基于服务器的“机密”应用程序（如 Web 应用程序）不同，后者使用自己的凭据进行注册。 
    - **重定向 URI** - 由于 SDK 使用简单的控制台客户端应用程序，因此请使用格式为 `<app-name>://authorize` 的 URI。

2. 完成后，将返回“已注册的应用”页面查看新的应用程序注册。 请将 GUID 复制并保存在“应用程序 ID”字段中，以便在快速入门中使用。 

3. 然后单击“设置”，添加客户端需要访问的 API 和权限。 在“设置”页面上，单击“必需权限”。

4. 现在，将添加应用程序在运行时需要的 MIP API 和权限：
   - 在“必需权限”页面上，单击“添加”。 
   - 在“添加 API 访问”页面上，单击“选择 API”。
   - 在“选择 API”页面上，单击“Microsoft Rights Management Services”API，然后单击“选择”。
   - 上**启用访问权限**API 的可用权限页上，单击"**创建和访问受保护的内容的用户**"，然后**选择**，然后**完成**.

5. 重复步骤 #4，但这次当进入“选择 API”页面时，需要搜索 API。
   - 在“选择 API”页面的搜索框中，键入“Microsoft 信息保护同步服务”，然后单击 API 并单击“选择”。
   - 在 API 可用权限的“启用访问权限”页面上，单击“为用户创建并授权访问受保护的内容”，单击“选择”，再单击“完成”

6. 当返回“必需权限”页面时，请单击“授予权限”，然后单击“是”。 此步骤预先同意应用程序使用该注册，在指定权限下访问 API。 如果以全局管理员身份登录，则会为运行该应用程序的租户中的所有用户记录同意；反之，它仅适用于你的个人用户帐户。 

完成后，应用程序注册和 API 权限应类似于以下示例：

   [![Azure AD 应用注册](media/setup-mip-client/aad-app-registration.png)](media/setup-mip-client/aad-app-registration.png#lightbox)


将 Api 和权限添加到注册的详细信息，请参阅[配置客户端应用程序以访问 web Api](/azure/active-directory/develop/quickstart-v1-update-azure-ad-app#configure-a-client-application-to-access-web-apis)。 此处可以找到有关添加客户端应用程序所需的 API 和权限信息。  

## <a name="request-an-information-protection-integration-agreement-ipia"></a>请求信息保护集成协议 (IPIA)

您可以发布使用 MIP 开发的应用程序之前，必须申请并完成与 Microsoft 达成的正式协议。

1. 向 [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Requesting%20IPIA%20for%20<company-name>) 发送一封包含以下信息的电子邮件以获取 IPIA：

   **主题：** 为公司名称请求 IPIA

   电子邮件的正文中应包含：
   - 应用程序和产品名称
   - 请求者的姓氏和名字
   - 请求者的电子邮件地址

2. 收到 IPIA 请求后，我们会将一份表格（Word 文档格式）发送给你。 请查看 IPIA 的条款和条件，然后将包含以下信息的表格通过电子邮件发送到 [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=IPIA%20Response%20for%20<company-name>)：

   - 公司依法登记的名称
   - 公司注册地的州/省（美国/加拿大）或国家/地区
   - 公司 URL
   - 联系人的电子邮件地址
   - 公司的其他地址（可选）
   - 公司应用程序名称
   - 应用程序的简要描述
   - Azure 租户 ID
   - 应用程序的*应用程序 ID*
   - 用于紧急情况通信的公司联系人、电子邮件和电话号码

3. 收到你的表格后，我们会将用于数字签名的最终 IPIA 链接发送给你。 你在协议上签名后，协议将由相应的 Microsoft 客户代表签名，协议就此完成。

### <a name="already-have-a-signed-ipia"></a>已有已签名的 IPIA？

如果已有已签名的 IPIA 并希望为要发布的应用程序添加新的应用程序 ID，请发送电子邮件至 [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Updating%20IPIA%20for%20<company-name>)，向我们提供以下信息：

- 公司应用程序名称
- 应用程序的简要描述
- Azure 租户 ID (即使相同前面所述)
- 应用程序的应用程序 ID
- 用于紧急情况通信的公司联系人、电子邮件和电话号码

在发送电子邮件，允许最多 72 个小时的回执确认。

## <a name="next-steps"></a>后续步骤

- 如果您是 c + + 开发人员
  - 请务必阅读[观察者概念](concept-async-observers.md)开始快速入门部分中，若要了解有关 c + + Api 的异步特性之前。
  - 如果你已准备好获取 SDK 的一些经验，开始[快速入门：客户端应用程序初始化 （c + +）](quick-app-initialization-cpp.md)。
- 如果你是C#开发人员，如果你已准备好获取一些经验 SDK，请使用启动[快速入门：客户端应用程序初始化 (C#)](quick-app-initialization-csharp.md)。


