---
title: "如何配置 Azure 信息保护的全局策略设置 | Azure 权限管理"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 508161474bf6fd7406668de3976206947de254de


---

# 如何配置 Azure 信息保护的全局策略设置

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

Azure 信息保护策略中有 3 个设置适用于所有用户、所有设备：

![Azure 信息保护策略全局设置](../media/info-protect-policy-settings.png)


配置这些设置：

1. 如果尚未这样做，请登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“浏览”，然后在“筛选”框中开始键入**信息**。 选择“Azure 信息保护”。

2. 在“**Azure 信息保护**”边栏选项卡上，配置这些全局设置：

    - **所有文档和电子邮件都必须有标签**：此选项设置为“**打开**”时，所有已保存的文档和发送的电子邮件都必须应用标签。 标记可能由用户手动分配，或因[条件](configure-policy-classification.md)自动分配，或（通过设置“**选择默认标签**”选项）默认分配。 

    如果在用户保存文档或发送电子邮件时未分配标签，系统会提示你选择一个标签：

    ![Azure 信息保护提示新分类是否较低](../media/info-protect-enforce-label.png)

    - **选择默认标签**：当设置此选项时，选择标签以分配给没有标签的文档和电子邮件。 如果具有子标签，不能将标签设置为默认标签。 

    - **在降低的敏感度级别时，用户必须提供理由**：此选项设置为“**打开**”且用户将现有文档或电子邮件的标签更改为具有较低敏感度级别的标签时（例如，从“**秘密**”到“**公共**”），系统会提示用户提供此操作的说明。 例如，用户可能会解释该文档不再包含敏感信息。 在其本地 Windows 事件日志中记录他们的操作和理由：**应用程序** > **Microsoft Azure 信息保护**。  

    ![Azure 信息保护提示新分类是否较低](../media/info-protect-lower-justification.png)

    此选项不适用于子标签。

3. 单击“**保存**”以保存更改。

4. 若要使所做的更改应用于用户，请单击“**发布**”。

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organization-s-policy)(#配置组织的策略) 部分中的链接。  












<!--HONumber=Aug16_HO2-->


