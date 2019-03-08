---
title: 为应用程序配置 ADAL 身份验证 - AIP
description: 配置 Azure 信息保护应用以使用基于 Azure ADAL 的身份验证的步骤
keywords: 身份验证, RMS, ADAL, 信息保护,
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 03/13/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: ec7e59cec6afe2eb4012c17bb520daa03feebd81
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331073"
---
# <a name="configure-your-app-for-adal-authentication"></a>配置应用以进行 ADAL 身份验证

本主题介绍配置应用以进行基于 Azure Active Directory 身份验证库 (ADAL) 的步骤。

## <a name="azure-authentication-setup"></a>Azure 身份验证设置

你将需要以下各项：

- [Microsoft Azure 订阅](https://azure.microsoft.com/)（使用免费试用版即可）。 有关详细信息，请参阅[用户如何注册个人 RMS](../rms-for-individuals-user-sign-up.md)
- Microsoft Azure Rights Management 的订阅（使用免费的[个人 RMS](https://technet.microsoft.com/library/dn592127.aspx) 帐户即可）。

> [!NOTE]
> 询问你的 IT 管理员你是否具有 Microsoft Azure Rights Management 订阅，请你的 IT 管理员执行以下步骤。 如果你的组织没有订阅，应请 IT 管理员创建订阅。 此外，你的 IT 管理员应使用*工作或学校帐户*而不是 *Microsoft 帐户*（即 Hotmail）进行订阅。

注册 Microsoft Azure 后：

- 使用具有管理权限的帐户登录到组织的 [Azure 管理门户](https://manage.windowsazure.com)。

![Azure 登录名](../media/AzurePortalLogin.png)

- 向下浏览到门户右侧的 **Active Directory** 应用程序。

![选择“Active Directory”](../media/AzureADPick.png)

- 如果尚未创建目录，请选择门户左下角的**新建**按钮。

![选择“新建”](../media/AzureNewBtn.png)

- 选择 **Rights Management** 选项卡，确保 **Rights Management 状态**为**活动**、**未知**或**未授权**。 如果状态为**非活动**，请选择门户正下方的**激活**按钮并确认选择。

![选择“激活”](../media/RMTab.png)

- 现在，选择目录并选择“应用程序”，以便在该目录中创建新的*本机应用程序*。

![选择“应用程序”](../media/CreateNativeApp.png)

- 然后选择门户正下方的**添加**按钮。

![选择“添加”](../media/AddAppBtn.png)

- 出现提示时，选择**添加我的组织正在开发的应用程序**。

![选择“添加我的组织正在开发的应用程序”](../media/AddAnAppPick.png)

- 选择**本机客户端应用程序**，然后选择**下一步**按钮，以便对应用程序进行命名。

![对应用进行命名](../media/TellUsInput.png)

- 添加重定向 URI，并选择“下一步”。
  重定向 URI 必须是有效的 URI 且对你的目录唯一。 例如，可以使用与 `https://contoso.azurewebsites.net/.auth/login/done` 类似的 URI

![添加重定向 URI](../media/RedirectURI.png)

- 在目录中选择你的应用程序，然后选择**配置**。

![选择“配置”](../media/ConfigYourApp.png)

>[!NOTE]
> 配置 RMS 客户端时，复制**客户端 ID** 和**重定向 URI** 并将其存储供将来使用。

- 浏览到应用程序设置的底部，选择**其他应用程序的权限**下的**添加应用程序**按钮。

>[!NOTE]
> 向 Windows Azure Active Directory 显示的**委托权限**默认情况下是正确的 – 仅应选择一个选项，即**登录并读取用户配置文件**。

![选择“添加应用程序”](../media/PermissionsToOtherBtn.png)

- 选择 **Microsoft Rights Management** 旁边的加号按钮。

![选择“+”按钮](../media/ChoosePlusBtn.png)

- 现在，选中对话框左下角的复选标记。

![选中复选标记](../media/choosecheck01.png)

- 现在即可向应用程序添加 Azure RMS 依赖关系。 若要添加依赖关系，请选择**其他应用程序的权限**下的新增 **Microsoft Rights Management Services** 项，然后选择**委托的权限:** 下拉框下的**创建和访问用户受保护内容**复选框。

![设置权限](../media/AddDependency.png)

- 选择门户正下方的**保存**图标，保存应用程序以保留更改。

![选择“保存”](../media/SaveApplication.png)

