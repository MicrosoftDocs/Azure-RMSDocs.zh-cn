---
title: 如何在 Azure 信息保护中续订对称密钥
description: 本文介绍了在 Azure 信息保护中续订对称密钥的过程。
keywords: ''
author: msmbaldwin
manager: barbkess
ms.author: mbaldwin
ms.date: 03/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0b8c8f0-6ed5-48bb-8155-ac4f319ec178
ms.openlocfilehash: 353365a1619ae9f87b0d92ab4b956c8cf7b1d6cc
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178431"
---
# <a name="how-to-renew-the-symmetric-key-in-azure-information-protection"></a>如何：在 Azure 信息保护中续订对称密钥

**对称密钥**是对称密钥加密算法中用于加密和解密消息的密钥。  

在 Azure Active Directory (Azure AD) 中，创建一个服务主体对象来代表一个应用程序时，该过程还会生成一个用于验证该应用程序的 256 位对称密钥。 此对称密钥的默认有效期为一年。 

下面逐步介绍了如何续订对称密钥。 

## <a name="prerequisites"></a>先决条件

* 必须按照 [Azure AD Powershell 参考](https://docs.microsoft.com/powershell/msonline/)中的指示安装 Azure Active Directory (Azure AD) PowerShell 模块。


## <a name="renewing-the-symmetric-key-after-expiry"></a>到期后续订对称密钥

与应用程序关联的对称密钥过期后，你无需创建新的服务主体。 相反，可以使用 Microsoft Online Services (MSol) 提供的 [PowerShell commandlet](https://docs.microsoft.com/powershell/module/msonline) 为现有的服务主体颁发新的对称密钥。

为了说明这一过程，我们假定你已使用 [`New-MsolServicePrincipal`](https://docs.microsoft.com/powershell/msonline/v1/new-msolserviceprincipalcredential) 命令创建了一个新的服务主体。

```
New-MsolServicePrincipalCredential -ServicePrincipalName "SupportExampleApp"
```

如下所示，创建过程将创建一个对称密钥和一个 **AppPrincipalId**。

```
The following symmetric key was created as one was not supplied
ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

DisplayName : SupportExampleApp
ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
TrustedForDelegation : False
AccountEnabled : True
Addresses : []
KeyType : Symmetric
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

此对称密钥的到期时间为 2018 年 3 月 22 日下午 3:27:53。 若要在此时间之后使用服务主体，需要续订对称密钥。 为此，请运行 [`New-MsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/new-msolserviceprincipalcredential) 命令。 

```
New-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963
```

这将为指定的 **AppPrincipalId** 创建一个新的对称密钥。

```
The following symmetric key was created as one was not supplied ON8YYaMYNmwSfMX625Ei4eC6N1zaeCxbc219W090v28-
```
如下所示，可以使用 [`GetMsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/get-msolserviceprincipalcredential) 命令验证新对称密钥是否与正确的服务主体相关联。 请注意，此命令会列出当前与服务主体关联的所有密钥。

```
Get-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963 -ReturnKeyValues $true

Type : Symmetric
Value :
KeyId : c1ac145f-e899-4c90-8a02-2cef40054fc5
StartDate : 3/24/2017 10:11:07 PM
EndDate : 3/24/2018 10:11:07 PM
Usage : Verify

Type : Symmetric
Value :
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

一旦验证对称密钥确实与正确的服务主体相关联后，即可使用新密钥更新服务主体的身份验证参数。 

然后，可以使用 [`Remove-MsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/remove-msolserviceprincipalcredential) 命令删除旧的对称密钥，并使用 `Get-MsolServicePrincipalCredential` 命令验证密钥是否已删除。

```
Remove-MsolServicePrincipalCredential -KeyId acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe -ObjectId 0ee53770-ec86-409e-8939-6d8239880518
```

## <a name="related-topics"></a>相关主题

* [如何：让服务应用可以使用基于云的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
* [Azure Active Directory MSOnline Powershell 参考](https://docs.microsoft.com/powershell/msonline/)
