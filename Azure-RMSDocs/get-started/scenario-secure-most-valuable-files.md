---
title: "AIP 方案 - 保护最（较为）重要的文件"
description: "此方案和支持性的用户文档使用 Azure Rights Management 手动并自定义保护你已标识为最重要的几个文件，这保证了对文件提供最高级别的保护以阻止未经授权的访问。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 95f1844a-612c-4e67-bbe6-4b6b92295221
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: f096a4ad7333d24c7bce0dd729b40ebb203726c5
ms.lasthandoff: 02/24/2017


---

# <a name="scenario---secure-your-most-few-valuable-files"></a>方案 - 保护你最重要的（几个）文件

>*适用于：Azure 信息保护、Office 365*

此方案和支持性的用户文档使用 Azure 信息保护中的 Azure Rights Management 技术，手动并自定义保护已标识为最重要的几个文件，这保证了对文件提供最高级别的保护以阻止未经授权的访问。 通常只有少数人可以访问这些文件。 例如，公司招牌食物产品的食谱说明，或者在指定日期前不允许公开的收购计划。

这些指令适用于下面一组情况：

-   你已标识要保护的小部分文件。

-   这些文件的格式是支持 Rights Management 的一种 Office 文件格式。 如果这些文件为其他文件格式（例如，CAD 文件），请确保这些格式支持 Azure RMS，同时部署的应用程序本机支持 Azure RMS。 有关详细信息，请参阅[应用程序如何支持 Azure Rights Management 服务](../understand-explore/applications-support.md)。

-   这些文件包含只有少数人有权访问的高度机密的敏感信息。

-   对于这些人来说，一种可以接受的折衷方式是每次通过 Internet 连接获得对文件单独访问的权限，因为这样操作安全性更高。

-   他们不会要求进一步与他人共享此信息，但是可以修改信息并保存更改。

-   管理员必须能够跟踪访问文件的人员和访问时间，如有必要，还需撤销访问权限。

## <a name="deployment-instructions"></a>部署说明
![Azure RMS 快速部署的管理员指令](../media/AzRMS_AdminBanner.png)

请确保已满足以下要求，然后在进入到用户文档环节前按照支持过程的说明进行操作。

## <a name="requirements-for-this-scenario"></a>本方案的要求
针对此方案，必须做好以下准备：

|要求|需要更多信息|
|---------------|--------------------------------|
|已准备好 Office 365 或 Azure Active Directory 的帐户和组：<br /><br />- 一个名为**特别访问权**并已启用邮件的组，其中的成员应有权访问这些高度机密的文档<br /><br />- 一个名为 **IT 合规性管理员**并已启用邮件的组，其中包含负责电子发现、监视和审核的管理人员<br /><br />- 一个名为 **RMS 管理员**的启用邮件的组，将配置 Azure RMS 的所有管理员均为此组的成员|[准备 Azure 信息保护](../plan-design/deployment-roadmap.md)|
|已激活 Azure Rights Management|[激活 Azure Rights Management](../deploy-use/activate-service.md)|
|已按下文所述配置了自定义模板|[为 Azure Rights Management 服务配置自定义模板](../deploy-use/configure-custom-templates.md)|
|将 Rights Management 共享应用程序部署到 Windows 计算机中，以便你就地保护这些文件，如下一部分所述|[下载和安装 Rights Management 共享应用程序](../rms-client/install-sharing-app.md)|
|已授权的用户具有最低版本 Office 2013|如果用户安装的是 Office 2010，则还需安装 Rights Management 共享应用程序。|
|你的 Azure 信息保护订阅包括文档跟踪|如果订阅不包括文档跟踪和撤销功能，则将无法使用文档跟踪站点以查看访问这些文档的人员，也无法根据需要撤销访问权限。 在这种情况下，可以选择购买支持文档跟踪的订阅，或者接受此限制条件。 还可以考虑使用 Azure 权限管理服务的[使用日志记录](../deploy-use/log-analyze-usage.md)功能，它可以提供信息（如访问过每个文件的人员及访问时间），以帮助检测潜在的可疑行为。<br /><br />查看 Azure 信息保护网站上的[功能列表](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)。|

### <a name="to-configure-the-custom-template"></a>配置自定义模板

1.  在 Azure 经典门户中：为 Azure Rights Management 创建一个新的自定义模板，其中包含以下值和设置：

    -   名称：**特别访问权**

    -   权限：授予已启用邮件的**特别访问权**组**合著者**权限

    -   范围：选择已启用邮件的**特别访问权**组、已启用邮件的 **IT 合规性管理员**组和已启用邮件的 **RMS 管理员**组。

    -   脱机访问：**仅在建立 Internet 连接的情况下内容才可用**

