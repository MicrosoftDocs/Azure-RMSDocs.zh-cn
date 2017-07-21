---
title: "Azure 信息保护支持的文件类型"
description: "有关支持的文件类型、文件扩展名以及负责适用于 Windows 的 Azure 信息保护客户端的管理员的保护级别的技术详细信息。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: cf36e96ff7399188818ef0afdbefc223a82b9900
ms.sourcegitcommit: 12c9a4e3fe8e92d816f0a13003062f20dd2716df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2017
---
# <a name="file-types-supported-by-the-azure-information-protection-client"></a>Azure 信息保护客户端支持的文件类型

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

Azure 信息保护客户端可以将以下内容应用于文档和电子邮件：

- 仅分类

- 分类和保护

- 仅保护

使用以下信息查看支持的文件类型、不同的保护级别、如何更改默认保护级别，以及哪些文件会自动从分类和保护中排除（跳过）。

## <a name="file-types-supported-for-classification-only"></a>支持仅分类的文件类型

以下文件类型仅支持分类。 当其他文件类型也受到保护时，支持对这些类型进行分类（请参阅[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)部分）。

- **Adobe 可移植文档格式**：pdf

- **Microsoft Visio**：.vsdx、.vsdm、.vssx、.vssm、.vsd、.vdw、.vst

- **Microsoft Project**：.mpp、.mpt

- **Microsoft Publisher**：.pub

- **Microsoft Office 97、Office 2010、Office 2003**：.xls、.xlt、.doc、.dot、.ppt、.pps、.pot
- **Microsoft XPS**：.xps .oxps

- **图像**：.jpg、.jpe、.jpeg、.jif、.jfif、.jfi.png、.tif、.tiff

- **SolidWorks**：.sldprt、.slddrw、.sldasm

- **Autodesk Design Review 2013**：.dwfx

- **Adobe Photoshop**：.psd

- **数码底片**：.dng

## <a name="file-types-supported-for-protection"></a>支持保护的文件类型

Azure 信息保护客户端支持两个不同级别的保护，如下表中所述。

|保护类型|本机|泛型|
|----------------------|----------|-----------|
|说明|对于文本、图像、Microsoft Office（Word、Excel、PowerPoint）文件、pdf 文件和其他支持 Rights Management 服务的应用程序文件类型，本机保护提供了同时包括权限的加密和强制执行的强保护级别。|对于其他所有应用程序和文件类型，常规保护提供了一种保护级别，该保护级别既包括使用 .pfile 文件类型的文件封装，又包括用于验证用户是否有权打开该文件的身份验证。|
|保护|通过以下方式强制执行文件保护：<br /><br />- 必须在通过电子邮件接收文件的用户或通过文件被授予访问权限或共享权限的用户成功通过身份验证之后，才能呈现受保护的内容。<br /><br />- 此外，无论是使用 Azure 信息保护查看器（适用于受保护的文本和图像文件）还是关联的应用程序（适用于其他所有受支持的文件类型）呈现内容，都会完全执行内容所有者在文件处于受保护状态时所设置的使用权限和策略。|通过以下方式强制执行文件保护：<br /><br />- 必须在经授权可打开文件的用户或被授予访问权限的用户成功通过身份验证之后，才能呈现受保护的内容。 如果授权失败，则文件不会打开。<br /><br />- 将显示由内容所有者设置的使用权限和策略，以向授权用户通知预期使用策略。<br /><br />- 将对已授权的用户打开和访问文件的操作执行审核日志记录。 但不强制执行使用权限。|
|文件类型默认值|这是以下文件类型的默认保护级别：<br /><br />- 文本和图像文件<br /><br />- Microsoft Office（Word、Excel、PowerPoint）文件<br /><br />- 可移植文档格式 (.pdf)<br /><br />有关详细信息，请参阅以下部分：[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)。|这是针对不受本机保护支持的其他所有文件类型（例如 .vsdx、.rtf 等）的默认保护。|

