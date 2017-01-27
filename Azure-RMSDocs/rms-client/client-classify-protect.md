---
title: "使用 Azure 信息保护对文件或电子邮件进行分类和保护 | Azure 信息保护"
description: "说明如何对文档和电子邮件进行分类和保护。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 171a47f9c22dec24f72f8f21392d6577efd807a5
ms.openlocfilehash: d050629999c3a886eb8d422f4f38c22d586e0824


---

# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>使用 Azure 信息保护对文件或电子邮件进行分类和保护

>适用于：Active Directory Rights Management Services、Azure 信息保护、Windows 10、Windows 8.1、Windows 8、具有 SP1 的 Windows 7

**[此版本的客户端为预览版，随时可能更改。]**

在 Office 桌面应用中（**Word**、**Excel**、**PowerPoint**、**Outlook**）创建和编辑文档和电子邮件时对其进行分类和保护最为简单。 

但是，你也可以使用**文件资源管理器**对文件进行分类和保护，此方法支持其他文件类型，并且是一次性分类和保护多个文件的便捷方式。

## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>使用 Office 应用对文档和电子邮件进行分类和保护

使用 Azure 信息保护栏并选择其中一个已为你配置的标签。 例如：

![Azure 信息保护栏示例](../media/info-protect-bar-not-set-callout.png)


## <a name="using-file-explorer-to-classify-and-protect-files"></a>使用文件资源管理器对文件进行分类和保护

使用文件资源管理器时，可快速对单个文件、多个文件或文件夹进行分类和保护。 

选择文件夹时，将自动为你设置的分类和保护选项选择该文件夹及其所有子文件夹中的所有文件。 但是，在该文件夹或子文件夹中创建的新文件不会自动配置这些选项。

使用文件资源管理器对文件进行分类和保护时，你可能会注意到标签并不总是可用。 选择的文件不支持分类时，就会发生这种情况。 对于这些文件，只有在管理员已将标签配置为应用保护时，你才能选择标签。 或者，你可以指定自己的保护设置。 

有关文件资源管理器支持的文件类型列表，请参阅此页面上的[支持分类和保护的文件类型](#file-types-supported-for-classification-and-protection)部分。


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>使用文件资源管理器对文件进行分类和保护

1.  在文件资源管理器中，选择你的文件、多个文件或文件夹。 右键单击，然后选择“分类和保护(预览)”。 

2. 在“分类和保护 - Azure信息保护”对话框中，请像在 Office 应用程序中那样使用标签，这样可以按管理员定义的方式设置分类和保护。 如果无法选择标签（它不可用），则所选文件不支持分类，但你可以保护它。

3. 如果想要指定自己的保护设置，而不使用管理员可能已包含在所选标签中的保护设置，请选择“使用自定义权限保护”。
    
    指定的任何自定义权限将替换而不是补充管理员可能已为所选标签定义的保护设置。  

4. 如果已选择自定义权限选项，此时指定以下项：

    - **选择权限**：选择你希望用户在保护所选文件时具有的访问级别。
    
    - **选择用户**：指定应对文件具有选定权限的人员。 对于组织中的人员和组，可使用通讯簿进行搜索和选择。 对于另一组织中的人员，必须指定其完整的电子邮件地址。 请确保你使用的是业务电子邮件地址，因为当前不支持个人电子邮件地址。
        
    - **访问过期日期**：仅对具有时效性的文件选择此选项，以使指定的人员无法在指定日期后打开选定的一个文件或多个文件。 你仍可以打开原始文件，但在选定日期的午夜（当前时区）过后，指定的人员将无法打开该文件。

5. 单击“应用”，然后单击“关闭”。

根据你的选择，现已对所选择的一个或多个文件进行分类和保护。 在某些情况下（添加的保护更改了文件扩展名时），文件资源管理器中的原始文件将替换为具有 Azure 信息保护锁状图标的新文件。 例如：

![Azure 信息保护中具有锁状图标的受保护文件](../media/Pfile.png)

如果改变了有关分类和保护的想法，或稍后需要更改设置，仅需通过重复此过程进行新的设置。

指定的分类和保护会保留在文件中，即使你通过电子邮件发送文件或将其保存到其他位置也是如此。 如果已保护该文件，则可跟踪用户如何使用它，如果有必要，还可撤销对它的访问。 有关详细信息，请参阅[使用 Azure 信息保护时跟踪和撤销已保护的文档](client-track-revoke.md)。 

#### <a name="file-types-supported-for-classification-and-protection"></a>支持分类和保护的文件类型

以下文件类型仅支持分类。 其他文件类型在受保护时也支持分类。

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


[文件 API 配置](../develop/file-api-configuration.md)中记录的文件类型支持使用 Rights Management 服务进行保护。 选择管理员配置的标签时，可以自动应用此保护，也可以使用[权限级别](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels)指定自己的保护设置。 


## <a name="other-instructions"></a>其他说明
有关操作方法的说明，请参阅 Azure 信息保护用户指南中的以下部分：

-   [要执行什么操作？](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


