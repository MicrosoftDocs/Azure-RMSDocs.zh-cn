---
title: 概念 - MIP SDK 中的身份验证。
description: 本文将帮助你了解 MIP SDK 如何实现身份验证，以及客户端应用程序提供 OAuth2 访问令牌获取逻辑的要求。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 55bfba6da57fa07614165f4d5fcc5fba226cfca7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886234"
---
# <a name="microsoft-information-protection-sdk---authentication-concepts"></a>Microsoft 信息保护 SDK - 身份验证概念

通过扩展类 `mip::AuthDelegate` 实现首选身份验证方法，来执行 MIP SDK 中的身份验证。 `mip::AuthDelegate` 包含：

- `mip::AuthDelegate::OAuth2Challenge`：管理 OAuth2 颁发机构信息并提供给客户端应用程序的类。
- `mip::AuthDelegate::OAuth2Token`：管理 OAuth2 访问令牌获取（从客户端应用程序）和令牌存储的类。
- `mip::AuthDelegate::AcquireOAuth2Token()`：纯虚函数，其实现决定了访问令牌获取方法。 在被 SDK 调用之后，它会获取访问令牌，然后将其返回给 SDK 的身份验证逻辑。

`mip::AuthDelegate::AcquireOAuth2Token` 接受以下参数，并返回一个布尔值，指示令牌获取是否成功：

- `mip::Identity`：要进行身份验证的用户或服务 (如果已知) 的标识。
- `mip::AuthDelegate::OAuth2Challenge`：接受四个参数、**颁发机构**、**资源**、**声明**和**作用域**。 **Authority** 是将针对其生成令牌的服务。 **Resource** 是我们正在尝试访问的服务。 如果被调用，SDK 会负责将这些参数传递给委托。 **声明**是保护服务所需的标签特定声明。 **范围**是访问资源所需的 Azure AD 权限范围。 
- `mip::AuthDelegate::OAuth2Token`：标记结果将写入此对象。 加载引擎时，SDK 将使用它。 除了我们的身份验证实现，没必要在任何地方获取或设置此值。

**重要提示：** 应用程序不`AcquireOAuth2Token`能直接调用。 SDK 将在需要时调用此函数。

## <a name="consent"></a>决不

在应用程序获权访问帐户标识下的受保护资源/API 之前，Azure AD 要求应用程序先获得同意。 同意记录为帐户的租户中的权限的永久确认, 适用于特定帐户 (用户同意) 或所有帐户 (管理员同意)。 根据所访问的 API、应用程序所寻求的权限以及用于登录的帐户，同意过程会出现在各种场景中： 

- 如果你或管理员未通过“授予权限”功能显式预先同意访问权限，则应用程序注册所在的*同一租户*中的帐户登录时会出现同意过程。
- 如果应用程序注册为多租户，并且租户管理员未事先代表所有用户预先同意，则*不同租户*中的帐户登录时会出现同意过程。

`mip::Consent` 枚举类实现了一种易于使用的方法，允许应用程序开发人员根据 SDK 正在访问的终结点提供自定义同意体验。 通知可以告知用户将收集哪些数据、如何删除数据或者法律或符合性策略要求的任何其他信息。 用户授予同意后，应用程序即可继续运行。 

### <a name="implementation"></a>实现

通过扩展 `mip::Consent` 基类并实现 `GetUserConsent` 来返回其中一个 `mip::Consent` 枚举值，从而实现同意。 

从 `mip::Consent` 派生的对象会传递到 `mip::FileProfile::Settings` 或 `mip::ProtectionProfile::Settings` 构造函数中。

当用户执行需要提供同意的操作时，SDK 会调用 `GetUserConsent` 方法，并将目标 URL 作为参数传入。 在此方法中，将实现向用户显示必要的信息，从而允许他们决定是否同意使用该服务。 

### <a name="consent-options"></a>同意选项

- **AcceptAlways**:同意并记住决定。
- **接受**:只同意一次。
- **拒绝**:不要同意。

如果 SDK 通过这种方法请求获取用户许可，客户端应用程序应向用户显示 URL。 客户端应用程序应提供一些用于获取用户许可的方法，并返回与用户决定对应的相应许可枚举。

### <a name="sample-implementation"></a>实现示例

#### <a name="consent_delegate_implh"></a>consent_delegate_impl.h

```cpp
class ConsentDelegateImpl final : public mip::ConsentDelegate {
public:
  ConsentDelegateImpl() = default;
  
  virtual mip::Consent GetUserConsent(const std::string& url) override;

};
```

#### <a name="consent_delegate_implcpp"></a>consent_delegate_impl.cpp

当 SDK 需要同意时，SDK *会*调用 `GetUserConsent` 方法，并将 URL 作为参数传入。 在下面的示例中, 通知用户 SDK 将连接到所提供的 URL, 并为用户提供命令行选项。 根据用户的选择, 用户接受或拒绝向 SDK 传递的许可。 如果用户拒绝同意, 则应用程序将引发异常, 并且不会对保护服务进行调用。 

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  //Print the consent URL, ask user to choose
  std::cout << "SDK will connect to: " << url << std::endl;

  std::cout << "1) Accept Always" << std::endl;
  std::cout << "2) Accept" << std::endl;
  std::cout << "3) Reject" << std::endl;
  std::cout << "Select an option: ";
  char input;
  std::cin >> input;

  switch (input)
  {
  case '1':
    return Consent::AcceptAlways;
    break;
  case '2':
    return Consent::Accept;
    break;
  case '3':
    return Consent::Reject;
    break;
  default:
    return Consent::Reject;
  }  
}
```

对于测试和开发目的, 可以实现`ConsentDelegate`如下所示的简单操作:

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

但是, 在生产代码中, 用户可能需要向用户提供一种同意选项, 具体取决于区域或业务要求和法规。 

## <a name="next-steps"></a>后续步骤

为简单起见，演示委托的示例将通过调用外部脚本来实现令牌获取。 此脚本可以替换为任何其他类型的脚本（开源 OAuth2 库或自定义 OAuth2 库）。

- [使用 PowerShell 获取访问令牌](concept-authentication-acquire-token-ps.md)
- [使用 Python 获取访问令牌](concept-authentication-acquire-token-py.md)
