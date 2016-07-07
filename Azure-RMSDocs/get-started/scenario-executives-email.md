---
title: "方案 - 高级管理人员安全地交换特权信息 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e18cf5df-859e-4028-8d19-39b0842df33d
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: def8b7e98fd55a3d028978ffc9f8e41e38a5622c


---

# 方案 - 高级管理人员安全地交换特权信息

*适用于：Azure Rights Management、Office 365*

此方案和支持用户文档使用 Azure Rights Management 以便高级管理人员可以安全地通过电子邮件彼此交换电子邮件和附件，而策略会自动将访问权限限制为高级管理人员而无需他们采取任何特殊操作。 电子邮件和所有附件将自动由 Azure Rights Management 保护。

如果需要，可以向该规则中添加一条例外情况，如电子邮件主题中的 DNP（表示“不保护”）缩写，以便高级管理人员如需向其他高级管理人员发送未受保护的电子邮件时指定此规则 - 例如，在转发给其他人前进行审阅。

这些指令适用于下面一组情况：

-   高级管理人员彼此间共享不能与他人共享的机密信息。

-   除了发送到工作电子邮件地址而不是私人电子邮件地址外，高级管理人员在发送电子邮件时需要执行的操作没有任何不同。

-   高级管理人员如需向其他高级管理人员发送未受保护的电子邮件消息，他们有自行替代此规则的方法。

## 部署说明
![Azure RMS 快速部署的管理员指令](../media/AzRMS_AdminBanner.png)

请确保已满足以下要求，然后在进入到用户文档环节前按照支持过程的说明进行操作。

## 本方案的要求
要让针对此方案的说明生效，必须做好以下准备：

