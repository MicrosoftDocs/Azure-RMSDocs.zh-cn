---
title: "如何发现用户是否已注册个人 RMS | Azure RMS"
description: "作为管理员，可以使用本文中所描述的任何一种方法或多种方法的组合来确定用户是否已注册个人 RMS。"
author: cabailey
manager: mbaldwin
ms.date: 09/01/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79d098e47cdfe608bc62ed385a5c8236fb7c6d3c
ms.openlocfilehash: 6a8a6ac7aae7c8e370af47e1d39a9f69acc1e12c


---


# 如何发现你的用户注册了个人 RMS？

>*适用于：Azure Rights Management*

作为管理员，你如何知道用户是否注册了个人 RMS？ 你可以使用以下任意一种方法，或者结合使用多种方法：

-   询问用户如何保护高度机密文件，特别是在与组织外部人员协作时。

-   如果你拥有组织的 Azure 订阅，请使用 [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) cmdlet 查看 **RIGHTSMANAGEMENT_ADHOC** 是否返回为订阅之一。 如果是，这是授予该组织的个人订阅 RMS，提供有可供用户使用自助服务注册过程的活动单元池。

-   使用 System Center Configuration Manager 等系统管理解决方案来清点已安装软件和在用软件。 Rights Management 共享应用程序是通过使用 **ipviewer.exe** 程序运行的，你可以免费 [下载和安装该应用程序](http://go.microsoft.com/fwlink/?LinkId=303970) ，以了解有关此应用程序的其他特征，然后将其用于软件清单。

-   请注意权限管理共享应用程序创建的文件扩展名。 .pfile 和 .ppdf 文件扩展名是最明显的示例，但是也有一些其他文件在原本就受 Rights Management 保护时会更改其文件扩展名。 有关详细信息，请参阅[Rights Management 共享应用程序管理员指南](http://technet.microsoft.com/library/dn339003.aspx)中的[支持的文件类型和文件扩展名](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)部分。




<!--HONumber=Sep16_HO1-->


