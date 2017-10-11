---
title: "从 Azure 信息保护为 Azure Rights Management 服务配置 Exchange Online IRM"
description: "当 Office 365 租户不支持 Office 365 邮件加密中的新功能时，管理员为 Azure Rights Management 服务配置 Exchange Online 的信息和说明。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a0c6fe7f7b6a34eea21b646ce5573ca03b13be3c
ms.sourcegitcommit: cd3320fa34acb90f05d5d3e0e83604cdd46bd9a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2017
---
# <a name="exchange-online-irm-configuration-when-you-have-imported-a-trusted-publishing-domain"></a>已导入受信任的发布域时的 Exchange Online IRM 配置

>*适用于：Azure 信息保护、Office 365*

仅在先前已通过导入受信任的发布域 (TPD) 为 IRM 配置了 Exchange Online 且需要解密先前已加密的电子邮件时才使用这些说明。

如果上述任何条件皆不适用，请勿使用这些说明，应改为使用 [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)（设置构建在 Azure 信息保护之上新的 Office 365 邮件加密功能）中的说明。

## <a name="exchange-online-irm-configuration-if-you-have-an-imported-tpd"></a>具有已导入的 TPD 时的 Exchange Online IRM 配置

若要配置 Exchange Online 以支持 Azure Rights Management 服务，你必须为 Exchange Online 配置信息权限管理 (IRM) 服务。 为此，你可以使用 Windows PowerShell（无需安装单独的模块）并运行[适用于 Exchange Online 的 PowerShell 命令](https://technet.microsoft.com/library/jj200677.aspx)。

> [!NOTE]
> 在 Microsoft 迁移你的 Office 365 租户之前，如果你为 Azure 信息保护使用客户管理的租户密钥 (BYOK)，而不是默认配置（即 Microsoft 管理的租户密钥），则不能将 Exchange Online 配置为支持 Azure Rights Management 服务。
>
> 如果你尝试在 Azure Rights Management 服务使用 BYOK 时配置 Exchange Online，则导入密钥命令（下面过程中的步骤 5）将失败并显示错误消息 **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**。

以下步骤提供了一组典型的命令，你可以针对此方案运行这些命令，使 Exchange Online 能够使用 Azure Rights Management 服务：

1.  如果这是你第一次在计算机上使用 Windows PowerShell for Exchange Online，必须配置 Windows PowerShell 以运行签名的脚本。 使用“以管理员身份运行”选项启动 Windows PowerShell 会话，然后键入  ：

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  在 Windows PowerShell 会话中，使用为远程 Shell 访问启用的帐户登录到 Exchange Online。 默认情况下，将允许在 Exchange Online 中创建的所有帐户进行远程 Shell 访问，但可以使用 [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx) 命令将此项禁用（和启用）。

    若要登录，请键入：

    ```
    $UserCredential = Get-Credential
    ```
    在“Windows PowerShell 凭据请求”对话框中，提供你的 Office 365 用户名和密码  。

3.  通过运行以下两个命令连接到 Exchange Online 服务：

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  根据组织的租户创建位置指定 Azure 信息保护租户密钥的位置：

    适用于北美：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    适用于欧洲：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    适用于亚洲：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    适用于南美：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    适用于 Office 365 政府版（政府社区云）：

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.govus.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  以受信任的发布域 (TPD) 的形式从 Azure Rights Management 服务将配置数据导入到 Exchange Online。 这包括 Azure 信息保护租户密钥和 Azure Rights Management 模板：

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    在此命令中，我们将 **RMS Online** 的名称用作 Exchange Online 中 Azure Rights Management 的 TPD 的基名称。 导入 TPD 后，它将在 Exchange Online 中名为 **RMS Online - 1**。

6.  启用 Azure Rights Management 功能，以便 IRM 功能可用于 Exchange Online：

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    运行此命令后，将自动为 Outlook 客户端、Outlook Web 应用和 Exchange Active Sync 启用 Rights Management。

7.  （可选）使用以下命令测试此配置是否成功：

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    例如：**Test-IRMConfiguration -Sender  adams@contoso.com**

    此命令将运行一系列检查，包括验证与服务的连接，检索配置，检索 URI、许可证和任何模板。 在 Windows PowerShell 会话中，你将看到每一项的结果并在结束时看到是否所有内容均已通过这些检查： **总体结果：通过**

8.  与远程 PowerShell 会话断开连接：

    ```
    Remove-PSSession $Session
    ```

现在用户可以使用 Azure Rights Management 服务来保护其电子邮件。 例如，在 Outlook Web App 中，从扩展菜单 (...) 中选择“设置权限”，然后选择“不要转发”或可用模板之一，将信息保护应用于电子邮件和任何附件。 但是，由于 Outlook Web App 将缓存 UI 一天时间，请在运行这些配置命令后并在尝试将信息保护应用于电子邮件前，等待经过这段时间。 在 UI 更新以反映新配置之前，你将在“设置权限”菜单中看不到任何选项  。

> [!IMPORTANT]
> 如果为 Azure Rights Management 创建了新的[自定义模板](configure-custom-templates.md)或更新了这些模板，则每次都必须运行以下 Exchange Online PowerShell 命令（如有必要，请先运行步骤 2 和步骤 3）以将这些更改同步到 Exchange Online：`Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

作为 Exchange 管理员，你现在可以配置自动应用信息保护的功能，如[传输规则](https://technet.microsoft.com/library/dd302432.aspx)、[数据丢失防护 (DLP) 策略](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)和[受保护的语音邮件](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx)（统一消息传送）。


### <a name="office-365-message-encryption"></a>Office 365 消息加密
运行前一部分中所述的相同步骤，但如果不希望显示模板，请在步骤 6 之前运行以下命令，以防止在 Outlook Web 应用和 Outlook 客户端中提供 IRM 模板：`Set-IRMConfiguration -ClientAccessServerEnabled $false`

然后，你便可以将 [传输规则](https://technet.microsoft.com/library/dd302432.aspx) 配置为在收件人位于组织外部时自动修改消息安全性，并选择“应用 Office 365 消息加密”  选项。

有关消息加密的详细信息，请参阅 Exchange 库中的 [Office 365 中的加密](https://technet.microsoft.com/library/dn569286.aspx) 。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
