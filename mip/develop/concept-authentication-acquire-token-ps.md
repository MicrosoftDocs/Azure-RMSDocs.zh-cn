---
title: 概念 - 使用 PowerShell 获取访问令牌。
description: 本文将帮助你了解如何使用 PowerShell 获取 OAuth2 访问令牌。 这是实现身份验证委托所必需的。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/04/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: c66199f7ae22f6b4dca4406e847f41b56317beae
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82971653"
---
# <a name="acquire-an-access-token-powershell"></a>获取访问令牌 (PowerShell)

显示的示例演示如何调用外部 PowerShell 脚本以获取 OAuth2 标记。 身份验证委托的实现要求使用有效的 OAuth2 访问令牌。

## <a name="prerequisites"></a>先决条件

- 完成[（MIP） SDK 设置和配置](setup-configure-mip.md)。 在其他任务中，您将在 Azure Active Directory （Azure AD）租户中注册客户端应用程序。 Azure AD 将提供一个应用程序 ID （也称为客户端 ID），用于令牌获取逻辑。

此代码不用于生产。 它只能用于开发和理解身份验证概念。

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

我们创建一个名为 AcquireToken 的函数。 由于本教程中的返回值将是硬编码的，因此我们不接受任何参数并返回字符串（标记）。

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();
  }
}
```

### <a name="authcpp"></a>auth.cpp

源文件返回一个令牌值，此值将在以后的步骤中进行硬编码。

```cpp
//auth.cpp
#include <string>
#include "auth.h"

namespace sample {
  namespace auth {
    string AcquireToken() {
      std::string mToken = "your token here";
      return mToken;
    }
  }
}
```

## <a name="mint-a-token"></a>铸造令牌

最后，铸造一个令牌以放入 mToken 变量中。 以下示例演示了一个可用于在 Windows 上通过 ADAL 和 PowerShell 快速获取 OAuth2 令牌的 PowerShell 脚本。 仅向 Office 365 安全与合规中心终结点授予此令牌。 因此，除非更新资源 URL，否则保护操作将失败。

### <a name="install-adalps-from-ps-gallery"></a>从 PS 库安装 [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2)

如果之前已在[（MIP） SDK 设置和配置](setup-configure-mip.md)中完成此步骤，可以跳过此步骤。

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>使用 Get-ADALToken 获取访问令牌

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize"
#this is the security and compliance center endpoint
$resourceUrl = "https://syncservice.o365syncservice.com/"
#replace <application-id> and <redirect-uri>, with the Redirect URI and Application ID from your Azure AD application registration.
$clientId = "<application-id>"
$redirectUri = "<redirect-uri>"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

将令牌从剪贴板复制到 auth.cpp 作为 `string mToken` 的值，以替换上面的“your token here”。 可能需要再次运行脚本，具体取决于以下步骤的执行时间。
