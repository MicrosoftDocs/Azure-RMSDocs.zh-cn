---
title: 下载并安装 Azure 信息保护客户端
description: 说明用户如何安装适用于 Windows 的 Azure 信息保护客户端，以便分类和保护文档和电子邮件。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 1a6c9076f29d588464c03b33140a454a541b2891
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86046413"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-client"></a>用户指南：下载并安装 Azure 信息保护客户端

>*适用于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8*
>
> 说明：[适用于 Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)


如果管理员没有为你安装 Azure 信息保护客户端，你可自行安装。 必须是电脑的本地管理员才可安装此客户端，这样可对文档和电子邮件进行标记和保护。

此外：

- Azure 信息保护客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装此必备项。 在客户端安装过程中安装此必备项后，必须重启计算机。


## <a name="to-download-and-install-the-azure-information-protection-client"></a>下载并安装 Azure 信息保护客户端    

1. 请转到 Microsoft 网站上的 [Microsoft Azure 信息保护](https://go.microsoft.com/fwlink/?LinkId=303970)页。

    此页面包含指向所有可能使用的常用设备的链接，以便在需要打开受保护的文件时可轻松下载查看其应用。 如果不是电脑的本地管理员，仍可安装适用于 Windows 的查看器应用。 但这些说明用于安装完整的客户端，实现对文件的标记和保护。 

2. 找到 **Azure 信息保护客户端**部分，然后单击 Windows 图标。 单击“下载”**** 并保存 **AzInfoProtection.exe** 文件。     

3. 运行已下载的可执行文件。 如果系统提示你继续，请单击 **“是”**。    

4. 在“安装 Azure 信息保护客户端”**** 页面上：     
    - 如果无法连接到云，但出于演示目的，想要通过使用本地策略查看和体验 Azure 信息保护的客户端，则选择此选项以安装演示策略。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。    

    - 阅读许可条款和条件后，单击“我同意”****。    

5. 如果系统提示继续操作，请单击“是”****，然后等待安装完成。    

6. 单击“关闭” 。 开始使用 Azure 信息保护客户端之前：    

    - 如果你的计算机运行 Office 2010，请重启计算机，然后转到下一节完成最后步骤。    
        
    - 对于其他版本的 Office，请重新启动所有 Office 应用程序和文件管理器的所有实例。 安装已完成，现可使用客户端标记和保护文档及电子邮件。    

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>利用 Office 2010 安装 Azure 信息保护客户端    
通过上述说明安装 Azure 信息保护客户端之后：    

1. 打开 Microsoft Word。 安装 Azure 信息保护客户端后首次运行 Office 2010 应用程序时，将看到“Microsoft Azure 信息保护”**** 对话框。 此对话框显示需要管理员凭据才可完成登录过程。

2. 在“Microsoft Azure 信息保护”**** 对话框中，单击“确定”****。

3. 如果看到“用户访问控制”**** 对话框，请单击“是”****，以便 Azure 信息保护客户端更新注册表。

你的安装已完成，现可使用 Azure 信息保护来标识和保护文档及电子邮件。

## <a name="other-instructions"></a>其他说明    
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [你希望做什么？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅[管理员指南](client-admin-guide.md)中的[为用户安装 Azure 信息保护客户端](client-admin-guide-install.md)。
 
  
