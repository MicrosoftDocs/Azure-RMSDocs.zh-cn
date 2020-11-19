---
title: 教程 - 使用 Azure 信息保护 (AIP) 防止过度共享
description: 有关使用 Azure 信息保护 (AIP) 客户端以防止用户过度共享内容的详细教程。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 851bc48926c6634fc7d5a529aa2910e11974f3a7
ms.sourcegitcommit: df6ee1aca02e089e3a72006ecf0747f14213979c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "94503411"
---
# <a name="tutorial-preventing-oversharing-in-outlook-using-azure-information-protection-aip"></a>教程：使用 Azure 信息保护 (AIP) 防止 Outlook 中的过度共享

>适用范围：[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
>说明：[用于 Windows 的 Azure 信息保护统一标记客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

作为系统管理员，你需要确保组织的内容保持安全，并且仅与受信任的用户共享。 用户不当共享内容的最常见方式之一是通过电子邮件。 配置策略以防止通过 Outlook 过度共享，例如仅将访问权限限制于特定用户，或仅允许用户与受信任的外部用户共享内容。

所需时间：可在 30 分钟内完成本教程。

在本教程中，你将了解：
> [!div class="checklist"]
> * 为特定标记条件配置警告、解释和阻止行为
> * 在实际操作中查看设置
> * 查看事件日志中记录的用户消息和操作 

## <a name="tutorial-prerequisites"></a>教程先决条件

在开始本教程之前，请确保满足以下系统要求。

|先决条件  |说明  |
|---------|---------|
|计算机需求     | 请确保： <br /><br />- 有 Windows 计算机，其中安装了 Azure 信息保护统一标记客户端。 有关详细信息，请参阅[快速入门：部署 Azure 信息保护 (AIP) 统一标记客户端](quickstart-deploy-client.md)。 <br /><br />- 已安装 PowerShell，并且你可以以管理员身份运行 PowerShell。 <br /><br />- 可以登录到 Outlook。 做好在本教程中多次重启 Outlook 的准备。     |
|Azure 信息保护订阅     |   你需要包含 [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection/)的 Azure 订阅。 <br /><br />如果没有上述任一订阅，则请为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。       |
|敏感度标签和测试策略     |  在策略中配置的“常规”敏感度标签。 <br /><br />在标记管理中心（包括 Microsoft 365 合规中心、Microsoft 365 安全中心或 Microsoft 365 安全与合规中心）配置敏感度标签。 有关详细信息，请参阅 [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)。 <br /><br />建议使用测试策略完成本教程，以免影响活动策略。 <br />请确保你可以随时使用策略名称以及“常规”标签的 GUID。   |
| | |

现在就开始吧。 

## <a name="implement-a-warning-message-for-emails-labeled-as-general"></a>为标记为“常规”的电子邮件实施警告消息

此过程介绍如何配置策略，以在 Outlook 用户发送标记为“常规”的电子邮件之前向其显示警告。 

用户可以选择遵循警告更改标签或内容，也可以选择继续发送电子邮件。

1. 在客户端计算机上，以管理员身份运行 PowerShell。

1. 运行以下命令，为“常规”标签定义警告消息。 复制此命令时，请将“Global”替换为策略的名称，并将长字符串替换为你自己的标签 ID。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
    ```

    在本示例中，该策略名为“Global”，“常规”标签的 GUID 为“8faca7b8-8d20-48a3-8ea2-0f96310a848e”  。

    > [!TIP]
    > 如果要将此设置应用于多个标签，请在值中列出其 GUID，用逗号分隔。

1. 在 Outlook 中测试设置：

    1. 在客户端计算机上，打开或重启 Outlook 以拉取更新的设置。

    1. 创建新的电子邮件，并应用“常规”标签。 在消息工具栏中，选择 :::image type="icon" source="media/i-sensitivity.PNG" border="false":::“敏感度”按钮，然后选择“常规” 。

    1. 使用你自己的电子邮件地址定义“收件人”字段，并将“主题”字段定义为：`Testing a warning message for the General label`，然后发送电子邮件 。

        你应看到以下警告，要求在发送电子邮件之前进行确认。 例如：

        :::image type="content" source="media/qs-tutor/ul-see-warnmessage.png" alt-text="测试“常规”标签的警告消息":::

    1. 假设你是一名用户，失误地尝试通过电子邮件发送标记为“常规”的内容。 在本例中，我们要查看警告，因此请选择“取消”。

        不会发送电子邮件，而会使其保持打开，以便你可以更改内容或标签。

    1. 无需进行任何更改，你可以确定发送内容是正当行为。 再次选择“发送”。 这一次出现警告时，请选择“确认并发送”。

        电子邮件已发送。

继续[仅在外部发送常规电子邮件时显示警告消息](#show-a-warning-message-for-general-emails-only-when-theyre-sent-externally)。

## <a name="show-a-warning-message-for-general-emails-only-when-theyre-sent-externally"></a>仅在外部发送“常规”电子邮件时显示警告消息

此过程介绍如何向之前配置的警告消息添加异常，以便仅向外部收件人显示警告消息。

在内部发送“常规”电子邮件时，将不会显示警告消息。

1. 在客户端计算机上，以管理员身份运行 PowerShell。

1. 运行以下命令，将域定义为警告消息的受信任域。 复制此命令时，请将“Global”替换为策略名称，将“contoso.com”替换为你自己的域 。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnTrustedDomains="contoso.com"}    
    ```

    > [!TIP]
    > 如果要将此设置应用于多个域（例如要添加受信任的合作伙伴），请在值中列出域，用逗号分隔。

1. 在 Outlook 中测试设置：

    1. 在客户端计算机上，打开或重启 Outlook 以拉取更新的设置。

    1. 创建新的电子邮件，并应用“常规”标签。 在消息工具栏中，选择 :::image type="icon" source="media/i-sensitivity.PNG" border="false":::“敏感度”按钮，然后选择“常规” 。

    1. 使用你自己的电子邮件地址定义“收件人”字段，并将“主题”字段定义为：`Testing a warning message for the General label`，然后发送电子邮件 。

        电子邮件发送，不显示警告。

## <a name="request-users-to-justify-sending-unlabeled-content"></a>请求用户解释发送未标记内容的理由

此过程介绍如何配置高级设置，以要求用户解释其发送未标记内容的理由。 

1. 在客户端计算机上，以管理员身份运行 PowerShell。

1. 若要让 Outlook 在用户尝试发送未标记的电子邮件时显示要求其解释理由的消息，请将“Global”替换为你的策略的名称，然后运行：
 
    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Justify"}
    ```

1. 在 Outlook 中测试设置：

    1. 在客户端计算机上，打开或重启 Outlook 以拉取更新的设置。

    1. 创建新的电子邮件，并确保没有应用标签。
    
        例如，如果策略应用默认标签，请使用 :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: 按钮删除它。 

    1. 使用你自己的电子邮件地址定义“收件人”字段，并将“主题”字段定义为：`Testing the justification message for unlabeled content`，然后发送电子邮件 。
    
        弹出项将显示为以下相似示例：

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify.png" alt-text="未标记内容的示例解释消息":::

    1. 选择一个选项。 如果选择第三项“其他，如所述”，请在文本框中输入一些示例文本。 
    
    1. 选择“确认并发送”。
    
        电子邮件已发送。

继续[自定义自由文本解释提示](#customize-the-free-text-justification-prompt)。

## <a name="customize-the-free-text-justification-prompt"></a>自定义自由文本解释提示

此过程介绍如何自定义默认解释消息中的第三个选项。 

例如，你可能希望在此处添加文本以提示用户添加特定详细信息，或提醒用户不要输入任何敏感数据。

1. 在客户端计算机上，以管理员身份运行 PowerShell。

1. 若要自定义显示的解释消息中的自由文本提示，请将“Global”替换为你的策略名称，然后运行：

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{JustificationTextForUserText="Other (please explain) - Do not enter sensitive info"}
    ```

    > [!TIP]
    > 请将引号中的值替换为你想添加的任何其他文本。 

1. 在 Outlook 中测试设置：

    1. 在客户端计算机上，打开或重启 Outlook 以拉取更新的设置。

    1. 创建新的电子邮件，并确保没有应用标签。 

        例如，如果策略应用默认标签，请使用 :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: 按钮删除它。 

    1. 使用你自己的电子邮件地址定义“收件人”字段，并将“主题”字段定义为：`Testing a customized free text justification prompt`，然后发送电子邮件 。
    
        将显示要求解释理由的弹出窗口，这次它将包含你的自定义文本。 例如： 

        :::image type="content" source="media/qs-tutor/ul-see-nolabljustify-custom.png" alt-text="包含自定义自由文本提示的示例解释提示":::
        
## <a name="block-users-from-sending-unlabeled-powerpoint-messages"></a>阻止用户发送未标记的 PowerPoint 消息

此过程介绍如何阻止用户从 Outlook 发送未标记的 PowerPoint 文件。

1. 在客户端计算机上，以管理员身份运行 PowerShell。

1. 若要阻止从 Outlook 发送未标记的内容，请将“Global”替换为你的策略名称，然后运行：

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Block"}
    ```

1. 若要将阻止行为限制于特定 PowerPoint 文件类型，请将“Global”替换为你的策略名称，然后运行：

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.POTX,.POTM,.POT,.PPTX"}
    ```

1. 在 Outlook 中测试设置：

    1. 在客户端计算机上，打开 PowerPoint 并创建新的 .pptx 文件，确保将该文件保留为未标记。

    1. 打开或重启 Outlook 以拉取更新的设置。
    
    1. 将未标记的 PowerPoint 文件附加到新的 Outlook 消息。

    1. 使用你自己的电子邮件地址定义“收件人”字段，并将“主题”字段定义为：`Testing sending unlabeled PowerPoint files`，然后发送电子邮件 。
    
        Outlook 阻止发送电子邮件，并显示以下消息：

        :::image type="content" source="media/qs-tutor/ul-see-blockmessage.png" alt-text="未标记的 PowerPoint 附件的示例阻止消息":::

继续[为未标记的 PowerPoint 消息自定义阻止消息](#customize-the-block-message-for-unlabeled-powerpoint-messages)。

## <a name="customize-the-block-message-for-unlabeled-powerpoint-messages"></a>为未标记的 PowerPoint 消息自定义阻止消息

此过程介绍如何自定义消息，在用户尝试向外部用户发送未标记的 PowerPoint 文件时显示。

> [!IMPORTANT]
> 此过程将覆盖已使用 OutlookUnlabeledCollaborationAction 高级属性定义的任何设置，仅出于教程目的显示。
>
> 在生产环境中，建议使用 OutlookUnlabeledCollaborationAction 高级属性定义规则，或使用下述 json 文件定义复杂规则，而不要同时使用这两种方法，以避免将问题复杂化。
>

**使用 json 文件定义规则：**

1. 使用以下代码创建名为 OutlookCollaborationRule_1.json 的 .json 文件 ：

    ```JSON
    {   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",
                     "LabelId" : null,
                    "Extensions": [
                                    ".PPTX",
                                    ".PPTM",
                                    ".POTX",
                                    ".POTM",
                                    ".POT",
                                    ".PPTX"
                                 ]
                    
                },
                {                   
                    "type" : "EmailLabel",
                     "LabelId" : null
                }
            ]
        },      
        {           
            "type" : "Email Block",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Email Blocked",                 
                    "Body": "Sending PowerPoint files to external recipients requires that you label your files so that we can classify and protect Contoso content.<br><br>List of attachments that are not labeled:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br>Label your document and send it again."              
                },          
            },          
            "DefaultLanguage": "en-us"      
        }   
      ] 
    }
    ```
1. 将 OutlookCollaborationRule_1.json 文件保存在客户端计算机可访问的位置。

1. 在客户端计算机上，以管理员身份运行 PowerShell。

1. 若要自定义阻止消息，请复制以下代码，将 C:\OutlookCollaborationRule_1.json 替换为 .json 文件的路径，将“General”替换为你的策略的名称 。 

    ```PowerShell
    $filedata = Get-Content "C:\OutlookCollaborationRule_1.json”
    Set-LabelPolicy -Identity General -AdvancedSettings @{OutlookCollaborationRule_1 ="$filedata"}    
    ```

    运行代码来实现 .json 文件中定义的设置。

1. 在 Outlook 中测试设置：

    1. 在客户端计算机上，打开 PowerPoint 并创建新的 .pptx 文件，确保将该文件保留为未标记。

    1. 打开或重启 Outlook 以拉取更新的设置。
    
    1. 将未标记的 PowerPoint 文件附加到新的 Outlook 消息。

    1. 使用你自己的电子邮件地址定义“收件人”字段，并将“主题”字段定义为：`Testing customized blocking message for unlabeled PowerPoint files`，然后发送电子邮件 。
    
        Outlook 阻止发送电子邮件，并显示以下消息：

        :::image type="content" source="media/qs-tutor/ul-see-custom-blockmessage.png" alt-text="不带标签的 PowerPoint 文件的自定义阻止消息":::

继续[使用“事件日志”标识“常规”标签的消息和用户操作](#use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label)。

## <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>使用“事件日志”标识“常规”标签的消息和用户操作

在本教程中，你已了解如何在 Outlook 中自定义 AIP 的行为，以防止几种类型的过度分享，包括警告、解释和阻止消息。 你还查看了本地客户端计算机上 Outlook 的行为。

现在，可以启动 Windows 事件查看器，查看日志以了解发生的操作。

**查看事件查看器以寻找 AIP 日志记录事件：**

在客户端计算机上，打开 Windows 事件查看器应用程序，然后导航到“应用程序和服务日志” > “Azure 信息保护” 。

你将看到为你执行的每个测试记录的信息事件，包括有关消息和用户响应的详细信息：

- 警告消息：信息 ID 301
- 解释消息：信息 ID 302
- 阻止邮件：信息 ID 303

例如：

- [查看警告消息测试的事件日志](#check-the-event-log-for-your-warning-message-tests)
- [查看解释消息测试的事件日志](#check-the-event-log-for-your-justify-message-tests)
- [查看阻止消息测试的事件日志](#check-the-event-log-for-your-block-message-tests)

### <a name="check-the-event-log-for-your-warning-message-tests"></a>查看警告消息测试的事件日志

第一次测试是向用户发出警告，你选择了“取消”。 在本例中，第一个事件 301 的“用户响应”显示“已忽略” ：

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

但随后你选择了“确认并发送”，这反映在下一个事件 301 中，其中“用户响应”显示为“已确认”：

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing a warning message for the General label.msg
Item Name: Testing a warning message for the General label
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

### <a name="check-the-event-log-for-your-justify-message-tests"></a>查看解释消息测试的事件日志

对于证明消息重复相同的模式，其具有事件 302。 第一个事件的“用户响应”为“已取消”，第二个事件显示所选的理由。 例如：

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the justification message for unlabeled content.msg
Item Name: Testing the justification message for unlabeled content
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

### <a name="check-the-event-log-for-your-block-message-tests"></a>查看阻止消息测试的事件日志

在事件日志的顶部，可以看到已记录的阻止邮件，其中有一个事件 303。 例如：

```
Client Version: 2.8.85.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing sending unlabeled PowerPoint files.msg
Item Name: Testing sending unlabeled PowerPoint files
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

## <a name="clean-up-resources"></a>清理资源

完成本教程后，可以保留测试策略以作进一步参考，或删除该策略以清理资源。

如果要删除策略，请到创建策略的管理中心执行此操作、包括 Microsoft 365 合规性中心、Microsoft 365 安全中心或 Microsoft 365 安全与合规中心。

有关详细信息，请参阅 [Microsoft 365 文档](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)

删除后，在客户端计算机上重启 Outlook，使其不再配置为本教程中定义的设置。

## <a name="next-steps"></a>后续步骤

为了更快地进行测试，本教程使用电子邮件发送给单个收件人，并且没有附件。 

将相同的方法应用于多个收件人和标签，或应用于附件，其中标记状态有时对用户不太明显。

例如，你可能想要在标记为“公共”的电子邮件中显示一条弹出消息，但附加了标记为“常规”的 PowerPoint 演示文稿 。

有关高级属性和 Outlook 自定义的详细信息，请参阅[管理员指南：Azure 信息保护统一标记客户端的自定义配置](rms-client/clientv2-admin-guide-customizations.md)。
