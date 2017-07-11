---
title: "AIP 方案 - 控制在 SharePoint 中存储的文档"
description: "此方案和支持性的用户文档使用 Azure Rights Management 保护，通过使用受保护的库确保对存储在 SharePoint 中的 Office 文档保留控制。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/11/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3815ed1fdfd7b5201dfec258e6c20364c0397a8b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
<a id="scenario---retain-control-of-documents-stored-in-sharepoint" class="xliff"></a>

# 方案 - 保留对 SharePoint 中所存储文档的控制

>*适用于：Azure 信息保护、Office 365*

此方案和支持性的用户文档使用 Azure 信息保护中的 Azure Rights Management 技术，通过使用受保护的库确保对存储在 SharePoint 中的 Office 文档保留控制。 例如，文档会自动防范由用户意外或有意泄露，并且即使在下载或同步后，你也可以阻止对内容的访问。 你想要保护的文件可能是用于在设计文档或计划上进行内部协作的，或者是用于其他交付的。 为 SharePoint 配置受保护的库时，存储在其中的 Office 文件将受 Azure Rights Management 的保护。

这些指令适用于下面一组情况：

-   员工使用 SharePoint 库中的 Office 文档进行共享和协作。

-   员工不需要设置或更改管理员在库级别设置的权限。

-   员工不需要与组织外部的人员共享这些文档。

<a id="deployment-instructions" class="xliff"></a>

## 部署说明
![Azure RMS 快速部署的管理员指令](../media/AzRMS_AdminBanner.png)

在进入到用户文档环节前，请确保已满足以下要求并完成了以下支持流程。

<a id="requirements-for-this-scenario" class="xliff"></a>

## 本方案的要求
要让此应用场景成立，必须做好以下准备：

