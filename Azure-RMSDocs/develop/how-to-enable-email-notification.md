---
title: "启用电子邮件通知 | Azure RMS"
description: "受保护的内容所有者通过电子邮件通知可以在其内容受到访问时收到通知。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5FB975EE-E4E5-4089-B8E1-CAFD5B9B34EC
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: dc7b6fe403a95eae50e81ca87e46e68d412535c7


---

# 操作说明：启用电子邮件通知

受保护的内容所有者通过电子邮件通知可以在其内容受到访问时收到通知。

若要针对给定许可证设置电子邮件通知，请使用 [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)，其中属性类型参数 *dwPropID* 为 [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)，并且应用程序数据字段格式化为 [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)。

    C++

    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {&quot;MS.Conetent.Name&quot;, 0, &quot;FinancialReport.docx&quot;};
    propertyValuePairs[1] = {&quot;MS.Notify.Enabled&quot;,0 , &quot;true&quot;};
    propertyValuePairs[2] = {&quot;MS.Notify.Culture&quot;,0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);
        

下表包含用于 RMS 电子邮件通知的应用程序数据字段、属性名称和值对。


|属性名称 | 数据类型 | 示例值 | 注意 |
|--------------|-----------|---------------|-------|
|MS.Content.Name|字符串|“FinancialReport.docx”|这是与受保护的内容关联的标识符。<br><br> 对于受保护的文件，此值应是文件的名称（不包含任何路径信息）。<br><br> 对于其他类型的内容（如电子邮件），这可能是电子邮件的主题，也可能为空。|
|MS.Notify.Enabled|字符串|“true”&#124;“false”|如果此值设置为“true”，则当有人尝试使用发布许可证来获取最终用户许可证时，会向发布许可证所有者发送通知电子邮件。|
|MS.Notify.Culture|字符串|“en-US”| **源：** System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>此值用于确定通知电子邮件的本地化语言以及应在电子邮件中使用的日期/时间和数字格式设置。<br><br>其设置应基于用于创建发布许可证的计算机的用户设置，或基于发布许可证的所有者的首选区域性。|
|MS.Notify.TZID|字符串|“太平洋标准时间”|**源：** TimeZoneInfo.Local.Id - Windows 时区 ID。<br><br>此值用于描述特定时区及其特征的 Microsoft Windows 操作系统时区标识符。|
|MS.Notify.TZO|字符串|“-480”|这是发布许可证所有者的时区相对于 UTC 时间在分钟方面的偏移。<br><br>如果提供了有效 TZID 值，则会使用它指定的时区偏移，而忽略此值。<br><br>此值很可能由基于非 Windows 的发布平台使用，这些平台无权访问 Windows 操作系统时区 ID 值的列表。<br><br>如果未提供 TZID 值，则此值用于计算通知消息的时间偏移，而 TZSN 用于（与时区值无关）指示时区的名称。 这会导致时区固定，不会在夏令时适用时针对夏令时进行更新。<br><br>例如：<br><br>如果 TXID 为空并且 TZ0 设置为“-420”，而 TZSN 设置为“太平洋标准时间”，则通知电子邮件中显示的所有值都会调整为“太平洋标准时间”，即使夏令时当前已不再生效也会显示为这样。<br><br>另一方面，如果随 TZSN 和 TZDN 一起提供了 TZID，则通知电子邮件中指定的时间会基于日期和时间应以夏令时模式还是标准模式来显示而进行调整和显示。|
|MS.Notify.TZSN|字符串|“太平洋标准时间”|**源：** TimeZoneInfo.Local.StandardName - 标准时区名称。<br><br>这应是时区标准时区名称的本地化名称。|
|MS.Notify.TZDN|字符串|“太平洋夏令时”|**源：** TimeZoneInfo.Local.DaylightName - 夏令时时区名称。<br><br>这应是时区夏令时名称的本地化名称。 如果时区不支持夏令时，则它可能与标准名称相同。|

## 相关主题

* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
* [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)
* [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)
 

 



<!--HONumber=Aug16_HO4-->


