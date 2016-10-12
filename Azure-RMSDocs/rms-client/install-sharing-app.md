---
title: "下载并安装 Rights Management 共享应用程序 | Azure 信息保护"
description: "有关以交互方式安装适用于 Windows 的 RMS 共享应用程序，以便可以安全地与他人共享文档的说明。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: aac3c6c7b5167d729d9ac89d9ae71c50dd1b6a10
ms.openlocfilehash: c705bfec85bb93cb03d7e3edc9f3ce5949a8b61d


---

# 下载和安装 Rights Management 共享应用程序

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、具有 SP1 的 Windows 7、Windows 8、Windows 8.1*

你无需是本地管理员就能安装 RMS 共享应用程序。 但是，如果你不是本地管理员而使用 Office 2010，就会有一些限制。 有关详细信息，请参阅本页上的[如果你不是本地管理员，并且使用 Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) 部分。

## 下载并安装权限管理共享应用程序

1.  转到 Microsoft 网站上的 [Microsoft 权限管理](http://go.microsoft.com/fwlink/?LinkId=303970) 页。

2.  在“计算机”  部分中，单击“适用于 Windows 的 RMS 应用”  图标，并保存用于安装 Microsoft Rights Management 共享应用程序的 **Setup.exe** 文件。

3.  双双击已下载的 Setup.exe 文件。 如果系统提示你继续，请单击 **“是”**。

4.  在 **“安装 Microsoft RMS”** 页上，单击 **“下一步”**，然后等待安装完成。

    > [!NOTE]
    > RMS 共享应用程序需要 Microsoft .NET Framework（最低版本 4.0）。 安装程序会进行检查以查看是否安装了此组件，如果未安装，你将看到一封包含安装链接的邮件。

5.  安装完成后，请单击 **“重启”** 以重新启动计算机并完成安装。 或者，单击“关闭”  ，在稍后重启计算机以完成安装。

现在，你可以随时开始保护你的文件或阅读其他人保护的文件。

## 如果你不是本地管理员，而且使用 Office 2010
如果你登录到计算机而没有本地管理权限，并且安装程序检测到你已安装 Office 2010，就会显示一条警告消息，指出某些方案将不适用于此配置。 这些方案包括：

-   如果组织使用 Azure 信息保护中的 Azure Rights Management 服务，而不是本地版本的 Rights Management，那么：

    -   Office 的信息权限管理 (IRM) 功能将不可用。 例如，电子邮件的“不转发”选项，以及可在 Word 和 Excel 的“文件”菜单中设置的“限制访问”权限。 你可以使用功能区中的“共享保护项”选项，以及文件资源管理器中的右键单击选项。

-   如果组织使用的是本地版本的 Rights Management，而不是 Azure 信息保护中的 Azure Rights Management 服务，那么：

    -   无法读取使用 Azure Rights Management 服务的另一个组织中的人员发送给你的受保护的文档。

如果你不是本地管理员而使用 Office 365 或 Office 2013，你将不会看到此消息，并且支持这些方案。

你可以继续安装并接受这些已知限制。 也可停止安装，在步骤 3 中运行 Setup.exe 时使用“以管理员身份运行”选项重新运行它或请管理员为你安装。 管理员可为你[编写此安装的脚本](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)，使它可以自动安装。

## 示例和其他说明
有关如何使用 Rights Management 共享应用程序以及操作说明的示例，请参阅以下 Rights Management 共享应用程序用户指南部分：

-   [使用 RMS 共享应用程序的示例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [要执行什么操作？](sharing-app-user-guide.md#what-do-you-want-to-do)

## 另请参阅
[权限管理共享应用程序用户指南](sharing-app-user-guide.md)




<!--HONumber=Sep16_HO4-->