|要求|需要更多信息|
|---------------|--------------------------------|
|已准备好 Office 365 或 Azure Active Directory 的帐户和组|[准备 Azure 信息保护](../plan-design/prepare.md)|
|已激活 Azure Rights Management|[激活 Azure Rights Management](../deploy-use/activate-service.md)|
|如果使用 SharePoint Server：部署 RMS 连接器并针对 SharePoint 进行配置|[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)|
|为要保护的 SharePoint 站点配置权限|[管理列表、库、文件夹、文档或列表项的权限](https://support.office.com/en-ca/article/Manage-permissions-for-a-list-library-folder-document-or-list-item-9d13e7df-a770-4646-91ab-e3c117fcef45)<br /><br />[将信息权限管理应用于列表或库](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|
|为 IRM 和受保护的库配置 SharePoint|[在 SharePoint 管理中心设置信息权限管理 (IRM)](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[将信息权限管理应用于列表或库](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

<a id="to-configure-the-sharepoint-library-for-irm-settings" class="xliff"></a>

### 为 IRM 设置配置 SharePoint 库

1.  配置了 SharePoint 以使用 IRM 服务后，请导航到 SharePoint 库以使用 Azure RMS 进行保护。 在站点的“设置”&gt;“信息权限管理(IRM)”页中，除选择“下载时限制此库的权限”为管理员指定策略标题、为用户指定策略说明外，还应单击“显示选项”。

2.  选择以下项：

    -   **不允许用户上传不支持 IRM 的文档**

    -   可选：**允许组保护。默认组**，然后指定可能需要协作处理存储在此库中但位于 SharePoint 外部的文档的其他组的名称。 例如，销售组对站点具有编辑权限，而该组中有人下载了文档，将其保存到磁盘，并通过电子邮件将其发送给同事。 只有当该同事是设计组的成员时，才能访问该文档（具有编辑权限）。

        如果不使用此选项，则只有具有 SharePoint 库访问权限的用户才能通过直接从 SharePoint 下载该文档对其进行协作处理。 此限制适用于很多情况。

<a id="user-documentation-instructions" class="xliff"></a>

## 用户文档说明
本方案没有针对用户的过程说明，因为受保护的库不需要用户采取任何特殊操作。 根据 SharePoint 管理员为站点设置的权限，文档在下载时会自动受到保护。 但是，请通知用户有关此更改的信息以便他们可以心里有数，并让技术支持了解受保护的库有哪些，以及这将如何限制文档的使用。 例如，由于当前限制，这些文档可以查看但不能在移动设备上进行编辑。 如果配置了组保护，请让用户知道哪些组可以访问和编辑 SharePoint 外部的文档。

使用以下模板，将此公告复制并粘贴到最终用户的通信中，并进行这些修改以反映你的环境：

1.  将 *&lt;SharePoint 库的名称&gt;*的每个实例替换为你为 Azure Rights Management 配置的 SharePoint 库的名称和链接。 如果此通信用于多个受保护的库，请相应地更改说明。

2.  如果配置了**允许组保护。默认组**选项，将*&lt;组名&gt;*替换为已配置的组的名称并提供&lt;此组具有可对文件进行协作处理的访问权限但不是通过使用 SharePoint 库实现的原因&gt;的原因。 如果未配置此选项，请删除此语句。

3.  将*&lt;联系人详细信息&gt;*替换为有关用户如何与技术支持联系的说明，例如网站链接、电子邮件地址或电话号码。

4.  对该公告进行其他任何所需的修改，然后将其发送给这些用户。

示例文档演示了在你完成自定义后，用户看到此公告的可能形式。

![Azure RMS 快速部署的用户文档模板](../media/AzRMS_UsersBanner.png)

<a id="it-announcement-changes-to-the-ltname-of-sharepoint-librarygt-site" class="xliff"></a>

### IT 公告：对 &lt;SharePoint 库的名称&gt;站点的更改
SharePoint 站点 **&lt;SharePoint 库的名称&gt;**现已进行了安全协作配置。 现在，只有&lt;组名&gt;的成员可以从此站点打开这些文档，即使将这些文档保存在本地或通过电子邮件发送给其他人也是如此。 例外情况是，你可以在下载了这些文档后将其共享给&lt;组名&gt;的成员，以便&lt;此组具有可对文件进行协作处理的访问权限但不是通过使用 SharePoint 库实现的原因&gt;。 当你编辑这些文件时，你会在文档顶部看到黄色信息横幅，让你知道它已受到此保护以及谁可以访问它们。

此更改有助于确保我们的公司机密数据安全，而不会让不应看到它的人读取。 如果你使用移动设备访问这些受保护的文档，你可以查看它们，但你必须使用桌面设备才能编辑它们。

如果 &lt;SharePoint 站点的名称&gt;站点不支持安全协作，则无法将文档上传到该站点。

**需要帮助吗？**

-   与技术支持联系：&lt;联系人详细信息&gt;

<a id="example-user-documentation" class="xliff"></a>

### 示例用户文档
![Azure RMS 快速部署的用户文档示例](../media/AzRMS_ExampleBanner.png)

<a id="it-announcement-changes-to-the-sales-forecasts-and-reports-site" class="xliff"></a>

#### IT 公告：对“销售预测和报告”站点的更改
SharePoint 站点 **销售预测和报告**现已进行了安全协作配置。 现在，只有销售和营销团队的成员可以从此站点打开这些文档，即使你将这些文档保存在本地或通过电子邮件发送给其他人，也是如此。 例外情况是，你可以在下载这些文档后与财务团队的成员共享这些文档，以便他们可以提取每月预测数字。 当你编辑这些文件时，你会在文档顶部看到黄色信息横幅，让你知道它已受到此保护以及谁可以访问它们。

此更改有助于确保我们的公司机密数据安全，而不会让不应看到它的人读取。 如果你使用移动设备访问这些受保护的文档，你可以查看它们，但你必须使用桌面设备才能编辑它们。

如果“销售预测和报告”站点不支持安全协作，你不能将文档上载到该站点。

**需要帮助吗？**

-   与技术支持联系：helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]