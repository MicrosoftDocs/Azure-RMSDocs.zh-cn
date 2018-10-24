---
title: 概念 - 身份验证委托实现 (C++)
description: 本文将帮助你了解如何在 C++ 中实现身份验证委托。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9a9256d4c67845f43eeb1598926ea5c02f07f822
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445727"
---
# <a name="microsoft-information-protection-sdk---implementing-an-authentication-delegate-c"></a>Microsoft 信息保护 SDK - 实现身份验证委托 (C++)

MIP SDK 实现了一个身份验证委托，用于处理身份验证质询以及使用令牌进行响应。 它本身并不实现令牌获取。 令牌获取过程取决于开发人员，并通过扩展 `mip::AuthDelegate` 类，特别是 `AcquireOAuth2Token` 成员函数来完成。

## <a name="building-authdelegateimpl"></a>生成 AuthDelegateImpl

为了扩展基类 `mip::AuthDelegate`，我们创建一个名为 `sample::auth::AuthDelegateImpl` 的新类。 此类实现 `AcquireOAuth2Token` 功能，并设置构造函数来接收我们的身份验证参数。

### <a name="authdelegateimplh"></a>auth_delegate_impl.h

在此示例中，默认构造函数仅接受用户名、密码和应用程​​序的[应用程序 ID](/azure/active-directory/develop/developer-glossary.md#application-id-client-id)。 这些信息将存储在私有变量 `mUserName`、`mPassword` 和 `mClientId` 中。

请务必注意，不必实现标识提供者或资源 URI 等信息，至少不必在 `AuthDelegateImpl` 构造函数中实现。 这些信息作为 `OAuth2Challenge` 对象中 `AcquireOAuth2Token` 的一部分传递。 而我们将这些详细信息传递给 `AcquireOAuth2Token` 中的 `AcquireToken` 调用。

```cpp
//auth_delegate_impl.h
#include <string.h>
#include "mip/common_types.h"

namespace sample {
namespace auth {
class AuthDelegateImpl final : public mip::AuthDelegate { //extend mip::AuthDelegate base class
public:
  AuthDelegateImpl() = delete;

  //constructor accepts username, password, and clientId, all plain strings.
  AuthDelegateImpl(
    const std::string& userName,
    const std::string& password,
    const std::string& clientId
  );

  bool AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) override;

private:
  std::string mUserName;
  std::string mPassword;
  std::string mClientId;
};

}
}
```

### <a name="authdelegateimplcpp"></a>auth_delegate_impl.cpp

`AcquireOAuth2Token` 是对 OAuth2 提供程序进行调用的地方。 以下示例对 `AcquireToken()` 进行了两次调用。 实际上只会进行一次调用。 [后续步骤](#next-steps)下提供的章节将介绍这些实现

```cpp
//auth_delegate_impl.cpp
#include "auth_delegate_impl.h"
#include <stdexcept>
#include "auth.h" //contains the auth class used later for token acquisition

using std::runtime_error;
using std::string;

namespace sample {
namespace auth {

AuthDelegateImpl::AuthDelegateImpl(
    const string& userName,
    const string& password,
    const string& clientId)
    : mUserName(userName),
    mPassword(password),
    mClientId(clientId) {
}

//Here we could simply add our token acquisition code to AcquireOAuth2Token
//Instead, that code is implemented in auth.h/cpp to demonstrate calling an external library
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/, //This won't be used
    const OAuth2Challenge& challenge,
    const OAuth2Token& token) {

      //sample::auth::AcquireToken is the code where the token acquisition routine is implemented.
      //AcquireToken() returns a string that contains the OAuth2 token.

      //Simple example for getting hard coded token. Comment out if not used.
      string accessToken = sample::auth::AcquireToken();

      //Practical example for calling external OAuth2 library with provided authentication details.
      string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetAuthority(), challenge.GetResource());  

      //set the passed in OAuth2Token value to the access token acquired by our provider
      token.SetAccessToken(accessToken);
      return true;
    }
}
}
```

## <a name="next-steps"></a>后续步骤

若要完成身份验证实现，必须在 `AcquireToken()` 函数后面生成代码。 以下示例介绍了几种获取令牌的方法。

- [简单/PowerShell 令牌获取示例](concept-authentication-acquire-token-ps.md)
- [Python 令牌获取示例](concept-authentication-acquire-token-py.md)
