---
title: 支持的文件类型-Azure 信息保护客户端
description: 有关支持的文件类型、文件扩展名以及负责适用于 Windows 的 Azure 信息保护客户端的管理员的保护级别的技术详细信息。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4c9a13c0bfcaa98d19c3ed39c6e00d921c6f572a
ms.sourcegitcommit: f32928f7dcc03111fc72d958cda9933d15065a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2020
ms.locfileid: "84665412"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-client"></a>管理员指南：Azure 信息保护客户端支持的文件类型

>*适用于： Active Directory Rights Management Services， [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)，windows 10，Windows 8.1，windows 8，windows server 2019，windows server 2016，windows Server 2012 R2，windows server 2012*
>
> *适用于[Windows 的 Azure 信息保护客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)的说明*

>[!NOTE] 
> 为了提供统一、简化的客户体验，Azure 门户中的 Azure 信息保护客户端（经典）**** 和标签管理**** 将于 2021 年 3 月 31 日**** 弃用****。 在此时间框架内，所有 Azure 信息保护客户都可以使用 Microsoft 信息保护统一标记平台转换到我们的统一标记解决方案。 有关详细信息，请参阅官方[弃用通知](https://aka.ms/aipclassicsunset)。

Azure 信息保护客户端可以将以下内容应用于文档和电子邮件：

- 仅分类

- 分类和保护

- 仅保护

Azure 信息保护客户端还可以使用已知的敏感信息类型或用户定义的正则表达式来检查某些文件类型的内容。

使用以下信息查看 Azure 信息保护客户端支持的文件类型，了解不同的保护级别、如何更改默认保护级别，以及如何确定哪些文件会自动从分类和保护中被排除（跳过）。

对于列出的文件类型，WebDav 位置不受支持。

## <a name="file-types-supported-for-classification-only"></a>支持仅分类的文件类型

可对以下文件类型进行分类（即使在它们未受保护时也可）。

- **Adobe 可移植文档格式**：pdf

- **Microsoft Project**：.mpp、.mpt

- **Microsoft Publisher**：.pub

- **Microsoft XPS**：.xps .oxps

- 图像****：.jpg、.jpe、.jpeg、.jif、.jfif、.jfi、 .png、.tif、.tiff

- **Autodesk Design Review 2013**：.dwfx

- **Adobe Photoshop**：.psd

- **数码底片**：.dng

- **Microsoft Office**：下表中的文件类型。

    这些文件类型的受支持文件格式是以下 Office 程序的 97-2003 文件格式和 Office Open XML 格式：Word、Excel 和 PowerPoint。

    |Office 文件类型|Office 文件类型|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

其他文件类型在受保护时也支持分类。 有关这些文件类型，请参阅[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)部分。

例如，在当前[默认策略](../configure-policy-default.md)中，“常规”**** 标签适用于分类，而不适用于保护。 可以将“常规”**** 标签应用到名为 sales.pdf 的文件，但不可将该标签应用到名为 sales.txt 的文件。 

此外，在当前默认策略中，“机密\所有员工”**** 适用于分类和保护。 此标签可应用到名为 sales.pdf 和名为 sales.txt 的文件。 还可以只对这些文件应用保护，而不应用分类。

## <a name="file-types-supported-for-protection"></a>支持保护的文件类型

Azure 信息保护客户端支持两个不同级别的保护，如下表中所述。

|保护类型|本机|泛型|
|----------------------|----------|-----------|
|说明|对于文本、图像、Microsoft Office（Word、Excel、PowerPoint）文件、pdf 文件和其他支持 Rights Management 服务的应用程序文件类型，本机保护提供了同时包括权限的加密和强制执行的强保护级别。|对于其他所有应用程序和文件类型，常规保护提供了一种保护级别，该保护级别既包括使用 .pfile 文件类型的文件封装，又包括用于验证用户是否有权打开该文件的身份验证。|
|保护|通过以下方式强制执行文件保护：<br /><br />- 必须在通过电子邮件接收文件的用户或通过文件被授予访问权限或共享权限的用户成功通过身份验证之后，才能呈现受保护的内容。<br /><br />- 此外，无论是使用 Azure 信息保护查看器（适用于受保护的文本和图像文件）还是使用关联的应用程序（适用于其他所有受支持的文件类型）呈现内容时，都会强制执行内容所有者在文件处于受保护状态时所设置的使用权限和策略。|通过以下方式强制执行文件保护：<br /><br />- 必须在经授权可打开文件的人员以及被授予访问权限的人员成功通过身份验证之后才能呈现受保护的内容。 如果授权失败，则文件不会打开。<br /><br />- 将显示由内容所有者设置的使用权限和策略，以向授权用户通知预期使用策略。<br /><br />- 将对已授权的用户打开和访问文件的操作执行审核日志记录。 但不强制执行使用权限。|
|文件类型默认值|这是以下文件类型的默认保护级别：<br /><br />- 文本和图像文件<br /><br />- Microsoft Office（Word、Excel、PowerPoint）文件<br /><br />- 可移植文档格式 (.pdf)<br /><br />有关详细信息，请参阅以下部分：[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)。|这是针对不受本机保护支持的其他所有文件类型（例如 .vsdx、.rtf 等）的默认保护。|

可以更改 Azure 信息保护客户端应用的默认保护级别。 可以将默认级别从本机更改为常规，从常规更改为本机，甚至可以禁止 Azure 信息保护客户端应用保护。 有关详细信息，请参阅本文中的[更改文件的默认保护级别](#changing-the-default-protection-level-of-files)部分。

用户选择管理员配置的标签时，可以自动应用数据保护，也可以使用[权限级别](../configure-usage-rights.md#rights-included-in-permissions-levels)指定自己的自定义保护设置。 

### <a name="file-sizes-supported-for-protection"></a>支持保护的文件大小

Azure 信息保护客户端支持保护的最大文件大小。

- **Office 文件：**


  |                                                     Office 应用程序                                                      |                                                支持的最大文件大小                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2007（仅受 AD RMS 支持）<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 位：512 MB<br /><br />64 位：512 MB                                          |
  |           Excel 2007（仅受 AD RMS 支持）<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 位：2 GB<br /><br />64 位：仅受可用磁盘空间和内存限制                       |
  | PowerPoint 2007（仅受 AD RMS 支持）<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 位：仅受可用磁盘空间和内存限制<br /><br />64 位：仅受可用磁盘空间和内存限制 |


- **对于其他所有文件**： 

  - 若要保护其他文件类型，并在 Azure 信息保护查看器中打开这些文件类型：文件大小上限仅受可用磁盘空间和内存限制。

  - 若要使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 取消保护文件：.pst 文件支持的文件大小上限为 5GB。 其他文件类型的文件大小上限仅受可用磁盘空间和内存限制

    提示：如果需要在大型 .pst 文件中搜索或恢复受保护的项目，请参阅[使用 Unprotect-RMSFile 进行电子数据展示的指南](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery)。

### <a name="supported-file-types-for-classification-and-protection"></a>支持用于分类和保护的文件类型

下表列出了文件类型的一个子集，这些文件类型支持 Azure 信息保护客户端提供的本机保护，并可进行分类。 

这些文件类型单独进行标识，因为它们受到本机保护时，原始文件扩展名将更改，这些文件将变为只读。 请注意，以常规形式保护文件时，原始文件扩展名将始终更改为 .pfile。

> [!WARNING]
> 如果拥有可根据文件扩展名进行检查并采取操作的防火墙、Web 代理或者安全软件，你可能需要重新配置这些网络设备和软件以支持这些新的文件扩展名。

|原始文件扩展名|受保护的文件扩展名|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.pdf|.ppdf [[1]](#footnote-1)|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|

###### <a name="footnote-1"></a>脚注 1
使用 Azure 信息保护客户端的最新版本时，[在默认情况下](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)，受保护 PDF 文档的文件扩展名仍为 .pdf。

下一个表列出了其余的文件类型，这些文件类型通过 Azure 信息保护客户端支持本机保护，并且还可进行分类。 会将它们识别为用于 Microsoft Office 应用的文件类型。 这些文件类型的受支持文件格式是以下 Office 程序的 97-2003 文件格式和 Office Open XML 格式：Word、Excel 和 PowerPoint。

对于这些文件，在文件受 Rights Management 服务保护后，文件扩展名仍保持不变。

|Office 支持的文件类型|Office 支持的文件类型|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>更改文件的默认保护级别
你可以通过编辑注册表来更改 Azure 信息保护客户端保护文件的方式。 例如，可以强制 Azure 信息保护客户端向支持本机保护的文件提供常规保护。

可能要执行此操作的原因是：

- 如果用户没有支持本机保护的应用程序，请确保所有用户都可以打开该文件。

- 为了适应根据文件扩展名对文件采取操作的安全系统，可将其重新配置为适应 .pfile 文件扩展名，但无法将其重新配置为适应已应用本机保护的多个文件扩展名。

同样，也可以强制 Azure 信息保护客户端将本机保护应用到已默认应用常规保护的文件。 如果你拥有支持 RMS API 的应用程序，则可能适合采取此操作。 例如，由内部开发人员编写的业务线应用程序或从独立软件供应商 (ISV) 处购买的应用程序。

也可以强制 Azure 信息保护客户端阻止文件保护（而不是应用本机保护或常规保护）。 例如，如果你拥有一个必须能够打开特定文件才能处理其内容的自动应用程序或服务，则可能需要采取此操作。 当阻止保护某一文件类型时，用户无法使用 Azure 信息保护客户端保护具有该文件类型的文件。 他们将在尝试保护此类文件时看到一条消息，提示管理员已阻止保护，并且他们必须取消保护该文件的操作。

若要将 Azure 信息保护客户端配置为将常规保护应用于已默认应用本机保护的所有文件，请对注册表进行以下编辑。 请注意，如果不存在 FileProtection 项，则必须手动创建。

1. 为以下注册表路径创建名为 * 的新项，该项使用文件扩展名表示文件：

    - 对于 32 位版本 Windows：HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection****

    - 对于64位版本的 Windows： **HKEY_LOCAL_MACHINE \software\wow6432node\microsoft\msipc\fileprotection**和**HKEY_LOCAL_MACHINE \software\microsoft\msipc\fileprotection**

2. 在新添加的项（例如 HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*）中，创建一个名为“Encryption”****、数据值为 Pfile **** 的新字符串值 (REG_SZ)。

    此设置将导致 Azure 信息保护客户端应用常规保护。

这两个设置会导致 Azure 信息保护客户端将常规保护应用于具有某一文件扩展名的所有文件。 如果这是你的目标，则无需进行任何进一步的配置。 但是，你可以为特定文件类型定义例外，以便它们仍受本机保护。 为此，你必须针对每个文件类型对注册表执行三个（针对 32 位 Windows）或六个（针对 64 位 Windows）额外的编辑操作：

1. 对于**HKEY_LOCAL_MACHINE \software\microsoft\msipc\fileprotection**和**HKEY_LOCAL_MACHINE \software\wow6432node\microsoft\msipc\fileprotection** （如果适用）：添加一个具有该文件扩展名的新项（不带前面的句点）。

    例如，对于文件扩展名为 .docx 的文件，创建一个名为 **DOCX** 的项。

2. 在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**）中，创建一个名为 **AllowPFILEEncryption**、值为 **0** 的新 DWORD 值。

3. 在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**）中，创建一个名为 **Encryption**、值为 **Native** 的新字符串值。

应用这些设置后，所有文件均会受到常规保护，但文件扩展名为 .docx 的文件除外。 这些文件受到 Azure 信息保护客户端的本机保护。

对于要将其定义为例外的其他文件类型重复这三个步骤，因为它们支持本机保护，而你不希望它们由 Azure 信息保护客户端进行常规保护。

通过更改支持以下值的 **Encryption** 字符串的值，你可以在其他情况下进行类似的注册表编辑：

- **Pfile**:一般性保护

- **Native**：本机保护

- **Off**：阻止保护

进行这些注册表更改后，无需重启计算机。 不过，如果使用 PowerShell 命令来保护文件，必须启动新的 PowerShell 会话，这样更改才能生效。

若要详细了解如何通过编辑注册表来更改文件的默认保护级别，请参阅开发人员指南中的[文件 API 配置](../develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>从分类和保护中排除的文件类型

为了帮助阻止用户更改对计算机操作至关重要的文件，某些文件类型和文件夹会自动从分类和保护中排除。 如果用户尝试使用 Azure 信息保护客户端对这些文件进行分类或保护，则会看到一条消息，显示这些文件被排除。

- 排除的文件类型****：.lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、.msg、.msp、.msi、.pdb、.jar


- **排除的文件夹**： 
    - Windows
    - Program Files（\Program Files 和 \Program Files (x86)）
    - \ProgramData 
    - \AppData（适用于所有用户）

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序从分类和保护中排除的文件类型

默认情况下，扫描程序还会排除 Azure 信息保护客户端支持的相同文件类型，要排除的例外情况如下：

- .rtf 和 .rar 也会被排除在外

可更改扫描程序检查文件时包含或排除的文件类型：

- 通过[使用 Azure 门户](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal)，在扫描程序配置文件中配置“要扫描的文件类型”****。

> [!NOTE]
> 如果在扫描时包含 .rtf 文件，请仔细监视扫描程序。 扫描程序无法成功检查某些 .rtf 文件，对于这些文件，未完成检查，必须重启服务。 

默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 若要更改扫描程序的这一行为，请编辑注册表并指定想要得到保护的其他文件类型。 有关说明，请参阅注册表编辑以更改从扫描程序部署说明中[保护的文件类型](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected)。

### <a name="files-that-cannot-be-protected-by-default"></a>默认不受保护的文件

受密码保护的任何文件都不能由 Azure 信息保护客户端本机保护，除非该文件当前在应用保护的应用程序中打开。 最常看到的是受密码保护的 PDF 文件，但 Office 应用等其他应用程序也提供此功能。

通过更改 Azure 信息保护客户端的[默认行为](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)，来使其使用 .ppdf 文件扩展名保护 PDF 文件时，客户端无法对以下任一情况下的 PDF 文件进行本机保护或取消保护：

- 基于窗体的 PDF 文件。

- 文件扩展名为 .pdf 的受保护 PDF 文件。

    Azure 信息保护客户端可以保护不受保护的 PDF 文件，并且可取消保护和重新保护扩展名为 .ppdf 的受保护 PDF 文件。

### <a name="limitations-for-container-files-such-as-zip-files"></a>容器文件（如 .zip 文件）的限制

容器文件是包括其他文件的文件，典型示例是包括压缩文件的 .zip 文件。 其他示例包括 .rar、.7z、.msg 文件和包含附件的 PDF 文档。

可对这些容器文件进行分类和保护，但分类和保护不会应用到容器内每个文件。

如果容器文件包括已分类和受保护的文件，必须先提取这些文件，以更改其分类或保护设置。 但是，使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet，可删除受支持容器文件中所有文件的保护。

Azure 信息保护查看器无法打开受保护的 PDF 文档中的附件。 在这种情况下，在查看器中打开文档时，附件不可见。

## <a name="file-types-supported-for-inspection"></a>支持检查的文件类型

无需任何额外配置，Azure 信息保护客户端即可使用 Windows IFilter 来检查文档内容。 Windows Search 使用 Windows IFilter 来编制索引。 因此，使用 [Azure 信息保护扫描程序](../deploy-aip-scanner.md)或 [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell 命令时，可以检查下列文件类型。

|应用程序类型|文件类型|
|--------------------------------|-------------------------------------|
|Word|文档.docx; docm; .dot; normal.dotm;. dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|PDF |.pdf|
|文本|.txt; .xml; .csv|

通过进行额外配置，还可以检查其他文件类型。 例如，可以[注册自定义文件扩展名，使用现有 Windows 筛选器处理程序处理文本文件](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters)，还可以安装软件供应商提供的其他筛选器。

若要检查安装了哪些筛选器，请参阅 Windows Search 开发人员指南中的[查找给定文件扩展名的筛选器处理程序](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension)一节。

以下各节提供了检查 .zip 文件和 .tiff 文件的配置说明。

### <a name="to-inspect-zip-files"></a>检查 .zip 文件

请按照以下说明操作，使用 Azure 信息保护扫描程序和 [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell 命令检查 .zip 文件：

1. 对于运行扫描程序或 PowerShell 会话的计算机，请安装 [Office 2010 Filter Pack SP2](https://support.microsoft.com/help/2687447/description-of-office-2010-filter-pack-sp2)。

2. 对于扫描仪：查找敏感信息后，如果要使用标签对 .zip 文件进行分类和保护，请将此文件扩展名的注册表项添加为具有通用保护（.pfile），如注册表编辑中所述，可以更改从扫描程序部署说明中[保护的文件类型](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected)。

执行这些步骤后的示例方案： 

名为“accounts.zip”的文件包含带有信用卡号的 Excel 电子表格****。 Azure 信息保护策略具有名为“机密\财务”的标签，该标签配置为发现信用卡号，并自动应用带有保护的标签，以限制对财务组进行访问****。 

检查文件后，扫描程序将此文件归类为“机密\财务”，对文件应用通用保护，以便只有财务组的成员可以解压缩它，并重命名文件“accounts.zip.pfile”********。

### <a name="to-inspect-tiff-files-by-using-ocr"></a>使用 OCR 检查 .tiff 文件

如果运行扫描程序或 PowerShell 会话的计算机上安装 Windows TIFF IFilter 功能并配置 [Windows TIFF IFilter 设置](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29)，Azure 信息保护扫描程序和 [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell 命令可以使用光学字符识别 (OCR) 来检查文件扩展名为 .tiff 的 TIFF 图像。

对于扫描仪：查找敏感信息后，如果应使用标签对 tiff 文件进行分类和保护，请添加此文件扩展名的注册表项以具有本机保护，如注册表编辑中所述，用于更改从扫描程序部署说明中[保护的文件类型](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected)。

## <a name="next-steps"></a>后续步骤
现在你已识别了 Azure 信息保护客户端支持的文件类型，若要了解支持此客户端所需的其他信息，请参阅以下资源：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪](client-admin-guide-document-tracking.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

