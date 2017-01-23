---
title: "下载并安装 Azure 信息保护客户端 | Azure 信息保护"
description: "说明用户如何安装适用于 Windows 的 Azure 信息保护客户端，以便分类和保护文档和电子邮件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 22af60687ad030e686ba843ced6d450487353a0e
ms.openlocfilehash: 72266181c5334ed7e03b2022df61c4065f1c3ac7


---

# <a name="download-and-install-the-azure-information-protection-client"></a>下载并安装 Azure 信息保护客户端

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

**[此版本的客户端为预览版，随时可能更改。]**

如果管理员没有为你安装 Azure 信息保护客户端，你可自行安装。 只有电脑的本地管理员才可安装此客户端。 

### <a name="office-2010-only"></a>仅限 Office 2010

使用此版本的 Office 时，Azure 信息保护客户端必须设置需要管理员权限的注册表项： 

通过说明下载和安装客户端，然后按照下一节中的 Office 2010 相关说明进行操作。

## <a name="to-download-and-install-the-azure-information-protection-client"></a>下载并安装 Azure 信息保护客户端

1.  转到 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)并下载 Azure 信息保护客户端的**预览**版本。

2. 双击已下载的可执行文件。 

3. 在“安装 Azure 信息保护客户端”页面上： 
    
    - 如果无法连接到云，但出于演示目的，想要通过使用本地策略查看和体验 Azure 信息保护的客户端，则选择此选项以安装演示策略。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。
    
    - 阅读许可条款和条件后，单击“我同意”。

4. 如果系统提示继续操作，请单击“是”，然后等待安装完成。

3. 单击“关闭”。 开始使用 Azure 信息保护客户端之前：

    - 如果你的计算机运行 Office 2010，请重启计算机，然后转到下一节完成最后步骤。
    
    - 对于其他版本的 Office，请重新启动所有 Office 应用程序和文件管理器的所有实例。 你的安装已完成，现可使用客户端标识和保护文档及电子邮件。

> [!NOTE]
> 如果计算机运行的是 Windows 7 SP1，Azure 信息保护客户端需要特定更新 [KB 2533623](https://support.microsoft.com/en-us/kb/2533623)。 如果计算机需要此更新但未安装，将在尝试使用客户端前显示一条消息：“可使用 Azure 信息保护客户端的所有功能前必须安装此更新”。

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>利用 Office 2010 安装 Azure 信息保护客户端

通过上述说明安装 Azure 信息保护客户端之后：

1. 打开 Microsoft Word。 安装 Azure 信息保护客户端后首次运行 Office 2010 应用程序时，将看到“Microsoft Azure 信息保护”对话框。 此对话框显示需要管理员凭据才可完成登录过程。

2. 在“Microsoft Azure 信息保护”对话框中，单击“确定”。

2. 如果看到“用户访问控制”对话框，请单击“是”，以便 Azure 信息保护客户端更新注册表。

你的安装已完成，现可使用 Azure 信息保护来标识和保护文档及电子邮件。

## <a name="other-instructions"></a>其他说明
有关操作方法的说明，请参阅 Azure 信息保护用户指南中的以下部分：

-   [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息
[安装 Azure 信息保护客户端](info-protect-client.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO2-->


