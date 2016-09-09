---
title: "配置 Azure 信息保护策略 |Azure RMS"
description: "若要配置分类、标记和保护，必须配置 Azure 信息保护策略。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: da0145444a7d0abb6407ed2ccbb581d4dcdd10d6
ms.openlocfilehash: e5b8054b3b5cb38adf2f5ae1d2f4f399d98f6e23


---

# 配置 Azure 信息保护策略

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

若要配置分类、标记和保护，必须配置 Azure 信息保护策略。 然后将此策略下载到已安装 [Azure 信息保护客户端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)(#azure-信息保护客户端) 的计算机。

在预览版本的 Azure 信息保护中配置 Azure 信息保护策略：

1. 登录到 [Azure 门户](https://portal.azure.com)。

2. 导航到“Azure 信息保护”边栏选项卡：例如，在中心菜单上，单击“浏览”并在“筛选”框中开始键入**信息保护**。 在结果中选择“Azure 信息保护”。 

    然后，你将看到“**Azure 信息保护**”边栏选项卡，可在其中配置 Azure 信息保护策略，其中包含以下元素：

    - 用户在 Office 应用程序中看到的信息保护栏的标题和工具提示。

    - 让你和用户对文档和电子邮件进行分类的标签。

    - 在用户保存文档和发送电子邮件时强制执行分类的选项。

    - 将默认标签设置为对文档和电子邮件进行分类的起始点的选项。

    - 当用户选择比原始级别低的敏感度级别时提示用户提供相应原因的选项。


Azure 的信息保护附带 [默认策略](configure-policy-default.md)(#默认策略)，其中包含**个人**、**公共**、**内部**、**机密**和**秘密**标签。 可以使用无更改的默认标签，或者你可以自定义它们，或删除它们，并可以创建新标签。

当在“Azure 信息保护”边栏选项卡上进行任何更改时，请单击“**保存**”以保存更改，或者单击“**放弃**”以返回到上一个保存的设置。 

在完成所需更改后，单击“**发布**”。 

在受支持的 Office 应用程序启动并将所做的更改作为其 Azure 信息保护策略下载时，Azure 信息保护客户端会检查任何更改。

## 配置组织的策略

使用以下信息来帮助你配置你的 Azure 信息保护策略：

- [默认信息保护策略](configure-policy-default.md)

- [如何配置全局策略设置](configure-policy-settings.md)

- [如何创建新标签](configure-policy-new-label.md)

- [如何删除或重排标签](configure-policy-delete-reorder.md)

- [如何更改或自定义现有标签](configure-policy-change-label.md)

- [如何配置标签以应用保护](configure-policy-protection.md)

- [如何配置标签以应用可视标记](configure-policy-markings.md)

- [如何为自动和建议分类配置条件](configure-policy-classification.md)

## 后续步骤

有关如何自定义默认策略并在 Office 应用程序是查看所产生行为的示例，请尝试 [Azure 信息保护快速入门教程](infoprotect-quick-start-tutorial.md)(#azure-信息保护快速入门教程)。




<!--HONumber=Aug16_HO4-->


