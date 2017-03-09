---
title: "删除 Azure 信息保护标签"
description: "说明了如何从由 Azure 信息保护标记的文件中，或从受 Rights Management 保护的文件中，删除标签和保护。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/01/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f77200fa8a305c0306c41470bda7aa5a54951909
ms.openlocfilehash: e6fe5edfeb165839260371942cbf59922853a342
ms.lasthandoff: 03/02/2017


---

# <a name="remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>从由 Azure 信息保护标记的文件和电子邮件中，或从受 Rights Management 保护的文件和电子邮件中，删除标签和保护

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

如果[计算机上安装了 Azure 信息保护客户端](install-client-app.md)，你可以从文件和电子邮件中删除分类标签和保护。

如果你删除的标签已配置为应用保护，此操作也可从文件删除保护。 系统可能会提示你记录删除该标签的原因。

> [!IMPORTANT]
> 必须是文件所有者才能删除保护，或者已被授予删除保护的权限（Rights Management 提取或完全控制权限）。

如果想要选择其他标签或一组其他的保护设置，则无需删除标签或保护。 请改为选择一个新标签，如有必要，可定义自定义权限。 

在 Office 桌面应用程序（**Word**、**Excel**、**PowerPoint**、**Outlook**）中创建或编辑 Office 文档和电子邮件时，你可以从中删除标签和保护。 

你也可以使用**文件资源管理器**删除标签和保护，此方法支持其他文件类型，并且可以很方便地一次性从多个文件删除标签和保护。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>使用 Office 应用程序从文档和电子邮件删除标签和保护

在信息保护栏上，单击“删除标签”图标：

![Azure 信息保护栏 - 删除标签](../media/delete-label.png)

如果不能直接使用“删除标签”图标，请先单击“编辑标签”图标：

![Azure 信息保护栏 - 编辑标签](../media/edit-label.png)

> [!NOTE]
> 如果没有在 Office 应用程序中看到此信息保护栏：
> 
> - 你可能没有[安装](install-client-app.md) Azure 信息保护客户端，或客户端正以[仅保护模式](client-protection-only-mode.md)运行。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>使用文件资源管理器从文件中删除标签和保护

使用文件资源管理器时，可快速从单个文件、多个文件或文件夹中删除标签和保护。 选择文件夹时，将自动选择该文件夹及其所有子文件夹中的所有文件。 

1.  在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”。

2. 删除标签：在“分类和保护 - Azure 信息保护”对话框中，单击“删除标签”。 如果标签已配置为应用保护，将自动删除该保护。

3. 从单个文件删除自定义保护：在“分类和保护 - Azure 信息保护”对话框中，清除“使用自定义权限保护”选项。
    
4. 从多个文件删除自定义保护：在“分类和保护 - Azure 信息保护”对话框中，单击“删除自定义权限”。

5. 单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
