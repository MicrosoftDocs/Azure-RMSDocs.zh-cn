---
title: 使用 Azure 信息保护统一标签客户端删除标签
description: 有关如何使用 Azure 信息保护统一标签客户端从文件和电子邮件中删除敏感度标签和保护的说明。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: d22257f3c671a8a54f76ade8bb1ff4cc99ee2ed8
ms.sourcegitcommit: 9600ae255e7ccc8eeb49c50727a26e4666415fe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89447236"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>用户指南：从 Azure 信息保护标记的文件和电子邮件中删除标签和保护

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8*
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP For Windows And office 版本中的扩展支持](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。*
>
> *适用于以下内容的说明： [Azure 信息保护适用于 Windows 的统一标签客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

当 [你的计算机上安装](install-client-app.md)了 Azure 信息保护统一客户端时，你可以从文件和电子邮件中删除敏感度标签和保护。

如果你删除的敏感度标签已配置为应用保护，则此操作还会删除该文件的保护。 系统可能会提示你记录删除该标签的原因。

> [!IMPORTANT]
> 必须是文件所有者才能删除保护，或者已被授予删除保护的权限（导出**** 或完全控制**** Rights Management 权限）。

如果想要选择其他标签或一组其他的保护设置，则无需删除标签或保护。 您可以选择新标签，如有必要，您可以使用文件资源管理器定义自定义权限。 

在 Office 桌面应用程序（**Word**、**Excel**、**PowerPoint**、**Outlook**）中创建或编辑 Office 文档和电子邮件时，你可以从中删除标签和保护。 

你也可以使用**文件资源管理器**删除标签和保护，此方法支持其他文件类型，并且可以很方便地一次性从多个文件删除标签和保护。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>使用 Office 应用程序从文档和电子邮件删除标签和保护

从 " **开始** " 选项卡中，选择功能区上的 " **敏感度** " 按钮，然后清除当前选择的标签。

或者，如果选择了 "**敏感度**" 按钮中的 "**显示栏**"，则可以从 Azure 信息保护栏中选择 "**删除标签**" 图标：

![Azure 信息保护栏 - 删除标签](../media/v2delete-label.png)

如果 " **删除标签** " 图标无法立即使用，请先选择 " **编辑标签** " 图标：

![Azure 信息保护栏 - 编辑标签](../media/v2edit-label.png)

如果仍未看到 " **删除标签** " 图标，则管理员不允许你使用此选项，因为所有文档和电子邮件都必须有标签。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>使用文件资源管理器从文件中删除标签和保护

使用文件资源管理器时，可快速从单个文件、多个文件或文件夹中删除标签和保护。 选择文件夹时，将自动选择该文件夹及其所有子文件夹中的所有文件。 

1. 在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”****。

2. 删除标签：在“分类和保护 - Azure 信息保护”**** 对话框中，单击“删除标签”****。 如果标签已配置为应用保护，将自动删除该保护。

3. 从单个文件删除自定义保护：在“分类和保护 - Azure 信息保护”**** 对话框中，清除“使用自定义权限保护”**** 选项。 

4. 从多个文件删除自定义保护：在“分类和保护 - Azure 信息保护”**** 对话框中，单击“删除自定义权限”****。

5. 单击“应用”****，然后等到“工作完成”**** 消息出现即可查看结果。 然后单击 **“关闭”**。


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [您希望做什么？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    

请参阅 [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels)。

