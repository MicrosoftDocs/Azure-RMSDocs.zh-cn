---
title: 管理用于 Azure 信息保护的个人数据
description: 有关 Azure 信息保护所使用的个人数据的信息以及如何查看、导出和删除该数据的信息。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 99a51862-83e9-4a1e-873a-a84ae1465f07
ms.reviewer: aashishr
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d16e6e7f0667f9ac57bf772de272d23838b793e1
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "71966878"
---
# <a name="manage-personal-data-for-azure-information-protection"></a>管理用于 Azure 信息保护的个人数据

在配置和使用 Azure 信息保护时，Azure 信息保护服务会存储和使用电子邮件地址和 IP 地址。 可以在以下各项中找到此个人数据：

- Azure 信息保护策略

- 保护服务的模板

- 保护服务的超级用户和委派的管理员 

- 保护服务的管理日志

- 保护服务的使用日志

- 文档跟踪日志

- Azure 信息保护客户端和 RMS 客户端的使用情况日志 


[!INCLUDE [GDPR-related guidance](./includes/gdpr-intro-sentence.md)]


## <a name="viewing-personal-data-that-azure-information-protection-uses"></a>查看 Azure 信息保护使用的个人数据

使用 Azure 门户，管理员可为作用域内策略和标签配置中的保护设置指定电子邮件地址。 有关详细信息，请参阅[如何使用作用域内策略为特定用户配置 Azure 信息保护策略](configure-policy-scope.md)以及[如何为 Rights Management 保护配置标签](configure-policy-protection.md)。 

对于配置为从 Azure Rights Management 服务应用保护的标签，还可以通过使用[AIPService 模块](/powershell/module/aipservice)中的 PowerShell cmdlet 在保护模板中找到电子邮件地址。 此 PowerShell 模块还允许管理员按照电子邮件地址将用户指定为[超级用户](configure-super-users.md)，或 Azure Rights Management 服务的管理员。 

将 Azure 信息保护用于分类和保护文档和电子邮件时，可能会将电子邮件地址和用户的 IP 地址保存在日志文件中。


### <a name="protection-templates"></a>保护模板

运行[AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate) cmdlet 以获取保护模板列表。 可以使用模板 ID 获取特定模板的详细信息。 `RightsDefinitions` 对象显示个人数据，如果有的话。 

示例
```
PS C:\Users> Get-AipServiceTemplate -TemplateId fcdbbc36-1f48-48ca-887f-265ee1268f51 | select *


TemplateId              : fcdbbc36-1f48-48ca-887f-265ee1268f51
Names                   : {1033 -> Confidential}
Descriptions            : {1033 -> This data includes sensitive business information. Exposing this data to
                          unauthorized users may cause damage to the business. Examples for Confidential information
                          are employee information, individual customer projects or contracts and sales account data.}
Status                  : Archived
RightsDefinitions       : {admin@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT,
                          REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER,
                          AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@aip500.onmicrosoft.com -> VIEW,
                          VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT,
                          EDITRIGHTSDATA, OBJMODEL, OWNER, admin2@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT,
                          DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER}
ContentExpirationDate   : 1/1/0001 12:00:00 AM
ContentValidityDuration : 0
ContentExpirationOption : Never
LicenseValidityDuration : 7
ReadOnly                : False
LastModifiedTimeStamp   : 1/26/2018 6:17:00 PM
ScopedIdentities        : {}
EnableInLegacyApps      : False
LabelId                 :
```

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>保护服务的超级用户和委派的管理员

运行[AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser) cmdlet 和[aipservicerolebasedadministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator) cmdlet，以查看为哪些用户分配了 Azure 信息保护中的保护服务（azure Rights Management）的超级用户角色或全局管理员角色。 对于已分配了这些角色之一的用户，会显示其电子邮件地址。


### <a name="administration-logs-for-the-protection-service"></a>保护服务的管理日志

运行[AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) cmdlet，从 Azure 信息保护获取保护服务（azure Rights Management）的管理操作日志。 此日志包含电子邮件地址和 IP 地址形式的个人数据。 日志采用纯文本形式，下载它后，可以脱机搜索特定管理员的详细信息。

