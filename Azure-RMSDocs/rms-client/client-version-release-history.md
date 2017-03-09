---
title: "Azure 信息保护客户端&colon;版本发行历史记录"
description: "请参阅适用于 Windows 的 Azure 信息保护客户端版本的新增功能或改进功能。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/01/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 343ac5f79902379e45efcb6979a115ba4c00d1c5
ms.openlocfilehash: 503cb76825d0092e8562d39281b1d702edaf6438
ms.lasthandoff: 03/02/2017


---

# <a name="azure-information-protection-client-version-release-history"></a>Azure 信息保护客户端：版本发行历史记录

>*适用于：Azure 信息保护*

Azure 信息保护团队会定期更新 Azure 信息保护客户端，以提供修补程序和新功能。 客户端包含在 Microsoft 更新目录（类别：**Azure 信息保护**）中，还可以随时从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下载最新版本。

使用以下信息查看版本中的新增内容或更改的内容。 最新版本会最先列出。 正式发布前的版本并未列出。

> [!NOTE]
> 不会列出小修补程序，因此，如果 Azure 信息保护客户端遇到问题，请先检查它是否是最新版本的问题。
>  
> 如果仍有问题，请参阅[支持选项和社区资源](../get-started/information-support.md#support-options-and-community-resources)信息。 我们还邀请你加入 Azure 信息保护团队：[Yammer 站点](https://www.yammer.com/askipteam/)。

## <a name="version-131552"></a>版本 1.3.155.2

**发布日期**：2017/02/08

**新要求**：

Microsoft .NET Framework

- 此版本的 Azure 信息保护客户端要求使用的最低版本为 Microsoft .NET Framework 4.6.2，如果缺少此版本，安装程序会尝试下载并安装它。 Azure 信息保护客户端完成安装后，可能需要重启计算机。

- 如果单独安装 Azure 信息保护查看器，则要求的最低版本为 Microsoft .NET Framework 4.5.2，如果缺少此版本，安装程序会尝试下载并安装它。

**新增功能**：

- 一个新的统一客户端，它将适用于 Windows 的 Rights Management 共享应用程序中的功能与 Azure 信息保护客户端组合在一起。 包括：
    
    - 与 Windows 文件资源管理器集成（右键单击）以应用标签和保护。 支持其他文件格式和多个文件选择。
    - 适用于受保护文档的查看器（包括用于 SharePoint 的受保护 PDF）。
    - PowerShell cmdlet，可用于获取和设置存储在本地或存储在网络共享上的文件的标签。 这些 cmdlet 与 RMS 保护工具（RMSProtection 模块）之前随附的 cmdlet 一起安装。
    - 客户端使用情况日志，记录应用的标签、应用方式、应用者等信息。

此客户端版本是 2016 年 12 月首次发布的预览版客户端的[公开发行版本](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/)。 有关此版本的客户端的详细信息，请参阅以下指南：

- [Azure 信息保护客户端管理员指南](client-admin-guide.md)

- [Azure 信息保护用户指南](client-user-guide.md)


## <a name="version-1240"></a>版本 1.2.4.0

**发布日期**：2016/10/27

**修补程序**：

- 禁用 Windows 更新服务时，客户端安装完成。

- 在 Office 2016 中，在保存文档并且为页眉或页脚配置应用的标签时，光标不会跳转到页眉或页脚。

- 在 Word 中，自动分类适用于捆绑文本框中的文本。

**新功能**：

- 安装 Azure 信息保护客户端后，用户可从 Office 应用程序运行的诊断测试和重置选项：在“开始”选项卡的“保护”组中，单击“保护”、“帮助和反馈”，然后单击“运行诊断”。 

    有关此选项的详细信息，请参阅客户端安装文档中的[验证安装、连接状态或发送反馈](client-admin-guide.md#additional-checks-to-verify-installation-connection-status-or-send-feedback)部分。

## <a name="version-11230"></a>版本 1.1.23.0

**发布日期**：2016/10/01

正式发布。

## <a name="next-steps"></a>后续步骤

有关安装客户端的详细信息：

- 用户请参阅：[下载并安装客户端](install-client-app.md)

- 管理员请参阅：[Azure 信息保护客户端管理员指南](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
