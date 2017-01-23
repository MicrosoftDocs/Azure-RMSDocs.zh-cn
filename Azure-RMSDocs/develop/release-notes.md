---
title: "新增功能和发行说明 | Azure RMS"
description: "概述这一新版本的 RMS SDK 中的重要更改和功能。"
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: febd7d90a1a762de73894724f3cf3401aec0d7b9


---

# <a name="whats-new-and-release-notes"></a>新增功能和发行说明

## <a name="whats-new"></a>新增功能
Microsoft Rights Management SDK 4.2 将 RMS 应用程序实现提升到了一个新的易用性和灵活性级别。 本主题概述了该 RMS SDK 版本中的重要更改和功能。

### <a name="new-for-june-2016"></a>2016 年 6 月的新增功能

- **支持新式验证** - 将基于 Active Directory 身份验证库 (ADAL) 的登录引入到启用了 RMS 的应用中。 它可实现 Multi-Factor Authentication (MFA)、带 RMS 客户端应用程序且基于 SAML 的第三方标识提供者、智能卡和基于证书的身份验证等登录功能，且不再需要启用了 RMS 的应用即可使用基本身份验证协议。
- **文档跟踪支持** - 开发人员现可在保护其应用中的文档时启用文档跟踪
- 性能改进
- Bug 修复情况


### <a name="december-2015-update"></a>2015 年 12 月更新

在本版本中，适用于设备的 RMS SDK 现在为版本 4.2，并添加：

-   文档跟踪，仅限 RMS 联机，适用于 iOS/OS X 和 Android 操作系统。

    有关 iOS/OS X 的详细信息和使用指南，请参阅 [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) 类，其中提供了有关 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) 的跟踪信息以及额外的文档跟踪注册方法。 对于 Android 操作系统，也在 [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) 和 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) 中添加了类似功能。

    有关文档跟踪功能的详细说明，请参阅[操作方法：使用文档跟踪](how-to-use-document-tracking.md)。

