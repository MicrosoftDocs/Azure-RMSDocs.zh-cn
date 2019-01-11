---
title: 了解使用限制 | Azure RMS
description: 所有启用 RMS 的应用程序都必须强制实施使用限制。
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 1f46f11092270117686681662088c16f311963f7
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071516"
---
# <a name="understanding-usage-restrictions"></a>了解使用限制

所有启用 RMS 的应用程序都必须强制实施使用限制。 使用限制是在用户尝试执行操作时产生的结果（例如 打印文档），但该文档的 RMS 策略未授予他们执行该操作的权限（例如 打印权限）。

可以使用 [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx) 函数查询某个文档的用户权限。

## <a name="designing-with-usage-restrictions"></a>设计的使用限制

-   熟悉标准 RMS 权限

    有关应用程序可能会强制实施的完整 RMS 权限集，请参阅[使用限制参考](#usage-restriction-reference)。

    请注意，应用程序已定义了特定于你的情况的权限，且可能会创建超出标准 RMS 权限的权限。

-   确定使用限制强制点

    *使用限制强制点*是应用程序的控制流中的一个位置，此处需要强制实施使用限制。 [使用限制参考](#usage-restriction-reference)主题提供了几个常见强制点的示例。

    评估你自己的应用程序以确定应用哪些使用限制强制点。

    你的应用程序可能不需要[使用限制参考](#usage-restriction-reference)中所述的所有强制点。 例如，如果你的应用程序不允许用户打印内容，则不需要检查 **IPC\_GENERIC\_PRINT** 权限。

-   更新代码以在每个强制点执行访问检查

    有关如何强制实施特定权限的指南，请参阅[使用限制参考](#usage-restriction-reference)。

## <a name="usage-restriction-reference"></a>使用限制参考

使用限制由以下常量定义。

AD RMS 权限列中列出的每个用户权利都附带有一个说明、一个执行点和强制实施建议方法。

| AD RMS 权限/说明 | 如何强制 |
|--------------------------|----------------|
|**IPC_GENERIC_ALL** <br><br> 对用户授予所有权限。 <br><br> **常见强制点**：无 |此权限由系统使用，且通常不应直接检查。 <br><br> [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx) 使用此权限来确定是否要向用户授予其他权限，如本示例中所示。<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`|
|**IPC_GENERIC_READ** <br><br> 读取文档内容的权限。 <br><br> **常见强制点**：文档加载|不加载或显示文档内容|
|**IPC_GENERIC_WRITE** <br><br> 编辑文档内容的权限 <br><br> **常见强制点**：文档修改|将任何可用于修改文档内容的 UI 控件设置为不可编辑。 <br><br> 禁用任何触发文档更改的菜单项。 **编辑** > **剪切**、**编辑** > **粘贴**和**插入**是典型的示例。 <br><br>禁用任何触发文档更改的快捷方式菜单项。|
|无 AD RMS 权限 <br><br> 没有描述 <br><br> **常见强制点**：保存 | 禁用**文件** > **保存**菜单。 <br><br> **请注意**此权限不控制**文件** > **另存为**，因为该权限不表示对原始文档的更改。<br><br> 禁用可用于触发保存（例如 Ctrl+S）的任何键盘快捷方式。<br><br> **提示**如果用户不具有此权限，最佳做法是将核心**文件** > **保存**代码更新为失败状态。 如果你缺少可用于触发保存的任何 UX 机制，它将充当安全网。 |
|**IPC_GENERIC_EXTRACT** <br><br> 从受保护的格式中提取内容并将其置于未受保护的格式中的权限。 <br><br> **常见强制点**：复制到剪贴板 | 禁用**编辑** > **复制**菜单。 禁用**编辑** > **剪切**菜单。 <br><br>从任何快捷方式菜单中禁用“复制”和“剪切”。<br><br>禁用可用于触发复制（例如，Ctrl+C 或 Ctrl+X）的任何键盘快捷方式。<br><br>如果用户不具有此权限，则更新 [**WM_CUT**](https://msdn.microsoft.com/library/ms649023) 窗口消息处理程序以拒绝复制数据。 如果窗口正在使用默认 Windows 提供的消息处理程序，则将此窗口设为子类，并为 **WM_COPY** 和 **WM_CUT** 提供你自己的处理程序 。 |
|无 AD RMS 权限 <br><br> 没有描述 <br><br> **常见强制点**：另存为 |在“另存为”对话框中，禁用导致在没有 RMS 保护的情况下保存文档的任何文件格式。|
|无 AD RMS 权限 <br><br> 没有描述 <br><br> **常见强制点**：Alt+PrtScn|在呈现文档内容的任何窗口中调用 [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx)。|
|**IPC_GENERIC_EXPORT** <br><br> 用于从受保护的格式中提取内容并将其放在不同的 AD RMS 保护格式中的权限。 <br><br> **常见强制点**：另存为|在“另存为”对话框中，禁用保存到任何其他文件格式的功能。<br><br>**提示**如果用户尝试将此文件保存到另一种格式且不具有此权限时，最佳做法是将核心**文件** > **另存为**代码更新为失败状态。 如果你缺少可用于触发另存为的任何 UX 机制，它将充当安全网。|
|**IPC_GENERIC_PRINT** <br><br> 打印文档内容的权限。 <br><br> **常见强制点**：打印|禁用**文件** > **打印**菜单。<br><br>禁用可用于触发打印（例如 Ctrl+P）的任何键盘快捷方式。<br><br>禁用可用来触发打印的快捷菜单项。<br><br>**提示**如果用户不具有此权限，最佳做法是将核心**文件** > **打印**代码更新为失败状态。 如果你缺少可用于触发打印的任何 UX 机制，它将充当安全网。|
|**IPC_GENERIC_COMMENT** <br><br> 某些应用程序支持在不更新核心文档内容的情况下向文档中添加批注和注释的功能。<br><br>此权限授予用户对此功能的访问权限。 <br><br> **常见强制点**： <br><br> 查看 > 插入批注 <br><br> 查看 > 删除批注 | 禁用可用于修改文档批注或注释的任何菜单项。 示例为**查看** > **插入批注**和**查看** > **删除批注**。 <br><br>禁用可能触发修改文档批注的任何键盘快捷方式。<br><br>**请注意**默认实现需要同时使用 **IPC_GENERIC_COMMENT** 和 **IPC_GENERIC_WRITE** 来将新批注保存到文件中。 应用程序可以选择在授予了 **IPC_GENERIC_COMMENT** 权限而未授予 **IPC_GENERIC_WRITE** 权限的情况下添加支持。 在这种情况下，只要文档修改限制为仅对批注进行修改，便可以允许保存。|
|**IPC_VIEW_RIGHTS** <br><br> 没有描述 <br><br> **常见强制点**：不适用|由系统强制实施。 除非授予此权限，否则系统将不允许开发人员从许可证查询[**用户权限列表**](https://msdn.microsoft.com/library/hh535286.aspx)。
|**IPC_EDIT_RIGHTS** <br><br> 某些应用程序允许用户修改 AD RMS 保护的内容的用户和权限集。<br><br>此权限授予用户对此功能的访问权限。 <br><br> **常见强制点**：编辑 UI 控件的应用程序权限|禁止用户访问可用于编辑文档的 RMS 策略的任何 UI。|


## <a name="related-topics"></a>相关主题

* [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx)
