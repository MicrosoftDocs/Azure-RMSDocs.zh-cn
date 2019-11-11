---
title: 教程 - 使用 Azure 信息保护控制过度共享 - AIP
description: 入门教程，可便于配置和了解 Azure 信息保护客户端的高级客户端的实际效果，这些设置可发出警告、提示提供理由或阻止邮件从 Outlook 发送。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/01/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: ef93a0ee7bdcfd2caf2216bed15bd2d1d9e5436e
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559355"
---
# <a name="tutorial-configure-azure-information-protection-to-control-oversharing-of-information-using-outlook"></a>教程：配置 Azure 信息保护以使用 Outlook 控制信息的过度共享

>适用范围：  [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)
>
> 说明：  [适用于 Windows 的 Azure 信息保护客户端](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

在本教程中，你将了解如何执行以下操作：
> [!div class="checklist"]
> * 配置在 Outlook 中实现警告、证明或阻止弹出邮件的设置
> * 在实际操作中查看设置
> * 查看事件日志中记录的用户消息和操作 

用户共享信息最常见的方法之一就是通过电子邮件进行共享，但无论是以电子邮件本身还是以附件形式，这种方法都不太妥当。 可以使用数据丢失防护 (DLP) 解决方案来识别已知的敏感信息，并帮助防止敏感信息流出组织边界。 但还可以将 Azure 信息保护客户端与一些高级客户端设置一起使用，以帮助防止过度共享，并以提供实时反馈的交互式消息引导用户。

本教程将指导你完成一个基本配置，该配置仅使用一个标签来说明警告、证明以及用户可查看和答复的阻止邮件。

完成本教程需要 15 分钟。

## <a name="prerequisites"></a>必备条件 

若要完成本教程，你需要：

1. 包含 Azure 信息保护计划 2 的订阅。
    
    如果没有包含此计划的订阅，可以为组织创建一个[免费](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)帐户。

2. “Azure 信息保护”窗格已添加到 Azure 门户，并在 Azure 信息保护全局策略中发布了至少一个标签。
    
    虽然本教程使用默认标签“常规”，但如果你愿意，可以将此标签替换为另一个标签  。 如果在添加“Azure 信息保护”窗格时需要帮助，或者还没有向全局策略发布任何标签，请参阅[快速入门：将 Azure 信息保护添加到 Azure 门户和查看策略](quickstart-viewpolicy.md)。

3. 一台运行 Windows（最低配置为 Windows 7 Service Pack 1）的计算机，并在此计算机上，你可以登录 Outlook。 做好在本教程中多次重启 Outlook 的准备。

4. Windows 计算机上已安装 Azure 信息保护客户端（经典）。
    
    若要安装经典客户端，可以转到 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)，然后从“Azure 信息保护”页下载 AzInfoProtection.exe  。 
    
    如果使用的是统一标签客户端而不是经典客户端，请参阅以下说明，其中讲解了如何对本教程中的等效配置使用 PowerShell 高级设置：
    
    - 管理员指南说明：[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](./rms-client/clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - 视频：[Azure 信息保护 Outlook 弹出配置](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/)

有关使用 Azure 信息保护的先决条件的完整列表，请参阅 [Azure 信息保护的要求](requirements.md)。

让我们开始吧。

## <a name="identify-a-label-id-for-testing"></a>标识用于测试的标签 ID

对于本教程，我们将只使用一个标签来查看用户引发的行为。 可使用任何标签，但建议使用名为“常规”的默认标签进行测试，该标签通常适用于不打算供公众使用且不应用保护的业务数据  。

若要指定所选标签，必须知道其在 Azure 门户中标识的 ID：

1. 打开新的浏览器窗口，以全局管理员身份登录到 [Azure 门户](https://portal.azure.com)。然后导航到“Azure 信息保护”  。 
    
    例如，在资源、服务和文档的搜索框中：开始键入“信息”  并选择“Azure 信息保护”  。
    
    如果你不是全局管理员，请使用以下链接获取替代角色：[登录到 Azure 门户](configure-policy.md#signing-in-to-the-azure-portal)

2. 选择“分类” > “标签”，然后选择“常规”边栏选项卡以打开“标签:     。 

3. 找到窗格底部的标签 ID：
    
    ![Azure 信息保护教程 - 找到标签 ID](./media/label-id.png)

4. 复制标签 ID 值并将其粘贴到临时文件中，以便在以后的步骤中可轻松复制该值。 在本示例中，此标签 ID 值是“0e421e6d-ea17-4fdb-8f01-93a3e71333b8”  。

5. 关闭“标签: 常规”窗格，但不要关闭 Azure 门户  。

## <a name="create-a-scoped-policy-to-test-the-new-advanced-client-settings"></a>创建作用域内策略以测试新的高级客户端设置

我们将创建新的作用域内策略，以便新的高级客户端设置仅应用于你进行测试。

1. 在“Azure 信息保护 - 策略”窗格上，选择“添加新策略”   。 然后，你会看到“策略”窗格，它显示现有全局策略中的标签和设置  。

2. 指定“过度共享教程”的策略名称，可选择指定“使用 Outlook 控制过度共享的高级客户端设置”的说明   。

3. 选择“指定获取此策略的用户/组”，并使用后续窗格指定你自己的用户帐户  。

4. 帐户名显示在“策略”窗格上后，请选择“保存”且不对此窗格上的标签或设置进行其他更改   。 系统可能会提示你确认你的选择。 

此作用域内策略现已准备就绪，可添加高级客户端设置。 关闭“策略: 过度共享教程”窗格，但不要关闭 Azure 门户  。

## <a name="configure-and-test-advanced-client-settings-to-warn-prompt-for-justification-or-block-emails-that-have-the-general-label"></a>配置并测试以下高级客户端设置：警告、提示提供理由或阻止具有“常规”标签的电子邮件。

对于本教程的此步骤，我们将指定以下高级客户端设置，并依次测试每个设置：

- **OutlookWarnUntrustedCollaborationLabel**
- **OutlookJustifyUntrustedCollaborationLabel**
- **OutlookBlockUntrustedCollaborationLabel**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>创建用以警告用户电子邮件或附件具有“常规”标签的高级客户端设置

使用新创建的作用域内策略，我们将添加一个名为“OutlookWarnUntrustedCollaborationLabel”的新高级客户端设置，其中包含“常规”标签的 ID   ： 

1. 返回到“Azure信息保护 - 策略”窗格，选择“过度共享教程”旁边的上下文菜单 (...)    。 再选择“高级设置”  。

2. 在“高级设置”窗格上，键入高级设置名称“OutlookWarnUntrustedCollaborationLabel”，并为该值粘贴自己的标签 ID   。 使用示例标签 ID：
    
    
    ![Azure 信息保护教程 - 创建 OutlookWarnUntrustedCollaborationLabel 高级客户端设置 ](./media/configure-warnmessage.png)

3. 选择“保存和关闭”  。

不要关闭“策略”窗格或 Azure 门户  。

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-or-attachment-has-the-general-label"></a>如果电子邮件或附件具有“常规”标签，请测试用以警告用户的高级客户端设置

在客户端计算机上，我们现在将看到配置此高级客户端设置的结果。

1. 在客户端计算机上，打开 Outlook。 
    
    如果 Outlook 已打开，则重启它。 需要重启才能下载我们刚刚进行的更改。

2. 创建新的电子邮件，并应用“常规”标签  。 例如，在“文件”选项卡中，选择“保护”按钮，然后选择“常规”    。

3. 为“收件人”字段指定自己的电子邮件地址，并为主题键入“测试警告消息的常规标签”   。 然后，发送电子邮件。

4. 作为高级客户端设置的结果，你会看到以下警告，要求在发送电子邮件之前进行确认。 例如：
    
    ![Azure 信息保护教程 - 请参阅 OutlookWarnUntrustedCollaborationLabel 高级客户端设置 ](./media/see-warnmessage.png)
    
5. 如果作为用户，你失误地尝试通过电子邮件发送标记为“常规”的内容，请选择“取消”   。 你将看到没有发送电子邮件，但是电子邮件消息仍然存在，因此可以进行更改，例如更改内容或标签。

6. 不做任何更改，再次选择“发送”  。 这一次，如果你已确认内容适合发送，请选择“确认并发送”  。 电子邮件已发送。

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>更改提示用户证明电子邮件具有“常规”标签的高级客户端设置

我们将编辑现有的高级客户端设置以保留你的“常规”标签 ID，但会将名称更改为“OutlookJustifyUntrustedCollaborationLabel”   ： 

1. 在“Azure信息保护 - 策略”窗格上，选择“过度共享教程”旁边的上下文菜单 (...)    。 再选择“高级设置”  。

2. 在“高级设置”窗格上，使用新名称“OutlookJustifyUntrustedCollaborationLabel”替换你先前创建的高级设置名称“OutlookWarnUntrustedCollaborationLabel”    ：
    
    ![Azure 信息保护教程 - 创建 OutlookJustifyUntrustedCollaborationLabel 高级客户端设置 ](./media/configure-justifymessage.png)

3. 选择“保存和关闭”  。

不要关闭“策略”窗格或 Azure 门户  。

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-has-the-general-label"></a>测试提示用户证明电子邮件具有“常规”标签的高级客户端设置

在客户端计算机上，我们现在将看到此新高级客户端设置的结果。

1. 在客户端计算机上，重启 Outlook 以下载我们刚刚进行的更改。

2. 创建新的电子邮件，并像以前一样，应用“常规”标签  。 例如，在“文件”选项卡中，选择“保护”按钮，然后选择“常规”    。

3. 为“收件人”字段指定自己的电子邮件地址，并为主题键入“测试证明消息的常规标签”   。 然后，发送电子邮件。

4. 此时，你会看到以下消息，要求在发送电子邮件之前提供理由。 例如：
    
    ![Azure 信息保护教程 - 请参阅 OutlookJustifyUntrustedCollaborationLabel 高级客户端设置 ](./media/see-justifymessage.png)
    
5. 如果作为用户，你失误地尝试通过电子邮件发送标记为“常规”的内容，请选择“取消”   。 你将看到没有发送电子邮件，但是电子邮件消息本身仍然存在，因此可以进行更改，例如更改内容或标签。

6. 不做任何更改，再次选择“发送”  。 此时，选择其中一个理由选项，例如“我确认收件人已获得批准，有权共享此内容”，然后选择“确认并发送”   。 电子邮件已发送。

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>更改阻止用户发送具有“常规”标签的电子邮件的高级客户端设置

我们将再次编辑现有的高级客户端设置以保留你的“常规”标签 ID，但会将名称更改为“OutlookBlockUntrustedCollaborationLabel”   ： 

1. Azure 门户中，在“Azure信息保护 - 策略”窗格上，选择“过度共享教程”旁边的上下文菜单 (...)    。 再选择“高级设置”  。

2. 在“高级设置”窗格上，使用新名称“OutlookBlockUntrustedCollaborationLabel”替换你先前创建的高级设置名称“OutlookJustifyUntrustedCollaborationLabel”    ：
    
    ![Azure 信息保护教程 - 创建 OutlookBlockUntrustedCollaborationLabel 高级客户端设置 ](./media/configure-blockmessage.png)

3. 选择“保存和关闭”  。

不要关闭“策略”窗格或 Azure 门户  。

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label"></a>测试阻止用户发送具有“常规”标签的电子邮件的高级客户端设置

在客户端计算机上，我们现在将看到此新高级客户端设置的结果。

1. 在客户端计算机上，重启 Outlook 以下载我们刚刚进行的更改。

2. 创建新的电子邮件，并像以前一样，应用“常规”标签  。 例如，在“文件”选项卡中，选择“保护”按钮，然后选择“常规”    。

3. 为“收件人”字段指定自己的电子邮件地址，并为主题键入“测试阻止消息的常规标签”   。 然后，发送电子邮件。

4. 此时，会显示阻止发送电子邮件的以下消息。 例如：
    
    ![Azure 信息保护教程 - 阻止电子邮件弹出消息](./media/see-blockmessage.png)

5. 作为你的用户，你会看到唯一可用的选项是“确定”，该选项将你带回到可进行更改的电子邮件中  。 选择“确定”，并取消这封电子邮件  。

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-general-label"></a>使用“事件日志”标识“常规”标签的消息和用户操作

在我们转到下一个方案之前，当电子邮件或附件没有标签时，请启动事件查看器并导航到“应用程序和服务日志” > Azure 信息保护   。

对于执行的每个测试，都会创建信息事件以记录消息和用户响应：

- 警告消息：信息 ID 301

- 验证消息：信息 ID 302

- 阻止邮件：信息 ID 303

例如，第一个测试是警告用户，你选择了“取消”，因此第一个事件 301 中的“用户响应”显示为“已取消”    。 例如：

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Dismissed
```

但随后你选择了“确认并发送”，这反映在下一个事件 301 中，其中“用户响应”显示为“已确认”    ：

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Warn message.msg
Item Name: Testing the General label for the Warn message
Process Name: OUTLOOK
Action: Warn
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
User Response: Confirmed
```

对于证明消息重复相同的模式，其具有事件 302。 第一个事件的“用户响应”为“已取消”，第二个事件显示所选的理由   。 例如：

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Justify message.msg
Item Name: Testing the General label for the Justify message
Process Name: OUTLOOK
Action: Justify
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
User Justification: I confirm the recipients are approved for sharing this content
Action Source: 
User Response: Confirmed

```

在事件日志的顶部，可以看到已记录的阻止邮件，其中有一个事件 303。 例如：

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing the General label for the Block message.msg
Item Name: Testing the General label for the Block message
Process Name: OUTLOOK
Action: Block
Label After Action: General
Label ID After Action: 0e421e6d-ea17-4fdb-8f01-93a3e71333b8
Action Source: 
```

### <a name="optional-create-an-additional-advanced-client-setting-to-exempt-these-messages-for-internal-recipients"></a>可选：创建附加高级客户端设置，以便为内部收件人免除这些邮件

使用自己的电子邮件地址作为收件人测试了警告、证明邮件的合理性并阻止邮件。 在生产环境中，只有当收件人位于组织外部时，才可以选择仅为指定的标签显示这些邮件。 可以将该免除扩展到组织经常与之合作的合作伙伴。

为了说明这个过程，我们将创建一个名为“OutlookBlockTrustedDomains”的附加高级客户端设置，并从电子邮件地址指定你自己的域名  。 这样可以防止你之前看到的阻止邮件向在其电子邮件地址中共享你的域名的收件人显示，但仍会向其他收件人显示。 同样，可以为“OutlookWarnTrustedDomains”和“OutlookJustifyTrustedDomains”创建附加高级客户端设置   。

1. Azure 门户中，在“Azure信息保护 - 策略”窗格上，选择“过度共享教程”旁边的上下文菜单 (...)    。 再选择“高级设置”  。

2. 在“高级设置”窗格上，键入高级设置名称“OutlookBlockTrustedDomains”，然后从电子邮件地址中粘贴域名以获取该值   。 例如：
    
    ![Azure 信息保护教程 - 创建 OutlookBlockTrustedDomains 高级客户端设置](./media/configure-exemptblockdomain.png)

4. 选择“保存和关闭”  。 不要关闭“策略”窗格或 Azure 门户  。

5. 现在重复[上一个测试以阻止用户发送包含“常规”标签的电子邮件](#test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-has-the-general-label)，当你使用自己的电子邮件地址时，不再看到阻止邮件。 电子邮件不间断地发送。
    
    要确认仍然显示外部收件人的阻止邮件，请再次重复测试，但这次指定一个组织外部的收件人。 此时，你再次看到阻止邮件，同时将新收件人地址列为不可信。

## <a name="configure-and-test-an-advanced-client-setting-to-warn-prompt-for-justification-or-block-emails-that-dont-have-a-label"></a>配置和测试以下高级客户端设置：警告、提示提供理由或阻止没有标签的电子邮件

对于本教程的此步骤，我们将指定一个具有不同值的新高级客户端设置，并依次测试每个设置：

- **OutlookUnlabeledCollaborationAction**

### <a name="create-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>如果电子邮件没有标签，请创建用以警告用户的高级客户端设置

此名为“OutlookUnlabeledCollaborationAction”的新高级客户端设置不需要标签 ID，但指定了对未标记内容采取的操作  ： 

1. Azure 门户中，返回到“Azure信息保护 - 策略”窗格上，选择“过度共享教程”旁边的上下文菜单 (...)    。 再选择“高级设置”  。

2. 在“高级设置”窗格上，键入高级设置名称“OutlookUnlabeledCollaborationAction”，并为值指定“警告”    ：
    
    ![Azure 信息保护教程 - 使用警告值创建 OutlookUnlabeledCollaborationAction 高级客户端设置 ](./media/configure-nolablewarn.png)

3. 选择“保存和关闭”  。

不要关闭“策略”窗格或 Azure 门户  。

### <a name="test-the-advanced-client-setting-to-warn-users-if-an-email-doesnt-have-a-label"></a>如果电子邮件没有标签，请测试用以警告用户的高级客户端设置

在客户端计算机上，我们现在将看到在内容没有标签时配置此新的高级客户端设置的结果：

1. 在客户端计算机上，重启 Outlook 以下载我们刚刚进行的更改。

2. 创建新的电子邮件，这次不要应用标签。

3. 为“收件人”字段指定自己的电子邮件地址，并为主题键入“测试发送不带警告消息的标签的电子邮件”   。 然后，发送电子邮件。

4. 这次可看到“需要确认”消息，可选择“确认并发送”或“取消”    ：
    
    ![Azure 信息保护教程 - 请参阅使用警告值的 OutlookUnlabeledCollaborationAction 高级客户端设置](./media/see-nolablewarn.png)

5. 选择“确认并发送”  。

### <a name="change-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-is-unlabeled"></a>更改提示用户证明电子邮件为未标记的高级客户端设置

我们将编辑现有的高级客户端设置以保留“OutlookUnlabeledCollaborationAction”的名称，但将值更改为“证明”   ： 

1. 在“Azure信息保护 - 策略”窗格上，选择“过度共享教程”旁边的上下文菜单 (...)    。 再选择“高级设置”  。

2. 在“高级设置”窗格上，找到“OutlookUnlabeledCollaborationAction”设置，并使用新值“证明”替换之前的“警告”值     ：
    
    ![Azure 信息保护教程 - 将 OutlookUnlabeledCollaborationAction 高级客户端设置更改为证明值](./media/configure-justifymessage2.png)

3. 选择“保存和关闭”  。

不要关闭“策略”窗格或 Azure 门户  。

### <a name="test-the-advanced-client-setting-to-prompt-users-to-justify-if-an-email-isnt-labeled"></a>测试提示用户证明电子邮件为未标记的高级客户端设置

在客户端计算机上，我们现在将看到更改此高级客户端设置的值的结果。

1. 在客户端计算机上，重启 Outlook 以下载我们刚刚进行的更改。

2. 创建新的电子邮件，与以前一样，不要应用标签。

3. 为“收件人”字段指定自己的电子邮件地址，并为主题键入“测试发送不带证明消息的标签的电子邮件”   。 然后，发送电子邮件。

4. 这次，会显示“所需理由”消息，其中包含不同的选项  ：
    
    ![Azure 信息保护教程 - 请参阅使用证明值的 OutlookUnlabeledCollaborationAction 高级客户端设置](./media/see-nolabljustify.png)

5. 选择一个选项，例如“我的经理批准共享此内容”  。 然后，选择“确认并发送”  。

### <a name="change-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>更改阻止用户发送未标记的电子邮件的高级客户端设置

和之前一样，我们将编辑现有的高级客户端设置以保留“OutlookUnlabeledCollaborationAction”的名称，但将值更改为“阻止”   ： 

1. 在“Azure信息保护 - 策略”窗格上，选择“过度共享教程”旁边的上下文菜单 (...)    。 再选择“高级设置”  。

2. 在“高级设置”窗格上，找到“OutlookUnlabeledCollaborationAction”设置，并将上一个值“证明”替换为新值“阻止”     ：
    
    ![Azure 信息保护教程 - 将 OutlookUnlabeledCollaborationAction 高级客户端设置更改为阻止值](./media/configure-blockmessage2.png)

3. 选择“保存和关闭”  。

不要关闭“策略”窗格或 Azure 门户  。

### <a name="test-the-advanced-client-setting-to-block-users-from-sending-an-email-that-isnt-labeled"></a>测试阻止用户发送未标记电子邮件的高级客户端设置

在客户端计算机上，我们现在将看到更改此高级客户端设置的值的结果。

1. 在客户端计算机上，重启 Outlook 以下载我们刚刚进行的更改。

2. 创建新的电子邮件，与以前一样，不要应用标签。

3. 为“收件人”字段指定自己的电子邮件地址，并为主题键入“测试发送不带阻止消息的标签的电子邮件”   。 然后，发送电子邮件。

4. 此时，会显示以下消息，以阻止发送电子邮件，并附有用户说明。 例如：
    
    ![Azure 信息保护教程 - 请参阅使用“阻止”值的 OutlookWarnUntrustedCollaborationLabel 高级客户端设置](./media/see-blockmessage2.png)

5. 作为你的用户，你会看到唯一可用的选项是“确定”，该选项将带你回到可以选择标签的电子邮件中  。
    
    选择“确定”，并取消这封电子邮件  。

### <a name="use-event-log-to-identify-the-messages-and-user-actions-for-the-unlabeled-email"></a>使用“事件日志”标识未标记电子邮件的消息和用户操作

与以前一样，消息和用户响应记录在事件查看器“应用程序和服务日志” > “Azure 信息保护”中，并具有相同的事件 ID   。

- 警告消息：信息 ID 301

- 验证消息：信息 ID 302

- 阻止邮件：信息 ID 303

例如，电子邮件没有标签时，理由提示会显示以下结果：

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Testing send an email without a label for the Justify message.msg
Item Name: Testing send an email without a label for the Justify message
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```

## <a name="clean-up-resources"></a>清理资源

如果你不想保留在本教程中所做的更改，请执行以下操作：

1. Azure 门户中，在“Azure信息保护 - 策略”窗格上，选择“过度共享教程”旁边的上下文菜单 (...)    。 然后选择“删除策略”  。

2. 如果系统提示你确认，请选择“确定”  。

重启 Outlook，以便不再为我们为本教程配置的设置进行配置。

## <a name="next-steps"></a>后续步骤

为了更快地进行测试，本教程使用电子邮件发送给单个收件人，并且没有附件。 但是，你可以对多个收件人、多个标签应用相同的方法，并将相同的逻辑应用于电子邮件附件，其标签状态通常对用户不太明显。 例如，电子邮件本身标记为“公共”，但附加的 PowerPoint 演示文稿标记为“常规”。 有关配置选项的详细信息，请参阅管理指南中的以下部分：[在 Outlook 中实现弹出消息，针对正在发送的电子邮件发出警告、进行验证或阻止](./rms-client/client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)

管理指南还包含有关可用于自定义客户端行为的其他高级客户端设置的信息。 有关完整列表，请参阅[可用的高级客户端设置](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings)。
