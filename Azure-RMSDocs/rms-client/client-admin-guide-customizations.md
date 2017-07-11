---
title: "Azure 信息保护客户端的自定义配置"
description: "有关自定义适用于 Windows 的 Azure 信息保护客户端的信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ab5465db1527e6236d2dca466936c36b260f03d
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
<a id="custom-configurations-for-the-azure-information-protection-client" class="xliff"></a>

# Azure 信息保护客户端的自定义配置

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、带 SP1 的 Windows 7、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用以下高级配置的相关信息，在管理 Azure 信息保护客户端时，你可能需要将其用于特定方案或用户子集。 

<a id="prevent-sign-in-prompts-for-ad-rms-only-computers" class="xliff"></a>

## 阻止针对仅 AD RMS 计算机出现的登录提示

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务。 对于只与 AD RMS 通信的计算机，这可能导致不必要的用户登录提示。 可以通过编辑注册表阻止此登录提示：

找到以下值名称，然后将值数据设置为“0”：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

无论此设置如何，Azure 信息保护客户端遵循标准的 [RMS 服务发现进程](../rms-client/client-deployment-notes.md#rms-service-discovery)，查找其 AD RMS 群集。

<a id="sign-in-as-a-different-user" class="xliff"></a>

## 以其他用户身份登录

在生产环境中，如果用户使用的是 Azure 信息保护客户端，则通常不需要以其他用户身份登录。 但是，如果拥有多个租户，则可能需要以管理员身份执行此操作。 例如，除了拥有组织使用的 Office 365 或 Azure 租户外，还拥有一个测试租户。

可以使用“Microsoft Azure 信息保护”对话框验证当前登录的帐户身份：打开 Office 应用程序，在“主页”选项卡上的“保护”组中，单击“保护”，然后单击“帮助和反馈”。 帐户名称会显示在“客户端状态”部分中。

特别是在使用管理员帐户时，请务必检查所显示的登录帐户的域名。 例如，如果在两个不同的租户中都拥有“admin”帐户，则很容易忽略登录的帐户名正确但域错误的情况。 出现此情况可能导致下载 Azure 信息保护策略失败，或无法看到期望的标签或行为。

以其他用户身份登录：

1. 使用注册表编辑器，导航到“HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP”并删除“TokenCache”值（及其关联的值数据）。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果在 Office 应用程序中没有看到登录到 Azure 信息保护服务的提示，请返回“Microsoft Azure信息保护”对话框，然后从更新的“客户端状态”部分中单击“登录”。

此外：

- 如果使用的是单一登录，则需要在编辑注册表后注销 Windows，然后使用其他用户帐户登录。 Azure 信息保护客户端会使用当前登录的用户帐户自动进行身份验证。

- 如果要重新初始化 Azure Rights Management 服务的环境（也称为引导），可以使用 [RMS Analyzer工具](https://www.microsoft.com/en-us/download/details.aspx?id=46437)中的“重置”选项进行此操作。

- 如果要删除当前下载的 Azure 信息保护策略，可以从 **%localappdata%\Microsoft\MSIP** 文件夹中删除 **Policy.msip** 文件。

<a id="hide-the-classify-and-protect-menu-option-in-windows-file-explorer" class="xliff"></a>

## 隐藏 Windows 文件资源管理器中的“分类和保护”菜单选项

如果你具有 1.3.0.0 或更高版本的 Azure 信息保护客户端，可以通过编辑注册表配置此高级配置。 

创建以下 DWORD 值名称（以及任何数值数据）：

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

<a id="support-for-disconnected-computers" class="xliff"></a>

## 对断开连接的计算机的支持

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务，以下载最新的 Azure 信息保护策略。 如果你知道你的计算机在一段时间无法内连接到 Internet，可以通过编辑注册表阻止客户端尝试连接到该服务。 找到以下值名称并将值数据设置为 **0**：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

确保客户端在 **%localappdata%\Microsoft\MSIP** 文件夹中具有一个名为 **Policy.msip** 的有效策略文件。 如有必要，可以从 Azure 门户中导出策略，并将导出的文件复制到客户端计算机。 此外，还可以使用此方法将已过时的策略文件替换为已发布的最新策略。

<a id="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution" class="xliff"></a>

## 与 Exchange 邮件分类集成以实现移动设备标记解决方案

虽然 Outlook 网页版尚不支持本机 Azure 信息保护分类和保护，但可以使用 Exchange 邮件分类将 Azure 信息保护标签扩展到移动用户。

要实现此解决方案： 

1. 使用 [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell cmdlet 创建邮件分类，其 Name 属性映射到 Azure 信息保护策略中的标签名称。 

2. 为每个标签创建 Exchange 传输规则：邮件属性包括配置的分类时应用规则，并修改邮件属性以设置邮件头。 

    对于邮件头，可通过检查所发送的的电子邮件的 Internet 邮件头来查找要指定的信息，这些邮件头是使用 Azure 信息保护标签进行分类的。 查找邮件头 **msip_labels**，以及紧随其后的字符串，直至分号（包括分号）。 以上述示例为例：
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    然后，对于此规则中的邮件头，将 **msip_labels** 指定为邮件头，此字符串的其余部分指定为邮件头的值。 例如：
    
    ![示例 Exchange Online 传输规则，用于为特定 Azure 信息保护标签设置邮件头](../media/exchange-rule-for-message-header.png)

测试此规则前，请记住，创建或编辑传输规则时通常会存在延迟（例如，等待一个小时）。 当规则生效后，用户使用 Outlook 网页版或支持 Rights Management 保护的移动设备客户端时，会发生以下情况： 

- 用户选择 Exchange 邮件分类，并发送电子邮件。

- Exchange 规则检测 Exchange 分类，并对应修改邮件头以添加 Azure 信息保护分类。

- 运行 Azure 信息保护客户端的收件人在 Outlook 中查看电子邮件时，他们将看到分配的 Azure 信息保护标签以及所有对应的电子邮件标头、页脚或水印。 

如果 Azure 信息保护标签应用权限管理保护，请将其添加到规则配置，方法是选择修改邮件安全性的选项，应用权限保护，然后选择 RMS 模板或“不要转发”选项。

你还可以配置传输规则来执行反向映射：检测到 Azure 信息保护标签时，请设置相应的 Exchange 邮件分类。 为此，请执行以下操作：

- 对于每个 Azure 信息保护标签，请创建在 **msip_labels** 标头包含标签名称（例如 **General**）时应用的传输规则，并应用映射到此标签的邮件分类。


<a id="next-steps" class="xliff"></a>

## 后续步骤
现在你已自定义 Azure 信息保护客户端，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
