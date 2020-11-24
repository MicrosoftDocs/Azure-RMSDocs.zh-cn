---
title: 支持的文件类型-Azure 信息保护统一标签客户端
description: 有关受支持的文件类型、文件扩展名以及负责 Windows 的 Azure 信息保护统一标签客户端的管理员的保护级别的技术详细信息。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b9f8a53135407e91d04542bc53c709b82662a19a
ms.sourcegitcommit: c6b0b092735504fd76d74a46d024321673482098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "95566456"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>管理员指南： Azure 信息保护统一标签客户端支持的文件类型

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*>
>
>*如果你具有 Windows 7 或 Office 2010，请参阅 [AIP For Windows And office 版本中的扩展支持](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)。*
>
> 说明：[用于 Windows 的 Azure 信息保护统一标记客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

Azure 信息保护统一标签客户端可以将以下内容应用于文档和电子邮件：

- 仅分类

- 分类和保护

- 仅保护

Azure 信息保护统一标签客户端还可以使用已知的敏感信息类型或你定义的正则表达式来检查某些文件类型的内容。

使用以下信息查看 Azure 信息保护统一标签客户端支持的文件类型，了解不同级别的保护，以及如何更改默认保护级别，以及如何确定哪些文件被自动排除 (从分类和保护中跳过) 。

对于列出的文件类型，WebDav 位置不受支持。

## <a name="file-types-supported-for-classification-only"></a>支持仅分类的文件类型

可对以下文件类型进行分类（即使在它们未受保护时也可）。

- **Adobe 可移植文档格式**：pdf

- **Microsoft Project**：.mpp、.mpt

- **Microsoft Publisher**：.pub

- **Microsoft XPS**：.xps .oxps

- 图像：.jpg、.jpe、.jpeg、.jif、.jfif、.jfi、 .png、.tif、.tiff

- **Autodesk Design Review 2013**：.dwfx

- **Adobe Photoshop**：.psd

- **数码底片**：.dng

- **Microsoft Office**：下表中的文件类型。

    这些文件类型的受支持文件格式是以下 Office 程序的 97-2003 文件格式和 Office Open XML 格式：Word、Excel 和 PowerPoint。

    |Office 文件类型|Office 文件类型|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

其他文件类型在受保护时也支持分类。 有关这些文件类型，请参阅[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)部分。

示例:

- 如果 " **常规** 敏感度" 标签应用分类并且不应用保护：可以将 " **常规** " 标签应用到名为 sales.pdf 的文件，但不能将此标签应用于名为 sales.txt 的文件。

- 如果 " **机密 \ 所有员工** " 敏感度标签应用分类和保护：可以将此标签应用于名为 sales.pdf 的文件和名为 sales.txt 的文件。 还可以只对这些文件应用保护，而不应用分类。

## <a name="file-types-supported-for-protection"></a>支持保护的文件类型

Azure 信息保护统一标签客户端支持两个不同级别的保护，如下表中所述。

|保护类型|本机|泛型|
|----------------------|----------|-----------|
|说明|对于文本、图像、Microsoft Office（Word、Excel、PowerPoint）文件、pdf 文件和其他支持 Rights Management 服务的应用程序文件类型，本机保护提供了同时包括权限的加密和强制执行的强保护级别。|对于其他支持的文件类型，通用保护提供了一种保护级别，其中包括使用 .pfile 文件类型和身份验证的文件封装，以验证用户是否有权打开该文件。|
|保护|通过以下方式强制执行文件保护：<br /><br />- 必须在通过电子邮件接收文件的用户或通过文件被授予访问权限或共享权限的用户成功通过身份验证之后，才能呈现受保护的内容。<br /><br />- 此外，无论是使用 Azure 信息保护查看器（适用于受保护的文本和图像文件）还是使用关联的应用程序（适用于其他所有受支持的文件类型）呈现内容时，都会强制执行内容所有者在文件处于受保护状态时所设置的使用权限和策略。|通过以下方式强制执行文件保护：<br /><br />- 必须在经授权可打开文件的人员以及被授予访问权限的人员成功通过身份验证之后才能呈现受保护的内容。 如果授权失败，则文件不会打开。<br /><br />- 将显示由内容所有者设置的使用权限和策略，以向授权用户通知预期使用策略。<br /><br />- 将对已授权的用户打开和访问文件的操作执行审核日志记录。 但不强制执行使用权限。|
|文件类型默认值|这是以下文件类型的默认保护级别：<br /><br />- 文本和图像文件<br /><br />- Microsoft Office（Word、Excel、PowerPoint）文件<br /><br />- 可移植文档格式 (.pdf)<br /><br />有关详细信息，请参阅以下部分：[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)。|这是针对不受本机保护支持的其他所有文件类型（例如 .vsdx、.rtf 等）的默认保护。|

不能更改 Azure 信息保护统一标签客户端或扫描程序应用的默认保护级别。 但是，您可以更改受保护的文件类型。 有关详细信息，请参阅 [更改要保护的文件类型](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)。

当用户选择管理员配置的敏感度标签，或者用户可以使用 [权限级别](../configure-usage-rights.md#rights-included-in-permissions-levels)指定自己的自定义保护设置时，可以自动应用保护。

### <a name="file-sizes-supported-for-protection"></a>支持保护的文件大小

Azure 信息保护统一标签客户端支持保护的最大文件大小。

- **Office 文件：**

  |                                                     Office 应用程序                                                      |                                                支持的最大文件大小                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 位：512 MB<br /><br />64 位：512 MB                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 位：2 GB<br /><br />64 位：仅受可用磁盘空间和内存限制                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 位：仅受可用磁盘空间和内存限制<br /><br />64 位：仅受可用磁盘空间和内存限制 |

- **对于其他所有文件**：

  - 若要保护其他文件类型，并在 Azure 信息保护查看器中打开这些文件类型：文件大小上限仅受可用磁盘空间和内存限制。

  - 若要使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 取消保护文件：.pst 文件支持的文件大小上限为 5GB。 其他文件类型的文件大小上限仅受可用磁盘空间和内存限制

    提示：如果需要在大型 .pst 文件中搜索或恢复受保护的项目，请参阅[使用 Unprotect-RMSFile 进行电子数据展示的指南](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery)。

### <a name="supported-file-types-for-classification-and-protection"></a>支持用于分类和保护的文件类型

下表列出了支持 Azure 信息保护统一标签客户端的本机保护的文件类型的子集，还可以进行分类。

这些文件类型单独进行标识，因为它们受到本机保护时，原始文件扩展名将更改，这些文件将变为只读。 请注意，以常规形式保护文件时，原始文件扩展名将始终更改为 .pfile。

> [!WARNING]
> 如果拥有可根据文件扩展名进行检查并采取操作的防火墙、Web 代理或者安全软件，你可能需要重新配置这些网络设备和软件以支持这些新的文件扩展名。

|原始文件扩展名|受保护的文件扩展名|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|

下表列出了支持 Azure 信息保护统一标签客户端的本机保护的其他文件类型，还可以进行分类。 会将它们识别为用于 Microsoft Office 应用的文件类型。 这些文件类型的受支持文件格式是以下 Office 程序的 97-2003 文件格式和 Office Open XML 格式：Word、Excel 和 PowerPoint。

对于这些文件，在文件受 Rights Management 服务保护后，文件扩展名仍保持不变。

|Office 支持的文件类型|Office 支持的文件类型|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>从分类和保护中排除的文件类型

为了帮助阻止用户更改对计算机操作至关重要的文件，某些文件类型和文件夹会自动从分类和保护中排除。 如果用户尝试使用 Azure 信息保护统一标签客户端来分类或保护这些文件，则会看到一条排除的消息。

- **排除的文件类型**：.lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、.msp、.msi、.pdb、.jar

- **排除的文件夹**：
    - Windows
    - Program Files（\Program Files 和 \Program Files (x86)）
    - \ProgramData
    - \AppData（适用于所有用户）

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序从分类和保护中排除的文件类型

默认情况下，扫描器还会排除与 Azure 信息保护统一标签客户端相同的文件类型，但有以下例外：

- 也排除 .msg、.rtf 和 rar

可更改扫描程序检查文件时包含或排除的文件类型：

- 通过[使用 Azure 门户](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal)，在扫描程序配置文件中配置“要扫描的文件类型”。
    
    > [!NOTE]
    > 如果在扫描时包含 .rtf 文件，请仔细监视扫描程序。 扫描程序无法成功检查某些 .rtf 文件，对于这些文件，未完成检查，必须重启服务。

默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 若要为扫描程序更改此行为，请使用 PowerShell 高级设置 **PFileSupportedExtensions**。 有关详细信息，请参阅使用 PowerShell 更改从扫描程序部署说明中 [保护的文件类型](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) 。

### <a name="files-that-cannot-be-protected-by-default"></a>默认不受保护的文件

受密码保护的任何文件都不能通过 Azure 信息保护统一标签客户端进行本机保护，除非该文件当前在应用保护的应用程序中打开。 最常看到的是受密码保护的 PDF 文件，但 Office 应用等其他应用程序也提供此功能。

### <a name="limitations-for-container-files-such-as-zip-files"></a>容器文件（如 .zip 文件）的限制

有关详细信息，请参阅 [Azure 信息保护已知问题](../known-issues.md#client-support-for-container-files-such-as-zip-files)。

## <a name="file-types-supported-for-inspection"></a>支持检查的文件类型

如果没有任何其他配置，Azure 信息保护统一标签客户端将使用 Windows IFilter 来检查文档的内容。 Windows Search 使用 Windows IFilter 来编制索引。 因此，使用 [Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell 命令时，可以检查以下文件类型。

|应用程序类型|文件类型|
|--------------------------------|-------------------------------------|
|Word|文档.docx; docm; .dot; normal.dotm;. dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|PDF |.pdf|
|文本|.txt; .xml; .csv|

通过进行额外配置，还可以检查其他文件类型。 例如，可以[注册自定义文件扩展名，使用现有 Windows 筛选器处理程序处理文本文件](/windows/desktop/search/-search-ifilter-registering-filters)，还可以安装软件供应商提供的其他筛选器。

若要检查安装了哪些筛选器，请参阅 Windows Search 开发人员指南中的[查找给定文件扩展名的筛选器处理程序](/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension)一节。

以下各节提供了检查 .zip 文件和 .tiff 文件的配置说明。

### <a name="to-inspect-zip-files"></a>检查 .zip 文件

请按照以下说明操作，使用 Azure 信息保护扫描程序和 [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell 命令检查 .zip 文件：

1. 对于运行扫描程序或 PowerShell 会话的计算机，请安装 [Office 2010 Filter Pack SP2](https://support.microsoft.com/help/2687447/description-of-office-2010-filter-pack-sp2)。

2. 对于扫描仪：查找敏感信息后，如果要使用标签对 .zip 文件进行分类和保护，请使用 PowerShell 高级设置 **PFileSupportedExtensions** 指定 .zip 文件扩展名，如使用 powershell 更改从扫描程序部署说明中 [保护的文件类型](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) 中所述。

执行这些步骤后的示例方案：

名为“accounts.zip”的文件包含带有信用卡号的 Excel 电子表格。 你有一个名为 " **机密 \ 财务**" 的敏感度标签，该标签配置为发现信用卡号，并自动应用带有限制访问财务组的保护的标签。

检查文件后，来自 PowerShell 会话的统一标签客户端会将此文件归类为 **机密 \ 财务**，并对该文件应用常规保护，以便只有财务组的成员可以将该文件解压缩，并将该文件重命名 **accounts.zip .pfile**。

### <a name="to-inspect-tiff-files-by-using-ocr"></a>使用 OCR 检查 .tiff 文件

[AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) powershell 命令可以使用光学字符识别 (OCR) 在安装 Windows TIFF IFilter 功能时使用 tiff 文件扩展名检查 tiff 图像，然后在运行 PowerShell 会话的计算机上配置[Windows tiff ifilter 设置](/previous-versions/windows/it-pro/windows-7/dd744701(v=ws.10))。

对于扫描仪：查找敏感信息后，如果应使用标签对 tiff 文件进行分类和保护，请使用 PowerShell 高级设置 **PFileSupportedExtensions** 指定此文件扩展名，如使用 powershell 更改从扫描程序部署说明中 [保护的文件类型](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) 中所述。

## <a name="next-steps"></a>后续步骤

现在，已确定 Azure 信息保护统一标签客户端支持的文件类型，请参阅以下资源，了解支持此客户端所需的其他信息：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)