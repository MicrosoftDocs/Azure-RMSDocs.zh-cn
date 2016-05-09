---
# required metadata

title: 如何&#58;使用文档跟踪 | Azure RMS
description: 文档跟踪功能需要对管理关联元数据以及向服务注册有一些简单了解。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d193afec-6dc5-477d-8e67-f820a97480ff

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 如何：使用文档跟踪

使用文档跟踪功能需要对管理关联元数据以及向服务注册有一些简单了解。

## 管理文档跟踪元数据

支持文档跟踪的每个操作系统都具有类似实现。 这包括一组表示元数据的属性、一个添加到用户策略创建方法的新参数以及一个用于向文档跟踪服务注册要跟踪的策略的方法。

在操作上，只有 **内容名称** 和 **通知类型** 属性对于文档跟踪是必需的。

用于为给定的一段内容设置文档跟踪的步骤序列是：

-   创建 **许可证元数据** 对象。

    有关详细信息，请参阅 [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) 或 [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc)。

-   设置 **内容名称** 和 **通知类型**。 这些是唯一的必需属性。

    有关详细信息，请参阅平台相应许可证元数据类（[**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) 或 [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc)）的属性访问方法。

-   按照策略类型；模板或临时

    -   对于基于模板的文档跟踪，创建 **用户策略** 对象（将许可证元数据作为参数进行传递）。

        有关详细信息，请参阅 [**UserPolicy.create**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_class_java) 和 [**MSUserPolicy.userPolicyWithTemplateDescriptor**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_templatedescriptor_property_objc)。

    -   对于基于临时的文档跟踪，对 **策略描述符** 对象设置 **许可证元数据** 属性。

        有关详细信息，请参阅 [**PolicyDescriptor.getLicenseMetadata**](https://stage.docs.microsoft.com/en-us/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java)、[**PolicyDescriptor.setLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_setlicensemetadata_java) 和 [**MSPolicyDescriptor.licenseMetadata**](/rights-management/sdk/4.2/api/iOS/mspolicydescriptor#msipcthin2_mspolicydescriptor_licensemetadata_property_objc)。

    **注意**  许可证元数据对象只能在针对给定用户策略设置文档跟踪的过程中直接访问。 创建用户策略对象之后，便无法访问关联许可证元数据，即更改许可证元数据的值会不起作用。

     

-   调用文档跟踪的平台注册方法。

    请参阅 [**MSUserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) 或 [**UserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc)。

 

 





<!--HONumber=Apr16_HO3-->


