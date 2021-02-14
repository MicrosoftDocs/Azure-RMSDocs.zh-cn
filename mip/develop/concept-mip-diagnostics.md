---
title: 概念-MIP SDK 诊断控件中的核心概念
description: 本文将帮助你了解如何选择退出诊断数据，以及在选择退出时仍发送哪些事件。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 10/01/2019
ms.author: tommos
ms.openlocfilehash: a0c8cd7d551f68242f67c8a3619fd0ff6fea64e9
ms.sourcegitcommit: 0f694bf6c7ea9c7709954bfb5dbd1c5f009b85a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2021
ms.locfileid: "100360716"
---
# <a name="microsoft-information-protection-sdk---diagnostic-configuration"></a>Microsoft 信息保护 SDK-诊断配置

## <a name="diagnostic-data"></a>诊断数据

默认情况下，Microsoft 信息保护 SDK 会将诊断数据发送给 Microsoft。 此数据可用于排查 SDK 安装基础上的 bug、质量和性能问题，我们在内部测试中可能无法捕获这些问题。 在用 SDK 实现应用程序时，如果需要，请务必让用户和管理员选择不发送诊断数据。

## <a name="diagnostic-configuration"></a>诊断配置

可以通过控制 MIP SDK 中的诊断选项 `DiagnosticConfiguration` 。 创建此类的实例，然后将 **isMinimalTelemetryEnabled** 设置为 true。 将 **DiagnosticConfiguration** 类的对象提供给用于创建 **MipContext** 的函数。

### <a name="minimum-diagnostic-events"></a>最小诊断事件

当诊断配置设置为最小值时，会将最小数据集发送给 Microsoft。 所有个人身份信息都从此信息中进行了清理。 此数据包括检测信号信息，以了解使用 SDK 和系统元数据。 **没有用户内容或最终用户身份信息设置为服务。**

查看下表，了解在启用最小诊断的情况下发送的事件和数据。

#### <a name="event-heartbeat"></a>事件：检测信号

| 名称                                 | 说明                                                                            | 清理 |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| 应用. ApplicationId                    | 通过 mip：： ApplicationInfo 提供的应用程序标识符。                          | 否       |
| ApplicationName                  | 通过 mip：： ApplicationInfo 提供的应用程序名称。                                | 否       |
| ApplicationVersion               | 通过 mip：： ApplicationInfo 提供的应用程序版本。                             | 否       |
| ApplicationId                        | 通过 mip：： ApplicationInfo 提供的应用程序版本。                             | 否       |
| ApplicationName                      | 通过 mip：： ApplicationInfo 提供的应用程序名称。                                | 否       |
| CreationTime                         | 生成时间事件。                                                              | 否       |
| DefaultLabel.Id                      | 租户默认标签 ID。                                                               | 否       |
| Engine                      | 经过身份验证的用户的主租户 GUID。                                            | 否       |
| UserObjectId                  | Azure Active Directory 中的用户对象 ID。                                              | 否       |
| 事件 CorrelationId                  | 生成的与触发事件的对象相关联的唯一 ID。                   | 否       |
| CorrelationIdDescription       | 触发事件的对象的 c + + 类名。                                     | 否       |
| ParentCorrelationId            | 父事件相关 ID。                                                           | 否       |
| ParentCorrelationIdDescription | 生成的与触发事件的对象的父对象关联的唯一 ID。 | 否       |
| 事件。 UniqueId                       | 为事件生成的唯一 ID。                                             | 否       |
| MachineName                          | 生成事件的系统的名称。                                           | **是**  |
| MIP.版本                          | MIP SDK 的版本。                                                                | 否       |
| 操作                            | 检测信号                                                                              | 否       |
| OrganizationId                       | 经过身份验证的用户的主租户 GUID。                                            | 否       |
| 平台                             | 操作系统版本。                                                              | 否       |
| ProcessName                          | 使用 SDK 的进程的名称。                                                     | 否       |
| ProductVersion                       | 与 "ApplicationVersion" 相同。                                                      | 否       |
| SDKVersion                           | 与 MIP 相同。版本。                                                                   | 否       |
| UserId                               | 用户的电子邮件地址。                                                             | **是**  |
| UserObjectId                         | 用户 Azure AD 对象 ID。                                                        | 否       |
| Version                              | 审核版本架构 ( "1.1" ) 。                                                          | 否       |