可以更改 Azure 信息保护客户端应用的默认保护级别。 可以将默认级别从本机更改为常规，从常规更改为本机，甚至可以禁止 Azure 信息保护客户端应用保护。 有关详细信息，请参阅本文中的[更改文件的默认保护级别](#changing-the-default-protection-level-of-files)部分。

用户选择管理员配置的标签时，可以自动应用数据保护，也可以使用[权限级别](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels)指定自己的自定义保护设置。 

### <a name="file-sizes-supported-for-protection"></a>支持保护的文件大小

Azure 信息保护客户端支持保护的最大文件大小。

- **Office 文件：**
    
    |Office 应用程序|支持的最大文件大小|
    |--------------------------------|-------------------------------------|
    |Word 2007（仅受 AD RMS 支持）<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016|32 位：512 MB<br /><br />64 位：512 MB
    |Excel 2007（仅受 AD RMS 支持）<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016|32 位：2 GB<br /><br />64 位：仅受可用磁盘空间和内存限制|
    |PowerPoint 2007（仅受 AD RMS 支持）<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016|32 位：仅受可用磁盘空间和内存限制<br /><br />64 位：仅受可用磁盘空间和内存限制

- **对于其他所有文件**：
    
    - 对于客户端正式发布版：1GB
    
    - 对于预览客户端（最低版本为 1.8.41.0）：仅受可用磁盘空间和内存限制

### <a name="supported-file-types-for-classification-and-protection"></a>支持用于分类和保护的文件类型

下表列出了文件类型的一个子集，这些文件类型支持 Azure 信息保护客户端提供的本机保护，并可进行分类。 

这些文件类型单独进行标识，因为它们受到本机保护时，原始文件扩展名将更改，这些文件将变为只读。 请注意，以常规形式保护文件时，原始文件扩展名将始终更改为 .pfile。

> [!WARNING]
> 如果你拥有可根据文件扩展名检查并采取操作的防火墙、Web 代理或者安全软件，你可能需要重新配置它们以支持这些新的文件扩展名。

|原始文件扩展名|受保护的文件扩展名|
|--------------------------------|-------------------------------------|
|.txt|。ptxt|
|。xml|.pxml|
|。jpg|.pjpg|
|。jpeg|。pjpeg|
|。pdf|。ppdf|
|。png|。ppng|
|.tif|.ptif|
|。tiff|.ptiff|
|。bmp|。pbmp|
|.gif|。pgif|
|。jpe|。pjpe|
|。jfif|。pjfif|
|。jt|。pjt|

下一个表列出了其余的文件类型，这些文件类型通过 Azure 信息保护客户端支持本机保护，并且还可进行分类。 会将它们识别为用于 Microsoft Office 应用的文件类型。 

对于这些文件，在文件受 Rights Management 服务保护后，文件扩展名仍保持不变。

|Office 支持的文件类型|Office 支持的文件类型|
|----------------------------------|----------------------------------|
|。doc<br /><br />。docm<br /><br />。docx<br /><br />。dot<br /><br />。dotm<br /><br />。dotx<br /><br />。potm<br /><br />。potx<br /><br />。pps<br /><br />。ppsm<br /><br />。ppsx<br /><br />。ppt<br /><br />。pptm|。pptx<br /><br />。thmx<br /><br />。xla<br /><br />。xlam<br /><br />。xls<br /><br />。xlsb<br /><br />。xlt<br /><br />。xlsm<br /><br />。xlsx<br /><br />。xltm<br /><br />。xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>更改文件的默认保护级别
你可以通过编辑注册表来更改 Azure 信息保护客户端保护文件的方式。 例如，可以强制 Azure 信息保护客户端向支持本机保护的文件提供常规保护。

可能要执行此操作的原因是：

- 为了确保所有用户都可以在没有支持本机保护的应用程序的情况下打开该文件。

- 为了适应根据文件扩展名对文件采取操作的安全系统，可将其重新配置为适应 .pfile 文件扩展名，但无法将其重新配置为适应已应用本机保护的多个文件扩展名。

同样，也可以强制 Azure 信息保护客户端将本机保护应用到已默认应用常规保护的文件。 这在你具有支持 RMS API 的应用程序（例如，由内部开发人员编写的业务线应用程序或从独立软件供应商 (ISV) 处购买的应用程序）时可能正合适。

也可以强制 Azure 信息保护客户端阻止文件保护（而不是应用本机保护或常规保护）。 例如，如果你具有一个必须能够打开特定文件才能处理其内容的自动应用程序或服务，这可能是必需的。 当阻止保护某一文件类型时，用户无法使用 Azure 信息保护客户端保护具有该文件类型的文件。 他们将在尝试保护此类文件时看到一条消息，提示管理员已阻止保护，并且他们必须取消保护该文件的操作。

若要将 Azure 信息保护客户端配置为将常规保护应用于已默认应用本机保护的所有文件，请对注册表进行以下编辑。 请注意，如果不存在 FileProtection 项，则必须手动创建。

1. 为以下注册表路径创建名为 * 的新项，该项使用文件扩展名表示文件：
    
    - 对于 32 位版本 Windows：HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection
    
    - 对于 64 位版本 Windows：HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection

2. 在新添加的项（例如 HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*）中，创建一个名为“Encryption”、数据值为 Pfile 的新字符串值 (REG_SZ)。

    此设置将导致 Azure 信息保护客户端应用常规保护。

这两个设置会导致 Azure 信息保护客户端将常规保护应用于具有某一文件扩展名的所有文件。 如果这是你的目标，则无需进行任何进一步的配置。 但是，你可以为特定文件类型定义例外，以便它们仍受本机保护。 为此，你必须针对每个文件类型对注册表执行三个额外的编辑操作：

1. 对于 HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection（32 位 Windows）或 HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection（64 位 Windows）：添加一个具有该文件扩展名的新项（不带前面的句点）。

    例如，对于文件扩展名为 .docx 的文件，创建一个名为 **DOCX**的项。

2. 在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**）中，创建一个名为 **AllowPFILEEncryption**、值为 **0** 的新 DWORD 值。

3. 在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**）中，创建一个名为 **Encryption**、值为 **Native** 的新字符串值。

应用这些设置后，所有文件均受常规保护，但文件扩展名为 .docx 的文件除外，因为它们受 Azure 信息保护客户端的本机保护。

对于要将其定义为例外的其他文件类型重复这三个步骤，因为它们支持本机保护，而你不希望它们由 Azure 信息保护客户端进行常规保护。

通过更改支持以下值的 **Encryption** 字符串的值，你可以在其他情况下进行类似的注册表编辑：

- **Pfile**:一般性保护

- **Native**：本机保护

- **Off**：阻止保护

有关其他信息，请参阅开发人员指南中的[文件 API 配置](../develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。 

## <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-client"></a>Azure 信息保护客户端从分类和保护中排除的文件类型

为了帮助阻止用户更改对计算机操作至关重要的文件，某些文件类型和文件夹会自动从分类和保护中排除。 如果用户尝试对这些文件进行分类或保护，会看到一条消息，显示这些文件被排除。

- **排除的文件类型**：.lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、.msp、.msi、.pdb、.jar

- **排除的文件夹**： 
    - Windows
    - Program Files（\Program Files 和 \Program Files (x86)）
    - \ProgramData 
    - \AppData（适用于所有用户）


## <a name="next-steps"></a>后续步骤
现在你已识别了 Azure 信息保护客户端支持的文件类型，若要了解支持此客户端所需的其他信息，请参阅以下内容：

- [自定义](client-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](client-admin-guide-files-and-logging.md)

- [文档跟踪、](client-admin-guide-document-tracking.md)

- [PowerShell 命令](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
