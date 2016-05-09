---
# required metadata

title: 安装并配置服务器 | Azure RMS
description: 安装并配置 RMS 服务器以便测试启用权限的应用程序。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e51adc12-4ee1-4819-bd8e-08ccf654fa00

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 安装并配置服务器

本主题介绍用于安装并配置 RMS 服务器以便测试启用权限的应用程序的步骤。

**重要说明**  如果要通过在单框 RMS ISV 环境上运行来测试应用程序，则无需安装 RMS 服务器，因为已在单框环境中安装并配置了一台服务器。
有关单框 AD RMS ISV 环境的详细信息，请参阅 [设置测试环境](how-to-set-up-your-test-environment.md)。

 

## 说明

### 步骤 1：设置 RMS 服务器

以下步骤指导你设置 RMS 服务器，包括：

-   配置注册表
-   安装服务器
-   注册服务器

1.  **配置注册表**

    若要指定在使用预生产证书层次结构，请设置以下注册表值。

    **注意**  如果使用 Windows Server 2008 R2 或 Windows Server 2008，请在安装 AD RMS 服务之前设置注册表值。

    如果要在 Windows Server 2008 R2 上使用 AD RMS，则必须设置以下 **REG\_DWORD** 值。 将此值更改为 0（零）可切换到生产层次结构。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**Hierarchy** = 0x00000001

    如果要在 Windows Server 2008 R2 上使用 AD RMS，并且其他 AD RMS 服务已作为预生产服务部署在 Active Directory 中，请向注册表添加以下空字符串值。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**GICURL** = ""

    如果要在 Windows Server 2008 上使用 AD RMS，则必须设置以下 **REG\_DWORD** 值。 将此值更改为 0（零）可切换到生产层次结构。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**Hierarchy** = 0x00000001

    如果要在 Windows Server 2008 上使用 AD RMS，并且其他 AD RMS 服务已作为预生产服务部署在 Active Directory 中，请向注册表添加以下空字符串值。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**GICURL** = ""

2.  **安装服务器**

    Active Directory Rights Management Services (AD RMS) 由单独的客户端和服务器组件组成。 服务器组件作为一组 Web 服务实现，可以用于管理 RMS 基础结构、向内容使用者和发布者颁发许可证以及向计算机和用户颁发证书。

    从 Windows Server 2008 开始，客户端和服务器组件包括在操作系统中。 可以从以下位置下载以前操作系统的服务器组件。

    -   [RMS Server v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    若要在 Windows Server 2008 上配置服务器组件，必须安装 AD RMS 角色。 但是在这样做之前，必须配置注册表，以指定将使用预生产证书层次结构而不是生产层次结构。 但是，如果要针对以前的服务器操作系统开发应用程序，请在安装 RMS server v1.0 SP2 之后，但是设置 RMS 服务之前配置注册表。

    有关详细信息，请参阅上一个步骤（步骤 1）“配置注册表”。

3.  **注册服务器**

    必须注册 Rights Management Services (RMS) 服务器才能在预生产或生产层次结构中标识它。 注册过程会在服务器计算机上留下一个服务器许可发放方证书。 此证书会链接回 Microsoft 信任根。 如何注册服务器取决于所使用的 RMS 版本。

    -   **自动注册**

        从 Windows Server 2008 开始，你可以在相应的层次结构中注册 RMS 服务器而不向 Microsoft 发送信息。 安装 RMS 角色时，还会安装自动注册证书和私钥。 这些用于自动创建服务器许可发放方证书。 不会与 Microsoft 交换任何信息。

    -   **联机注册** 如果使用的是 AD RMS v1.0 SP2，则可以联机注册服务器。 注册会在设置过程中在后台进行，但是你必须具有 Internet 连接且必须指定相应注册表值以确定在其中注册服务器的层次结构。 若要在预生产层次结构中注册，请添加以下 **REG\_SZ** 值并设置服务器。 若要在生产层次结构中注册，请清除此值并设置服务器。

        有关详细信息，请参阅上一个步骤（步骤 1）“配置注册表”。

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

### 相关主题

* [使用方法](how-to-use-msipc.md)
 

 





<!--HONumber=Apr16_HO3-->


