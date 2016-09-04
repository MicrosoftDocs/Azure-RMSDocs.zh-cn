---
title: "如何启用文档跟踪和撤销 | Azure RMS"
description: "实现文档跟踪的基本指导"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experimental: true
experiment_id: priyamo-test-20160729
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 156ffcc021fee129557d485cb80bf9c3fcb8950b


---

# 跟踪内容

# 操作说明：启用文档跟踪和撤销

本主题涵盖实现文档内容跟踪的基本指导，并提供用于元数据更新和为应用创建**“跟踪使用情况”按钮**的示例代码。

## 实现文档跟踪的步骤

步骤 1 和步骤 2 可允许跟踪文档。 第 3 步可允许应用用户访问文档跟踪站点，以便跟踪和撤销受保护的文档。

1. 添加文档跟踪元数据
2. 向 RMS 服务注册文档
3. 向应用添加“跟踪使用情况”按钮

这些步骤的实现详细信息如下。

## 1.添加文档跟踪元数据

文档跟踪是 Rights Management 系统的一个功能。 通过在文档保护过程中添加特定的元数据，可以使用提供多个跟踪选项的跟踪服务门户来注册文档。

使用此 API 添加/更新具有文档跟踪元数据的内容许可证。


在操作上，只有 **内容名称** 和 **通知类型** 属性对于文档跟踪是必需的。


- [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
- [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

  我们期望你能设置所有元数据属性。 就是以下这些按类型列出的属性。

  有关详细信息，请参阅[许可证元数据属性类型](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types)。

  - **IPC_MD_CONTENT_PATH**

    用于标识跟踪的文档。 如果完整的路径不可用，则只需提供文件名。

  - **IPC_MD_CONTENT_NAME**

    用于标识跟踪的文档名称。

  - **IPC_MD_NOTIFICATION_TYPE**

    用于指定发送通知的时间。 有关详细信息，请参阅“通知类型”。

  - **IPC_MD_NOTIFICATION_PREFERENCE**

    用于指示通知的类型。 有关详细信息，请参阅通知偏好设置。

  - **IPC_MD_DATE_MODIFIED**

    我们建议在每次用户单击“保存”时设置此日期。

  - **IPC_MD_DATE_CREATED**

    用于设置文件的发放日期

- [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

使用其中一个合适的 API 将元数据添加到文件或流中。

- [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
- [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

最后，使用此 API 注册具有跟踪系统的跟踪文档。

- [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)


## 2.向 RMS 服务注册文档

以下是代码段，显示了设置文档跟踪元数据的示例和对跟踪系统中注册的调用。

      C++
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

      LOGSTATUS_EX(L"Encrypt file with official template...");

      hr =IpcfEncryptFileWithMetadata( wszWorkingFile.c_str(),
                               m_wszTestTemplateID.c_str(),
                               IPCF_EF_TEMPLATE_ID,
                               0,
                               NULL,
                               NULL,
                               &md,
                               &wszOutputFile);

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

## 向应用添加**跟踪使用情况**按钮

向应用添加**跟踪使用情况** UI 项非常简单，使用以下任一 URL 格式即可：

- 使用内容 ID
  - 如果许可证已序列化，请使用 [IpcGetLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetlicenseproperty) 或 [IpcGetSerializedLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetserializedlicenseproperty) 获取内容 ID，并使用许可证属性 **IPC_LI_CONTENT_ID**。 有关详细信息，请参阅[许可证属性类型](/rights-management/sdk/2.1/api/win/constants#msipc_license_property_types)。
  - 对于 **ContentId** 和 **Issuer** 元数据，使用以下格式： `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    示例 - `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- 如果你无权访问该元数据（即检查文档的不受保护版本时），可以下列格式使用 **Content_Name**： `https://track.azurerms.com/#/?q={ContentName}`

  示例 - https://track.azurerms.com/#/?q=Secret!.txt

客户端只需要使用适当的 URL 打开浏览器。 RMS 文档跟踪门户将处理身份验证和任何所需重定向。

## 相关主题

* [许可证元数据属性类型](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types)
* [通知参考](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [通知类型](/rights-management/sdk/2.1/api/win/constants#msipc_notification_type)
* [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

 



<!--HONumber=Aug16_HO4-->


