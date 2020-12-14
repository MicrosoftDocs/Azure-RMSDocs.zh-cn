---
title: 下载 & 安装 Azure 信息保护统一标签客户端
description: 用户安装 Azure 信息保护统一标签客户端的说明，以便你可以对文档和电子邮件进行分类和保护。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/06/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: dcb0cf2946c59868eba0226850b5c8edb9a0f08f
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385074"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>用户指南：下载并安装 Azure 信息保护统一标签客户端

>***适用** 于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
> *适用 **于**： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 对于经典客户端，请参阅 [经典客户端用户指南](install-client-app.md)。 *

如果管理员没有为你安装 Azure 信息保护统一标签客户端，你可以自行完成此操作。 必须是电脑的本地管理员才可安装此客户端，这样可对文档和电子邮件进行标记和保护。

> [!NOTE]
> Azure 信息保护统一标签客户端要求最低版本的 Microsoft .NET Framework 4.6.2。 如果缺少此项，安装程序会尝试下载并安装此必备组件。 在客户端安装过程中安装此必备项后，必须重启计算机。
>

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>下载并安装 Azure 信息保护统一标签客户端

在安装 Azure 信息保护统一标签客户端之前，请与管理员或技术支持人员确认你使用的是 [敏感度标签](/microsoft-365/compliance/sensitivity-labels) 来分类和保护文档和电子邮件。

1. 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=53018)下载 **AzInfoProtection_UL.exe** 。

2. 运行已下载的可执行文件，如果系统提示你继续，请单击 **"是"**。

3. 在“安装 Azure 信息保护客户端”页上，阅读完许可条款和条件后，单击“我同意”。

4. 如果系统提示继续操作，请单击“是”，然后等待安装完成。

6. 单击“关闭”  。 开始使用 Azure 信息保护统一标签客户端之前：

    - 如果你的计算机运行 Office 2010，请重启计算机，然后转到下一节完成最后步骤。    
        
    - 对于其他版本的 Office，请重新启动所有 Office 应用程序和文件管理器的所有实例。 安装已完成，现可使用客户端标记和保护文档及电子邮件。

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>利用 Office 2010 安装 Azure 信息保护统一标签客户端

通过上述说明安装 Azure 信息保护统一标签客户端之后：

1. 打开 Microsoft Word。 安装 Azure 信息保护客户端后首次运行 Office 2010 应用程序时，将看到“Microsoft Azure 信息保护”对话框。 此对话框显示需要管理员凭据才可完成登录过程。

2. 在“Microsoft Azure 信息保护”对话框中，单击“确定”。

3. 如果看到“用户访问控制”对话框，请单击“是”，以便 Azure 信息保护客户端更新注册表。

安装已完成，现可使用 Azure 信息保护统一标签客户端来对文档及电子邮件进行标签和保护。

## <a name="other-instructions"></a>其他说明    
Azure 信息保护统一标签客户端用户指南中的更多操作说明。

- [您希望做什么？](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
请参阅[管理员指南](clientv2-admin-guide.md)中的[为用户安装 Azure 信息保护统一标签客户端](clientv2-admin-guide-install.md)。