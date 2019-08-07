---
title: 如何安装、配置 RMS 服务器并用其进行测试| Azure RMS
description: 安装并配置 RMS 服务器以便测试启用权限的应用程序。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 59aa02318a0c6d7ee5e9857bead4c79248546320
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794115"
---
# <a name="how-to-install-configure-and-test-with-an-rms-server"></a>操作说明：安装和配置 RMS 服务器并用其进行测试

本主题介绍用于连接 RMS 服务器或 Azure RMS 以便测试启用权限的应用程序的步骤。
 
## <a name="instructions"></a>说明

### <a name="step-1-setup-your-rms-server"></a>步骤 1：设置 RMS 服务器

以下步骤指导你设置 RMS 服务器，包括：

-   安装服务器
-   注册服务器

1. **安装服务器**

   Active Directory Rights Management Services (AD RMS) 由单独的客户端和服务器组件组成。 服务器组件作为一组 Web 服务实现，可以用于管理 RMS 基础结构、向内容使用者和发布者颁发许可证以及向计算机和用户颁发证书。

   从 Windows Server 2008 开始，客户端和服务器组件包括在操作系统中。 可以从以下位置下载以前操作系统的服务器组件。

   -   [RMS Server v1.0 SP2](https://go.microsoft.com/fwlink/p/?linkid=73722)

   若要在 Windows Server 2008 上配置服务器组件，必须安装 AD RMS 角色。 如果要针对以前的服务器操作系统开发应用程序，请在安装 RMS server v1.0 SP2 之后，但是设置 RMS 服务之前配置注册表。

2. **注册服务器**

   必须注册 Rights Management Services (RMS) 服务器才能在预生产或生产层次结构中标识它。 注册过程会在服务器计算机上留下一个服务器许可发放方证书。 此证书会链接回 Microsoft 信任根。 如何注册服务器取决于所使用的 RMS 版本。

   -   **自动注册**

       从 Windows Server 2008 开始，你可以在相应的层次结构中注册 RMS 服务器而不向 Microsoft 发送信息。 安装 RMS 角色时，还会安装自动注册证书和私钥。 这些用于自动创建服务器许可发放方证书。 不会与 Microsoft 交换任何信息。

   -   **联机注册**

       如果使用的是 AD RMS v1.0 SP2，则可以联机注册服务器。 预配过程中将在后台注册，但必须具有 Internet 连接。

       **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **使用 RMS 服务器进行测试**

    要使用 RMS 服务器进行测试，请配置服务器端发现或客户端发现，以使 Rights Management 服务客户端 2.1 可以发现预生产 RMS 服务器并与之建立通信。

    > [!Note]
    > 使用 Azure RMS 进行测试不需要发现配置。

   - 在服务器端发现中，管理员会向 Active Directory 注册 RMS 根群集的服务连接点 (SCP)，客户端会查询 Active Directory 以发现该 SCP 并与服务器建立连接。
   - 在客户端发现中，会在运行 RMS 客户端 2.1 的计算机上，在注册表中配置 RMS 服务发现设置。 这些设置使 RMS 客户端 2.1 指向 RMS 服务器。 当它们存在时，不会执行服务器端发现。

   若要配置客户端发现，可以设置以下注册表项以指向 RMS 服务器。 有关如何配置服务端发现的信息，请参阅 [RMS 客户端 2.0 部署说明](https://technet.microsoft.com/library/jj159267(WS.10).aspx)。

4. **EnterpriseCertification**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterpriseCertification

   **值**：（默认）：[http|https]://RMSClusterName/_wmcs/Certification

5. **EnterprisePublishing**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterprisePublishing
                  
   **值**：（默认）：[http|https]://RMSClusterName/_wmcs/Licensing

> [!NOTE]
> 默认情况下，这些项在注册表中不存在，必须创建。
> 
> [!IMPORTANT]
> 如果在 64 位版本的 Windows 上运行 32 位应用程序，则必须在以下项位置设置这些项：<p>
>   ```    
>   HKEY_LOCAL_MACHINE
>     SOFTWARE
>       Wow6432Node
>         Microsoft
>           MSIPC
>             ```
