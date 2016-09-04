---
title: "如何从 Azure 经典门户激活 Azure Rights Management | Azure RMS"
description: "如果你有权访问 Azure 门户，请使用这些说明。 例如，你有企业移动性套件订阅或 Azure Rights Management Premium 订阅。"
author: cabailey
manager: mbaldwin
ms.date: 06/27/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 573aa437d8449212bd2f22b532342e4c7e3a1be6


---

# 如何从 Azure 经典门户激活 Azure Rights Management

>*适用于：Azure Rights Management*


如果你有权访问 Azure 门户，请使用这些说明。 例如，你有企业移动性套件订阅或 Azure Rights Management Premium 订阅。

> [!TIP]
> 观看 2 分钟的视频：[如何激活 Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  注册 Azure 帐户后，[登录到 Azure 经典门户](http://go.microsoft.com/fwlink/p/?LinkID=275081)。 使用全局管理员帐户，例如用于获取包含 Azure Rights Management 的订阅的帐户。

2.  在左窗格中，单击“ACTIVE DIRECTORY” 。

3.  在 **“Active Directory”** 页中，单击 **“权限管理”**。

4.  选择要进行 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的待管理目录，单击“激活”，然后确认你的操作。

    > [!NOTE]
    >如果看到激活错误，可能是因为你的服务计划或产品版本不包括 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。
    >
    >使用 [支持 Azure RMS 的云订阅](../get-started/requirements-subscriptions.md) 中的信息确认是否提供 RMS 支持。 若要获取有关此问题的帮助，请发送电子邮件至 [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS)。


**“权限管理状态”** 现在应该显示 **“活动”** ，而 **“激活”** 选项将替换为 **“停用”**。

## Azure 经典门户中的 Rights Management 状态值和说明
除了 **“活动”** 状态（该状态指示权限管理服务已启用并可供使用）外，你可能还会看到 **“非活动”**、**“不可用”** 或 **“未授权”**。

|状态值|说明|
|----------------|---------------|
|**“活动”**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 已启用并可供使用。|
|**非活动**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 已禁用，必须先将其激活，然后组织才能保护文件。|
|**Unavailable**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务已关闭。 请稍后重试。|
|**未授权**|你无权查看[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]服务的状态。 例如，你的帐户已被锁定，或者你不是所选租户的全局管理员。|

## 后续步骤
返回 [激活 Azure Rights Management](activate-service.md)。


<!--HONumber=Aug16_HO4-->