-   一组同步方法，使 Android API 的异步版本实现平行：

    [CustomProtectedInputStream.create 同步方法](https://msdn.microsoft.com/library/mt631362.aspx)

    [CustomProtectedOutputStream.create 同步方法](https://msdn.microsoft.com/library/mt631363.aspx)

    [ProtectedFileInputStream.create 同步方法](https://msdn.microsoft.com/library/mt631375.aspx)

    [ProtectedFileOutputStream.create 同步方法](https://msdn.microsoft.com/library/mt631376.aspx)

    [TemplateDescriptor.getTemplates 同步方法](https://msdn.microsoft.com/library/mt631380.aspx)

    [UserPolicy.acquire 同步方法](https://msdn.microsoft.com/library/mt631384.aspx)

    [UserPolicy.create (PolicyDescriptor…) 同步方法**](https://msdn.microsoft.com/library/mt631385.aspx)

    [UserPolicy.create (TempalteDescriptor…) 同步方法](https://msdn.microsoft.com/library/mt631386.aspx)

-   Android API 中添加了一个新的 [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) 类。
-   引入更新以改进错误消息传送和故障排除体验。
-   加密操作的显著性能改进。

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>2015 年 7 月更新 - 添加针对 Linux / C++ 开发的支持

此版本添加了以下功能：

-   适用于 Linux 平台的 RMS SDK 4.1

    有关详细信息，请参阅[入门](get-started.md)。

### <a name="may-2015-update---adds-logging-control"></a>2015 年 5 月更新 - 添加日志记录控制

此版本添加了针对以下操作系统的支持：

-   iOS

    应用程序加密和解密操作可以独立地并行运行。

    有关详细信息，请参阅 [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx)。

    日志级别控件设置已启用。

    有关详细信息，请参阅[如何：启用错误和性能日志记录](enabling-logging.md)

    已添加缓存清除支持。

    有关详细信息，请参阅 [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx)。

### <a name="february-2015-update---adds-windows-store-application-support"></a>2015 年 2 月更新 - 添加 Windows 应用商店应用程序支持

此版本添加了针对 Windows 应用商店应用程序的支持，并且与 Windows Phone、Android 和 iOS/OS X 版本的 RMS SDK 4.1 具有相同功能。

### <a name="january-2015-update---adds-winphone-platform-support"></a>2015 年 1 月更新 - 添加 WinPhone 平台支持

此版本添加了针对 Windows Phone 操作系统的支持，并且与 Android 和 iOS/OS X 版本的 RMS SDK 4.1 具有相同功能。

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>2014 年 10 月更新 - 升级到 Microsoft RMS SDK 4.1

4.1 版本的 RMS SDK 向 Google Android 和 Apple iOS / OS X 添加了以下新功能。

-   用于*用户许可*处理的 Android 和 iOS/OS X SDK API 扩展，允许用户确认 SDK 行为。 目前，文档跟踪和访问未知 AD RMS 服务 URL 是受支持的许可类型。

    有关详细信息，请参阅 Android API 版本的 [ConsentCallback 接口](https://msdn.microsoft.com/library/dn833503.aspx)作为示例。

-   iOS 8 和 OS X 10.10 (Yosemite) 现在受支持。 还有一些 Xcode 6 要求的属性名称更改。

    例如：MSUserPolicy.name 更改为 [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx)。

## <a name="release-notes"></a>发行说明

此部分概述了开发人员应当知晓的与当前和以前版本的 Microsoft Rights Management SDK 4.x API 相关的信息。

**AD RMS SDK 4.1 - iOS / OS X 和 Android 平台全球可用性版本**

-   **AD RMS 支持** - IT 管理员可以在带有全新 AD RMS 服务器的移动设备扩展的移动设备上使用启用 RMS 的应用程序。
-   **脱机使用** - 最终用户可以脱机访问受 RMS 保护的数据。
-   **隔离式身份验证** - 开发人员可以使用自己的 Azure RMS 和 AD RMS 身份验证库（或使用推荐的 [Azure AD 身份验证库 (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx)）。
-   **隔离式 UI** - 开发人员可以构建自己的用户界面以保护和使用受 RMS 保护的文档。
-   **重新设计的 API** - 开发人员现在可以获得简单、透明的加密和解密 API，这样只需最少的努力即可获得一致的 RMS 行为和用户体验。

**所有平台通用**

-   RMS SDK 4.x API 并非*线程安全*。

**Android**

-   当你在 Amazon® Kindle 设备上使用示例应用程序以查看 .ptxt 附件时，必须首先下载文件，然后才能查看。

    **解决方案** - 这是已知问题，将在后续版本中解决。

-   如果允许多个实例，则使用 SDK 的应用程序可能会崩溃。

    **解决方案** - 确保应用程序不允许对 Android API 的多实例调用。

-   使用长度与 *array.length* 值不同的 [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array, int offset, int length) 方法后，无法通过 SDK 使用内容。

    **解决方案** - 这是一个已知问题。 为了缓解问题，可始终传递长度值与长度参数相同的 *byte \[\]*阵列，也可使用 [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array) 方法。

**iOS 和 OS X**

-   我们的 iOS 和 OS X SDK 支持葡萄牙语的两种区域语言。 很遗憾，由于存在 bug，我们目前无法完全支持第一种语言的本地化。 受此 bug 影响，葡萄牙语并非完全受支持。 大多数文本已翻译，但 UI 部分除外。

    1. 葡萄牙语

    2. 葡萄牙语（葡萄牙）

**仅限 iOS**

-   RMS SDK 4.x 不显示网络活动指示器。

    这是《Apple 人机接口指南》中提及的 iOS 的已知可选行为。

**仅限 OS X**

-   RMS SDK 4.x 不显示网络活动指示器。

    这是《Apple 人机接口指南》中提及的 OS X 的已知可选行为。

-   **解决方案** - 若要使用我们的 OS X SDK 创建多文档接口 (MDI) 应用程序，请遵循以下指南。

    以下方法不得同时运行。 为了监控执行完成情况，请使用所说明的完成块方法。

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**注意**：我们的 iOS API 不支持 MDI 应用程序。

## <a name="frequently-asked-questions"></a>常见问题

**所有平台**

**Q**：我在保护工作流中未看到**自定义权限**选择 UI。 原因是什么？

**答**：这是已知问题，将在后续版本中解决。

**问**：如何获取新的组织租户以试用 SDK 和示例应用程序？

**答**：若要申请用于 Azure AD RMS 测试组织的凭据，请发送电子邮件至 <rmcstbeta@microsoft.com>。

**Q**：我在文档此处未看到任何有关测试层次结构的讨论。 原因是什么？

**A**：新的 AD RMS SDK 不存在任何测试层次结构概念。 你将始终使用生产层次结构。

**Q**：在 2.1 版本的 RMS SDK 中，每个实施信息保护的应用程序都需要一个生成的清单，4.0 及更高版本的 SDK 中是否也是这样？

**A**：不是，从 3.0 版本开始的 Rights Management SDK 中不再需要清单。

**Android**

**Q**：已使用哪些开发环境对 SDK 进行了测试？

**A**：使用 Google API 15 及以上版本的 Eclipse Juno。

**Q**：我能否从 UI 线程调用 cancel() 取消方法？
**A**：你应该从非 UI 线程调用 cancel()，因为这可能造成网络连接中断。

**iOS**

**Q**：哪些平台经过验证可用于 SDK 开发？

**A**：包含 iOS 7 及更高版本的 Xcode 5.0。

**Q**：我对某个操作调用了 cancel() 方法，但我仍然收到了操作已完成的通知。 原因是什么？

**A**：并非所有操作都可以取消，因此最好在可能的情况下执行取消操作。

**OS x**

**Q**：示例应用程序框架经过调整以适应 Xcode 5，我能否使用 Xcode 4.6？

**A**：OS X SDK 仅使用 Xcode 4.6 及更高版本以及 OS X 10.8 和更高版本。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