例如：
```
PS C:\Users> Get-AipServiceAdminLog -Path '.\Desktop\admin.log' -FromTime 4/1/2018 -ToTime 4/30/2018 -Verbose
The Rights Management administration log was successfully generated and can be found at .\Desktop\admin.log.
```

### <a name="usage-logs-for-the-protection-service"></a>保护服务的使用日志
运行[AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog) cmdlet，以检索使用 Azure 信息保护中的保护服务的最终用户操作的日志。 此日志可包含电子邮件地址和 IP 地址形式的个人数据。 日志采用纯文本形式，下载它后，可以脱机搜索特定管理员的详细信息。

例如：
```
PS C:\Users> Get-AipServiceUserLog -Path '.\Desktop\' -FromDate 4/1/2018 -ToDate 4/30/2018 -NumberOfThreads 10
Acquiring access to your user log…
Downloading the log for 2018-04-01.
Downloading the log for 2018-04-03.
Downloading the log for 2018-04-06.
Downloading the log for 2018-04-09.
Downloading the log for 2018-04-10.
Downloaded the log for 2018-04-01. The log is available at .\Desktop\rmslog-2018-04-01.log.
Downloaded the log for 2018-04-03. The log is available at .\Desktop\rmslog-2018-04-03.log.
Downloaded the log for 2018-04-06. The log is available at .\Desktop\rmslog-2018-04-06.log.
Downloaded the log for 2018-04-09. The log is available at .\Desktop\rmslog-2018-04-09.log.
Downloaded the log for 2018-04-10. The log is available at .\Desktop\rmslog-2018-04-10.log.
Downloading the log for 2018-04-12.
Downloading the log for 2018-04-13.
Downloading the log for 2018-04-14.
Downloading the log for 2018-04-16.
Downloading the log for 2018-04-18.
Downloaded the log for 2018-04-12. The log is available at .\Desktop\rmslog-2018-04-12.log.
Downloaded the log for 2018-04-13. The log is available at .\Desktop\rmslog-2018-04-13.log.
Downloaded the log for 2018-04-14. The log is available at .\Desktop\rmslog-2018-04-14.log.
Downloaded the log for 2018-04-16. The log is available at .\Desktop\rmslog-2018-04-16.log.
Downloaded the log for 2018-04-18. The log is available at .\Desktop\rmslog-2018-04-18.log.
Downloading the log for 2018-04-24.
Downloaded the log for 2018-04-24. The log is available at .\Desktop\rmslog-2018-04-24.log.
```   

### <a name="document-tracking-logs"></a>文档跟踪日志

运行[AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) cmdlet，以从文档跟踪站点检索有关特定用户的信息。 若要获取与文档日志关联的跟踪信息，请使用[AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog?view=azureipps) cmdlet。

例如：
```
PS C:\Users> Get-AipServiceDocumentLog -UserEmail "admin@aip500.onmicrosoft.com"


ContentId             : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer                : admin@aip500.onmicrosoft.com
Owner                 : admin@aip500.onmicrosoft.com
ContentName           :
CreatedTime           : 3/6/2018 10:24:00 PM
Recipients            : {
                        PrimaryEmail: johndoe@contoso.com
                        DisplayName: JOHNDOE@CONTOSO.COM
                        UserType: External,
                        PrimaryEmail: alice@contoso0110.onmicrosoft.com
                        DisplayName: ALICE@CONTOSO0110.ONMICROSOFT.COM
                        UserType: External
                        }
TemplateId            :
PolicyExpires         :
EULDuration           :
SendRegistrationEmail : True
NotificationInfo      : Enabled: False
                        DeniedOnly: False
                        Culture:
                        TimeZoneId:
                        TimeZoneOffset: 0
                        TimeZoneDaylightName:
                        TimeZoneStandardName:

RevocationInfo        : Revoked: False
                        RevokedTime:
                        RevokedBy:


PS C:\Users> Get-AipServiceTrackingLog -UserEmail "admin@aip500.onmicrosoft.com"

ContentId            : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer               : admin@aip500.onmicrosoft.com
RequestTime          : 3/6/2018 10:45:57 PM
RequesterType        : External
RequesterEmail       : johndoe@contoso.com
RequesterDisplayName : johndoe@contoso.com
RequesterLocation    : IP: 167.220.1.54
                       Country: US
                       City: redmond
                       Position: 47.6812453974602,-122.120736471666

Rights               : {VIEW,OBJMODEL}
Successful           : False
IsHiddenInfo         : False
```

