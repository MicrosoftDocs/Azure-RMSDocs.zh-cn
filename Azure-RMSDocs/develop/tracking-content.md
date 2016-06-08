---
# required metadata

title: 跟踪内容 | Azure RMS
description: 实现文档跟踪的基本指导
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 此 SDK 内容不是最新的。 在短时间内，请在 MSDN 上找到[最新版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)的文档。 **
# 跟踪内容

本主题涵盖了用于实现跟踪受 Rights Management Services SDK 2.1 保护内容的文档的基本指南。

文档跟踪是 Rights Management 系统的一个功能。 通过在文档保护过程中添加特定的元数据，可以使用提供多个跟踪选项的跟踪服务门户来注册文档。

使用此 API 添加/更新具有文档跟踪元数据的内容许可证。

-   [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
-   [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

    我们期望你能设置所有元数据属性。 就是以下这些按类型列出的属性。

    有关详细信息，请参阅[**许可证元数据属性类型**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)。

    -   **IPC\_MD\_CONTENT\_PATH**

        用此标识跟踪的文档。 如果完整的路径不可用，则只需提供文件名。

    -   **IPC\_MD\_CONTENT\_NAME**

        用此标识跟踪的文档名称。

    -   **IPC\_MD\_NOTIFICATION\_TYPE**

        用于指定发送通知的时间。 有关详细信息，请参阅[**通知类型**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)。

    -   **IPC\_MD\_NOTIFICATION\_PREFERENCE**

        用于指示通知的类型。 有关详细信息，请参阅[**通知参考**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)。

    -   **IPC\_MD\_DATE\_MODIFIED**

        我们建议在每次用户单击“保存”时设置该日期。

    -   **IPC\_MD\_DATE\_CREATED**

        文件的发放日期。

-   [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

使用其中一个合适的 API 将元数据添加到文件或流中。

-   [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
-   [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

最后，使用此 API 注册具有跟踪系统的跟踪文档。

-   [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

以下是代码段，显示了设置文档跟踪元数据的示例和对跟踪系统中注册的调用。



    HRESULT hr = S_OK;
    LPCWSTR wszOutputFile = NULL;
    wstring wszWorkingFile;
    IPC_LICENSE_METADATA md = {0};

    md.cbSize = sizeof(IPC_LICENSE_METADATA);
    md.dwNotificationType = IPCD_CT_NOTIFICATION_TYPE_ENABLED;
    md.dwNotificationPreference = IPCD_CT_NOTIFICATION_PREF_DIGEST;
    //file origination date, current time for this example
    md.ftDateCreated = GetCurrentTime();
    md.ftDateModified = GetCurrentTime();

    LOGSTATUS_EX(L&quot;Encrypt file with official template...&quot;);

    hr =IpcfEncryptFileWithMetadata(  wszWorkingFile.c_str(),
                                       m_wszTestTemplateID.c_str(),
                                       IPCF_EF_TEMPLATE_ID,
                                       0,
                                       NULL,
                                       NULL,
                                       &amp;md,
                                       &amp;wszOutputFile);

    /* This will contain the serialized license */
    PIPC_BUFFER pSerializedLicense;

    /* the context to use for the call */
    PCIPC_PROMPT_CTX pContext;

    wstring wstrContentName(“MyDocument.txt”);
    bool sendLicenseRegistrationNotificationEmail = FALSE;

    hr = IpcRegisterLicense( pSerializedLicense,
                              0,
                              pContext,
                              wstrContentName.c_str(),
                              sendLicenseRegistrationNotificationEmail);


## 相关主题


* [**许可证元数据属性类型**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)
* [**通知参考**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [**通知类型**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)
* [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)
 

 


<!--HONumber=Jun16_HO1-->


