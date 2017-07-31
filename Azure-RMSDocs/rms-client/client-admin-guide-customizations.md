---
title: "Azure 信息保护客户端的自定义配置"
description: "有关自定义适用于 Windows 的 Azure 信息保护客户端的信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 32226274c8b50b02e453f1c1b6655fb01b4ec942
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2017
---
# <a name="custom-configurations-for-the-azure-information-protection-client"></a>Azure 信息保护客户端的自定义配置

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

请参阅以下高级配置相关信息，在管理 Azure 信息保护客户端时，可能需要用于特定方案或一部分用户。

其中一些设置需要编辑注册表，一些使用的是高级设置，必须先在 Azure 门户中进行配置，再发布以供客户端下载。 此外，一些设置可能仅在预览版 Azure 信息保护客户端中可用。 对于这些设置，已记录最低客户端版本。 对于客户端正式发布版支持的设置和配置，未记录最低客户端版本号。

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>在门户中配置高级客户端配置设置的具体步骤

此配置目前处于预览状态。

1. 如果尚未执行此操作，请在新的浏览器窗口中以安全管理员或全局管理员身份登录到 [Azure 门户](https://portal.azure.com)，然后导航到“Azure 信息保护”边栏选项卡。

2. 在最初的“Azure 信息保护”边栏选项卡中，选择“作用域内策略”。

3. 在“Azure 信息保护 - 作用域内策略”边栏选项卡中，选择此策略旁边的上下文菜单 (...)，以添加高级设置。 再选择“高级设置”。
    
    可以为全局策略和作用域内策略配置高级设置。

4. 在“高级设置”边栏选项卡中，键入高级设置名称和值，再选择“保存并关闭”。

5. 单击“发布”，并确保此策略的用户重启打开过的任何 Office 应用程序。

6. 如果不再需要此设置，并希望还原为默认行为：在“高级设置”边栏选项卡中，选择不再需要的设置旁边的上下文菜单 (...)，再选择“删除”。 然后，单击“保存并关闭”，再重新发布已修改的策略。

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>阻止针对仅 AD RMS 计算机出现的登录提示

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务。 对于只与 AD RMS 通信的计算机，此配置可能导致不必要的用户登录提示。 可以通过编辑注册表阻止此登录提示：

找到以下值名称，然后将值数据设置为“0”：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

无论此设置如何，Azure 信息保护客户端遵循标准的 [RMS 服务发现进程](../rms-client/client-deployment-notes.md#rms-service-discovery)，查找其 AD RMS 群集。

## <a name="sign-in-as-a-different-user"></a>以其他用户身份登录

在生产环境中，如果用户使用的是 Azure 信息保护客户端，则通常不需要以其他用户身份登录。 不过，作为管理员，你在测试阶段可能需要以其他用户身份登录。 

可以使用“Microsoft Azure 信息保护”对话框验证当前登录的帐户身份：打开 Office 应用程序，在“主页”选项卡上的“保护”组中，单击“保护”，然后单击“帮助和反馈”。 帐户名称会显示在“客户端状态”部分中。

请确保还要检查所显示的登录帐户的域名。 很容易忽视的一点是，使用正确的帐户名登录，但域不正确。 使用错误帐户的症状是，无法下载 Azure 信息保护策略，或看不到预期的标签或行为。

以其他用户身份登录：

1. 具体取决于 Azure 信息保护客户端的版本： 
    
    - 对于 Azure 信息保护客户端的正式发布版本：使用注册表编辑器，导航到“HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP”并删除“TokenCache”值（及其关联的值数据）。
    
    - 对于 Azure 信息保护客户端的当前预览版本：导航到“%localappdata%\Microsoft\MSIP”并删除“TokenCache”文件。

2. 重新启动任何打开的 Office 应用程序，并使用其他用户帐户登录。 如果在 Office 应用程序中没有看到登录到 Azure 信息保护服务的提示，请返回“Microsoft Azure信息保护”对话框，然后从更新的“客户端状态”部分中单击“登录”。

此外：

- 此解决方案支持以同一租户中的其他用户身份登录。 不支持以不同租户中的其他用户身份登录。 若要使用多个租户测试 Azure 信息保护，请使用不同的计算机。

- 如果使用的是单一登录，必须在编辑注册表后注销 Windows，再使用其他用户帐户登录。 然后，Azure 信息保护客户端会使用当前登录的用户帐户，自动进行身份验证。

- 若要重置 Azure Rights Management 服务的用户设置，可以使用“帮助和反馈”选项。

- 如果要删除当前下载的 Azure 信息保护策略，可以从 **%localappdata%\Microsoft\MSIP** 文件夹中删除 **Policy.msip** 文件。

- 如果有 Azure 信息保护客户端的当前预览版本，则可以使用“帮助和反馈”中的“重置设置”选项注销并删除当前已下载的 Azure 信息保护策略。

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>隐藏 Windows 文件资源管理器中的“分类和保护”菜单选项

此配置选项目前处于预览状态。

如果 Azure 信息保护客户端版本为 1.3.0.0 或更高版本，可以通过编辑注册表来配置此高级配置。 

创建以下 DWORD 值名称（以及任何数值数据）：

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>对断开连接的计算机的支持

默认情况下，Azure 信息保护客户端会自动尝试连接到 Azure 信息保护服务，以下载最新的 Azure 信息保护策略。 如果你知道你的计算机在一段时间无法内连接到 Internet，可以通过编辑注册表阻止客户端尝试连接到该服务。 

找到以下值名称并将值数据设置为 **0**：

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

确保客户端在 **%localappdata%\Microsoft\MSIP** 文件夹中具有一个名为 **Policy.msip** 的有效策略文件。 如有必要，可以从 Azure 门户中导出策略，并将导出的文件复制到客户端计算机。 此外，还可以使用此方法，将已过时的策略文件替换为已发布的最新策略。

## <a name="hide-the-do-not-forward-button-in-outlook"></a>在 Outlook 中隐藏“不转发”按钮

此配置选项目前处于预览状态。

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 此设置还要求使用最低版本为 1.8.41.0 的预览版 Azure 信息保护客户端。

配置此设置后，将在 Outlook 的功能区中隐藏“不转发”按钮。 但不会在 Office 菜单中隐藏此选项。

若要配置此高级设置，请输入以下字符串：

- 键：DisableDNF

- 值：True

## <a name="make-the-custom-permissions-options-unavailable-to-users"></a>让用户无法使用“自定义权限”选项

此配置选项目前处于预览状态。

此配置使用必须在 Azure 门户中配置的[高级客户端设置](#how-to-configure-advanced-client-configuration-settings-in-the-portal)。 

配置此设置并为用户发布策略后，用户将无法在以下位置选择“自定义权限”选项：

- 在 Office 应用程序中：“主页”选项卡 >“保护组”>“保护” > “自定义权限”

- 在文件资源管理器中：右键单击 >“分类并保护” > “自定义权限”

此设置对可以使用 Office 菜单选项配置的自定义权限没有任何影响。 

若要配置此高级设置，请输入以下字符串：

- 键：EnableCustomPermissions

- 值：False

## <a name="permanently-hide-the-azure-information-protection-bar"></a>永久隐藏 Azure 信息保护栏

此配置使用必须在 Azure 门户中配置的高级设置。 此设置还要求使用最低版本为 1.9.58.0 的预览版 Azure 信息保护客户端。

配置此设置并为用户发布策略后，如果用户选择不在 Office 应用程序中显示 Azure 信息保护栏，此栏保持隐藏。 当用户通过依次单击“主页”选项卡、“保护组”和“保护”按钮取消选中“显示栏”选项时，就会发生这种情况。 如果用户使用“关闭信息保护栏”图标关闭此栏，此设置将不起作用。

即使 Azure 信息保护栏保持隐藏，如果已配置了推荐分类，或者文档或电子邮件必须有标签，用户仍可以从临时显示的栏中选择标签。 此设置也不会影响你或其他人配置的标签，如手动或自动分类，或设置的默认标签。

若要配置此高级设置，请输入以下字符串：

- 键：EnableBarHiding

- 值：True

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>与 Exchange 邮件分类集成以实现移动设备标记解决方案

虽然 Outlook 网页版尚不支持本机 Azure 信息保护分类和保护，但可以使用 Exchange 邮件分类将 Azure 信息保护标签扩展到移动用户。

要实现此解决方案： 

1. 使用 [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell cmdlet 创建邮件分类，其 Name 属性映射到 Azure 信息保护策略中的标签名称。 

2. 为每个标签创建 Exchange 传输规则：邮件属性包括配置的分类时应用规则，并修改邮件属性以设置邮件头。 

    对于邮件头，可检查已发送且使用 Azure 信息保护标签进行分类的电子邮件的 Internet 邮件头，查找要指定的信息。 查找邮件头 **msip_labels**，以及紧随其后的字符串，直至分号（包括分号）。 以上述示例为例：
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    然后，对于此规则中的邮件头，将 **msip_labels** 指定为邮件头，此字符串的其余部分指定为邮件头的值。 例如：
    
    ![示例 Exchange Online 传输规则，用于为特定 Azure 信息保护标签设置邮件头](../media/exchange-rule-for-message-header.png)

测试此配置前，请注意，创建或编辑传输规则时通常都会有延迟（例如，等待一小时）。 当规则生效后，如果用户使用 Outlook 网页版或支持 Rights Management 保护的移动设备客户端，则会发生以下事件： 

- 用户选择 Exchange 邮件分类，并发送电子邮件。

- Exchange 规则检测 Exchange 分类，并对应修改邮件头以添加 Azure 信息保护分类。

- 当收件人在 Outlook 中查看电子邮件，且已安装 Azure 信息保护客户端时，他们将看到分配的 Azure 信息保护标签，以及所有对应的电子邮件头、页脚或水印。 

如果 Azure 信息保护标签应用权限管理保护，请将此保护添加到规则配置，具体方法是选择用于修改邮件安全性的选项，应用权限保护，再选择 RMS 模板或“不转发”选项。

还可以通过配置传输规则来执行反向映射。 检测到 Azure 信息保护标签时，请设置相应的 Exchange 邮件分类：

- 对于每个 Azure 信息保护标签，请创建在 msip_labels 头包含标签名称（例如 General）时应用的传输规则，并应用映射到此标签的邮件分类。


## <a name="next-steps"></a>后续步骤
至此，已自定义 Azure 信息保护客户端。若要了解支持此客户端所需的其他信息，请参阅以下资源：

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
