---
title: 概念 - 使用 Python 获取访问令牌。
description: 本文将帮助你了解如何使用 Python 获取 OAuth2 访问令牌。 这是实现身份验证委托所必需的。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/04/2019
ms.author: bryanla
ms.openlocfilehash: 423ae80df11dcf8031f845fdabf881606daf89c7
ms.sourcegitcommit: fa7551060aaecc62d0c1f9179dd07f035d86651f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55742161"
---
# <a name="acquire-an-access-token-python"></a>获取访问令牌 (Python)

此示例演示如何调用外部 Python 脚本来获取 OAuth2 令牌。 需要有效的 OAuth2 访问令牌的身份验证委托的实现。

## <a name="prerequisites"></a>必备组件

若要运行下面的示例：

- 安装 Python 2.7。
- 在项目中实现 utils.h/cpp。 
- Auth.py 应添加到你的项目，并在生成的二进制文件所在的目录中存在。
- 完整[(MIP) SDK 设置和配置](setup-configure-mip.md)。 以及执行其他任务将在 Azure Active Directory (Azure AD) 租户中注册客户端应用程序。 Azure AD 将提供一个应用程序 ID，也称为客户端 ID，在你获取令牌的逻辑中使用。

此代码不被适用于生产环境中使用。 它可能仅用于开发和了解身份验证概念。 此示例跨平台。

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

在简单的身份验证的示例中，我们演示了一个简单`AcquireToken()`不利用任何参数，并返回硬编码的标记值的函数。 在此示例中，我们将重载 AcquireToken() 以接受身份验证参数并调用外部 Python 脚本来返回令牌。

### <a name="authh"></a>auth.h

在 auth.h 中，重载 `AcquireToken()`，重载的函数和更新的参数如下所示：

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();

    std::string AcquireToken(
        const std::string& userName, //A string value containing the user's UPN.
        const std::string& password, //The user's password in plaintext
        const std::string& clientId, //The Azure AD client ID (also known as Application ID) of your application.
        const std::string& resource, //The resource URL for which an OAuth2 token is required. Provided by challenge object.
        const std::string& authority); //The authentication authority endpoint. Provided by challenge object.
    }
}
```

前三个参数将由用户输入提供或硬编码到应用程序中。 最后两个参数由 SDK 提供给身份验证委托。 


### <a name="authcpp"></a>auth.cpp

在 auth.cpp 中，我们添加重载的函数定义，然后定义调用 Python 脚本所需的代码。 该函数接受提供的所有参数并将它们传递给 Python 脚本。 该脚本执行并返回字符串格式的令牌。

```cpp
#include "auth.h"
#include "utils.h"

#include <fstream>
#include <functional>
#include <memory>
#include <string>

using std::string;
using std::runtime_error;

namespace sample {
    namespace auth {

    string AcquireToken() { //ignore in this sample
    }

    //This function implements token acquisition in the application by calling an external Python script.
    //The Python script requires username, password, clientId, resource, and authority.
    //Username, Password, and ClientId are provided by the user/developer
    //Resource and Authority are provided as part of the OAuth2Challenge object that is passed in by the SDK to the AuthDelegate.
    string AcquireToken(
        const string& userName,
        const string& password,
        const string& clientId,
        const string& resource,
        const string& authority) {

    string cmd = "python";
    if (sample::FileExists("auth.py"))
        cmd += " auth.py -u ";

    else
        throw runtime_error("Unable to find auth script.");

    cmd += userName;
    cmd += " -p ";
    cmd += password;
    cmd += " -a ";
    cmd += authority;
    cmd += " -r ";
    cmd += resource;
    cmd += " -c ";
    // Replace <application-id> with the Application ID provided during your Azure AD application registration.
    cmd += (!clientId.empty() ? clientId : "<application-id>");

    string result = sample::Execute(cmd.c_str());
    if (result.empty())
        throw runtime_error("Failed to acquire token. Ensure Python is installed correctly.");

    return result;
    }
    }
}

```

## <a name="python-script"></a>Python 脚本

此脚本通过简单的 http 请求直接获取身份验证令牌。 这仅作为一种获取示例应用所用身份验证令牌的方法，而不适用于生产代码。 该脚本仅适用于支持普通旧用户名/密码 http 身份验证的租户。 MFA 或基于证书的身份验证将失败。

```python
import getopt
import sys
import json
import urllib
import urllib2
import re

def printUsage():
  print('auth.py -u <username> -p <password> -a <authority> -r <resource> -c <clientId>')

def main(argv):
  try:
    options, args = getopt.getopt(argv, 'hu:p:a:r:c:')
  except getopt.GetoptError:
    printUsage()
    sys.exit(-1)

  username = ''
  password = ''
  authority = ''
  resource = ''
  clientId = ''

  for option, arg in options:
    if option == '-h':
      printUsage()
      sys.exit()
    elif option == '-u':
      username = arg
    elif option == '-p':
      password = arg
    elif option == '-a':
      authority = arg
    elif option == '-r':
      resource = arg
    elif option == '-c':
      clientId = arg

  if username == '' or password == '' or authority == '' or resource == '' or clientId == '':
    printUsage()
    sys.exit(-1)

  # Find everything after the last '/' and replace it with 'token'
  if not authority.endswith('token'):
    regex = re.compile('^(.*[\/])')
    match = regex.match(authority)
    authority = match.group()
    authority = authority + 'token'

  # Build REST call
  headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'application/json'
  }

  params = {
    'resource': resource,
    'client_id': clientId,
    'grant_type': 'password',
    'username': username,
    'password': password
  }

  req = urllib2.Request(
    url = authority,
    headers = headers,
    data = urllib.urlencode(params))

  f = urllib2.urlopen(req)
  response = f.read()
  f.close()
  sys.stdout.write(json.loads(response)['access_token'])

if __name__ == '__main__':
  main(sys.argv[1:])
```

## <a name="update-acquireoauth2token"></a>更新 AcquireOAuth2Token

最后，更新 `AuthDelegateImpl` 中的 `AcquireOAuth2Token` 函数以调用重载的 `AcquireToken` 函数。 通过读取 `challenge.GetResource()` 和 `challenge.GetAuthority()` 获取资源和颁发机构 URL。 添加引擎时，将 `OAuth2Challenge` 传入身份验证委托。 这项工作由 SDK 完成，不需要开发人员额外操作。 

```cpp
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/,
    const OAuth2Challenge& challenge,
    OAuth2Token& token) {

    //call our AcquireToken function, passing in username, password, clientId, and getting the resource/authority from the OAuth2Challenge object
    string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetResource(), challenge.GetAuthority());
    token.SetAccessToken(accessToken);
    return true;
}
```

添加 `engine` 时，SDK 将调用 `AcquireOAuth2Token 函数，传入质询，执行 Python 脚本，接收令牌，然后将令牌提供给服务。


