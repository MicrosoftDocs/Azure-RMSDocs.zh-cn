---
title: 下载并安装 Azure 信息保护统一标记客户端
description: 有关用户如何安装 Windows，Azure 信息保护统一标记客户，以便可以进行分类和保护的文档和电子邮件的说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 563ddb6d91ef59ee96cf00dba973b7e612bbc780
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180936"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>用户指南：下载并安装 Azure 信息保护统一标记客户端

>适用对象：*[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）*
>
> *说明：[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

如果你的管理员不会安装 Azure 信息保护统一标记的客户端为您，可以执行此操作。 必须是电脑的本地管理员才可安装此客户端，这样可对文档和电子邮件进行标记和保护。

此外：

- Azure 信息保护统一标签客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装此必备项。 在客户端安装过程中安装此必备项后，必须重启计算机。

- 如果计算机运行的是 Windows 7 SP1，Azure 信息保护统一标签客户端需要特定更新 KB 2533623。 如果电脑需要此更新但未安装更新，则安装完成后会显示一条消息，即 Azure 信息保护统一标签客户端需要此更新。 此更新安装完成后，才能使用 Azure 信息保护统一标签客户端的所有功能。 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>下载并安装 Azure 信息保护统一标签客户端

安装 Azure 信息保护统一标记客户端之前，请咨询管理员或支持人员使用 Office 365 敏感度标签。

1. 下载**AzInfoProtection_UL.exe**从[Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。

2. 运行已下载的可执行文件，如果提示你继续时，请单击**是**。

3. 在“安装 Azure 信息保护客户端”页上，阅读完许可条款和条件后，单击“我同意”。

4. 如果系统提示继续操作，请单击“是”，然后等待安装完成。

6. 单击“关闭”。 开始使用 Azure 信息保护统一标签客户端之前：

    - 如果你的计算机运行 Office 2010，请重启计算机，然后转到下一节完成最后步骤。    
        
    - 对于其他版本的 Office，请重新启动所有 Office 应用程序和文件管理器的所有实例。 安装已完成，现可使用客户端标记和保护文档及电子邮件。

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>利用 Office 2010 安装 Azure 信息保护统一标签客户端

通过上述说明安装 Azure 信息保护统一标签客户端之后：

1. 打开 Microsoft Word。 安装 Azure 信息保护客户端后首次运行 Office 2010 应用程序时，将看到“Microsoft Azure 信息保护”对话框。 此对话框显示需要管理员凭据才可完成登录过程。

2. 在“Microsoft Azure 信息保护”对话框中，单击“确定”。

3. 如果看到“用户访问控制”对话框，请单击“是”，以便 Azure 信息保护客户端更新注册表。

安装已完成，现可使用 Azure 信息保护统一标签客户端来对文档及电子邮件进行标签和保护。

## <a name="other-instructions"></a>其他说明    
Azure 信息保护中的多个操作说明统一标记的客户端用户指南：

- [要执行什么操作？](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅[安装用户的 Azure 信息保护统一标记客户](clientv2-admin-guide-install.md)从[管理员指南](clientv2-admin-guide.md)。
