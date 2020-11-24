---
title: 下载并安装 Azure 信息保护客户端
description: 说明用户如何安装适用于 Windows 的 Azure 信息保护客户端，以便分类和保护文档和电子邮件。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 49d684dc4eb0852d4545abc86f725107732ad6e9
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2020
ms.locfileid: "95565356"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-client"></a>用户指南：下载并安装 Azure 信息保护客户端

>*适用于： Active Directory Rights Management Services、 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8*
>
> 说明：  [适用于 Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)


如果管理员没有为你安装 Azure 信息保护客户端，你可自行安装。 必须是电脑的本地管理员才可安装此客户端，这样可对文档和电子邮件进行标记和保护。

此外：

- Azure 信息保护客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装此必备项。 在客户端安装过程中安装此必备项后，必须重启计算机。


## <a name="to-download-and-install-the-azure-information-protection-client"></a>下载并安装 Azure 信息保护客户端

Azure 信息保护经典客户端在3月2021中被弃用。 

若要部署 AIP 经典客户端，请打开支持票证以获取下载访问权限。

1. 运行 **AzInfoProtection.exe** 文件以开始安装。 如果系统提示你继续，请单击 **“是”**。    

1. 在“安装 Azure 信息保护客户端”页面上：     
    - 如果无法连接到云，但出于演示目的，想要通过使用本地策略查看和体验 Azure 信息保护的客户端，则选择此选项以安装演示策略。 当客户端连接到 Azure 信息保护服务时，此演示策略被替换为组织的 Azure 信息保护策略。    

    - 阅读许可条款和条件后，单击“我同意”。    

1. 如果系统提示继续操作，请单击“是”，然后等待安装完成。    

1. 单击“关闭”  。 开始使用 Azure 信息保护客户端之前：    

    - 如果你的计算机运行 Office 2010，请重启计算机，然后转到下一节完成最后步骤。    
        
    - 对于其他版本的 Office，请重新启动所有 Office 应用程序和文件管理器的所有实例。 安装已完成，现可使用客户端标记和保护文档及电子邮件。    

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>利用 Office 2010 安装 Azure 信息保护客户端    
通过上述说明安装 Azure 信息保护客户端之后：    

1. 打开 Microsoft Word。 安装 Azure 信息保护客户端后首次运行 Office 2010 应用程序时，将看到“Microsoft Azure 信息保护”对话框。 此对话框显示需要管理员凭据才可完成登录过程。

2. 在“Microsoft Azure 信息保护”对话框中，单击“确定”。

3. 如果看到“用户访问控制”对话框，请单击“是”，以便 Azure 信息保护客户端更新注册表。

你的安装已完成，现可使用 Azure 信息保护来标识和保护文档及电子邮件。

## <a name="other-instructions"></a>其他说明    
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [您希望做什么？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅[管理员指南](client-admin-guide.md)中的[为用户安装 Azure 信息保护客户端](client-admin-guide-install.md)。
 
  