#### <a name="event-discovery"></a>事件：发现

| 名称                                 | 说明                                                                            | 清理 |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | 用于事件关联的此事件的唯一操作 ID。                           | 否       |
| 应用. ApplicationId                    | 通过 mip：： ApplicationInfo 提供的应用程序标识符。                          | 否       |
| ApplicationName                  | 通过 mip：： ApplicationInfo 提供的应用程序名称。                                | 否       |
| ApplicationVersion               | 通过 mip：： ApplicationInfo 提供的应用程序版本。                             | 否       |
| ApplicationId                        | 通过 mip：： ApplicationInfo 提供的应用程序版本。                             | 否       |
| ApplicationName                      | 通过 mip：： ApplicationInfo 提供的应用程序名称。                                | 否       |
| CreationTime                         | 生成时间事件。                                                              | 否       |
| DataState                            | 当应用程序在其上操作时，数据的状态为 "REST"、"移动"、"使用"。           | 否       |
| DefaultLabel.Id                      | 租户默认标签标识符。                                                       | 否       |
| Engine                      | 经过身份验证的用户的主租户 GUID。                                            | 否       |
| UserObjectId                  | Azure Active Directory 中的用户对象标识符。                                      | 否       |
| 事件 CorrelationId                  | 生成的与触发事件的对象相关联的唯一 ID。                   | 否       |
| CorrelationIdDescription       | 触发事件的对象的 c + + 类名。                                     | 否       |
| ParentCorrelationId            | 父事件相关 ID。                                                           | 否       |
| ParentCorrelationIdDescription | 生成的与触发事件的对象的父对象关联的唯一 ID。 | 否       |
| 事件。 UniqueId                       | 为事件生成的唯一 ID。                                             | 否       |
| 面部                              | 打开的文件或数据上的内容标签标识符。                                   | 否       |
| MachineName                          | 生成事件的系统的名称。                                           | **是**  |
| MIP.版本                          | MIP SDK 的版本。                                                                | 否       |
| ObjectId                             | 文件路径/文件或数据的说明。                                             | **是**  |
| 操作                            | "发现"。                                                                           | 否       |
| OrganizationId                       | 经过身份验证的用户的主租户 GUID。                                            | 否       |
| 平台                             | 操作系统版本。                                                              | 否       |
| ProcessName                          | 使用 SDK 的进程的名称。                                                     | 否       |
| Protected                            | 布尔值，指示文件是否受保护。                                       | 否       |
| 保护                           | 保护模板标识符。                                                    | **是**  |
| ProtectionOwner                      | 保护所有者的电子邮件地址。                                                 | **是**  |
| SDKVersion                           | 与 MIP 相同。版本。                                                                   | 否       |
| UserId                               | 用户的电子邮件地址。                                                             | **是**  |
| UserObjectId                         | 用户 Azure AD 对象 ID。                                                        | 否       |
| Version                              | 审核版本架构 ( "1.1" ) 。                                                          | 否       |

#### <a name="event-label-change"></a>事件：标签更改

