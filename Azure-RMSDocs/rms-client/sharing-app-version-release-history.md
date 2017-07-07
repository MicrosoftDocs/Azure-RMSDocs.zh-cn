---
title: "RMS 共享应用&colon;版本发行历史记录 - AIP"
description: "查看适用于 Windows 的 Rights Management 共享应用程序版本中新增或更改的内容。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 811c89ef6922f6939e7a7d13ed707c6ebe6aafd6
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2017
---
# <a name="rights-management-sharing-application-version-release-history"></a>权限管理共享应用程序：版本发行历史记录

>*适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

Azure 信息保护团队定期更新 Rights Management 共享应用程序，以提供修补程序和新功能。 使用以下信息查看版本中的新增内容或更改的内容。 最新版本会最先列出。

不会列出 2015 年 1 月 1 日之前的版本。

> [!NOTE]
> 如果你有关于 RMS 共享应用程序的反馈或问题，请发送电子邮件到 [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question)。

## <a name="version-1022170"></a>版本 1.0.2217.0

**发布日期**：2016/07/13

**修补程序**：

- 组织中的用户使用联合身份验证和多重身份验证保护文档时不再收到错误 0x800704DC。



## <a name="version-1021910"></a>版本 1.0.2191.0
**发布日期**：2016/06/16

**修补程序**：

- 文档跟踪站点现在显示每个被跟踪文档的正确视图数目。

- 所有区域设置的模板现在均显示为可供用户使用。

- 在对 PowerPoint 文件使用“共享保护项”之后，对该文件本地版本的更改现在可以正确保存。

- 少量小缺陷修复和错误消息改进。


## <a name="version-1020040"></a>版本 1.0.2004.0
**发布日期**：2015/12/11

**修补程序**：

-   只有文件所有者和具有**共有者**权限级别的人员才能取消保护文件。 此前，所有者与具有**合著者**和**共有者**权限级别的人员都能够取消保护文件。

-   对 **.tif** 文件的本机保护（除 .tiff 文件之外），旨在生成受 RMS 保护的只读 **.ptif** 文件。

-   错误消息改进（准确性和清晰性）。

-   加密和解密内容的性能改进。

**新增功能**：

-   支持非管理员安装，使标准用户可以安装 RMS 共享应用程序。

    对运行 Office 2010 的标准用户有一些限制。 有关详细信息，请参阅[下载和安装 Rights Management 共享应用程序](install-sharing-app.md)用户说明中的[如果你不是本地管理员且使用 Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010) 部分。

## <a name="version-1019080"></a>版本 1.0.1908.0
**发布日期**：2015/9/16

**修补程序**：

-   对 Azure RMS 的 Multi-Factor Authentication (MFA) 的支持也将删除 Microsoft 登录助手（使用新式身份验证）的依赖关系。

    有关详细信息，请参阅 [Azure 信息保护的 Azure Active Directory 要求](../get-started/requirements-azure-ad.md)中的[多重身份验证 (MFA) 和 Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection) 部分。

## <a name="version-1017840"></a>版本 1.0.1784.0
**发布日期**：2015/7/30

**修补程序**：

-   权限策略模板的默认刷新间隔从 7 天减少到 1 天。

-   少量的回归测试和较小的 Bug。

## <a name="version-1017700"></a>版本 1.0.1770.0
**发布日期**：2015/4/25

**修补程序**：

-   现在，只有所有者和共同所有者可以删除保护。 合著者不能删除保护。

-   现在可以保护网络共享上的文件。

**新增功能**：

-   支持文档跟踪和撤消。 有关详细信息，请参阅[使用 RMS 共享应用程序跟踪和撤销文档](sharing-app-track-revoke.md)。

-   选择“共享保护” 时的模板支持：

    -   你现在可以选择模板。

    -   你看到的不是滑块，而是包含模板和自定义权限的列表框。

    -   你将不会再看到“允许在所有设备上使用”  和“强制实施使用限制” 选项。 相反，根据文件类型，将自动选择“一般性保护”  。

    有关详细信息，请参阅 [Rights Management 共享应用程序的对话框选项](sharing-app-dialog-box.md)。

## <a name="version-1016670"></a>版本 1.0.1667.0
**发布日期**：2015/1/19

**修补程序**：

-   RMS 共享应用 PPDF 查看器中的中文字体支持。

-   改进的错误处理和消息传送。

-   更高版本的应用可用于下载时，对于自动更新通知问题的修复。

**新增功能**：

-   **在你的组织内支持多个电子邮件域**：如果你使用 AD RMS，并且组织中的用户具有多个电子邮件域，此更新可让你的用户使用其他域中的组织中的用户保护的内容。 有关详细信息，请参阅 [Rights Management 共享应用程序管理员指南](sharing-app-admin-guide.md)中的[仅限 AD RMS：在组织中支持多个电子邮件域](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization)部分。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
