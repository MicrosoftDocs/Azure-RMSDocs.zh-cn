---
title: File types supported - Azure Information Protection unified labeling client
description: Technical details about supported file types, file name extensions, and levels of protection for admins who are are responsible for the Azure Information Protection unified labeling client for Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bf386685847f10ecead59ac59c44620f03372d6d
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474275"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>Admin Guide: File types supported by the Azure Information Protection unified labeling client

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*>
>
> *Instructions for: [Azure Information Protection unified labeling client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

The Azure Information Protection unified labeling client can apply the following to documents and emails:

- 仅分类

- 分类和保护

- 仅保护

The Azure Information Protection unified labeling client can also inspect the content of some file types using well-known sensitive information types or regular expressions that you define.

Use the following information to check which file types the Azure Information Protection unified labeling client supports, understand the different levels of protection and how to change the default protection level, and to identify which files are automatically excluded (skipped) from classification and protection.

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
    |。doc<br /><br />。docm<br /><br />。docx<br /><br />。dot<br /><br />。dotm<br /><br />。dotx<br /><br />。potm<br /><br />。potx<br /><br />。pps<br /><br />。ppsm<br /><br />。ppsx<br /><br />。ppt<br /><br />。pptm<br /><br />。pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />。xls<br /><br />。xlsb<br /><br />。xlt<br /><br />。xlsm<br /><br />。xlsx<br /><br />。xltm<br /><br />。xltx|

其他文件类型在受保护时也支持分类。 有关这些文件类型，请参阅[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)部分。

例如：

- If the **General** sensitivity label applies classification and does not apply protection: You could apply the **General** label to a file named sales.pdf but you could not apply this label to a file named sales.txt. 

- If the **Confidential \ All Employees** sensitivity label applies classification and protection: You could apply this label to a file named sales.pdf and a file named sales.txt. 还可以只对这些文件应用保护，而不应用分类。

## <a name="file-types-supported-for-protection"></a>支持保护的文件类型

The Azure Information Protection unified labeling client supports protection at two different levels, as described in the following table.

|保护类型|本机|常规|
|----------------------|----------|-----------|
|描述|对于文本、图像、Microsoft Office（Word、Excel、PowerPoint）文件、pdf 文件和其他支持 Rights Management 服务的应用程序文件类型，本机保护提供了同时包括权限的加密和强制执行的强保护级别。|对于其他所有应用程序和文件类型，常规保护提供了一种保护级别，该保护级别既包括使用 .pfile 文件类型的文件封装，又包括用于验证用户是否有权打开该文件的身份验证。|
|Protection|通过以下方式强制执行文件保护：<br /><br />- 必须在通过电子邮件接收文件的用户或通过文件被授予访问权限或共享权限的用户成功通过身份验证之后，才能呈现受保护的内容。<br /><br />- 此外，无论是使用 Azure 信息保护查看器（适用于受保护的文本和图像文件）还是使用关联的应用程序（适用于其他所有受支持的文件类型）呈现内容时，都会强制执行内容所有者在文件处于受保护状态时所设置的使用权限和策略。|通过以下方式强制执行文件保护：<br /><br />- 必须在经授权可打开文件的人员以及被授予访问权限的人员成功通过身份验证之后才能呈现受保护的内容。 如果授权失败，则文件不会打开。<br /><br />- 将显示由内容所有者设置的使用权限和策略，以向授权用户通知预期使用策略。<br /><br />- 将对已授权的用户打开和访问文件的操作执行审核日志记录。 但不强制执行使用权限。|
|文件类型默认值|这是以下文件类型的默认保护级别：<br /><br />- 文本和图像文件<br /><br />- Microsoft Office（Word、Excel、PowerPoint）文件<br /><br />- 可移植文档格式 (.pdf)<br /><br />有关详细信息，请参阅以下部分：[支持分类和保护的文件类型](#supported-file-types-for-classification-and-protection)。|这是针对不受本机保护支持的其他所有文件类型（例如 .vsdx、.rtf 等）的默认保护。|

You cannot change the default protection level that the Azure Information Protection unified labeling client or the scanner applies. However, you can change which file types are protected. For more information, see [Change which file types to protect](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

The protection can be applied automatically when a user selects a sensitivity label that an administrator has configured, or users can specify their own custom protection settings by using [permission levels](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>支持保护的文件大小

There are maximum file sizes that the Azure Information Protection unified labeling client supports for protection.

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

The following table lists a subset of file types that support native protection by the Azure Information Protection unified labeling client, and that can also be classified. 

这些文件类型单独进行标识，因为它们受到本机保护时，原始文件扩展名将更改，这些文件将变为只读。 请注意，以常规形式保护文件时，原始文件扩展名将始终更改为 .pfile。

> [!WARNING]
> 如果拥有可根据文件扩展名进行检查并采取操作的防火墙、Web 代理或者安全软件，你可能需要重新配置这些网络设备和软件以支持这些新的文件扩展名。

|原始文件扩展名|受保护的文件扩展名|
|--------------------------------|-------------------------------------|
|。txt|.ptxt|
|。xml|.pxml|
|。jpg|.pjpg|
|。jpeg|。pjpeg|
|。png|。ppng|
|.tif|.ptif|
|。tiff|.ptiff|
|。bmp|.pbmp|
|。gif|。pgif|
|.jpe|。pjpe|
|.jfif|.pjfif|
|。jt|.pjt|

The next table lists the remaining file types that support native protection by the Azure Information Protection unified labeling client, and that can also be classified. 会将它们识别为用于 Microsoft Office 应用的文件类型。 这些文件类型的受支持文件格式是以下 Office 程序的 97-2003 文件格式和 Office Open XML 格式：Word、Excel 和 PowerPoint。

对于这些文件，在文件受 Rights Management 服务保护后，文件扩展名仍保持不变。

|Office 支持的文件类型|Office 支持的文件类型|
|----------------------------------|----------------------------------|
|。doc<br /><br />。docm<br /><br />。docx<br /><br />。dot<br /><br />。dotm<br /><br />。dotx<br /><br />。potm<br /><br />。potx<br /><br />。pps<br /><br />。ppsm<br /><br />。ppsx<br /><br />。ppt<br /><br />。pptm<br /><br />。pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />。xla<br /><br />。xlam<br /><br />。xls<br /><br />。xlsb<br /><br />。xlt<br /><br />。xlsm<br /><br />。xlsx<br /><br />。xltm<br /><br />。xltx<br /><br />。xps|


## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>从分类和保护中排除的文件类型

为了帮助阻止用户更改对计算机操作至关重要的文件，某些文件类型和文件夹会自动从分类和保护中排除。 If users try to classify or protect these files by using the Azure Information Protection unified labeling client, they see a message that they are excluded.

- **排除的文件类型**：.lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、.msp、.msi、.pdb、.jar
    
    > [!NOTE]
    > Unlike the classic client, .msg files are not excluded. Currently, there is a known issue with .msg files that are classified and protected as ".msg.pfile" and you cannot open these files. For these files, remove the label to open the file.

- **排除的文件夹**： 
    - Windows
    - Program Files（\Program Files 和 \Program Files (x86)）
    - \ProgramData 
    - \AppData（适用于所有用户）

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Azure 信息保护扫描程序从分类和保护中排除的文件类型

By default, the scanner also excludes the same file types as the Azure Information Protection unified labeling client with the following exceptions:

- .msg, .rtf, and .rar, are also excluded

可更改扫描程序检查文件时包含或排除的文件类型：

- 通过[使用 Azure 门户](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal)，在扫描程序配置文件中配置“要扫描的文件类型”。
    
    > [!NOTE]
    > Because of the known issue for .msg files detailed in the previous section, we recommend you keep .msg files as excluded.
    > 
    > 如果在扫描时包含 .rtf 文件，请仔细监视扫描程序。 扫描程序无法成功检查某些 .rtf 文件，对于这些文件，未完成检查，必须重启服务。 

默认情况下，扫描程序仅保护 Office 文件类型，以及 PDF 文件（使用 ISO PDF 加密标准进行保护时）。 To change this behavior for the scanner, use the PowerShell advanced setting, **PFileSupportedExtensions**. For more information, see [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.

### <a name="files-that-cannot-be-protected-by-default"></a>默认不受保护的文件

Any file that is password-protected cannot be natively protected by the Azure Information Protection unified labeling client unless the file is currently open in the application that applies the protection. 最常看到的是受密码保护的 PDF 文件，但 Office 应用等其他应用程序也提供此功能。

### <a name="limitations-for-container-files-such-as-zip-files"></a>容器文件（如 .zip 文件）的限制

容器文件是包括其他文件的文件，典型示例是包括压缩文件的 .zip 文件。 其他示例包括 .rar、.7z、.msg 文件和包含附件的 PDF 文档。

可对这些容器文件进行分类和保护，但分类和保护不会应用到容器内每个文件。

如果容器文件包括已分类和受保护的文件，必须先提取这些文件，以更改其分类或保护设置。

Azure 信息保护查看器无法打开受保护的 PDF 文档中的附件。 在这种情况下，在查看器中打开文档时，附件不可见。

## <a name="file-types-supported-for-inspection"></a>支持检查的文件类型

Without any additional configuration, the Azure Information Protection unified labeling client uses Windows IFilter to inspect the contents of documents. Windows Search 使用 Windows IFilter 来编制索引。 As a result, the following file types can be inspected when you use the [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell command.

|应用程序类型|文件类型|
|--------------------------------|-------------------------------------|
|Word|.doc; docx; .docm; .dot; .dotm; .dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|PDF |。pdf|
|文本|.txt; .xml; .csv|

通过进行额外配置，还可以检查其他文件类型。 例如，可以[注册自定义文件扩展名，使用现有 Windows 筛选器处理程序处理文本文件](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters)，还可以安装软件供应商提供的其他筛选器。

若要检查安装了哪些筛选器，请参阅 Windows Search 开发人员指南中的[查找给定文件扩展名的筛选器处理程序](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension)一节。

以下各节提供了检查 .zip 文件和 .tiff 文件的配置说明。

### <a name="to-inspect-zip-files"></a>检查 .zip 文件

请按照以下说明操作，使用 Azure 信息保护扫描程序和 [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell 命令检查 .zip 文件：

1. 对于运行扫描程序或 PowerShell 会话的计算机，请安装 [Office 2010 Filter Pack SP2](https://support.microsoft.com/en-us/help/2687447/description-of-office-2010-filter-pack-sp2)。

2. For the scanner: After finding sensitive information, if the .zip file should be classified and protected with a label, specify the .zip file name extension with the PowerShell advanced setting, **PFileSupportedExtensions**, as described in [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.


执行这些步骤后的示例方案： 

名为“accounts.zip”的文件包含带有信用卡号的 Excel 电子表格。 You have a sensitivity label named **Confidential \ Finance**, which is configured to discover credit card numbers and automatically apply the label with protection that restricts access to the Finance group. 

After inspecting the file, the unified labeling client from your PowerShell session classifies this file as **Confidential \ Finance**, applies generic protection to the file so that only members of the Finance groups can unzip it, and renames the file **accounts.zip.pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>使用 OCR 检查 .tiff 文件

The [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell command can use optical character recognition (OCR) to inspect TIFF images with a .tiff file name extension when you install the Windows TIFF IFilter feature, and then configure [Windows TIFF IFilter Settings](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29) on the computer running the PowerShell session.

For the scanner: After finding sensitive information, if the .tiff file should be classified and protected with a label, specify this file name extension with the PowerShell advanced setting, **PFileSupportedExtensions**, as described in [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.

## <a name="next-steps"></a>后续步骤
Now that you've identified the file types supported by the Azure Information Protection unified labeling client, see the following resources for additional information that you might need to support this client:

- [自定义](clientv2-admin-guide-customizations.md)

- [客户端文件和使用情况日志记录](clientv2-admin-guide-files-and-logging.md)

- [PowerShell 命令](clientv2-admin-guide-powershell.md)

