---
title: Azure 信息保护标签的 Exchange Online 邮件流规则
description: 与配置 Azure 信息保护标签的 Exchange Online 邮件流规则相关的说明和示例。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ROBOTS: NOINDEX
ms.reviewer: shakella
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7c76e7e79acb0cd12bfcbe2d71a1fee3ce78b1ba
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164277"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>配置 Azure 信息保护标签的 Exchange Online 邮件流规则

>适用范围：**[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)
>
>***相关** 内容：适用于 [Windows 的 Azure 信息保护经典客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 有关统一的标记客户端，请参阅 Microsoft 365 文档中的 " [了解敏感度标签](/microsoft-365/compliance/sensitivity-labels) 和 [DLP 标签](/microsoft-365/compliance/dlp-sensitivity-label-as-condition) "。 *

> [!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护经典客户端和标签管理将于 2021 年 3 月 31 日弃用   。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

下面介绍了如何将 Exchange Online 邮件流规则配置为使用 Azure 信息保护标签，并为特定方案应用其他保护。 例如：

- 默认标签为不应用保护的“常规”。 对于有此标签且在外部发送的电子邮件，额外应用“不转发”保护操作。

- 如果通过电子邮件将包含 **机密 \ 合作伙伴** 标签的附件通过电子邮件发送给组织外部的人员，而不保护电子邮件，请应用 "仅加密" 保护操作。

如果电子邮件受保护，将保护配置应用为操作的邮件流规则会遭忽略。 例如，通过 "不转发" 保护的电子邮件无法被 Exchange 邮件流规则更改为使用 "仅加密" 选项。  

可以扩展和修改这些示例。 例如，添加更多条件。 有关配置邮件流规则的详细信息，请参阅 exchange online 文档 [中的邮件流规则 (传输规则) 在 Exchange online 中](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) 。

有关配置邮件流规则以加密电子邮件的详细信息，请参阅 Office 文档 [中的定义用于加密电子邮件的邮件流规则 Microsoft 365](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8) 。 

## <a name="prerequisite-know-your-label-guid"></a>必备组件：知道标签 GUID

因为 Azure 信息保护标签存储在元数据中，所以 Exchange Online 邮件流规则可以为邮件和 Office 文档附件读取此类信息。 邮件流规则不支持为 PDF 文档检查元数据。

将邮件流规则配置为确定已标记的邮件和文档前，请确保自己知道要使用的 Azure 信息保护标签的 GUID。 

若要详细了解标签存储的元数据，以及如何确定标签 GUID，请参阅[电子邮件和文档中存储的标签信息](configure-policy.md#label-information-stored-in-emails-and-documents)。

## <a name="example-configurations"></a>示例配置

对于下面的示例，请按照以下步骤操作，新建邮件流规则：

1. 在 web 浏览器中，使用已被授予全局管理员权限的工作或学校帐户登录到 Microsoft 365。 

2. 选择 " **管理员** " 磁贴。

3. 在 Microsoft 365 管理中心，选择 "**管理中心**  >  **Exchange**"。

4. 在 Exchange 管理中心中：**邮件流**  >  **规则**  >  **+**  >  **创建新规则**。 

> [!TIP]
> 如果在配置规则时无法使用用户界面，请尝试使用其他浏览器（如 Internet Explorer）。

当电子邮件在组织外部发送时，下面的示例有一个保护应用条件。 有关您可以选择的其他条件的详细信息，请参阅 [Exchange Online 中的邮件流规则条件和异常 (谓词) ](/exchange/security-and-compliance/mail-flow-rules/conditions-and-exceptions)。


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>示例 1：向在组织外部发送时包含“常规”标签的电子邮件应用“不转发”选项的规则

在此示例中，“常规”标签的 GUID 为 0e421e6d-ea17-4fdb-8f01-93a3e71333b8。 替换为要对此规则使用的自己的标签或子标签 GUID。 

在 Azure 信息保护策略中，此标签已配置为默认标签来将电子邮件分类为“常规”，此标签未应用保护。 

1. 在“名称”中，键入规则名称（如 `Apply Do Not Forward for General emails sent externally`）。
 
2. 对于“此规则的应用条件”：依次选择“收件人位于”、“组织外部”和“确定”。

3. 依次选择“更多选项”和“添加条件”。
 
4. 对于“和”，依次选择“邮件头”和“包含任意这些字词”：
     
    a. 选择“输入文本”，再输入“`msip_labels`”。
     
    b. 选择“输入字词”，再输入“`MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True`”
    
    c. 选择 **+** ""，然后选择 **"确定"**。

5. 对于“执行以下操作”：依次选择“修改消息安全性” > “应用 Office 365 消息加密和权限保护” > “不转发”和“确定”。
    
    规则配置现在应如下所示：  ![ 为 Azure 信息保护标签配置的 Exchange Online 邮件流规则-示例1](./media/aip-exo-rule-ex1.png)

7. 选择“保存” 

若要详细了解“不转发”选项，请参阅[适用于电子邮件的“不转发”选项](configure-usage-rights.md#do-not-forward-option-for-emails)。

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>示例2：当电子邮件具有标记为 " **机密 \ 伙伴** " 的附件，并且在组织外部发送这些电子邮件时，将 "仅加密" 选项应用于电子邮件的规则

在此示例中，机密\合作伙伴子标签的 GUID 为 0e421e6d-ea17-4fdb-8f01-93a3e71333b8。 替换为要对此规则使用的自己的标签或子标签 GUID。 

此标签用于分类和保护合作伙伴协作文档。   

1. 在“名称”中，键入规则名称（如 `Apply Encrypt to emails sent externally if protected attachments`）。
 
2. 对于“此规则的应用条件”：依次选择“收件人位于”、“组织外部”和“确定”。

3. 依次选择“更多选项”和“添加条件”。
 
4. 对于“和”：依次选择“任何附件”和“包含这些属性，包括任意这些字词”：
     
    a. 选择 " **+**  >  **指定自定义附件属性**"。
  
    b. 对于“属性”，输入“`MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`”。
    
    c. 对于“值”，输入“`True`”
    
    d. 依次选择“保存”和“确定”。

5. 对于“执行以下操作”：依次选择“修改消息安全性” > “应用 Office 365 消息加密和权限保护” > “加密”和“确定”。
    
    规则配置现在应如下所示：  ![ 为 Azure 信息保护标签配置的 Exchange Online 邮件流规则-示例2](./media/aip-exo-rule-ex2.png)

6. 选择“保存” 

有关加密选项的详细信息，请参阅 [电子邮件的仅加密选项](configure-usage-rights.md#encrypt-only-option-for-emails)。


## <a name="next-steps"></a>后续步骤

若要了解如何创建和配置用于 Exchange Online 邮件流规则的标签，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

此外，若要分类包含附件的电子邮件，请考虑使用以下 Azure 信息保护[策略设置](configure-policy-settings.md)：对于有附件的电子邮件，应用与这些附件的最高分类匹配的标签。