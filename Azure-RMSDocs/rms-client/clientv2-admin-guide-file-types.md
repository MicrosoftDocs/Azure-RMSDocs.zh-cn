---
title: 文件类型支持的 Azure 信息保护统一标记客户端
description: 有关受支持的文件类型、 文件扩展名和保护的管理员级别的技术详细信息负责 Windows 的 Azure 信息保护统一标记客户。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 61d7dfa6fa1fe86c930e9c6a6d2c21a807433583
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64768133"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>管理员指南：Azure 信息保护统一标记客户端支持的文件类型

>适用对象：*Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7（含 SP1）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*>
>
> 说明：*[Azure 信息保护统一标记适用于 Windows 的客户端](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure 信息保护统一标记客户端可以将以下应用于文档和电子邮件：

- 仅分类

- 分类和保护

- 仅保护

Azure 信息保护统一标记客户端还可以检查使用的已知的敏感信息类型或正则表达式定义的某些文件类型的内容。

使用以下信息查看 Azure 信息保护统一标记客户端支持的文件类型，了解不同级别的保护和如何更改默认保护级别，以及如何确定哪些文件会被自动排除 （跳过） 从分类和保护。

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

- Microsoft Office：下表中的文件类型。

    这些文件类型的受支持文件格式是以下 Office 程序的 97-2003 文件格式和 Office Open XML 格式：Word、Excel 和 PowerPoint。

    |Office 文件类型|Office 文件类型|
    |----------------------------------|----------------------------------|
    |。doc<br /><br />。docm<br /><br />。docx<br /><br />。dot<br /><br />。dotm<br /><br />。dotx<br /><br />。potm<br /><br />。potx<br /><br />。pps<br /><br />。ppsm<br /><br />。ppsx<br /><br />。ppt<br /><br />。pptm<br /><br />。pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />。xls<br /><br />。xlsb<br /><br />。xlt<br /><br />。xlsm<br /><br />。xlsx<br /><br />。xltm<br /><br />。xltx|

其他文件类型在受保护时也支持分类。 有关这些文件类型，请参阅[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)部分。

例如：

- 如果**常规**敏感度标签适用于分类，而不适用于保护：可以将“常规”标签应用到名为 sales.pdf 的文件，但不可将该标签应用到名为 sales.txt 的文件。 

- 如果**机密 \ 所有员工**敏感度标签适用于分类和保护：此标签可应用到名为 sales.pdf 和名为 sales.txt 的文件。 还可以只对这些文件应用保护，而不应用分类。

## <a name="file-types-supported-for-protection"></a>支持保护的文件类型

下表中所述，Azure 信息保护统一标记客户端支持在两个不同级别的保护。

|保护类型|本机|泛型|
|----------------------|----------|-----------|
|描述|对于文本、图像、Microsoft Office（Word、Excel、PowerPoint）文件、pdf 文件和其他支持 Rights Management 服务的应用程序文件类型，本机保护提供了同时包括权限的加密和强制执行的强保护级别。|对于其他所有应用程序和文件类型，常规保护提供了一种保护级别，该保护级别既包括使用 .pfile 文件类型的文件封装，又包括用于验证用户是否有权打开该文件的身份验证。|
|保护|通过以下方式强制执行文件保护：<br /><br />- 必须在通过电子邮件接收文件的用户或通过文件被授予访问权限或共享权限的用户成功通过身份验证之后，才能呈现受保护的内容。<br /><br />- 此外，无论是使用 Azure 信息保护查看器（适用于受保护的文本和图像文件）还是使用关联的应用程序（适用于其他所有受支持的文件类型）呈现内容时，都会强制执行内容所有者在文件处于受保护状态时所设置的使用权限和策略。|通过以下方式强制执行文件保护：<br /><br />- 必须在经授权可打开文件的人员以及被授予访问权限的人员成功通过身份验证之后才能呈现受保护的内容。 如果授权失败，则文件不会打开。<br /><br />- 将显示由内容所有者设置的使用权限和策略，以向授权用户通知预期使用策略。<br /><br />- 将对已授权的用户打开和访问文件的操作执行审核日志记录。 但不强制执行使用权限。|
|文件类型默认值|这是以下文件类型的默认保护级别：<br /><br />- 文本和图像文件<br /><br />- Microsoft Office（Word、Excel、PowerPoint）文件<br /><br />- 可移植文档格式 (.pdf)<br /><br />有关详细信息，请参阅以下部分：[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)。|这是针对不受本机保护支持的其他所有文件类型（例如 .vsdx、.rtf 等）的默认保护。|

可以更改 Azure 信息保护统一标记客户端应用的默认保护级别。 可以更改为常规，从常规为本机，本机的默认级别和应用保护，甚至阻止 Azure 信息保护统一标记客户端。 有关详细信息，请参阅本文中的[更改文件的默认保护级别](#changing-the-default-protection-level-of-files)部分。

当用户选择管理员配置的敏感度标签可以自动应用保护或用户可以通过使用指定其自己的自定义保护设置[权限级别](../configure-usage-rights.md#rights-included-in-permissions-levels)。 

### <a name="file-sizes-supported-for-protection"></a>支持保护的文件大小

有 Azure 信息保护统一标记客户端支持保护的最大文件大小。

- **Office 文件：**


  |                                                     Office 应用程序                                                      |                                                支持的最大文件大小                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 位：512 MB<br /><br />64 位：512 MB                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 位：2 GB<br /><br />64 位：仅受可用磁盘空间和内存限制                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 位：仅受可用磁盘空间和内存限制<br /><br />64 位：仅受可用磁盘空间和内存限制 |


- **对于其他所有文件**： 

  - 若要保护其他文件类型，并在 Azure 信息保护查看器中打开这些文件类型：最大文件大小仅受可用磁盘空间和内存限制。

  - 若要使用 [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) cmdlet 取消文件保护：.pst 文件支持的最大文件大小为 5 GB。 其他文件类型的文件大小上限仅受可用磁盘空间和内存限制

    提示：如果需要在大型 .pst 文件中搜索或恢复受保护的项目，请参阅[使用 Unprotect-RMSFile 进行电子数据展示的指南](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery)。

### <a name="supported-file-types-for-classification-and-protection"></a>支持用于分类和保护的文件类型

下表列出了的支持本机保护的 Azure 信息保护统一标记客户端，并且还可进行分类的文件类型的子集。 

这些文件类型单独进行标识，因为它们受到本机保护时，原始文件扩展名将更改，这些文件将变为只读。 请注意，以常规形式保护文件时，原始文件扩展名将始终更改为 .pfile。

> [!WARNING]
> 如果拥有可根据文件扩展名进行检查并采取操作的防火墙、Web 代理或者安全软件，你可能需要重新配置这些网络设备和软件以支持这些新的文件扩展名。

|原始文件扩展名|受保护的文件扩展名|
|--------------------------------|-------------------------------------|
|.txt|。ptxt|
|。xml|.pxml|
|。jpg|.pjpg|
|。jpeg|.pjpeg|
|。png|。ppng|
|.tif|.ptif|
|。tiff|.ptiff|
|。bmp|。pbmp|
|.gif|。pgif|
|。jpe|。pjpe|
|。jfif|。pjfif|
|。jt|.pjt|

下表列出了剩余的文件类型的支持本机保护的 Azure 信息保护统一标记客户端，并且还可进行分类。 会将它们识别为用于 Microsoft Office 应用的文件类型。 这些文件类型的受支持文件格式是以下 Office 程序的 97-2003 文件格式和 Office Open XML 格式：Word、Excel 和 PowerPoint。

对于这些文件，在文件受 Rights Management 服务保护后，文件扩展名仍保持不变。

|Office 支持的文件类型|Office 支持的文件类型|
|----------------------------------|----------------------------------|
|。doc<br /><br />。docm<br /><br />。docx<br /><br />。dot<br /><br />。dotm<br /><br />。dotx<br /><br />。potm<br /><br />。potx<br /><br />。pps<br /><br />。ppsm<br /><br />。ppsx<br /><br />。ppt<br /><br />。pptm<br /><br />。pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />。xla<br /><br />。xlam<br /><br />。xls<br /><br />。xlsb<br /><br />。xlt<br /><br />。xlsm<br /><br />。xlsx<br /><br />。xltm<br /><br />。xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>更改文件的默认保护级别
您可以更改 Azure 信息保护统一标记客户端通过编辑注册表来保护文件的方式。 例如，您可以强制支持本机保护由 Azure 信息保护统一标记客户端进行常规保护的文件。

可能要执行此操作的原因是：

- 为了确保所有用户都可以在没有支持本机保护的应用程序的情况下打开该文件。

- 为了适应根据文件扩展名对文件采取操作的安全系统，可将其重新配置为适应 .pfile 文件扩展名，但无法将其重新配置为适应已应用本机保护的多个文件扩展名。

同样，可以强制 Azure 信息保护统一标记的客户端将本机保护应用到默认情况下，已应用常规保护的文件。 如果你拥有支持 RMS API 的应用程序，则可能适合采取此操作。 例如，由内部开发人员编写的业务线应用程序或从独立软件供应商 (ISV) 处购买的应用程序。

您也可以强制 Azure 信息保护统一标记的客户端阻止文件保护 （不应用本机保护或常规保护）。 例如，如果你拥有一个必须能够打开特定文件才能处理其内容的自动应用程序或服务，则可能需要采取此操作。 当阻止保护某一文件类型时，用户无法使用 Azure 信息保护统一标记客户端保护具有该文件类型的文件。 他们将在尝试保护此类文件时看到一条消息，提示管理员已阻止保护，并且他们必须取消保护该文件的操作。

若要配置 Azure 信息保护统一标记的客户端将常规保护应用于所有文件，默认情况下，已应用本机保护，进行以下注册表编辑。 请注意，如果不存在 FileProtection 项，则必须手动创建。

1. 为以下注册表路径创建名为 * 的新项，该项使用文件扩展名表示文件：

    - 对于 32 位版本的 Windows：HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection

    - 对于 64 位版本的 Windows：HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection 和 HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection

2. 在新添加的项（例如 HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*）中，创建一个名为“Encryption”、数据值为 Pfile 的新字符串值 (REG_SZ)。

    此设置将导致 Azure 信息保护客户端应用常规保护。

这两个设置会导致 Azure 信息保护统一标记的客户端将常规保护应用于具有文件扩展名的所有文件。 如果这是你的目标，则无需进行任何进一步的配置。 但是，你可以为特定文件类型定义例外，以便它们仍受本机保护。 为此，你必须针对每个文件类型对注册表执行三个（针对 32 位 Windows）或六个（针对 64 位 Windows）额外的编辑操作：

1. 对于 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** 和 **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection**（如果适用）：添加新的密钥名称的文件扩展名 （不带前面的句点）。

    例如，对于文件扩展名为 .docx 的文件，创建一个名为 **DOCX**的项。

2. 在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**）中，创建一个名为 **AllowPFILEEncryption**、值为 **0** 的新 DWORD 值。

3. 在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**）中，创建一个名为 **Encryption**、值为 **Native** 的新字符串值。

应用这些设置后，所有文件均会受到常规保护，但文件扩展名为 .docx 的文件除外。 这些文件原本就受 Azure 信息保护统一标记客户端。

对于你想要定义为例外，因为它们支持本机保护，并且不希望它们由 Azure 信息保护统一标记客户端进行常规保护其他文件类型重复这三个步骤。

通过更改支持以下值的 **Encryption** 字符串的值，你可以在其他情况下进行类似的注册表编辑：

- **Pfile**：一般性保护

- **本机**：本机保护

- **关闭**：阻止保护

进行这些注册表更改后，无需重启计算机。 不过，如果使用 PowerShell 命令来保护文件，必须启动新的 PowerShell 会话，这样更改才能生效。

若要详细了解如何通过编辑注册表来更改文件的默认保护级别，请参阅开发人员指南中的[文件 API 配置](../develop/file-api-configuration.md)。 对于本文档中的开发人员，常规保护被称为“PFile”。

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>从分类和保护中排除的文件类型

为了帮助阻止用户更改对计算机操作至关重要的文件，某些文件类型和文件夹会自动从分类和保护中排除。 如果用户尝试进行分类或通过使用 Azure 信息保护统一标记客户端保护这些文件，他们将看到一条消息，不包括它们。

- 排除的文件类型：.lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、.msg、.msp、.msi、.pdb、.jar


- **排除的文件夹**： 
    - Windows
    - Program Files（\Program Files 和 \Program Files (x86)）
    - \ProgramData 
    - \AppData（适用于所有用户）


### <a name="files-that-cannot-be-protected-by-default"></a>默认不受保护的文件

除非文件为应用所保护的应用程序中当前打开，无法通过 Azure 信息保护统一标记客户端本机保护受密码保护任何文件。 最常看到的是受密码保护的 PDF 文件，但 Office 应用等其他应用程序也提供此功能。

### <a name="limitations-for-container-files-such-as-zip-files"></a>容器文件（如 .zip 文件）的限制

容器文件是包括其他文件的文件，典型示例是包括压缩文件的 .zip 文件。 其他示例包括 .rar、.7z、.msg 文件和包含附件的 PDF 文档。

可对这些容器文件进行分类和保护，但分类和保护不会应用到容器内每个文件。

如果容器文件包括已分类和受保护的文件，必须先提取这些文件，以更改其分类或保护设置。

Azure 信息保护查看器无法打开受保护的 PDF 文档中的附件。 在这种情况下，在查看器中打开文档时，附件不可见。

## <a name="next-steps"></a>后续步骤
现在，你已识别 Azure 信息保护统一标记客户端支持的文件类型，请参阅以下资源，可能需要支持此客户端的其他信息：

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)

