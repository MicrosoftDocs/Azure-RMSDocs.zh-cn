---
title: "为 Azure 信息保护标签配置条件"
description: "在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: 6934675385ebd6c65585510d2157d6037a7727a2
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>如何配置 Azure 信息保护的自动和建议分类的条件

>*适用于：Azure 信息保护*

在配置标签的条件时，可以自动将标签分配到文档或电子邮件。 或者，可以提示用户选择建议的标签： 

- 自动分类适用于 Word、Excel 和 PowerPoint（如果文件已保存，并在发送电子邮件时将应用到 Outlook）。 自动分类不能用于以前手动标记的文件。
 
- 保存文件时，将建议的分类应用于 Word、Excel 和 PowerPoint。

配置条件时，可以使用预定义的模式，如“信用卡号”或“美国身份证号”。 或者，你可以定义自定义字符串或模式作为自动分类的条件。 这些条件适用于文档和电子邮件中的正文文本和页眉及页脚。 有关条件的详细信息，请参阅 [内置条件的相关信息](#information-about-the-built-in-conditions)(#内置条件的相关信息) 部分。

它们应用于多个标签时，将如何计算多个条件：

1. 根据在策略中指定的位置，将标签排序以供评估：排在第一的标签具有最低的位置（敏感度最低），排在最后的标签具有最高位置（敏感度最高）。

2. 应用最敏感的标签。
 
3. 应用最后一个子标签。

> [!TIP]
>若要获取最佳用户体验并确保业务连续性，我们建议你从用户建议分类开始，而不是自动操作。 此配置使你的用户能够接受标记或保护操作中，或覆盖这些建议（如果它们不适用于其文档或电子邮件）。

通过自定义策略提示配置条件以将标签应用于建议的操作的示例提示：

![Azure 信息保护检测和建议](../media/info-protect-recommend-callouts.png)

在此示例中，用户可以单击“**立即更改**”应用建议的标签，或通过关闭栏来覆盖该建议。

## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>配置标签的建议或自动分类

1. 如果尚未执行此操作，请在新的浏览器窗口中以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。 
    
    例如，在中心菜单上单击“更多服务”，然后在筛选框中开始键入**信息**。 选择“Azure 信息保护”。

2. 如果为自动或推荐分类配置的标签将应用于所有用户，请从“策略: 全局”边栏选项卡中选择要更改的标签，然后在“标签”边栏选项卡和之后的任何所需边栏选项卡上进行更改。 

     如果要配置的标签位于[作用域内策略](configure-policy-scope.md)中，以便仅应用于所选用户，请首先从初始的“Azure 信息保护”边栏选项卡中选择作用域内策略。  

3. 在“**标签**”边栏选项卡上的“**配置条件以自动应用该标签**”部分中，单击“**添加新的条件**”。

4. 在“**条件**”边栏选项卡上，选择“**内置**”（如果想要使用预定义的条件），或“**自定义**”（如果想要指定自己的条件），然后单击“**保存**”：

    - 对于“**内置**”：从可用条件列表中选择，然后选择发生的最小数目以及发生计数中是否应具有唯一的值。
        
        有关这些条件的检测规则和一些示例的详细信息，请参阅 [内置条件的相关信息](#information-about-the-built-in-conditions)(#内置条件的相关信息) 部分。

    - 对于“**自定义**”：指定匹配的名称和短语，其必须排除引号和特殊字符。 然后指定是否匹配正则表达式，区分大小写，发生的最小数目以及发生计数中是否应具有唯一的值。
        
    **发生计数选项示例**：选择内置身份证号选项并将最小计数设置为 2，并且文档已列出两次同一身份证号码：如果设置“**仅计算唯一值的发生次数**”为“**打开**”，将不符合条件；如果此选项设置为“**关闭**”，将满足条件。

5. 在“**标签**”边栏选项卡上，配置以下内容，然后单击“**保存**”：

    - 选择自动或建议的分类：对于**选择如何应用该标签：自动或向用户建议**，选择“**自动**”或“**建议**”。

    - 指定用户提示或策略提示文本：保持默认文本或指定你自己的字符串。

6. 若要使所做的更改适用于用户，在“**Azure 信息保护**”边栏选项卡，单击“**发布**”。

## <a name="information-about-the-built-in-conditions"></a>有关内置条件的信息

你可以选择以下条件：

- [SWIFT 代码](#swift-code )

- [信用卡卡号](#credit-card-number )

- [ABA 银行代号](#aba-routing-number )

- [美国身份证号 (SSN)](#usa-social-security-number-ssn)

- [国际银行帐号 (IBAN)](#international-banking-account-number-iban)


### <a name="swift-code"></a>SWIFT 代码

内容包括以下项时与此信息类型匹配：  

1. 以下短语之一：**swift**、**swiftnumber**、**swiftroutingnumber** 

2. Swift 代码，具有以下格式化模式：  

    a. 4 个字母（银行代码）  

    b。 2 个字母（国家/地区代码）  

    c. 2 个字母或数字（位置代码）  

    d. 可选 3 个字母或数字（分支代码）  


用于测试的示例：

- **NEDSZAJJXXX Swiftroutingnumber**

- **NEDSZAJJ100 Swiftnumber** 

----


### <a name="credit-card-number"></a>信用卡号

内容包括以下项时与此信息类型匹配：  

- 格式化或非格式化模式的有效信用卡号，通过 [luhn 检查](https://wikipedia.org/wiki/Luhn_algorithm)(#luhn-检查)。 此信息类型从全球范围内的所有主要品牌（包括 Visa、MasterCard、Discover Card、American Express 和 Diners）中检测卡。

    - **格式化**：
    
        - 16 位：(dddd-dddd-dddd-dddd)  
        
    - **未格式化**：
    
        - (dddddddddddddddd)  


用于测试的示例：

- **4242-4242-4242-4242**

- **4242424242424242** 

----

### <a name="aba-routing-number"></a>ABA 路由号码

内容包括以下项时与此信息类型匹配：  

1. 至少一个以下短语：**aba**、**rtn**、**routing number** 

2. ABA 路由号码，包括格式化或非格式化模式的 9 位数： 

    - **格式化**： 
        
        a. 0、1、2、3、6、7 或 8 开头的四位数字 
        
        b。 连字符 
        
        c. 四位数字 
        
        d. 连字符 
        
        e. 一个数字 
        
        示例：3456-9876-1 ABA 
        
    - **未格式化**： 
        
        0、1、2、3、6、7 或 8 开头的 9 位连续数字 
        
        示例：345698761 RTN 
 

用于测试的示例：

- **3456-9876-1 ABA**

- **345698761 RTN** 

----

### <a name="usa-social-security-number-ssn"></a>美国身份证号 (SSN)

内容包括以下项时与此信息类型匹配：  

1. 至少一个以下短语：**ssn**、**social security**、**ssid**、**ss#** 

2. 身份证号：9 位数，可以是格式化或非格式化模式：

    - **格式化**： 
    
        - 采用以下格式的 9 位数：ddd-dd-dddd 或 ddd dd dddd 
        
    - **未格式化**： 
    
        - 采用以下格式的 9 位数：ddddddddd 


用于测试的示例：

- **SSN 123-45-6789**

- **SS# 123456789** 


----

### <a name="international-banking-account-number-iban"></a>国际银行帐号 (IBAN)

内容包括以下项时与此信息类型匹配：  

1. 以下短语：**IBAN** 

2. 国际银行账号：以国家/地区代码（两个字母）开头，然后检验位数（两位数字），然后是 bban 数字（最高包括 30 位）。


用于测试的示例：

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## <a name="next-steps"></a>后续步骤

有关配置 Azure 信息保护策略的详细信息，请使用 [配置组织的策略](configure-policy.md#configuring-your-organizations-policy)(#配置组织的策略) 部分中的链接。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


