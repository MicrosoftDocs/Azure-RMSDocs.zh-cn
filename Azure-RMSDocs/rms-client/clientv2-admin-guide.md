---
title: Azure 信息保护统一标记的客户端管理员指南
description: 说明和管理员的企业网络上的信息面向负责部署 Azure 信息保护统一标记适用于 Windows 的客户端。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 9f50eef590b684be95d410ed470bd0d0ee62a76a
ms.sourcegitcommit: b92f60a87f824fc2da1e599f526898e3a0c919c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2019
ms.locfileid: "67343713"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Azure 信息保护统一标记的客户端管理员指南

>适用对象：  Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2
>
> 说明： *[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

在本指南中使用的信息，如果你负责 Azure 信息保护统一标记客户端上的企业网络，或如果您希望更多技术信息不是处于[Azure 信息保护统一标记客户端用户指南](clientv2-user-guide.md)。 

例如：

- 了解此客户端的不同组件以及是否应安装这些组件

- 如何为用户安装客户端，以及有关先决条件、安装选项和参数及验证检查的信息

- 查找客户端文件和使用情况日志

- 确定客户端支持的文件类型

- 将客户端与 PowerShell 结合用于命令行控制

**是否有本文档未解决的问题？** 请访问 [Azure 信息保护 Yammer 站点](https://www.yammer.com/AskIPTeam)。 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Azure 信息保护统一标记客户端的技术概述

Azure 信息保护统一标记客户端包括：

- Office 外接程序，安装**敏感度**用户选择敏感度标签和一个选项以显示更好的标签可见性的 Azure 信息保护栏在功能区上的按钮。

- Windows 文件资源管理器，便于用户将分类标签和保护应用到文件的右键单击选项。

- 一个查看器，可在本机应用程序无法将其打开时显示受保护的文件。

- 一个 PowerShell 模块，用于从文件应用和删除分类标签和保护。 

- Rights Management 客户端与 Azure Rights Management (Azure RMS) 服务来加密和保护的文件进行通信。

除了查看器中，Azure 信息保护统一标记客户端不能使用应用程序和服务直接与 Azure Rights Management 服务或 Active Directory Rights Management Services 进行通信。

如果安装了 AD RMS，想迁移到 Azure 信息保护，请参阅[从 AD RMS 迁移到 Azure 信息保护](../migrate-from-ad-rms-to-azure-rms.md)。


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>你应该部署 Azure 信息保护统一标记客户端？

如果使用的部署 Azure 信息保护统一标记客户端[Office 365 安全与合规中心的敏感度标签](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels)，和以下任一适用：

- 你想要进行分类 （或保护） 文档和电子邮件通过选择从 Windows 计算机上在 Office 应用 （Word、 Excel、 PowerPoint、 Outlook） 中的标签。

- 想要通过使用文件资源管理器（支持除 Office、多选和文件夹支持的文件类型以外的其他文件类型）对文件进行分类（或保护）。

- 想要通过使用 PowerShell 命令运行对文档进行分类（或保护）的脚本。

- 想要在本机应用程序显示未安装文件或无法打开这些文档时查看受保护的文档。

示例显示 Office 外接程序的 Azure 信息保护统一标记的客户端，显示新**敏感度**在功能区和可选的 Azure 信息保护栏上的按钮：

![具有默认策略的 Azure 信息保护栏](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>安装和支持 Azure 信息保护统一标记客户端

可以使用可执行文件或 Windows installer 文件来安装 Azure 信息保护统一标记客户端。 有关每个选项和说明的详细信息，请参阅[安装用户的 Azure 信息保护统一标记客户](clientv2-admin-guide-install.md)。  

使用以下部分获取有关安装客户端的支持信息。 

### <a name="installation-checks-and-troubleshooting"></a>安装检查和疑难解答

安装客户端后，请使用“帮助和反馈”选项打开“Microsoft Azure 信息保护”对话框   ：

- 从 Office 应用程序：上**主页**选项卡上，在**敏感度**组中，选择**敏感度**，然后选择**帮助和反馈**。

- 从文件资源管理器中：右键单击选择一个/多个文件或文件夹，然后依次选择“分类和保护”和“帮助和反馈”   。 

#### <a name="help-and-feedback-section"></a>“**帮助和反馈**”部分

**告诉我详细信息链接**默认情况下，将转到[Azure 信息保护](https://www.microsoft.com/cloud-platform/azure-information-protection)网站。 你可以配置自己作为 Office 365 安全与合规中心中的策略设置之一转到某个自定义帮助页面的 URL 链接。

**导出日志**自动收集并附加日志文件，如果您还需要发送给 Microsoft 支持人员的 Azure 信息保护统一标记的客户端。 最终用户也可以使用此选项，将这些日志文件发送给你的支持人员。

**重置设置**注销用户、 删除当前下载的敏感度标签和策略，并将重置 Azure Rights Management 服务的用户设置。

##### <a name="more-information-about-the-reset-settings-option"></a>有关“重置设置”选项的详细信息

- 不是本地管理员也能使用此选项，并且不会在事件查看器中记录此操作。 

- 除非文件被锁定，否则此操作将删除以下位置中的所有文件。 这些文件包括客户端证书、 Rights Management 模板、 敏感度标签和策略从 Office 365 安全与合规中心和缓存的用户凭据。 不会删除客户端日志文件。
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- 将删除以下注册表项和设置。 如果以下任意注册表项具有自定义值，则必须在重置客户端后重新对其进行配置。 
    
    对于企业网络，通常使用组策略配置这些设置，在这种情况下，在计算机上刷新组策略时，将自动重新应用这些设置。 但是，某些设置可能通过脚本一次性配置，或手动配置。 在这些情况下，必须执行其他步骤来重新配置这些设置。 例如，由于要从 AD RMS 迁移并且网络上仍有服务连接点，因此计算机要运行一次脚本才能配置用于重定向到 Azure 信息保护的设置。 重置客户端后，计算机必须再次运行此脚本。
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC

- 当前登录的用户已注销。

#### <a name="client-status-section"></a>“**客户端状态**”部分

使用“**连接身份**”值来确认显示的用户名是否是要用于 Azure 信息保护身份验证的帐户。 此用户名必须与用于 Office 365 或 Azure Active Directory 的帐户匹配。 该帐户还必须属于为 Office 365 安全与合规中心的敏感度标签配置的 Office 365 租户。

如果您需要以与显示不同用户身份登录，请参阅[以不同用户身份登录](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user)说明。

使用“**版本**”信息可以确认安装的是哪个版本的客户端。 您可以检查是否为最新发行版本以及相应的修补程序和新功能，通过阅读[版本发布信息](unifiedlabelingclient-version-release-history.md)客户端。

## <a name="support-for-multiple-languages"></a>支持多种语言

Azure 信息保护统一标记客户端支持 Office 365 支持的相同语言。 有关这些语言的列表，请参阅 Office [国际可用性](https://products.office.com/business/international-availability)页面的 Office 365、Exchange Online Protection 和 Power BI  部分。

为这些语言、 菜单选项、 对话框和消息从 Azure 信息保护统一标记的客户端显示在用户的语言。 没有的单个安装程序检测语言，因此安装不同语言的 Azure 信息保护统一标记客户所不需的任何其他配置。 

但是，Azure 信息保护统一标记客户端不当前不支持不同语言的标签。 此外，视觉标记未翻译，且不支持多个语言。

## <a name="post-installation-tasks"></a>安装后的任务

安装 Azure 信息保护统一标记客户端后，请确保你提供有关如何标记其文档和电子邮件，用户说明和指南来为特定方案选择的标签。 例如：

- 联机用户指令：[Azure 信息保护统一标记的用户指南](clientv2-user-guide.md)

- 下载可自定义的用户指南：[Azure 信息保护最终用户采用指南](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>升级和维护 Azure 信息保护统一标记客户端

> [!NOTE]
> Azure 信息保护统一标记客户端支持升级 Azure 信息保护客户端，以及从以前版本的 Azure 信息保护统一标记客户端升级。

Azure 信息保护团队会定期更新 Azure 信息保护统一标记的客户端的新功能和修补程序。 公告会发布到团队的 [Yammer 网站](https://www.yammer.com/AskIPTeam)。

如果使用 Windows 更新，Azure 信息保护统一标记客户端自动升级此客户端，而不考虑如何安装客户端的正式发布版本。 新客户端版本会在发布后的几周内发布到目录中。

也可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载新版本，手动升级客户端。 然后，安装新版本来升级客户端。 您必须使用此方法升级预览版本，如果要从 Azure 信息保护客户端升级。

如果要从 Windows 7 上的 Azure 信息保护客户端升级，任何 Office 应用程序将自动重新启动客户端升级过程中。 此自动重启不适用于更高版本的操作系统，或如果从统一标记客户端的较旧版本进行升级。

手动升级时，只有当要更改安装方法时，才需要先卸载旧版本。 例如，从客户端的可执行文件 (.exe) 版本更改为客户端的 Windows 安装程序 (.msi) 版本。 或当需要安装旧版客户端时。 例如，出于测试目的已安装当前预览版，现在需要还原到当前正式版本。

使用[版本发行历史记录和支持策略](unifiedlabelingclient-version-release-history.md)若要了解有关 Azure 信息保护统一标记的客户端，目前支持哪些版本，并新增功能和更改的受支持的支持策略释放。 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>卸载 Azure 信息保护统一标记的客户端

可使用以下任一选项卸载客户端：

- 使用控制面板卸载程序：单击“Microsoft Azure 信息保护” > “卸载”  

- 重新运行该可执行文件 (例如， **AzInfoProtection_UL.exe**)，以及从**修改安装程序**页上，单击**卸载**。 

- 使用 **/uninstall** 运行可执行文件。 例如：`AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>后续步骤
若要安装客户端，请参阅[安装用户的 Azure 信息保护统一标记客户](clientv2-admin-guide-install.md)。

若已安装客户端，要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [支持的文件类型](client-admin-guide-file-types.md)

- [PowerShell 命令](client-admin-guide-powershell.md)


