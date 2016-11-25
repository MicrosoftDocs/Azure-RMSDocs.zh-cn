---
title: "如何从 Office 365 管理中心预览版激活 Azure Rights Management | Azure 信息保护"
description: "有关具有 Office 365 管理中心新预览版（Office 365 管理中心预览）访问权限时的 Azure Rights Management 服务激活说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a2b3e1a2-59a0-4191-bf4c-4485ae7a70a9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 986cb20b1cf4ecebb08e5f651bbc3af9e28d884b


---

# <a name="how-to-activate-azure-rights-management-from-the-office-365-admin-center-preview"></a>如何从 Office 365 管理中心预览激活 Azure Rights Management

>*适用于：Azure 信息保护、Office 365*


仅当你在使用新的预览版本的 Office 365 管理中心（**Office 365 管理中心预览**）时，才使用这些说明。

请注意，此版本的管理中心当前处于预览阶段，并且由于对 Azure Rights Management 到 Azure 信息保护持续的品牌重塑，因此，此版本管理中心的说明没有经典版中的说明那么可靠。 在使用此版本的管理中心时，不同的客户可能会看到不同的选项。

1. 在注册包含 Rights Management 的 Office 365 计划后，[使用你的工作或学校帐户登录到 Office 365](https://portal.office.com/)，该帐户应是 Office 365 部署的全局管理员。

2. 如果未自动显示 Office 365 管理中心，请选择左上方的“应用启动程序”图标，然后选择“管理”。 “管理”  磁贴只会向 Office 365 管理员显示。

    > [!TIP]
    > 有关管理中心的帮助，请参阅 [关于 Office 365 管理中心 - 管理员帮助](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)。

3. 导航到“权限管理”页，或使用搜索功能。

    如果你是第一次使用预览版本，并且发现查看相关配置选项非常有用，我们建议你导航，如果你熟悉预览版本，并且想要直接去激活 Azure 权限管理，那么我们建议你使用搜索。 如果导航说明与你看到的内容不相符，则你可能需要在使用管理中心的预览版本期间使用搜索选项。

    - 若要浏览：请选择“设置” > “服务和外接程序” > “Microsoft Azure 信息保护” > “管理 Microsoft Azure 信息保护设置”

    - 若要搜索：请在“开始”页上的搜索框中，键入“信息保护”，再从搜索结果中单击“Microsoft Azure 信息保护”，然后单击“管理 Microsoft Azure 信息保护设置”。 如果未返回搜索结果，请尝试键入“Rights Management”，然后在搜索结果中单击“Microsoft Azure Rights Management 设置”。

        > [!NOTE]
        >如果到此选项，那么根据你的显示器，可能需要进行滚动才能看到此选项。 但如果页面上未列出此选项，并且搜索结果中未返回此选项，则可能是因为你的服务计划不包括 Azure 信息保护的 Azure 权限管理服务。
        >
        >若要激活 Azure 权限管理服务，必须拥有 [Azure Information Protection Premium plan](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)（Azure 信息保护高级计划）或 [Office 365 plan that includes Rights Management](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)（包含权限管理的 Office 365 计划）。 若要获取有关此问题的帮助，请发送电子邮件至 [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS)。

4. 在“Rights Management”页上，单击“激活”。

5. 当提示 **“是否要激活权限管理?”**时，请单击 **“激活”**。

现在，应会显示“Rights Management 已激活”  和用于停用的选项。


## <a name="next-steps"></a>后续步骤
返回 [激活 Azure Rights Management](activate-service.md)。




<!--HONumber=Nov16_HO2-->


