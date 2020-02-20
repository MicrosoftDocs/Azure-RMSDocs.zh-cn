---
title: 快速入门 - 为用户配置可便于轻松保护电子邮件的标签 - AIP
description: 通过自动应用“不得转发”保护，为用户配置可保护电子邮件的标签。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: ec4271250f010156b60ff8da248ea5fcdd7e5f64
ms.sourcegitcommit: 98d539901b2e5829a2aad685d10fb13fd8d7dec4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/17/2020
ms.locfileid: "77423129"
---
# <a name="quickstart-configure-a-label-for-users-to-easily-protect-emails-that-contain-sensitive-information"></a>快速入门：为用户配置标签以便轻松保护包含敏感信息的电子邮件

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：  [适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)


本快速入门介绍如何配置现有 Azure 信息保护标签以自动应用“不得转发”保护设置。

当前的 Azure 信息保护策略已包含两个具有此配置的标签：

- 机密\仅收件人 

- 高度机密\仅收件人 

但是，如果你的策略较旧，或者在创建组织策略时未激活保护，将不会包含这些标签。 

在 5 分钟内即可完成此配置。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要具备以下条件：

1. 包含 Azure 信息保护计划 1 或计划 2 的订阅。
    
    如果没有上述任一订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

2. 已将“Azure 信息保护”窗格添加到 Azure 门户，并确认已激活保护服务。

    如果在执行这些操作时需要帮助，请参阅[快速入门：在 Azure 门户中开始](quickstart-viewpolicy.md)。

3. 用于配置的现有 Azure 信息保护。 
    
    可以使用其中一个默认标签，也可以使用已创建的标签。 如果需要有关创建新标签的帮助，请参阅[快速入门：为特定用户创建新的 Azure 信息保护标签](quickstart-label-specificusers.md)。

4. 测试新的标签：Azure 信息保护客户端（经典）必须安装在 Windows 计算机上。 
    
    若要安装经典客户端，可以转到 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection.exe  。
    
    如果对经典客户端使用了不同的标签客户端，请参阅 Microsoft 365 符合性文档，了解本教程的等效说明。 例如，[了解敏感度标签](/microsoft-365/compliance/sensitivity-labels)。

5. 测试新的标签：一台运行 Windows（最低配置为 Windows 7 Service Pack 1）的计算机，并在此计算机上，从以下类别之一登录到 Office 应用程序：
    
    - Office 应用最低版本 1805，Office 365 商业版或 Microsoft 365 商业版中的内部版本 9330.2078，前提是已为你分配了 Azure Rights Management（亦称为“适用于 Office 365 的 Azure 信息保护”）许可证。
    
    - Office 365 专业增强版。
    
    - Office 专业增强版 2019。
    
    - Office Professional Plus 2016。
    
    - Office Professional Plus 2013 Service Pack 1。
    
    - Office Professional Plus 2010 Service Pack 2。

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

## <a name="configure-an-existing-label-to-apply-the-do-not-forward-protection"></a>配置现有标签以应用“不得转发”保护

1. 打开新的浏览器窗口，以全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”  。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”  并选择“Azure 信息保护”  。
    
    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

2. 从“分类” > “标签”菜单选项中   ：在“Azure 信息保护 - 标签”  窗格上，选择要配置为应用保护的标签。 

3. 在“标签”  窗格上，查找“为包含此标签的文档和电子邮件设置权限”  。 如果之前已选择“未配置”或“删除保护”，那么在选中“保护”后，会自动打开“保护”窗格     。
    
    如果“保护”窗格未自动打开，请选择“保护”   ：
    
    ![为 Azure 信息保护标签配置保护权限](./media/info-protect-protection-bar-configured.png)。

4. 在“保护”窗格上，确保选中“Azure (云密钥)”   。
    
5. 选择“设置用户定义的权限(预览)”  。

6. 请确保选中以下选项：“在 Outlook 中应用‘不可转发’”  。

7. 如已选中，请清除以下选项：“在 Word、Excel、PowerPoint 和文件资源管理器中提示用户获取自定义权限”  。

8. 单击“保护”  窗格上的“确定”  ，再单击“标签”  窗格上的“保存”  。

标签现已配置为仅在 Outlook 中显示，并将“不得转发”保护应用于电子邮件。

## <a name="test-your-new-label"></a>测试新标签

配置的标签仅在 Outlook 中显示，适用于在为 Exchange Online 配置 [Office 365 邮件加密新功能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)时发送给组织外部任何收件人的电子邮件。

1. 在计算机上打开 Outlook 并创建新的电子邮件。 如果 Outlook 已打开，请重新启动它以强制执行策略刷新。

2. 指定收件人、电子邮件的部分文本，然后应用刚刚创建的标签。 
    
    电子邮件根据标签名称进行分类，并使用“不得转发”限制进行保护。

3. 发送电子邮件。 

于是，收件人无法转发或打印电子邮件，无法从电子邮件复制内容或保存附件，也无法将电子邮件另存为其他名称。 任何设备上的任何用户都可以读取受保护的电子邮件。

## <a name="clean-up-resources"></a>清理资源

如果不想保留此配置并返回标签以使其不应用保护，请执行以下操作：

1. 从“分类” > “标签”菜单选项中   ：在“Azure 信息保护 - 标签”  窗格上，选择配置的标签。 

3. 在“标签”  窗格上，找到“为包含此标签的文档和电子邮件设置权限”  ，选择“未配置”  ，然后选择“保存”  。

## <a name="next-steps"></a>后续步骤

此快速入门包括最少的选项，使用户可以快速配置标签，从而轻松保护其电子邮件。 但是，如果配置限制太多或限制不足，请参阅其他示例配置：

- [针对受保护电子邮件并提供限制性低于“不得转发”的权限的标签](configure-policy-protection.md#example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward)

- [加密内容但不限制谁能访问内容的标签](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)

若要了解配置可应用保护的标签的完整说明，请参阅[如何配置标签以进行 Rights Management 保护](configure-policy-protection.md)。 
