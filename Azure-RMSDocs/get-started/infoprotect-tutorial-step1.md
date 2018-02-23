---
title: "快速入门教程步骤 1 - AIP"
description: "快速试用 Azure 信息保护入门教程步骤 1 - 激活保护服务。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 30f86870bb2302ff61641ffa4c10e3da6b5c3f9b
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="step-1-activate-protection"></a>步骤 1：激活保护
 
>适用于：Azure 信息保护

> [!NOTE]
>即使已为租户激活了 Azure Rights Management 服务，仍请完成此步骤确认激活状态。 说明包括登录到 Azure 门户和创建 Azure 信息保护边栏选项卡的相关信息，以便为执行步骤 2 做好准备。 

如果已激活 Azure 权限管理服务，则可以保护组织最敏感的文档和电子邮件，并在将这些文档与其他人共享时跟踪受保护文档的使用状况。 激活保护的方式有多种，包括使用 Windows PowerShell，以及使用管理门户。

对于本教程，我们将使用 Azure 门户，该门户也是为用户配置标签的位置。 

## <a name="to-activate-the-azure-rights-management-service"></a>激活 Azure Rights Management 服务

1. 使用租户的全局管理员帐户登录到 [Azure 门户](https://portal.azure.com)。 
    
    如果你不是全局管理员，可以使用以下[管理角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)之一：信息保护管理员或安全管理员。

2. 在中心菜单上，单击“新建”，然后从 **MARKETPLACE** 列表中选择“安全 + 标识”。 
    
3.  在“安全 + 标识”边栏选项卡上，从“特别推荐的应用”列表中选择“Azure 信息保护”。 然后，在“Azure 信息保护”边栏选项卡上，单击“创建”。
    
    此操作将创建“Azure 信息保护”边栏选项卡，以便下次登录到门户时，可以从中心的“更多服务”列表中选择该服务。 
    
    > [!TIP] 
    > 选择“固定到仪表板”以便在仪表板上创建“Azure 信息保护”磁贴，这样，下次登录到门户时，就可以跳过浏览到该服务。

4. 注意：首次连接到该服务时，系统将自动打开“快速入门”页上的信息。 你可以稍后返回到此信息。 对于本教程，选择“保护激活”。 

5. 现在，可查看是否已为租户激活 Azure Rights Management 服务。 
    
    - 如果服务已激活，会看到以下确认信息：
        
        ![Azure RMS 的 Azure 信息保护状态](../media/info-protect-azurerms-activated.png)
        
    - 如果服务未激活，会在状态信息中看到此反馈和激活选项：
        
        ![Azure RMS 的 Azure 信息保护状态](../media/info-protect-azurerms-deactivated.png)

6. 如果服务未激活，请选择“激活”。 

    激活完成后，信息栏将显示“激活已成功完成”。

这就是完成本教程第一步所要执行的所有操作。 可以转到步骤 2。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于激活 Rights Management|[激活 Azure Rights Management](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; 简介](infoprotect-quick-start-tutorial.md)
[步骤 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