没有按 ObjectID 进行任何搜索。 但是，你不受 `-UserEmail` 参数限制，并且你提供的电子邮件地址不需要成为你租户的一部分。 如果提供的电子邮件地址存储在文档跟踪日志中的任意位置，则在 cmdlet 输出中返回文档跟踪条目。

### <a name="usage-logs-for-the-azure-information-protection-clients-and-rms-client"></a>Azure 信息保护客户端和 RMS 客户端的使用情况日志

将标签和保护应用于文档和电子邮件时，电子邮件地址和 IP 地址可以存储在用户计算机以下位置的日志文件中：

- 对于 Azure 信息保护，统一标签客户端和 Azure 信息保护客户端：%localappdata%\Microsoft\MSIP\Logs

- 对于 RMS 客户端：%localappdata%\Microsoft\MSIPC\msip\Logs

此外，Azure 信息保护客户端将此个人数据记录到本地 Windows 事件日志“应用程序和服务日志” > “Azure 信息保护”。

Azure 信息保护客户端运行扫描程序时，会将个人数据保存到运行此扫描程序的 Windows Server 计算机上的 %localappdata%\Microsoft\MSIP\Scanner\Reports。

可使用以下配置，为 Azure 信息保护客户端和扫描程序禁用日志记录信息：

- 对于 Azure 信息保护客户端：创建将**LogLevel**配置为**Off**的[高级客户端设置](./rms-client/client-admin-guide-customizations.md#change-the-local-logging-level)。

- 对于 Azure 信息保护扫描程序：使用[set-aipscannerconfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) Cmdlet 将*eportlevel*参数设置为**Off**。

[!INCLUDE [GDPR-related guidance](./includes/gdpr-hybrid-note.md)]

## <a name="securing-and-controlling-access-to-personal-information"></a>保护和控制对个人信息的访问
只有[通过 Azure Active Directory 分配有以下管理员角色](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)之一的用户可以访问你在 Azure 门户中查看和指定的个人数据：
    
- **Azure 信息保护管理员**

- **合规性管理员**

- **相容性数据管理员**

- **安全管理员**

- **安全读取者**

- **全局管理员**

- **全局读取器**

使用 AIPService 模块（或旧模块，AADRM）查看和指定的个人数据仅可供已向其分配了**Azure 信息保护管理员**、**合规性管理员**、**符合性数据管理员**或 Azure Active Directory 的**全局管理员**角色，或者保护服务的全局管理员角色。

## <a name="updating-personal-data"></a>更新个人数据

可以为 Azure 信息保护策略中的作用域内策略和保护设置更新电子邮件地址。 有关详细信息，请参阅[如何使用作用域内策略为特定用户配置 Azure 信息保护策略](configure-policy-scope.md)以及[如何为 Rights Management 保护配置标签](configure-policy-protection.md)。 

对于保护设置，你可以使用[AIPService 模块](/powershell/module/aipservice)中的 PowerShell cmdlet 来更新相同的信息。

无法更新超级用户和委派管理员的电子邮件地址。 请删除指定的用户帐户，添加包含更新电子邮件地址的用户帐户。 

### <a name="protection-templates"></a>保护模板

运行[AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) cmdlet 以更新保护模板。 由于个人数据位于 `RightsDefinitions` 属性内，因此还需要使用[AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) cmdlet 创建具有更新信息的权限定义对象，并将权限定义对象与 `Set-AipServiceTemplateProperty` cmdlet 结合使用。

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>保护服务的超级用户和委派的管理员

需要更新超级用户的电子邮件地址时：

1. 使用[AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser)删除用户和旧电子邮件地址。

2. 使用[AipServiceSuperUser](/powershell/module/aipservice/Add-AipServiceSuperUser)添加用户和新的电子邮件地址。

需要更新委派管理员的电子邮件地址时：

1. 使用[AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator)删除用户和旧电子邮件地址。

2. 使用[AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Add-AipServiceRoleBasedAdministrator)添加用户和新的电子邮件地址。

## <a name="deleting-personal-data"></a>删除个人数据
可以删除 Azure 信息保护策略中作用域内策略和保护设置的电子邮件地址。 有关详细信息，请参阅[如何使用作用域内策略为特定用户配置 Azure 信息保护策略](configure-policy-scope.md)以及[如何为 Rights Management 保护配置标签](configure-policy-protection.md)。 

对于保护设置，你可以使用[AIPService 模块](/powershell/module/aipservice)中的 PowerShell cmdlet 删除相同的信息。

若要删除超级用户和委派的管理员的电子邮件地址，请使用[AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser) Cmdlet 和[AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator)删除这些用户。 

若要删除保护服务的文档跟踪日志、管理日志或使用情况日志中的个人数据，请使用以下部分引发 Microsoft 支持部门的请求。

若要删除客户端日志文件中的个人数据和存储在计算机上的扫描程序日志，请使用任何标准的 Windows 工具来删除这些文件或文件中的个人数据。 

### <a name="to-delete-personal-data-with-microsoft-support"></a>通过 Microsoft 支持部门删除个人数据

使用以下三个步骤来请求 Microsoft 删除文档跟踪日志、管理日志或保护服务的使用日志中的个人数据。 

步骤 1：启动删除请求
[与 Microsoft 支持部门联系](information-support.md#to-contact-microsoft-support)，以打开带有删除租户数据请求的 Azure 信息保护支持案例。 必须证明你是 Azure 信息保护租户的管理员，并且了解需要几天时间才能确认此过程。 提交请求时，你将需要提供其他信息，具体取决于需要被删除的数据。

- 若要删除管理日志，请提供结束日期。 将删除直到该结束日期的所有管理日志。
- 若要删除使用情况日志，请提供结束日期。 将删除直到该结束日期的所有使用情况日志。
- 若要删除文档跟踪日志，请提供 UserEmail。 将删除所有与 UserEmail 相关的文档跟踪信息。

删除此数据是一种永久性操作。 处理完删除请求后，就无法恢复数据。 建议管理员在提交删除请求之前导出所需数据。

步骤 2：等待验证 Microsoft 将验证删除一个或多个日志的请求是否合法。 此过程最多可能需要五个工作日。

步骤 3：获得删除确认 Microsoft 客户支持服务部门 (CSS) 将向你发送数据已删除的确认电子邮件。 

## <a name="exporting-personal-data"></a>导入个人数据
当你使用 AIPService 或 AADRM PowerShell cmdlet 时，可以将个人数据作为 PowerShell 对象提供给搜索和导出。 PowerShell 对象可转换为 JSON，并使用 `ConvertTo-Json` cmdlet 进行保存。

## <a name="restricting-the-use-of-personal-data-for-profiling-or-marketing-without-consent"></a>在未征得同意的情况下，限制将个人数据用于分析或市场营销
对于基于个人数据的分析或市场营销，Azure 信息保护遵循 Microsoft 的[隐私条款](https://privacy.microsoft.com/privacystatement)。

## <a name="auditing-and-reporting"></a>审核和报告
只有被分配了[管理员权限](#securing-and-controlling-access-to-personal-information)的用户才能使用 AIPSERVICE 或 ADDRM 模块来搜索和导出个人数据。 这些操作记录于可下载的管理日志中。

对于删除操作，支持请求充当 Microsoft 执行的操作的审核和报告跟踪。 删除后，删除的数据将不能用于搜索和导出，管理员可以使用 AIPService 模块中的 Get cmdlet 来验证此数据。
