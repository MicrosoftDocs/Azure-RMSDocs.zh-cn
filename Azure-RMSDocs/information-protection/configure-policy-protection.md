---
title: "如何配置标签以应用权限管理保护 |Azure 权限管理"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 00b4cd2b1e7b1196cedd39d7052db534e781bb13
ms.openlocfilehash: 7a20b59c404959c4ec209e8c29ac61ab71233e87


---

# 如何配置标签以应用权限管理保护

>*适用于：Azure 信息保护预览版*

**[ 此信息是预发布版本，可能会进行更改。 ]**

你可以使用 Azure 权限管理的加密、标识和授权策略保护最敏感的文档和电子邮件，以帮助防止数据丢失。 配置标签以使用权限管理模板时，将应用此保护。 

此模板可以是激活 Azure 权限管理时自动创建的默认模板或自定义模板之一。 支持部门模板，但仅当文档或电子邮件作者属于模板配置的作用域时应用保护。 如果用户不在作用域内，则会看到 Azure 信息保护不能应用标签的消息。

## 保护的工作原理

Azure 权限管理接受文档或电子邮件时，它会在处于静态时和传输过程中进行加密，并只能由经过授权的用户进行解密。 文档或电子邮件的这种加密保持不变，即使将其重命名。 此外，你可以配置使用权限和限制，如下面的示例：

- 只有组织内的用户可以打开文档或电子邮件。

- 只有市场营销部门中的用户可以编辑和打印文档或电子邮件，而组织中的所有其他用户只能查看文档或电子邮件。

- 用户不能转发电子邮件。

- 不能在指定日期后打开发送到业务合作伙伴的文档或电子邮件。

有关这些模板以及如何配置这些使用权限和限制的详细信息，请参阅 [为 Azure 权限管理配置自定义模板](../deploy-use/configure-custom-templates.md)(#为-azure-权限管理配置自定义模板)。

有关 Azure 权限管理及其工作原理的详细信息，请参阅 [什么是 Azure 权限管理？](../understand-explore/what-is-azure-rms.md)(#什么是-azure-权限管理？)

> [!IMPORTANT]
> 若要配置标签来应用权限管理保护，必须为组织激活 Azure 权限管理服务。 如果尚未这样做，请参阅 [激活 Azure 权限管理](../deploy-use/activate-service.md)(#激活-azure-权限管理)。


## 配置标签以应用权限管理保护

1. 登录到 [Azure 门户](https://portal.azure.com)。
 
2. 在中心菜单上单击“浏览”，然后在筛选框中开始键入“信息”。 选择“Azure 信息保护”。

3. 在“**Azure 信息保护**”边栏选项卡上，选择要配置为可视标记的标签以应用权限管理保护。

4. 在“**标签**”边栏选项卡的“**设置 RMS 模板以保护包含此标签的文档和电子邮件**”部分中，配置以下各项：

    - 如果看到“**RMS 模板选择自**”：选择“**Azure RMS**”。 
    
        在没有 Microsoft 的帮助下，请不要选择“**AD RMS**”和关联的配置选项。 如果你有兴趣针对 Active Directory 权限管理服务测试 Azure 信息保护，请向 askipteam@microsoft.com 发送一封电子邮件。 
    
    - 对于“**选择 RMS 模板**”：单击下拉框，并选择想要使用此此标签来保护文档和电子邮件的模板。

        > [!NOTE] 如果在打开后“**标签**”边栏选项卡后创建了新模板，则关闭此边栏选项卡，并返回到步骤 3，以便从 Azure 中检索新创建的模板供你选择。

5. 单击“保存” 。

6. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## 后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organization-s-policy)(#配置组织的策略) 部分中的链接。  



<!--HONumber=Jul16_HO5-->