2.  发布新的模板。

### <a name="to-protect-the-files-in-place"></a>就地保护文件

1.  在文件资源管理器中，导航到包含要保护的文件的第一个文件夹：

    -   如果要保护文件夹中的所有文件，则选择该文件夹。

    -   如只需保护文件夹中的部分文件，则选择多个要保护的文件。

2.  右键单击该文件，选择“使用 RMS 保护”，然后选择“就地保护”。

3.  选择“特别访问权”。

4.  系统可能会提示你输入凭据。 等待完成对所有文件的保护，然后在看到“文件已受保护”页面时单击“关闭”。

5.  如果其他文件夹中还有要保护的文件，请对每个文件夹重复以上步骤 1 到 4。

有关就地保护文件的详细信息，请参阅[使用 Rights Management 共享应用程序保护设备上的文件（就地保护）](../rms-client/sharing-app-protect-in-place.md)

> [!TIP]
> 如果此手动过程要保护的文件数过多，可以考虑使用 [RMS 保护工具](https://www.microsoft.com/en-us/download/details.aspx?id=47256)借助模板批量保护文件。

### <a name="to-monitor-and-if-necessary-revoke-access-to-the-files"></a>监视并根据需要撤消对文件的访问权限

1.  在文件资源管理器中，右键单击受保护文件，选择“使用 RMS 保护”，然后选择“跟踪使用情况”。

2.  如有提示，请登录以访问文档跟踪站点。

3.  检查已访问该文件及已保护的其他文件的人员，尤其应注意访问失败的尝试以防其存在可疑行为。 如有必要，可以撤消对每个文件的访问权限。

## <a name="user-documentation-instructions"></a>用户文档说明
本方案没有针对用户的特别说明，因为这些文件不需要用户采取任何特殊操作。 你已保护并将监视这些文件。 但是，可能需要通知用户和你的支持渠道哪些文件会受到保护以及这些保护措施对他们使用文档有哪些限制。 例如，如果已授权的用户未建立 Internet 连接，则将无法打开该文件。

使用以下模板，将此公告复制并粘贴到最终用户的通信中，并进行这些修改：

1.  提供文件的实际名称，或使用已授权的用户能理解的明确引用。

2.  将*&lt;联系人详细信息&gt;*替换为有关这些用户可以如何通过一个与文档重要性相匹配的呈报支持渠道联系技术支持或 IT 部门寻求帮助的说明。 例如，提供 24 小时高严重性支持呼叫电话号码。

3.  对该公告进行其他任何所需的修改，然后将其发送给这些用户。

示例文档演示了在你完成自定义后，用户看到此公告的可能形式。

![Azure RMS 快速部署的用户文档模板](../media/AzRMS_UsersBanner.png)

### <a name="it-announcement-protecting-ltorganization-namegts-top-secret-documents"></a>IT 公告：保护&lt;组织名称&gt;的顶级机密文档
已对以下文件应用了极高的保护级别，因此只有&lt;受限制的用户&gt;才能访问和更改这些文件。 为了防止未经授权的访问，每次打开这些文件时应用程序都会自动请求授权，因此现在必须将其连接到 Internet，系统可能还会提示你输入凭据：

-   &lt;顶级机密文档、类型或位置 1&gt;

-   &lt;顶级机密文档、类型或位置 2&gt;

-   &lt;顶级机密文档、类型或位置 3&gt;

**需要帮助吗？**

-   如果无法访问这些文件或者如果发现文件&lt;操作和联系人详细信息&gt;中存在可疑更改。

#### <a name="example-customized-user-documentation"></a>自定义用户文档示例
![Azure RMS 快速部署的用户文档示例](../media/AzRMS_ExampleBanner.png)

##### <a name="it-announcement-protecting-vanarsdels-top-secret-documents"></a>IT 公告：保护 VanArsdel 的顶级机密文档
已对以下文件应用了极高的保护级别，以便只有此电子邮件的收件人才能访问和更改这些文件。 为了防止未经授权的访问，每次打开这些文件时应用程序都会自动请求授权，因此现在必须连接到 Internet 才能打开这些文件，系统可能还会提示你输入凭据：

-   为代码名“Mercury”设计规格

-   为代码名“Jupiter”设计规格

-   为代码名“Saturn”设计规格

-   为代码名“Neptune”设计规格

**需要帮助吗？**

-   如果无法访问这些文件或者如果发现这些文件中存在可疑更改，请呼叫 IT 部门通过受保护的电子邮件发送给你的全天候支持呈报热线。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
