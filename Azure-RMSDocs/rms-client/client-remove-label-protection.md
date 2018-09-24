---
title: 删除 Azure 信息保护标签
description: 说明了如何从由 Azure 信息保护标记的文件中，或从受 Rights Management 保护的文件中，删除标签和保护。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/28/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ''
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 31a325e31c8a7829f660080311f60181aa595ee7
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2018
ms.locfileid: "44148029"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>用户指南：从由 Azure 信息保护标记的文件和电子邮件中，或从受 Rights Management 保护的文件和电子邮件中，删除标签和保护

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7

如果[计算机上安装了 Azure 信息保护客户端](install-client-app.md)，你可以从文件和电子邮件中删除分类标签和保护。

如果你删除的标签已配置为应用保护，此操作也可从文件删除保护。 系统可能会提示你记录删除该标签的原因。

> [!IMPORTANT]
> 必须是文件所有者才能删除保护，或者已被授予删除保护的权限（导出或完全控制 Rights Management 权限）。

如果想要选择其他标签或一组其他的保护设置，则无需删除标签或保护。 转而选择新的标签，必要时可定义自定义权限（若管理员允许此配置）。 

在 Office 桌面应用程序（**Word**、**Excel**、**PowerPoint**、**Outlook**）中创建或编辑 Office 文档和电子邮件时，你可以从中删除标签和保护。 

你也可以使用**文件资源管理器**删除标签和保护，此方法支持其他文件类型，并且可以很方便地一次性从多个文件删除标签和保护。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>使用 Office 应用程序从文档和电子邮件删除标签和保护

在信息保护栏上，单击“删除标签”图标：

![Azure 信息保护栏 - 删除标签](../media/delete-label.png)

如果不能直接使用“删除标签”图标，请先单击“编辑标签”图标：

![Azure 信息保护栏 - 编辑标签](../media/edit-label.png)

如果仍然看不到“删除标签”图标，则表示管理员禁止你使用此选项。

> [!NOTE]
> 如果没有在 Office 应用程序中看到此信息保护栏：
>
> - 如果在功能区上看到“保护”按钮：选择“保护”，然后选择“显示栏”。
> 
> - 你可能没有[安装](install-client-app.md) Azure 信息保护客户端，或客户端正以[仅保护模式](client-protection-only-mode.md)运行。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>使用文件资源管理器从文件中删除标签和保护

使用文件资源管理器时，可快速从单个文件、多个文件或文件夹中删除标签和保护。 选择文件夹时，将自动选择该文件夹及其所有子文件夹中的所有文件。 

1. 在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护”。

2. 删除标签：在“分类和保护 - Azure 信息保护”对话框中，单击“删除标签”。 如果标签已配置为应用保护，将自动删除该保护。

3. 从单个文件删除自定义保护：在“分类和保护 - Azure 信息保护”对话框中，清除“使用自定义权限保护”选项。 
    
    如果未看到“使用自定义权限进行保护”选项，则表示管理员禁止你使用此选项。
    
4. 从多个文件删除自定义保护：在“分类和保护 - Azure 信息保护”对话框中，单击“删除自定义权限”。
    
    如果未看到“删除自定义权限”选项，则表示管理员禁止你使用此选项。

5. 单击“应用”，然后等到“工作完成”消息出现即可查看结果。 然后单击 **“关闭”**。


## <a name="other-instructions"></a>其他说明
有关操作方法说明的详细信息，请参阅 Azure 信息保护用户指南：

- [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>为管理员提供的其他信息    
有关启用“让自定义权限选项可供用户使用”策略设置的配置说明，请参阅[配置 Azure 信息保护策略设置](../configure-policy-settings.md)。

其他配置说明：[配置 Azure 信息保护策略](../configure-policy.md)。

