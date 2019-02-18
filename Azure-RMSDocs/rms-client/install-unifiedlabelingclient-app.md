---
title: 下载并安装 Azure 信息保护统一标签客户端（预览版）
description: 有关用户安装适用于 Windows 的 Azure 信息保护统一标签客户端预览版本，以便可以对文档和电子邮件进行分类和保护的说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/17/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ee27b9aedd35ae135fc7150a3211be43ca2f092
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56250885"
---
# <a name="download-and-install-the-azure-information-protection-unified-labeling-client-preview"></a>下载并安装 Azure 信息保护统一标签客户端（预览版）

>适用于：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）

> [!NOTE]
> 此客户端处于预览状态，随时可能更改。 客户端使用统一标签存储并从 Office 365 安全与合规中心下载带有敏感度标签的策略。 必须先由安全与合规中心发布标签，才能使用这些标签。 [详细信息](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)

必须是电脑的本地管理员才可安装此预览版客户端，这样可对文档和电子邮件进行标记和保护。

此外：

- Azure 信息保护统一标签客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装此必备项。 在客户端安装过程中安装此必备项后，必须重启计算机。

- 如果计算机运行的是 Windows 7 SP1，Azure 信息保护统一标签客户端需要特定更新 KB 2533623。 如果电脑需要此更新但未安装更新，则安装完成后会显示一条消息，即 Azure 信息保护统一标签客户端需要此更新。 此更新安装完成后，才能使用 Azure 信息保护统一标签客户端的所有功能。 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>下载并安装 Azure 信息保护统一标签客户端

在安装 Azure 信息保护统一标签客户端之前，请确认 Office 365 安全与合规中心中有为用户发布的敏感度标签。 

如果你有当前从 Azure 门户发布的用于 Azure 信息保护的标签，可以[将这些标签迁移](../configure-policy-migrate-labels.md)到安全与合规中心。

1. 从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=57440)下载预览版客户端。

2. 运行已下载的可执行文件 AzInfoProtection_For_Unified_Labeling.exe。 如果系统提示你继续，请单击 **“是”**。    

3. 在“安装 Azure 信息保护客户端”页面上：     
    - 如果无法连接到云，但出于演示目的，想要通过使用本地策略查看和体验 Azure 信息保护的客户端，则选择此选项以安装演示策略。 客户端连接到 Office 365 安全与合规中心时，此演示策略将替换为组织的标签策略。

    - 阅读许可条款和条件后，单击“我同意”。    

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

## <a name="next-steps"></a>后续步骤

若要详细了解 Office 365 安全与合规中心目前使用的统一标签存储，请阅读以下博客文章：[宣布推出安全与合规中心的统一标记管理](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)。