| 名称                                 | 说明                                                                            | 清理 |
| ------------------------------------ | -------------------------------------------------------------------------------------- | -------- |
| ActionId                             | 用于事件关联的此事件的唯一操作 ID。                           | 否       |
| ActionIdBefore                       | 上一个操作 ID。 用于链接到新操作 ID。                                    | 否       |
| ActionSource                         | MIP：： ActionSource 的值。                                                            | 否       |
| 应用. ApplicationId                    | 通过 mip：： ApplicationInfo 提供的应用程序 ID。                                  | 否       |
| ApplicationName                  | 通过 mip：： ApplicationInfo 提供的应用程序名称。                                | 否       |
| ApplicationVersion               | 通过 mip：： ApplicationInfo 提供的应用程序版本。                             | 否       |
| ApplicationId                        | 通过 mip：： ApplicationInfo 提供的应用程序 ID。                                  | 否       |
| ApplicationName                      | 通过 mip：： ApplicationInfo 提供的应用程序名称。                                | 否       |
| CreationTime                         | 生成事件的时间。                                                          | 否       |
| DataState                            | 当应用程序在其上操作时，数据的状态为 "REST"、"移动"、"使用"。           | 否       |
| DefaultLabel.Id                      | 租户默认标签标识符。                                                       | 否       |
| Engine                      | 经过身份验证的用户的主租户 GUID。                                            | 否       |
| UserObjectId                  | Azure Active Directory 中的用户对象标识符。                                      | 否       |
| 事件 CorrelationId                  | 生成的与触发事件的对象相关联的唯一 ID。                   | 否       |
| CorrelationIdDescription       | 触发事件的对象的 c + + 类名。                                     | 否       |
| ParentCorrelationId            | 父事件相关 ID。                                                           | 否       |
| ParentCorrelationIdDescription | 生成的与触发事件的对象的父对象关联的唯一 ID。 | 否       |
| 事件。 UniqueId                       | 为事件生成的唯一 ID。                                             | 否       |
| IsLabelChanged                       | 布尔值，指示标签是否已更改。                                                  | 否       |
| IsProtectionChanged                  | 布尔值，指示保护是否已更改。                                                 | 否       |
| 面部                              | 要应用于文件或数据的标签 ID。                                    | 否       |
| LabelIdBefore                        | 文件或数据上的以前的标签 ID。                                        | 否       |
| MachineName                          | 生成事件的系统的名称。                                           | **是**  |
| MIP.版本                          | MIP SDK 的版本。                                                                | 否       |
| ObjectId                             | 文件路径/文件或数据的说明。                                             | **是**  |
| 操作                            | "更改"。                                                                              | 否       |
| OrganizationId                       | 经过身份验证的用户的主租户 GUID。                                            | 否       |
| 平台                             | 操作系统版本。                                                              | 否       |
| ProcessName                          | 使用 SDK 的进程的名称。                                                     | 否       |
| 产品版本                      |                                                                                        | 否       |
| Protected                            | 布尔值，指示文件是否受保护。                                       | 否       |
| 之前的保护                     | 布尔值，指示文件以前是否受保护。                           | 否       |
| 保护                           | 保护模板标识符。                                                    | 否       |
| 之前的保护                    | 之前的保护模板标识符。                                           | 否       |
| ProtectionContentId                  | 新内容标识符 (GUID) 。                                                     | 否       |
| ProtectionContentIdBefore            | 上一个内容标识符 (GUID) 。                                                | 否       |
| ProtectionOwner                      | 保护所有者的电子邮件地址。                                                 | **是**  |
| ProtectionOwnerBefore                | 保护所有者的以前的电子邮件地址。                                        | **是**  |
| SDKVersion                           | 与 MIP 相同。版本。                                                                   | 否       |
| UserId                               | 用户的电子邮件地址。                                                             | **是**  |
| UserObjectId                         | 用户 Azure AD 对象 ID。                                                        | 否       |
| Version                              | 审核版本架构 ( "1.1" ) 。                                                          | 否       |

### <a name="opting-out-in-c"></a>在 c + + 中选择

若要仅将诊断设置为最小值，请创建一个具有 **mip：:D iagnosticconfiguration ()** 的共享指针，并将 **isMinimalTelemetryEnabled** 设置为 true。 将中的配置对象传递给 **MipContent：： Create ()**。

```cpp
auto diagnosticConfig = std::make_shared<mip::DiagnosticConfiguration>();
diagnosticConfig->isMinimalTelemetryEnabled = true;
                       
// Create MipContext, passing in mip::TelemetryConfiguration object.
mMipContext = mip::MipContext::Create(
    mAppInfo,
    "mip_data",
    mip::LogLevel::Trace,
    false,
    nullptr /*loggerDelegateOverride*/,
    diagnosticConfig /*diagnosticOverride*/
);
```

### <a name="opting-out-in-net"></a>在 .NET 中退出

若要仅将诊断数据设置为最小值，请创建 **DiagnosticConfiguration ()** 对象并将 **isMinimalTelemetryEnabled** 设置为 true。 将配置对象传递到 **MIP。CreateMipContext ()**。

```csharp
DiagnosticConfiguration diagnosticConfiguration = new DiagnosticConfiguration();
diagnosticConfiguration.IsTelemetryOptedOut = true;

// Create MipContext, passing in TelemetryConfiguration object.
mipContext = MIP.CreateMipContext(appInfo, 
    "mip_data", 
    LogLevel.Trace, 
    null, 
    diagnosticConfiguration);
```
