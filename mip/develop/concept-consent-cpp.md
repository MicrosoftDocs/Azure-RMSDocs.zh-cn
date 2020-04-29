---
title: 概念-在 MIP SDK 中同意。
description: 本文将帮助你了解 MIP SDK 如何实现许可流，以便用户同意连接到 RMS 服务。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 7025e042d0ded7164b26efbe9b453b4546c5ca05
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766535"
---
# <a name="microsoft-information-protection-sdk---consent"></a>Microsoft 信息保护 SDK-同意

`mip::Consent` 枚举类实现了一种易于使用的方法，允许应用程序开发人员根据 SDK 正在访问的终结点提供自定义同意体验。 通知可以告知用户将收集哪些数据、如何删除数据或者法律或符合性策略要求的任何其他信息。 用户授予同意后，应用程序即可继续运行。 

### <a name="implementation"></a>实现

通过扩展 `mip::Consent` 基类并实现 `GetUserConsent` 来返回其中一个 `mip::Consent` 枚举值，从而实现同意。 

从 `mip::Consent` 派生的对象会传递到 `mip::FileProfile::Settings` 或 `mip::ProtectionProfile::Settings` 构造函数中。

当用户执行需要提供同意的操作时，SDK 会调用 `GetUserConsent` 方法，并将目标 URL 作为参数传入。 在此方法中，将实现向用户显示必要的信息，从而允许他们决定是否同意使用该服务。 

### <a name="consent-options"></a>同意选项

- **AcceptAlways**：同意并记住该决定。
- **Accept**：同意一次。
- **Reject**：不同意。

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

当 SDK 需要同意时，SDK *会*调用 `GetUserConsent` 方法，并将 URL 作为参数传入。 在下面的示例中，通知用户 SDK 将连接到所提供的 URL，并为用户提供命令行选项。 根据用户的选择，用户接受或拒绝向 SDK 传递的许可。 如果用户拒绝同意，则应用程序将引发异常，并且不会对保护服务进行调用。 

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

对于测试和开发目的，可以实现`ConsentDelegate`如下所示的简单操作：

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

但是，在生产代码中，用户可能需要向用户提供一种同意选项，具体取决于区域或业务要求和法规。 