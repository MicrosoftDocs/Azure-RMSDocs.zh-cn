---
title: RMS 共享应用的技术概述 - AIP
description: 面向负责部署适用于 Windows 的 RMS 共享应用程序的企业网络管理员提供的技术详细信息。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/02/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f7b13fa4-4f8e-489a-ba46-713d7a79f901
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c4f37d2c3e7a90171662d91a4f78d61b629dd650
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
ms.locfileid: "30207472"
---
# <a name="technical-overview-and-protection-details-for-the-microsoft-rights-management-sharing-application"></a>Microsoft Rights Management 共享应用程序的技术概览和保护详细信息

>适用于：Active Directory Rights Management Services、[Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、带 SP1 的 Windows 7、Windows 8、Windows 8.1


Microsoft Rights Management 共享应用程序是一个可选且可下载的适用于 Microsoft Windows 和其他平台的应用程序，它提供以下功能：

-   单个文件保护、多个文件的批量保护以及对某个选定文件夹内所有文件的保护。

-   完全支持对任意类型文件的保护，并提供一个内置的查看器用于查看常用文本文件和图像文件类型。

-   对不支持 RMS 保护的文件的常规保护。

-   与使用 Office 信息权限管理 (IRM) 保护的文件的完全互操作性。

-   与通过文件分类基础结构（FCI）和支持的 PDF 创作工具保护的 PDF 文件的完全互操作性。

Microsoft Rights Management 共享应用程序使用 [AD RMS 客户端 2.1 运行时](http://www.microsoft.com/download/details.aspx?id=38396)。 通过使用 AD RMS 2.1 的功能，Microsoft Rights Management 共享应用程序为最终用户提供了简单的保护和使用体验。

借助 2013 年 10 月版的 RMS，可以使用 Office 2010 本机保护文档，还可以将这些文档发送给其他公司的用户，这样他们便可以通过使用 Azure 信息保护中的 Azure Rights Management 服务使用这些文档。 此外，在此版本中，如果在加密模式 2 中使用 AD RMS，则可以使用面向个人的 RMS，并可以使用其他公司中使用 Azure Rights Management 服务的用户提供的内容。 有关加密模式 2 的详细信息，请参阅 [AD RMS 加密模式](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx)。

有关部署信息，请参阅[自动部署 Microsoft Rights Management 共享应用程序](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)

## <a name="levels-of-protection--native-and-generic"></a>保护级别 – 本机和常规
Microsoft Rights Management 共享应用程序支持两个不同级别的保护，如下表中所述。

|保护类型|本机|泛型|
|----------------------|----------|-----------|
|描述|对于文本、图像、Microsoft Office（Word、Excel、PowerPoint）文件、pdf 文件和其他支持 Rights Management 服务的应用程序文件类型，本机保护提供了同时包括权限的加密和强制执行的强保护级别。|对于其他所有应用程序和文件类型，常规保护提供了一种保护级别，该保护级别既包括使用 .pfile 文件类型的文件封装，又包括用于验证用户是否有权打开该文件的身份验证。|
|保护|对文件进行完全加密，并采用以下方式强制执行保护：<br /><br />- 必须在通过电子邮件接收文件的用户或通过文件被授予访问权限或共享权限的用户成功通过身份验证之后，才能呈现受保护的内容。<br /><br />- 此外，无论是使用 IP 查看器（适用于受保护的文本和图像文件）还是关联的应用程序（适用于其他所有受支持的文件类型）呈现内容，都会完全执行内容所有者在文件处于受保护状态时所设置的使用权限和策略。|通过以下方式强制执行文件保护：<br /><br />- 必须在经授权可打开文件的用户或被授予访问权限的用户成功通过身份验证之后，才能呈现受保护的内容。 如果授权失败，则文件不会打开。<br /><br />- 将显示由内容所有者设置的使用权限和策略，以向授权用户通知预期使用策略。<br /><br />- 将出现授权用户打开和访问文件的审核日志记录，但是，不支持的应用程序不强制执行任何使用权限。|
|文件类型默认值|这是以下文件类型的默认保护级别：<br /><br />- 文本和图像文件<br /><br />- Microsoft Office（Word、Excel、PowerPoint）文件<br /><br />- 可移植文档格式 (.pdf)<br /><br />有关详细信息，请参阅以下部分：[支持的文件类型和文件扩展名](#supported-file-types-and-file-name-extensions)。|这是针对不受完整保护支持的其他所有文件类型（例如 .vsdx、.rtf 等）的默认保护。|
可以更改 RMS 共享应用程序所应用的默认保护级别。 可以将默认级别从本机更改为常规，从常规更改为本机，甚至可以禁止 RMS 共享应用程序应用保护。 有关详细信息，请参阅本文中的[更改文件的默认保护级别](#changing-the-default-protection-level-of-files)部分。

## <a name="supported-file-types-and-file-name-extensions"></a>支持的文件类型和文件扩展名
下表列出了本身受 Microsoft Rights Management 共享应用程序支持的文件类型。 对于这些文件类型，原始文件扩展名将在应用本机保护时发生变化，并且这些文件将变为只读形式。

此外，当 RMS 共享应用程序通过共享从本机保护受用户保护的 Word、Excel 或 PowerPoint 文件时，此操作将自动创建另一个文件，该文件是与原始文件同名的副本，但其文件扩展名¹为 **.ppdf**。 此版本的文件可确保安装 RMS 共享应用程序的接收方始终可以打开已应用本机保护的文件。

对于以常规形式进行保护的文件，原始文件扩展名将始终更改为 .pfile。

> [!WARNING]
> 如果你拥有可根据文件扩展名检查并采取操作的防火墙、Web 代理或者安全软件，你可能需要重新配置它们以支持这些新的文件扩展名。

|原始文件扩展名|受 RMS 保护的文件扩展名|
|--------------------------------|-------------------------------------|
|.txt|。ptxt|
|。xml|.pxml|
|。jpg|.pjpg|
|。jpeg|.pjeg|
|。pdf|。ppdf|
|。png|。ppng|
|.tif|.ptif|
|。tiff|.ptiff|
|。bmp|。pbmp|
|.gif|。pgif|
|。jpe|。pjpe|
|。jfif|。pjfif|
|。jt|.pjt|
¹ 由 Foxit 提供技术支持的 PDF Rendering。 Foxit Corporation 版权所有 © 2003–2014。

下表列出了 Microsoft Rights Management 共享应用程序本身在 Microsoft Office 2016、Office 2013 和 Office 2010 中支持的文件类型。 对于这些文件，在文件受 Rights Management 服务保护后，文件扩展名仍保持不变。

|Office 支持的文件类型|Office 支持的文件类型|
|----------------------------------|----------------------------------|
|。doc<br /><br />。docm<br /><br />。docx<br /><br />。dot<br /><br />。dotm<br /><br />。dotx<br /><br />。potm<br /><br />。potx<br /><br />。pps<br /><br />。ppsm<br /><br />。ppsx<br /><br />。ppt<br /><br />。pptm|。pptx<br /><br />。thmx<br /><br />。xla<br /><br />。xlam<br /><br />。xls<br /><br />。xlsb<br /><br />。xlt<br /><br />。xlsm<br /><br />。xlsx<br /><br />。xltm<br /><br />。xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>更改文件的默认保护级别
你可以通过编辑注册表来更改 RMS 共享应用程序保护文件的方式。 例如，你可以强制使支持本机保护的文件由 RMS 共享应用程序进行常规保护。

可能要执行此操作的原因是：

-   为了确保所有用户都能从其移动设备打开该文件。

-   为了确保所有用户都可以在没有支持本机保护的应用程序的情况下打开该文件。

-   为了适应根据文件扩展名对文件采取操作的安全系统，可将其重新配置为适应 .pfile 文件扩展名，但无法将其重新配置为适应已应用本机保护的多个文件扩展名。

同样，你也可以强制使 RMS 共享应用程序将本机保护应用到默认已应用常规保护的文件。 这在你具有支持 RMS API 的应用程序（例如，由内部开发人员编写的业务线应用程序或从独立软件供应商 (ISV) 处购买的应用程序）时可能正合适。

也可以强制使 RMS 共享应用程序阻止文件保护（而不是应用本机保护或常规保护）。 例如，如果你具有一个必须能够打开特定文件才能处理其内容的自动应用程序或服务，这可能是必需的。 当你阻止保护某一文件类型时，用户无法使用 RMS 共享应用程序保护具有该文件类型的文件。 他们将在尝试保护此类文件时看到一条消息，提示管理员已阻止保护，并且他们必须取消保护该文件的操作。

若要将 RMS 共享应用程序配置为将常规保护应用于默认已应用本机保护的所有文件，请对注册表进行以下编辑。 请注意，如果不存在 RmsSharingApp 或 FileProtection 项，必须手动创建它们。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection**：创建名为 * 的新项。

    此设置表示文件可具有任意文件扩展名。

2.  在新添加的项 HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\\\* 中，创建一个名为 **Encryption**、数据值为 **Pfile** 的新字符串值 (REG_SZ)。

    此设置会导致 RMS 共享应用程序应用常规保护。

这两个设置会导致 RMS 共享应用程序将常规保护应用于具有某一文件扩展名的所有文件。 如果这是你的目标，则无需进行任何进一步的配置。 但是，你可以为特定文件类型定义例外，以便它们仍受本机保护。 为此，你必须针对每个文件类型对注册表执行三个额外的编辑操作：

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection**：添加一个具有该文件扩展名的新项（不带前面的句点）。

    例如，对于文件扩展名为 .docx 的文件，创建一个名为 **DOCX**的项。

2.  在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**）中，创建一个名为 **AllowPFILEEncryption**、值为 **0** 的新 DWORD 值。

3.  在新添加的文件类型项（例如 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**）中，创建一个名为 **Encryption**、值为 **Native** 的新字符串值。

应用这些设置后，所有文件均受常规保护，但文件扩展名为 .docx 的文件除外，因为它们本身受 RMS 共享应用程序保护。

对于要将其定义为例外的其他文件类型重复这三个步骤，因为它们支持本机保护，而你不希望它们由 RMS 共享应用程序进行常规保护。

通过更改支持以下值的 **Encryption** 字符串的值，你可以在其他情况下进行类似的注册表编辑：

-   **Pfile**:一般性保护

-   **Native**：本机保护

-   **Off**：阻止保护

## <a name="see-also"></a>另请参阅
[权限管理共享应用程序用户指南](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
