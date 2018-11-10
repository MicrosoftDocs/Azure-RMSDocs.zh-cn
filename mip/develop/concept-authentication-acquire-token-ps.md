---
title: 概念 - 使用 PowerShell 获取访问令牌。
description: 本文将帮助你了解如何使用 PowerShell 获取 OAuth2 访问令牌。 这是实现身份验证委托所必需的。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a5ce346d044a9a56d37777e569582087026c9ce6
ms.sourcegitcommit: fa0be701b85b1fba5e75428714bb4525dd739a93
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223869"
---
# <a name="acquire-an-access-token-powershell"></a>获取访问令牌 (PowerShell)

此示例演示如何调用外部 PowerShell 脚本来获取 OAuth2 令牌。 这是实现身份验证委托所必需的。

此代码不能用于生产环境，但可用于开发和理解身份验证概念。 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

我们创建一个名为 AcquireToken 的函数。 由于本教程将对返回值进行硬编码，因此我们不接受任何参数，只返回一个字符串（令牌）。

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

我们的源文件返回一个令牌值，该值将在以后的步骤中进行硬编码。

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

最后，铸造一个令牌以放入 mToken 变量中。 以下示例演示了一个可用于在 Windows 上通过 ADAL 和 PowerShell 快速获取 OAuth2 令牌的 PowerShell 脚本。 仅向 Office 365 安全与合规中心终结点授予此令牌。 因此，除非更新资源 URL，否则保护操作将失败。 如果希望此时使用标记和保护进行测试，建议跳到[后续步骤](#next-steps)部分。

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>从 PS 库安装 [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2)

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>使用 Get-ADALToken 获取访问令牌

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://dataservice.o365filtering.com"
#clientId and redirectUri are from the RMS Sharing Application. 
#Once custom app registration is supported, a custom id and uri will be required. 
$clientId = "0edbblll-8773-44de-b87c-b8c6276d41eb"
$redirectUri = "com.microsoft.rms-sharing-for-win://authorize"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

将令牌从剪贴板复制到 auth.cpp 作为 `string mToken` 的值，以替换上面的“your token here”。 可能需要再次运行脚本，具体取决于以下步骤的执行时间。