|要求|需要更多信息|
|---------------|--------------------------------|
|已准备好 Office 365 或 Azure Active Directory 的帐户和组：<br /><br />- 一个名为**高级管理人员**的启用邮件的组，所有高级管理人员均为此组的成员<br /><br />- 一个名为 **RMS 管理员**的启用邮件的组，将配置 Azure RMS 的所有管理员均为此组的成员|[准备 Azure 权限管理](https://technet.microsoft.com/library/jj585029.aspx)|
|你的 Azure 权限管理租户密钥由 Microsoft 管理；你没有使用 BYOK|[计划和实现你的 Azure Rights Management 租户密钥](https://technet.microsoft.com/library/dn440580.aspx)|
|已激活 Azure Rights Management|[激活 Azure 权限管理](https://technet.microsoft.com/library/jj658941.aspx)|
|以下配置之一：<br /><br />- 已为 Azure Rights Management 启用了 Exchange Online<br /><br />- 已为 Exchange 内部部署安装和配置了 RMS 连接器|对于 Exchange Online：请参阅[为 Azure Rights Management 配置应用程序](https://technet.microsoft.com/library/jj585031.aspx)中的 **Exchange Online：IRM 配置**部分。<br /><br />对于 Exchange 内部部署：请参阅[部署 Azure Rights Management 连接器](https://technet.microsoft.com/library/dn375964.aspx)|
|已按下文所述配置了自定义模板|[为 Azure Rights Management 配置自定义模板](https://technet.microsoft.com/library/dn642472.aspx)|
|已按本文之后章节所述为 IRM 配置了传输保护规则|对于 Exchange Online：请参阅[创建传输保护规则](https://technet.microsoft.com/library/dd302432.aspx)<br /><br />对于 Exchange 2013：请参阅[创建传输保护规则](https://technet.microsoft.com/library/dd302432%28v=exchg.150%29.asp)<br /><br />对于 Exchange 2010：请参阅[创建传输保护规则](https://technet.microsoft.com/en-us/library/dd302432%28v=exchg.141%29.aspx)|

### 为高级管理人员配置自定义模板

1.  在 Azure 经典门户中：为 Azure Rights Management 创建一个新的自定义模板，其中包含以下值和设置：

    -   名称： **高级管理人员**

    -   权限：授予启用邮件的**高级管理人员**组**共有者**权限

    -   范围：选择启用邮件的**高级管理人员**组和启用邮件的 **RMS 管理员**组。

2.  发布新的模板。

3.  仅 Exchange Online 适用：使用 Windows PowerShell for Exchange Online 命令刷新模板：

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates -RMSOnline
    ```

### 为 IRM 配置传输规则

-   使用从过程信息表中引用的 Exchange 文档创建具有以下设置的传输规则：

    -   名称：**对高级管理人员电子邮件应用高级管理人员模板**

    -   将**高级管理人员**组指定为该规则和其他条件的发件人和收件人。

    -   有关如何进行操作，请选择“对以下邮件应用权限保护”，然后选择你配置的“高级管理人员”模板。

    -   添加要包含在主题中的 **DNP**（“不保护”的缩写）例外情况或你选择用于表示此例外的词。

    -   请确保已配置规则以“强制实施”。

## 用户文档说明
如果不想提供有关如何在电子邮件主题中指定 **DNP** 或者所选例外情况的词或短语的说明，则不会向用户提供此方案的过程信息，因为保护发送自/发送到高级管理人员的电子邮件不需要他们进行特殊操作。 电子邮件和所有附件会自动受到保护，以便只有高级管理人员组的成员可以访问它们。

但是，可能需要告知高级管理人员和技术支持这些电子邮件会自动受到保护以及这对他们使用电子邮件有哪些限制。 例如，如果这些电子邮件或附件之后转发给其他人，则无法被其他人成功查阅。 如已配置 DNP（或等效）例外，请确保技术支持了解此配置，以便高级管理人员可以自行替代该规则，而无需请求 Exchange 管理员进行操作。

使用以下模板，将此公告复制并粘贴到最终用户的通信中，并进行这些修改以反映你的环境：

1.  将该*&lt;组织名称&gt;*实例替换为你的组织的名称。

2.  如果从该例外的 DNP 中选择了不同的字符串，则相应地更换该值和指令。

3.  将 *&lt;emaildomain&gt;* 替换为你组织的电子邮件域名。

4.  将*&lt;联系人详细信息&gt;*替换为有关用户如何与技术支持联系的说明，例如网站链接、电子邮件地址或电话号码。

5.  对该公告进行其他任何所需的修改，然后将其发送给这些用户。

示例文档演示了在你完成自定义后，用户看到此公告的可能形式。

![Azure RMS 快速部署的用户文档模板](../media/AzRMS_UsersBanner.png)

### IT 公告：&lt;组织名称&gt;高级管理人员电子邮件现已自动受到保护
从现在起，每次将电子邮件发送给公司内的其他&lt;组织名称&gt;高级管理人员时，电子邮件的内容和所有附件将自动受到保护，只有公司内的其他高级管理人员可以访问并进行阅读、打印、复制信息等操作。 即使将电子邮件转发给其他人或保存附件，此限制仍适用。 这种保护可帮助防止机密和敏感信息的数据丢失。

请注意，如果希望其他不是&lt;组织名称&gt;高级管理人员的人能够阅读和编辑电子邮件中所发送的信息，必须单独向这些人发送电子邮件。 或者，在电子邮件信息主题中的任何地方键入字母 **DNP**（“不保护”的缩写）以替代自动保护。

将公司机密信息发送给其他&lt;组织名称&gt;高级管理人员时，请记得发送到其工作电子邮件地址（*名称*@&lt;emaildomain&gt;），而不要发送到私人电子邮件地址。

**需要帮助吗?**

-   与技术支持联系：&lt;联系人详细信息&gt;

### 示例用户文档
![Azure RMS 快速部署的用户文档示例](../media/AzRMS_ExampleBanner.png)

#### IT 公告：VanArsdel 高级管理人员电子邮件现已自动受到保护
从现在起，每次将电子邮件发送给公司内的其他 VanArsdel 高级管理人员时，电子邮件的内容和所有附件将自动受到保护，只有公司内的其他高级管理人员可以访问并进行阅读、打印、复制信息等操作。 即使将电子邮件转发给其他人或保存附件，此限制仍适用。 这种保护可帮助防止机密和敏感信息的数据丢失。

请注意，如果希望其他不是 VanArsdel 高级管理人员的人能够阅读和编辑电子邮件中所发送的信息，必须单独向这些人发送电子邮件。 或者，在电子邮件信息主题中的任何地方键入字母 **DNP**（“不保护”的缩写）以替代自动保护。

将公司机密信息发送给其他 VanArsdel 高级管理人员时，请记得发送到其工作电子邮件地址（*名称*@vanarsdelltd.com），而不要发送到私人电子邮件地址。

**需要帮助吗?**

-   请联系技术支持：helpdesk@vanarsdelltd.com




<!--HONumber=Jun16_HO4-->


