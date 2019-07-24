---
title: Azure 信息保护标签的 Exchange Online 邮件流规则
description: 与配置 Azure 信息保护标签的 Exchange Online 邮件流规则相关的说明和示例。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba4e4a4d-5280-4e97-8f5c-303907db1bf5
ms.reviewer: shakella
ms.suite: ems
ms.openlocfilehash: f738f990e6a4c2f79e4eede12431c1afe15803cd
ms.sourcegitcommit: 7992e1dc791d6d919036f7aa98bcdd21a6c32ad0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68428558"
---
# <a name="configuring-exchange-online-mail-flow-rules-for-azure-information-protection-labels"></a>配置 Azure 信息保护标签的 Exchange Online 邮件流规则

>适用对象： *[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

下面介绍了如何将 Exchange Online 邮件流规则配置为使用 Azure 信息保护标签，并为特定方案应用其他保护。 例如：

- 默认标签为不应用保护的“常规”。 对于有此标签且在外部发送的电子邮件，额外应用“不转发”保护操作。

- 如果有“机密\合作伙伴”标签的附件通过电子邮件方式发送给组织外部人员，且电子邮件不受保护，请额外应用“仅加密”保护操作。

如果电子邮件受保护，将保护配置应用为操作的邮件流规则会遭忽略。 例如，如果电子邮件受“不转发”保护，Exchange 邮件流规则无法将其更改为使用“仅加密”选项。  

可以扩展和修改这些示例。 例如，添加更多条件。 若要详细了解如何配置邮件流规则，请参阅 Exchange Online 文档 [Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx)。

若要详细了解如何将邮件流规则配置为加密电子邮件，请参阅 Office 文档[在 Office 365 中将邮件流规则定义为加密电子邮件](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)。 

## <a name="prerequisite-know-your-label-guid"></a>先决条件了解标签 GUID

因为 Azure 信息保护标签存储在元数据中，所以 Exchange Online 邮件流规则可以为邮件和 Office 文档附件读取此类信息。 邮件流规则不支持为 PDF 文档检查元数据。

将邮件流规则配置为确定已标记的邮件和文档前，请确保自己知道要使用的 Azure 信息保护标签的 GUID。 

若要详细了解标签存储的元数据，以及如何确定标签 GUID，请参阅[电子邮件和文档中存储的标签信息](configure-policy.md#label-information-stored-in-emails-and-documents)。

## <a name="example-configurations"></a>示例配置

对于下面的示例，请按照以下步骤操作，新建邮件流规则：

1. 在 Web 浏览器中，使用被授予全局管理员权限的工作或学校帐户，登录 Office 365。 

2. 选择“管理员”磁贴。

3. 在 Microsoft 365 管理中心，选择“管理中心” > “Exchange”。

4. 在 Exchange 管理中心内：依次选择“邮件流” > “规则” > “+” > “新建规则”。 

> [!TIP]
> 如果在配置规则时无法使用用户界面，请尝试使用其他浏览器（如 Internet Explorer）。

当电子邮件在组织外部发送时，下面的示例有一个保护应用条件。 若要详细了解可以选择的其他条件，请参阅 [Exchange Online 中的邮件流规则条件和异常（谓词）](https://technet.microsoft.com/library/jj919235(v=exchg.150).aspx)。


### <a name="example-1-rule-that-applies-the-do-not-forward-option-to-emails-that-are-labeled-general-when-they-are-sent-outside-the-organization"></a>示例 1：向在组织外部发送时包含“常规”标签的电子邮件应用“不转发”选项的规则

在此示例中，“常规”标签的 GUID 为 0e421e6d-ea17-4fdb-8f01-93a3e71333b8。 替换为要对此规则使用的自己的标签或子标签 GUID。 

在 Azure 信息保护策略中，此标签已配置为默认标签来将电子邮件分类为“常规”，此标签未应用保护。 

1. 在“名称”中，键入规则名称（如 `Apply Do Not Forward for General emails sent externally`）。
 
2. 对于“此规则的应用条件”：依次选择“收件人位于”、“组织外部”和“确定”。

3. 依次选择“更多选项”和“添加条件”。
 
4. 对于“和”：依次选择“邮件头”和“包含任意这些字词”：
     
    a. 选择“输入文本”，再输入“`msip_labels`”。
     
    b. 选择“输入字词”，再输入“`MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;`”
    
    c. 依次选择“+”和“确定”。

5. 对于“执行以下操作”：依次选择“修改消息安全性” > “应用 Office 365 消息加密和权限保护” > “不转发”和“确定”。
    
    规则配置应看似如下：![为 Azure 信息保护标签配置的 Exchange Online 邮件流规则-示例1](./media/aip-exo-rule-ex1.png)

7. 选择“保存” 

若要详细了解“不转发”选项，请参阅[适用于电子邮件的“不转发”选项](configure-usage-rights.md#do-not-forward-option-for-emails)。

### <a name="example-2-rule-that-applies-the-encrypt-only-option-to-emails-when-they-have-attachments-that-are-labeled-confidential--partners-and-these-emails-are-sent-outside-the-organization"></a>示例 2：向在组织外部发送时附件包含“机密/合作伙伴”标签的电子邮件应用“仅加密”选项的规则

在此示例中，机密\合作伙伴子标签的 GUID 为 0e421e6d-ea17-4fdb-8f01-93a3e71333b8。 替换为要对此规则使用的自己的标签或子标签 GUID。 

此标签用于分类和保护合作伙伴协作文档。   

1. 在“名称”中，键入规则名称（如 `Apply Encrypt to emails sent externally if protected attachments`）。
 
2. 对于“此规则的应用条件”：依次选择“收件人位于”、“组织外部”和“确定”。

3. 依次选择“更多选项”和“添加条件”。
 
4. 对于“和”：依次选择“任何附件”和“包含这些属性，包括任意这些字词”：
     
    a. 依次选择“+” > “指定自定义附件属性”。
  
    b. 对于“属性”，输入“`MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled`”。
    
    c. 对于“值”，输入“`True`”
    
    d. 依次选择“保存”和“确定”。

5. 对于“执行以下操作”：依次选择“修改消息安全性” > “应用 Office 365 消息加密和权限保护” > “加密”和“确定”。
    
    规则配置应看似如下：![为 Azure 信息保护标签配置的 Exchange Online 邮件流规则-示例2](./media/aip-exo-rule-ex2.png)

6. 选择“保存” 

若要详细了解“加密”选项，请参阅[适用于电子邮件的“仅加密”选项](configure-usage-rights.md#encrypt-only-option-for-emails)。


## <a name="next-steps"></a>后续步骤

若要了解如何创建和配置用于 Exchange Online 邮件流规则的标签，请参阅[配置 Azure 信息保护策略](configure-policy.md)。

此外，为了帮助对包含附件的电子邮件进行分类，请考虑使用以下 Azure 信息保护[策略设置](configure-policy-settings.md)：对于带有附件的电子邮件，使用与这些附件的最高等级相匹配的标签。


