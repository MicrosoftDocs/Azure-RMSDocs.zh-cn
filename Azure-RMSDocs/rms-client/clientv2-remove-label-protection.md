---
title: 通过用于 Windows 的 Azure 信息保护统一标记客户端删除敏感度标签
description: 若要从具有已标记为 Azure 信息保护的文件删除敏感度标签和保护的说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.suite: ems
ms.openlocfilehash: 187c36acddb8a6b2e5b1451500640dfd832a8f3f
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181104"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>用户指南：从文件和具有已标记为 Azure 信息保护的电子邮件删除标签和保护

>适用范围：*[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）*
>
> *说明：[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure 信息保护统一客户端何时[在计算机上安装](install-client-app.md)，可以从文件和电子邮件中删除敏感度标签和保护。

当您删除的敏感度标签配置为应用保护时，此操作还会从文件中移除保护。 系统可能会提示你记录删除该标签的原因。

> [!IMPORTANT]
> 必须是文件所有者才能删除保护，或者已被授予删除保护的权限（导出或完全控制 Rights Management 权限）。

如果想要选择其他标签或一组其他的保护设置，则无需删除标签或保护。 相反，选择一个新标签，如有必要，您可以通过使用文件资源管理器中定义自定义权限。 

在以下 Office 桌面应用程序中创建或编辑 Office 文档和电子邮件时，你可以删除其中的标签和保护：Word、Excel、PowerPoint、Outlook。 

你也可以使用**文件资源管理器**删除标签和保护，此方法支持其他文件类型，并且可以很方便地一次性从多个文件删除标签和保护。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>使用 Office 应用程序从文档和电子邮件删除标签和保护

从**主页**选项卡上，选择**敏感度**按钮在功能区上，清除当前所选的标签。

或者，如果所选**显示数据条**从**敏感度**按钮，可以选择**删除标签**图标从 Azure 信息保护栏：

![Azure 信息保护栏 - 删除标签](../media/v2delete-label.png)

如果**删除标签**图标不立即可用，请先选择**编辑标签**图标：

![Azure 信息保护栏 - 编辑标签](../media/v2edit-label.png)

如果仍未看到**删除标签**图标，你的管理员不允许你使用此选项，因为所有文档和电子邮件都必须都有标签。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>使用文件资源管理器从文件中删除标签和保护

使用文件资源管理器时，可快速从单个文件、多个文件或文件夹中删除标签和保护。 选择文件夹时，将自动选择该文件夹及其所有子文件夹中的所有文件。 

1. 在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”。

2. 删除标签：在“分类和保护 - Azure 信息保护”对话框中，单击“删除标签”。 如果标签已配置为应用保护，将自动删除该保护。

3. 从单个文件中删除自定义保护：在“分类和保护 - Azure 信息保护”对话框中，清除“使用自定义权限进行保护”选项。 

4. 从多个文件中删除自定义保护：在“分类和保护 - Azure 信息保护”对话框中，单击“删除自定义权限”。

5. 单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    

请参阅[概述的敏感度标签](/Office365/SecurityCompliance/sensitivity-labels)。

