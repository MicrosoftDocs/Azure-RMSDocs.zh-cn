---
title: 下载 & 安装 Azure 信息保护统一标签客户端
description: 用户安装 Azure 信息保护统一标签客户端的说明，以便你可以对文档和电子邮件进行分类和保护。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 8f9cef00aa9320b88bb756027d646415eb27301c
ms.sourcegitcommit: fbd1834eaacb17857e59421d7be0942a9a0eefb2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445130"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>用户指南：下载并安装 Azure 信息保护统一标签客户端

>适用于：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8，带 SP1 的 Windows 7
>
> *适用于以下内容的说明： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

如果管理员没有为你安装 Azure 信息保护统一标签客户端，你可以自行完成此操作。 必须是电脑的本地管理员才可安装此客户端，这样可对文档和电子邮件进行标记和保护。

此外：

- Azure 信息保护统一标签客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装此必备项。 在客户端安装过程中安装此必备项后，必须重启计算机。

- 如果计算机运行的是 Windows 7 SP1，Azure 信息保护统一标签客户端需要特定更新 KB 2533623。 如果电脑需要此更新但未安装更新，则安装完成后会显示一条消息，即 Azure 信息保护统一标签客户端需要此更新。 此更新安装完成后，才能使用 Azure 信息保护统一标签客户端的所有功能。 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>下载并安装 Azure 信息保护统一标签客户端

在安装 Azure 信息保护统一标签客户端之前，请与管理员或技术支持人员确认你使用的是[敏感度标签](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)来分类和保护文档和电子邮件。

1. 从[Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载**AzInfoProtection_UL** 。

2. 运行已下载的可执行文件，如果系统提示你继续，请单击 **"是"** 。

3. 在“安装 Azure 信息保护客户端”页上，阅读完许可条款和条件后，单击“我同意”。

4. 如果系统提示继续操作，请单击“是”，然后等待安装完成。

6. 单击 **“关闭”** 。 开始使用 Azure 信息保护统一标签客户端之前：

    - 如果你的计算机运行 Office 2010，请重启计算机，然后转到下一节完成最后步骤。    
        
    - 对于其他版本的 Office，请重新启动所有 Office 应用程序和文件管理器的所有实例。 安装已完成，现可使用客户端标记和保护文档及电子邮件。

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>利用 Office 2010 安装 Azure 信息保护统一标签客户端

通过上述说明安装 Azure 信息保护统一标签客户端之后：

1. 打开 Microsoft Word。 安装 Azure 信息保护客户端后首次运行 Office 2010 应用程序时，将看到“Microsoft Azure 信息保护”对话框。 此对话框显示需要管理员凭据才可完成登录过程。

2. 在“Microsoft Azure 信息保护”对话框中，单击“确定”。

3. 如果看到“用户访问控制”对话框，请单击“是”，以便 Azure 信息保护客户端更新注册表。

安装已完成，现可使用 Azure 信息保护统一标签客户端来对文档及电子邮件进行标签和保护。

## <a name="other-instructions"></a>其他说明    
有关 Azure 信息保护统一标签客户端用户指南的详细操作方法说明：

- [要执行什么操作？](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅[管理员指南](clientv2-admin-guide.md)中的[为用户安装 Azure 信息保护统一标签客户端](clientv2-admin-guide-install.md)。
