---
title: 快速入门 - Active Directory 权限管理服务器保护
description: 介绍了如何将 MIP SDK 配置为使用 Active Directory 权限管理服务器 (AD RMS) 的快速入门
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 04/17/2019
ms.author: tommos
ms.openlocfilehash: 49abf94c735b1ba14771adb9c2fe5dc126722b48
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070566"
---
# <a name="quickstart-active-directory-rights-management-server-ad-rms-protection"></a>快速入门：Active Directory 权限管理服务器 (AD RMS) 保护

本快速入门介绍了如何使用 MIP SDK 实现对 Active Directory 权限管理服务器 (AD RMS) 的支持。

> [!NOTE]
> 本快速入门中概述的步骤仅适用于 C# 或 C++ 文件 API，并仅适用于 C++ 保护 API。

## <a name="prerequisites"></a>必备条件

如果尚未准备，请务必：

- 首先完成[快速入门：客户端应用程序初始化 (C++)](quick-app-initialization-cpp.md)，生成 Visual Studio 初学者解决方案。
- 首先完成[快速入门：列出敏感度标签 (C++)](quick-file-list-labels-cpp.md) 或[快速入门：列出敏感度标签 (C#)](quick-file-list-labels-csharp.md)
- 使用[移动设备扩展](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11))部署 AD RMS。
- （可选）确保[用于 AD RMS MDE 的 DNS SRV 记录](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn673574(v%3dws.11)#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension)已发布。

## <a name="service-discovery"></a>服务发现

SDK 使用 UPN 或邮件地址后缀，根据通过 `FileEngineSettings` 或 `ProtectionEngineSettings` 提供的 `mip::Identity` 来执行服务发现。 它首先会在域层次结构中搜索用于 MDE 的 _rmsdisco  记录。 如需了解此过程的更多详情，请审阅[为 AD RMS 移动设备扩展指定 DNS SRV 记录](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn673574(v%3dws.11)#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension)。 如果找不到相应 DNS SRV 记录，它会默认使用 Azure 信息保护服务作为服务位置。

如果标识不可用，或用于 MDE 的 DNS SRV 记录尚未发布，可以通过显式设置[云终结点 URL](https://docs.microsoft.com/information-protection/develop/reference/class_mip_fileengine_settings#setpolicycloudendpointbaseurl-function) 来覆盖服务发现过程。

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>将 C# 文件 API 配置为使用 AD RMS

如果应用程序使用的是 Active Directory 身份验证库 (ADAL) 和 C# 文件 API，需要进行两个次要更改。 必须更新 `FileEngineSettings` 对象和 `AuthenticationContext` 构造函数，这样它们才能用于 AD RMS 和 Active Directory 联合身份验证服务 (ADFS)。

如果已部署移动设备扩展 DNS SRV 记录，并计划传入用户主体名称或电子邮件地址，[请遵循标识使用说明](#update-the-file-engine-settings-to-use-ad-rms-with-an-identity)。

如果没有移动设备扩展 DNS SRV 记录，或在运行时没有标识，[请遵循显式终结点说明](#update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint)。

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-identity"></a>将文件引擎设置更新为结合使用 AD RMS 与标识

如果用于 MDE 的 DNS SRV 记录已发布，并且 `Microsoft.InformationProtection.Identity` 已作为引擎设置的一部分提供，那么唯一需要的代码更改就是设置 `FileEngineSettings.ProtectionOnlyEngine = true`。 必须设置此属性，因为 AD RMS 保护终结点不支持标记（策略）操作。

```csharp
// Configure FileEngineSettings as protection only engine.
var engineSettings = new FileEngineSettings("", "", "en-US")
{
     // Provide the identity for service discovery.
     Identity = identity,
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true
};
```

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint"></a>将文件引擎设置更新为结合使用 AD RMS 与显式终结点

如果用于 MDE 的 DNS SRV 记录未发布，或 `Microsoft.InformationProtection.Identity` 无法在创建 `FileEngine` 时传入，那么需要进行两个代码更改。 其中一个更改是设置 `FileEngineSettings.ProtectionOnlyEngine = true`。 必须设置此属性，因为 AD RMS 保护终结点不支持标记（策略）操作。

```csharp
// Configure FileEngineSettings as protection only engine and generate a unique engine id.
var engineSettings = new FileEngineSettings("", "", "en-US")
{
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true,
     // Provide the explicit AD RMS endpoint
     ProtectionCloudEndpointBaseUrl = "https://rms.contoso.com"
};
```

### <a name="update-the-authentication-delegate"></a>更新身份验证委托

若要在 .NET 应用程序中使用 ADAL，需要更改 `Microsoft.InformationProtection.AuthDelegate` 实现来禁用颁发机构验证。 通过将 `AuthenticationContext` 构造函数中的 `validateAuthority` 设置为 false  ，禁用颁发机构验证。

   ```csharp
   AuthenticationContext authContext = new AuthenticationContext(authority, false, tokenCache);
   ```

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>将 C++ 文件 API 配置为使用 AD RMS

如果已部署移动设备扩展 DNS SRV 记录，并计划传入用户主体名称或电子邮件地址，[请遵循标识使用说明](#update-the-fileenginesettings-to-use-ad-rms-with-an-identity)。

如果没有移动设备扩展 DNS SRV 记录，或在运行时没有标识，[请遵循显式终结点说明](#update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint)。

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-identity"></a>将 FileEngine::Settings 更新为结合使用 AD RMS 与标识

如果用于 MDE 的 DNS SRV 记录已发布，并且 `mip::Identity` 已在 `FileEngine::Settings` 中提供，那么唯一需要执行的操作是，将引擎设置为仅保护引擎。

```cpp
FileEngine::Settings engineSettings(mip::Identity(mUsername), "");
engineSettings.SetProtectionOnlyEngine = true;
```

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>将 FileEngine::Settings 更新为结合使用 AD RMS 与显式终结点

如果用于 MDE 的 DNS SRV 记录未发布，或标识不可用于服务发现，必须将引擎设置为仅保护引擎，并使用通过 `SetProtectionCloudEndpointBaseUrl()` 提供的显式云终结点 URL。

```cpp
FileEngine::Settings engineSettings("", "");
engineSettings.SetProtectionOnlyEngine = true;
engineSettings.SetProtectionCloudEndpointBaseUrl("https://rms.contoso.com");
```

## <a name="configuring-protection-api-in-c-to-use-ad-rms"></a>将 C++ 保护 API 配置为使用 AD RMS

如果已部署移动设备扩展 DNS SRV 记录，并计划传入用户主体名称或电子邮件地址，[请遵循标识使用说明](#set-the-protectionenginesettings-to-use-ad-rms-with-an-identity)。

如果没有移动设备扩展 DNS SRV 记录，或在运行时没有标识，[请遵循显式终结点说明](#set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint)。

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-identity"></a>将 ProtectionEngine::Settings 设置为结合使用 AD RMS 与标识

如果用于移动设备扩展的 DNS SRV 记录已发布，并且标识已在 `ProtectionEngine::Settings` 中提供，无需进行额外的代码更改，即可使用 AD RMS。 服务发现会查找 AD RMS 终结点，并将它用于保护操作。

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity(mUsername), "");
```

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>将 ProtectionEngine::Settings 设置为结合使用 AD RMS 与显式终结点

如果 DNS SRV 记录未发布，或标识未在 `ProtectionEngine::Settings` 中提供，必须通过 `SetProtectionCloudEndpointBaseUrl()` 显式设置保护终结点 URL。

```cpp
ProtectionEngine::Settings engineSettings("", "");
engineSettings.SetProtectionCloudEndpointBaseUrl("https://RMS.CONTOSO.COM");
```

## <a name="remove-or-comment-label-references"></a>删除或注释掉标签引用

如果根据快速入门指南之一生成应用程序，就会发现应用程序引用了格式为 `fileEngine.SensitivityLabels` 或 `engine->ListSensitivityLabels();` 的标签。 由于应用程序已设置为仅保护，因此必须注释掉或删除这些代码块，因为运行它们会导致异常抛出。

## <a name="next-steps"></a>后续步骤

至此，已完成了支持 AD RMS 所需的更改。应用程序现在应该可以将 AD RMS 服务用作保护提供程序，执行任何仅保护操作。
