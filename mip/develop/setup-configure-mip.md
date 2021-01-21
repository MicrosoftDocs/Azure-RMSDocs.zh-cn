---
title: Microsoft 信息保护 (MIP) SDK 的安装和配置
description: 提供安装和配置先决条件，以便使用 Microsoft 信息保护 SDK 构建应用程序。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 06/13/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 5daada951fb888fc7aa01071236af751ec38e002
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215521"
---
# <a name="microsoft-information-protection-mip-sdk-setup-and-configuration"></a>Microsoft 信息保护 (MIP) SDK 的安装和配置

快速入门和教程文章主要介绍使用 MIP SDK 库和 API 构建应用程序。 本文介绍如何安装和配置 Microsoft 365 订阅和客户端工作站，为使用 SDK 做准备。

## <a name="prerequisites"></a>必备条件

在开始之前，请务必查看以下主题：

- [什么是 Office 365 安全与合规中心？](/office365/securitycompliance/security-and-compliance)
- [什么是 Azure 信息保护？](/azure/information-protection/understand-explore/what-is-information-protection)
- [如何使用 Azure 信息保护进行保护？](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

> [!IMPORTANT]
> 为了尊重用户隐私，你必须在启用自动日志记录之前取得用户同意。 以下示例是 Microsoft 用于日志记录通知的标准消息：
>
> *启用错误和性能日志记录即表示同意向 Microsoft 发送错误和性能数据。Microsoft 会通过 Internet 收集错误和性能数据（统称“数据”）。Microsoft 利用此数据来保证并改进 Microsoft 产品和服务的质量、安全性和完整性。例如，会分析性能和可靠性（如使用哪些功能、功能的响应速度、设备性能、用户界面交互和遇到的任何产品问题）。数据还包括当前运行的软件以及 IP 地址的配置信息。*

## <a name="sign-up-for-an-office-365-subscription"></a>注册 Office 365 订阅

许多 SDK 示例都需要访问 Office 365 订阅的权限。 如果尚未注册，请务必注册以下订阅类型之一：

| 名称                                               | 注册                                                                         |
| -------------------------------------------------- | ------------------------------------------------------------------------------- |
| Office 365 企业版 E3 试用版（30 天免费试用） | https://go.microsoft.com/fwlink/p/?LinkID=403802                                |
| Office 365 企业版 E3 或 E5                     | https://products.office.com/business/office-365-enterprise-e3-business-software |
| 企业移动性 + 安全性 E3 或 E5          | https://www.microsoft.com/cloud-platform/enterprise-mobility-security           |
| Azure 信息保护高级版 P1 或 P2      | https://azure.microsoft.com/pricing/details/information-protection/             |
| Microsoft 365 E3、E5、或 F1                        | https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans         |

## <a name="configure-sensitivity-labels"></a>配置敏感度标签

如果当前正在使用 Azure 信息保护，则必须将标签迁移到 Office 365 安全与合规中心。 有关该过程的详细信息，请参阅[如何将 Azure 信息保护标签迁移到 Office 365 安全与合规中心](/azure/information-protection/configure-policy-migrate-labels)。

## <a name="configure-your-client-workstation"></a>配置客户端工作站

接下来，完成以下步骤以确保正确安装和配置客户端计算机。

1. 如果使用 Windows 10 工作站：

   - 请使用 Windows 更新，将计算机更新到 Windows 10 Fall Creators Update（版本 1709）或更高版本。 验证当前的版本：
     - 单击左下角的 Windows 图标。
     - 键入“关于电脑”并按 Enter。
     - 向下滚动到“Windows 规范”并查看“版本”   。

   - 请确保工作站启用了“开发人员模式”：
     - 单击左下角的 Windows 图标。
     - 当看到“使用开发人员功能”项时，请键入“使用开发人员功能”并按 Enter  。
     - 在“设置”对话框中，“针对开发人员”选项卡，在“使用开发人员功能”下，选择“开发人员模式”选项    。
     - 关闭“设置”对话框  。

2. 使用以下工作负载和可选组件安装 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)：
   - **通用 Windows 平台开发** Windows 工作负载及以下可选组件：
     - **C++ 通用 Windows 平台工具**
     - Windows 10 SDK 10.0.16299.0 SDK 或更高版本（如果未包含在内） 
   - **C++ 桌面开发** Windows 工作负载及以下可选组件：
     - Windows 10 SDK 10.0.16299.0 SDK 或更高版本（如果未包含在内） 

     [![Visual Studio 设置](media/setup-mip-client/visual-studio-install.png)](media/setup-mip-client/visual-studio-install.png#lightbox)

3. 安装 [ADAL.PS PowerShell 模块](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2)：

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

   以下平台支持 MIP SDK，每个支持的平台/语言都有单独的下载项：

   [!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

   **Tar.gz/.Zip 下载**

   Tar.gz 和 .Zip 下载内容包含压缩文件，每个 API 对应一个。 这些压缩文件的命名如下，其中 \<API\> = `file`、`protection` 或 `upe` 和 \<OS\> = 平台：`mip_sdk_<API>_<OS>_1.0.0.0.zip (or .tar.gz)`。 例如，Debian 上用于保护 API 二进制文件和标头文件的文件将是：`mip_sdk_protection_debian9_1.0.0.0.tar.gz`。 每个包含的 .tar.gz/.zip 拆分到三个目录中：

   - **Bins:** 用于每个平台体系结构的编译的二进制文件（在适用情况下）。
   - **Include:** 头文件 (C++)。
   - **Samples:** 示例应用程序的源代码。

   **NuGet 包**

   如果正在进行 Visual Studio 开发，也可以通过 NuGet 包管理器控制台安装 SDK：

    ```console
    Install-Package Microsoft.InformationProtection.File
    Install-Package Microsoft.InformationProtection.Policy
    Install-Package Microsoft.InformationProtection.Protection
    ```

5. 如果不使用 NuGet 包，请将 SDK 二进制文件的路径添加到 PATH 环境变量。 PATH 变量使客户端应用程序可以在运行时找到从属的二进制文件 (DLL)（可选）：

   如果使用 Windows 10 工作站：

   - 单击左下角的 Windows 图标。
   - 看到“编辑系统环境变量”项目时，键入“路径”并按 Enter  。
   - 在“系统属性”对话框中，单击“环境变量”   。
   - 在“环境变量”对话框中，单击 \<user\>“用户变量”下的“路径”变量行，然后单击“编辑...”   。
   - 在“编辑环境变量”对话框中，单击“新建”，创建一个新的可编辑行   。 使用 `file\bins\debug\amd64`、`protection\bins\debug\amd64` 和 `upe\bins\debug\amd64` 子目录的完整路径，为每个子目录添加一个新行。 SDK 目录以 `<API>\bins\<target>\<platform>` 格式存储，其中：
     - \<API\> = `file`, `protection`, `upe`
     - \<target\> = `debug`, `release`
     - \<platform\> = `amd64` (x64), `x86` 等。

   - 完成更新“路径”变量后，单击“确定”   。 然后在返回到“环境变量”对话框时单击“确定”   。

6. 从 GitHub 下载 SDK 示例（可选）：

   - 如果还没有 GitHub，请先创建一个 [GitHub 配置文件](https://github.com/join)。
   - 然后安装最新版本的 [Software Freedom Conservancy Git 客户端工具 (Git Bash)](https://git-scm.com/download/)
   - 使用 Git Bash，下载感兴趣的示例：
     - 使用以下查询查看存储库： https://github.com/Azure-Samples?utf8=%E2%9C%93&q=MipSdk 。
     - 使用 Git Bash，使用 `git clone https://github.com/azure-samples/<repo-name>` 下载每个示例存储库。

## <a name="register-a-client-application-with-azure-active-directory"></a>向 Azure Active Directory 注册将客户端应用程序

在 Microsoft 365 订阅预配过程中，将创建关联的 Active Directory (Azure AD) 租户。 Azure AD 租户为 Microsoft 365 用户帐户和应用程序帐户提供标识和访问管理 。 应用程序需要应用程序帐户才能访问受保护的 API（例如 MIP API）。

对于运行时的身份验证和授权，帐户由安全主体表示，该安全主体派生自帐户的标识信息  。 表示应用程序帐户的安全主体称为 [*服务主体*](/azure/active-directory/develop/developer-glossary#service-principal-object)。

在 Azure AD 中注册应用程序帐户以用于快速入门和 MIP SDK 示例：

  > [!IMPORTANT]
  > 要访问 Azure AD 租户管理以创建帐户，需要使用用户帐户登录 Azure 门户，该用户帐户应是[订阅上“所有者”角色](/azure/billing/billing-add-change-azure-subscription-administrator)的成员。 根据租户的配置，可能还需要成为“全局管理员”目录角色的成员才能[注册应用程序](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)。
  > 建议使用受限帐户进行测试。 请确保该帐户仅具有访问必要 SCC 终结点的权限。 日志记录系统可收集通过命令行传递的明文密码。

1. 按照[向 Azure AD 注册应用，注册新应用程序](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad#register-a-new-application-using-the-azure-portal)一节中的步骤进行操作。 出于测试目的，在完成指导步骤时，请对给定属性使用以下值：
    - **支持的帐户类型** - 选择“仅此组织目录中的帐户”。
    - **重定向 URI** - 将重定向 URI 类型设置为“公共客户端(移动和桌面)”。 如果应用程序使用的是 Microsoft 身份验证库 (MSAL)，请使用 `http://localhost`。 否则，请使用 `<app-name>://authorize` 格式。

2. 完成后，将返回“已注册的应用”页面查看新的应用程序注册  。 复制并保存“应用程序(客户端) ID”  字段中的 GUID，因为稍后需要在快速入门中用到它。

3. 然后，单击“API 权限”  ，以添加客户端需要访问的 API 和权限。 单击“添加权限”  ，以打开“请求获取 API 权限”边栏选项卡。

4. 现在，将添加应用程序在运行时需要的 MIP API 和权限：
   - 在“选择 API”  页上，单击“Azure Rights Management Services”  。
   - 在“Azure Rights Management Services”  API 页上，单击“委托的权限”  。
   - 在“选择权限”  部分中，选中“user_impersonation”  权限。 此权限允许应用程序代表用户创建和访问受保护的内容。
   - 单击“添加权限”  以保存。

5. 重复步骤 #4，但这次当进入“选择 API”页面时，需要搜索 API  。
   - 在“选择 API”  页上，单击“我的组织使用的 API”  ，然后在搜索框中键入“Microsoft 信息保护同步服务”  并选择它。
   - 在“Microsoft 信息保护同步服务”  API 页上，单击“委托的权限”  。
   - 展开“UnifiedPolicy”  节点，并选中“UnifiedPolicy.User.Read” 
   - 单击“添加权限”  以保存。

6. 返回到“API 权限”  页后，依次单击“为(租户名称)授予管理员同意”  和“是”  。 此步骤预先同意应用程序使用该注册，在指定权限下访问 API。 如果以全局管理员身份登录，则会为运行该应用程序的租户中的所有用户记录同意；反之，它仅适用于你的个人用户帐户。

完成后，应用程序注册和 API 权限应如下面的示例所示：

   [![Azure AD 应用程序注册](media/setup-mip-client/aad-app-registration-overview.png)](media/setup-mip-client/aad-app-registration-overview.png#lightbox) [![Azure AD 应用程序注册](media/setup-mip-client/aad-app-api-permissions.png)](media/setup-mip-client/aad-app-api-permissions.png#lightbox)

要详细了解如何向注册添加 API 和权限，请参阅[配置客户端应用程序以访问 Web API](/azure/active-directory/develop/quickstart-v1-update-azure-ad-app#configure-a-client-application-to-access-web-apis)。 此处可以找到有关添加客户端应用程序所需的 API 和权限信息。

## <a name="request-an-information-protection-integration-agreement-ipia"></a>请求信息保护集成协议 (IPIA)

必须先申请并与 Microsoft 签订正式的协议，才能发布使用 MIP 开发的应用程序。

1. 向 [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Requesting%20IPIA%20for%20<company-name>) 发送一封包含以下信息的电子邮件以获取 IPIA：

   **主题：** 为公司名称请求 IPIA 

   电子邮件的正文中应包含：
   - 应用程序和产品名称
   - 请求者的姓氏和名字
   - 请求者的电子邮件地址

2. 收到你的 IPIA 请求后，我们将发送一份表单（Word 文档格式）给你。 请查看 IPIA 的条款和条件，然后将包含以下信息的表格通过电子邮件发送到 [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=IPIA%20Response%20for%20<company-name>)：

   - 公司依法登记的名称
   - 公司注册地的州/省（美国/加拿大）或国家/地区
   - 公司 URL
   - 联系人的电子邮件地址
   - 公司的其他地址（可选）
   - 公司应用程序名称
   - 应用程序的简要描述
   - Azure 租户 ID 
   - 应用程序的 *应用程序 ID*
   - 用于紧急情况通信的公司联系人、电子邮件和电话号码

3. 收到你的表格后，我们会将用于数字签名的最终 IPIA 链接发送给你。 你在协议上签名后，协议将由相应的 Microsoft 客户代表签名，协议就此完成。

### <a name="already-have-a-signed-ipia"></a>已有已签名的 IPIA？

如果已有已签名的 IPIA 并希望为要发布的应用程序添加新的应用程序 ID  ，请发送电子邮件至 [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Updating%20IPIA%20for%20<company-name>)，向我们提供以下信息：

- 公司应用程序名称
- 应用程序的简要描述
- Azure 租户 ID（即使与以前提供的信息相同，也需要再次提供）
- 应用程序的应用程序 ID
- 用于紧急情况通信的公司联系人、电子邮件和电话号码

允许在电子邮件发送后的最长 72 小时内确认收到邮件。

## <a name="ensure-your-app-has-the-required-runtime"></a>确保应用具有所需的运行时

> [!NOTE]
> 仅当将应用程序部署到没有 Visual Studio 的计算机，或者 Visual Studio 安装缺少 Visual C++ 运行时组件时，才需要执行此步骤。

使用 MIP SDK 生成的应用程序需要安装 Visual C++ 2015 或 Visual C++ 2017 运行时（如果尚未安装）。
- [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/download/details.aspx?id=53587)
- [Microsoft Visual C++ Redistributable for Visual Studio 2017](https://visualstudio.microsoft.com/downloads/#microsoft-visual-c-redistributable-for-visual-studio-2017)

这些仅在应用程序已生成为发行版时才有效。 如果应用程序生成为调试版，则应用程序中必须包含或计算机上必须安装 Visual C++ 运行时调试 DLL。

## <a name="next-steps"></a>后续步骤

- 如果你是 C++ 开发人员
  - 在开始快速入门部分之前，请务必阅读[观察程序概念](concept-async-observers.md)，了解 C++ API 的异步特性。
  - 如果已准备好获取一些 SDK 使用体验，请从[快速入门：客户端应用程序初始化 (C++)](quick-app-initialization-cpp.md) 开始。
- 如果你是 C# 开发人员，并且已准备好使用 SDK 体验某些操作，请从[快速入门：客户端应用程序初始化 (C#)](quick-app-initialization-csharp.md) 开始。