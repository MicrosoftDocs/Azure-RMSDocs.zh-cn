---
# required metadata

title: Azure RMS 要求&#58;支持 Azure Rights Management 的本地服务器 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Azure RMS 要求：支持 Azure RMS 的本地服务器
当你使用 Azure RMS 连接器时，它将充当本地服务器和 Azure RMS 之间的通信接口（一种中继），让 Azure RMS 能够支持以下本地服务器产品。 此外，这种配置要求你配置 Active Directory 林和 Azure Active Directory 之间的目录同步。

-   **Exchange Server**：

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**：

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **运行 Windows Server 和使用文件分类基础结构 (FCI) 的文件服务器**：

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > 由于运行 Windows Server 2008 R2 的文件服务器未使用内置文件管理任务操作来应用 RMS 保护，在这种情况下，你不能使用 RMS 连接器。 但是，如果你配置自定义文件管理任务以运行可通过使用 Azure RMS 来保护文件的可执行文件或脚本，则可以在这些操作系统上使用文件分类基础结构和 Azure RMS。 例如，使用 [RMS 保护 cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 的 Windows PowerShell 脚本。
    > 
    > 你也可以在运行更高版本的 Windows Server 的服务器上使用这些 cmdlet，好处是这些 cmdlet 可以保护所有文件类型。 RMS 连接器仅保护 Office 文件。 有关操作说明，请参阅[使用 Windows Server 文件分类基础结构 &#40;FCI&#41; 的 RMS 保护](../rms-client/configure-fci.md)。

Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 支持 RMS 连接器。

有关如何为这些本地服务器配置 RMS 连接器的详细信息，请参阅[部署 Azure Rights Management 连接器](../deploy-use/deploy-rms-connector.md)。

## 后续步骤
若要查看其他要求，请参阅 [Azure Rights Management 的要求](requirements-azure-rms.md)。


<!--HONumber=Apr16_HO3-->


