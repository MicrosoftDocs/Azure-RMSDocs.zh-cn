---
title: 函数
description: 函数。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 4/16/2020
ms.openlocfilehash: c10c13212bf19ea27442626aa4bd900aa57a340d
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764147"
---
# <a name="functions"></a>函数

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

用于获取 OAuth2 标记的回调函数定义

**Parameters**

参数 | 说明
|---|---|
| identity | 要获取其令牌的电子邮件地址 |
| challenge | OAuth2 质询 |
| 上下文 | 传递给导致此身份验证回调的 MIP API 的不透明应用程序上下文 |
| tokenBuffer | 输出要将令牌复制到其中的缓冲区。 如果为 null，则将填充 "actualTokenSize"，但 |
| tokenBufferSize | 输出缓冲区的大小（以字节为单位） |
| actualTokenSize | 输出标记的实际大小（以字节为单位） |

**返回**： True 是检索的令牌，否则为 false

```c
MIP_CC_CALLBACK(mip_cc_auth_callback,
    bool,
    const mip_cc_identity*,
    const mip_cc_oauth2_challenge*,
    const void*,
    uint8_t*,
    const int64_t,
    int64_t*);
```

## <a name="mip_cc_consent_callback"></a>mip_cc_consent_callback

允许用户访问外部服务终结点的回调函数定义

**Parameters**

参数 | 说明
|---|---|
| url | SDK 要求用户同意的 URL |

**返回**：用户同意响应

```c
MIP_CC_CALLBACK(mip_cc_consent_callback,
    mip_cc_consent,
    const char*);
```

## <a name="mip_cc_createdictionary"></a>MIP_CC_CreateDictionary

创建字符串键/值的字典

**Parameters**

参数 | 说明
|---|---|
| entries | 键/值对的数组 |
| 计数 | 键/值对的数目 |
| 字典 | 输出新创建的字典 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：必须通过调用 MIP_CC_ReleaseDictionary 释放 mip_cc_dictionary 

```c
mip_cc_result MIP_CC_CreateDictionary(
    const mip_cc_kv_pair* entries,
    const int64_t count,
    mip_cc_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_dictionary_getentries"></a>MIP_CC_Dictionary_GetEntries

获取构成字典的键/值对

**Parameters**

参数 | 说明
|---|---|
| 字典 | 源字典 |
| entries | 输出键/值对的数组、mip_cc_dictionary 对象拥有的内存 |
| 计数 | 输出键/值对的数目 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "条目" 的内存由 mip_cc_dictionary 对象拥有，因此不应独立释放 

```c
mip_cc_result MIP_CC_Dictionary_GetEntries(
    const mip_cc_dictionary dictionary,
    mip_cc_kv_pair** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasedictionary"></a>MIP_CC_ReleaseDictionary

释放与字典关联的资源

**Parameters**

参数 | 说明
|---|---|
| 字典 | 要释放的字典 |

```c
void MIP_CC_ReleaseDictionary(mip_cc_dictionary dictionary);
```

## <a name="mip_cc_http_send_callback_fn"></a>mip_cc_http_send_callback_fn

发出 HTTP 请求的回调函数定义

**Parameters**

参数 | 说明
|---|---|
| 请求 | 要由应用程序执行的 HTTP 请求 |
| 上下文 | 传递给由此 HTTP 请求导致的 MIP API 调用的不透明上下文 |

```c
MIP_CC_CALLBACK(mip_cc_http_send_callback_fn,
    void,
    const mip_cc_http_request*,
    const void*);
```

## <a name="mip_cc_http_cancel_callback_fn"></a>mip_cc_http_cancel_callback_fn

用于取消 HTTP 请求的回调函数定义

**Parameters**

参数 | 说明
|---|---|
| requestId | 要取消的 HTTP 请求的 ID |

```c
MIP_CC_CALLBACK(mip_cc_http_cancel_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_createhttpdelegate"></a>MIP_CC_CreateHttpDelegate

创建可用于重写 MIP 的默认 HTTP 堆栈的 HTTP 委托

**Parameters**

参数 | 说明
|---|---|
| sendCallback | 用于发出 HTTP 请求的函数指针 |
| cancelCallback | 用于取消 HTTP 请求的函数指针 |
| httpDelegate | 输出HTTP 委托对象的句柄 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateHttpDelegate(
    const mip_cc_http_send_callback_fn sendCallback,
    const mip_cc_http_cancel_callback_fn cancelCallback,
    mip_cc_http_delegate* httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_notifyhttpdelegateresponse"></a>MIP_CC_NotifyHttpDelegateResponse

通知 HTTP 委托 HTTP 响应已准备就绪

**Parameters**

参数 | 说明
|---|---|
| httpDelegate | HTTP 委托对象的句柄 |
| requestId | 与此操作关联的 HTTP 请求的 ID |
| result | 操作成功/失败状态 |
| 响应 | 如果操作成功，则为 HTTP 响应，否则为 nullptr |

**注意**：当 HTTP 操作完成后，应用程序必须调用此函数。 HTTP 响应的 ID 必须与 HTTP 请求的 ID 匹配，以允许 MIP 将响应与其请求关联 

```c
void MIP_CC_NotifyHttpDelegateResponse(
    const mip_cc_http_delegate httpDelegate,
    const char* requestId,
    const mip_cc_http_result result,
    const mip_cc_http_response* response);
```

## <a name="mip_cc_releasehttpdelegate"></a>MIP_CC_ReleaseHttpDelegate

释放与 HTTP 委托句柄关联的资源

**Parameters**

参数 | 说明
|---|---|
| httpDelegate | 要释放的 HTTP 委托 |

```c
void MIP_CC_ReleaseHttpDelegate(mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_logger_init_callback_fn"></a>mip_cc_logger_init_callback_fn

记录器初始化的回调函数定义

**Parameters**

参数 | 说明
|---|---|
| 存储路径 | 可以存储日志的文件路径 |

```c
MIP_CC_CALLBACK(mip_cc_logger_init_callback_fn,
    void,
    const char*);
```

## <a name="mip_cc_logger_write_callback_fn"></a>mip_cc_logger_write_callback_fn

用于写入 log 语句的回调函数定义

**Parameters**

参数 | 说明
|---|---|
| 级别 | log 语句的日志级别。 |
| 消息 | log 语句的消息。 |
| 函数 | log 语句的函数名称。 |
| 文件 | 生成日志语句的文件名。 |
| line | 生成日志语句的行号。 |

```c
MIP_CC_CALLBACK(mip_cc_logger_write_callback_fn,
    void,
    const mip_cc_log_level,
    const char*,
    const char*,
    const char*,
    const int32_t);
```

## <a name="mip_cc_createloggerdelegate"></a>MIP_CC_CreateLoggerDelegate

创建一个记录器委托，该委托可用于重写 MIP 的默认记录器

**Parameters**

参数 | 说明
|---|---|
| initCallback | 用于初始化的函数指针 |
| flushCallback | 用于刷新日志的函数指针 |
| writeCallback | 用于写入 log 语句的函数指针 |
| loggerDelegate | 输出记录器委托对象的句柄 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateLoggerDelegate(
    const mip_cc_logger_init_callback_fn initCallback,
    const mip_cc_logger_flush_callback_fn flushCallback,
    const mip_cc_logger_write_callback_fn writeCallback,
    mip_cc_logger_delegate* loggerDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseloggerdelegate"></a>MIP_CC_ReleaseLoggerDelegate

释放与记录器委托句柄关联的资源

**Parameters**

参数 | 说明
|---|---|
| loggerDelegate | 要释放的记录器委托 |

```c
void MIP_CC_ReleaseLoggerDelegate(mip_cc_logger_delegate loggerDelegate);
```

## <a name="mip_cc_createmipcontext"></a>MIP_CC_CreateMipContext

创建 MIP 上下文以管理所有配置文件实例中共享的状态

**Parameters**

参数 | 说明
|---|---|
| applicationInfo | 有关使用保护 SDK 的应用程序的信息 |
| path | 用于存储日志记录、遥测和其他保护宣传品的文件路径 |
| logLevel | Miplog 的最小日志级别 |
| isOfflineOnly | 启用/禁用网络操作（并非脱机时支持的所有操作） |
| loggerDelegateOverride | 可有可无记录器替代实现 |
| telemetryOverride | 可有可无已重写遥测设置。 如果为 NULL，则将使用默认设置 |
| mipContext | 输出新创建的 MIP 上下文实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateMipContext(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmipcontextwithcustomfeaturesettings"></a>MIP_CC_CreateMipContextWithCustomFeatureSettings

创建 MIP 上下文以管理所有配置文件实例中共享的状态

**Parameters**

参数 | 说明
|---|---|
| applicationInfo | 有关使用保护 SDK 的应用程序的信息 |
| path | 用于存储日志记录、遥测和其他保护宣传品的文件路径 |
| logLevel | Miplog 的最小日志级别 |
| isOfflineOnly | 启用/禁用网络操作（并非脱机时支持的所有操作） |
| loggerDelegateOverride | 可有可无记录器替代实现 |
| telemetryOverride | 可有可无已重写遥测设置。 如果为 NULL，则将使用默认设置 |
| featureSettings | 可有可无自定义功能重写数组 |
| featureSettingsSize | 自定义功能重写的大小（在重写的中） |
| mipContext | 输出新创建的 MIP 上下文实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateMipContextWithCustomFeatureSettings(
    const mip_cc_application_info* applicationInfo,
    const char* path,
    const mip_cc_log_level logLevel,
    const bool isOfflineOnly,
    const mip_cc_logger_delegate loggerDelegateOverride,
    const mip_cc_telemetry_configuration telemetryOverride,
    const mip_cc_feature_override* featureSettings,
    const int64_t featureSettingsSize,
    mip_cc_mip_context* mipContext,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemipcontext"></a>MIP_CC_ReleaseMipContext

释放与 MIP 上下文关联的资源

**Parameters**

参数 | 说明
|---|---|
| mipContext | 要释放的 MIP 上下文 |

```c
void MIP_CC_ReleaseMipContext(mip_cc_mip_context mipContext);
```

## <a name="mip_cc_protectiondescriptor_getprotectiontype"></a>MIP_CC_ProtectionDescriptor_GetProtectionType

获取保护类型，无论其是否由 RMS 模板定义

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| protectionType | 输出保护类型 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetProtectionType(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_protection_type* protectionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getownersize"></a>MIP_CC_ProtectionDescriptor_GetOwnerSize

获取存储所有者所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| ownerSize | 输出保留所有者的缓冲区大小（以字符数为限） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwnerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getowner"></a>MIP_CC_ProtectionDescriptor_GetOwner

获取保护所有者

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| ownerBuffer | 输出将所有者复制到的缓冲区。 |
| ownerBufferSize | OwnerBuffer 的大小（字符数）。 |
| actualOwnerSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 ownerBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualOwnerSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwner(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getnamesize"></a>MIP_CC_ProtectionDescriptor_GetNameSize

获取存储名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| nameSize | 输出保留名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetNameSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getname"></a>MIP_CC_ProtectionDescriptor_GetName

获取保护名称

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetName(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescriptionsize"></a>MIP_CC_ProtectionDescriptor_GetDescriptionSize

获取存储说明所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| descriptionSize | 输出要保存的缓冲区大小说明（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescriptionSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescription"></a>MIP_CC_ProtectionDescriptor_GetDescription

获取保护说明

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| descriptionBuffer | 输出将此说明复制到的缓冲区。 |
| descriptionBufferSize | DescriptionBuffer 的大小（字符数）。 |
| actualDescriptionSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 descriptionBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualDescriptionSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescription(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_gettemplateid"></a>MIP_CC_ProtectionDescriptor_GetTemplateId

获取模板 ID

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| templateId | 输出与保护关联的模板 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetTemplateId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getlabelid"></a>MIP_CC_ProtectionDescriptor_GetLabelId

获取标签 ID

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| 面部 | 输出与保护关联的标签 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetLabelId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentid"></a>MIP_CC_ProtectionDescriptor_GetContentId

获取内容 ID

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| Id 为 | 输出与保护关联的内容 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doescontentexpire"></a>MIP_CC_ProtectionDescriptor_DoesContentExpire

获取内容是否具有过期时间

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| doesContentExpire | 输出内容是否过期 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesContentExpire(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesContentExpire,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentvaliduntil"></a>MIP_CC_ProtectionDescriptor_GetContentValidUntil

获取保护过期时间（以秒计）

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| contentValidUntil | 输出内容过期时间（从 epoch 起的秒数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentValidUntil(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* contentValidUntil,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doesallowofflineaccess"></a>MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess

获取是否允许脱机访问

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| doesAllowOfflineAccess | 输出是否允许脱机访问 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesAllowOfflineAccess,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrersize"></a>MIP_CC_ProtectionDescriptor_GetReferrerSize

获取存储引用站点所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| referrerSize | 输出要保留引用的缓冲区大小（以字符数为限） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* referrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrer"></a>MIP_CC_ProtectionDescriptor_GetReferrer

获取保护引用

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| referrerBuffer | 输出将引用的缓冲区复制到中。 |
| referrerBufferSize | ReferrerBuffer 的大小（字符数）。 |
| actualReferrerSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 referrerBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualReferrerSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrer(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* referrerBuffer,
    const int64_t referrerBufferSize,
    int64_t* actualReferrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurlsize"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize

获取存储双关键字 URL 所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| url | 输出用于保存双引号的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurl"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl

获取双键 URL

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| urlBuffer | 输出将 url 复制到的缓冲区。 |
| urlBufferSize | UrlBuffer 的大小（字符数）。 |
| actualUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 urlBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualUrlSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl(
    const mip_cc_protection_descriptor protectionDescriptor,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectiondescriptor"></a>MIP_CC_ReleaseProtectionDescriptor

释放与保护描述符关联的资源

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 要发布的保护描述符 |

```c
void MIP_CC_ReleaseProtectionDescriptor(mip_cc_protection_descriptor protectionDescriptor);
```

## <a name="mip_cc_createstringlist"></a>MIP_CC_CreateStringList

创建字符串列表

**Parameters**

参数 | 说明
|---|---|
| 字符串 | 字符串数组 |
| 计数 | 字符串数 |
| stringList | 输出新创建的字符串列表 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：必须通过调用 MIP_CC_ReleaseStringList 释放 mip_cc_string_list 

```c
mip_cc_result MIP_CC_CreateStringList(
    const char** strings,
    const int64_t count,
    mip_cc_string_list* stringList,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_stringlist_getstrings"></a>MIP_CC_StringList_GetStrings

获取组成字符串列表的字符串

**Parameters**

参数 | 说明
|---|---|
| stringList | 源字符串列表 |
| 字符串 | 输出字符串数组、mip_cc_string_list 对象拥有的内存 |
| 计数 | 输出字符串数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "字符串" 的内存由 mip_cc_string_list 对象拥有，因此不应独立释放 

```c
mip_cc_result MIP_CC_StringList_GetStrings(
    const mip_cc_string_list stringList,
    const char*** strings,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasestringlist"></a>MIP_CC_ReleaseStringList

释放与字符串列表关联的资源

**Parameters**

参数 | 说明
|---|---|
| stringList | 要释放的字符串列表 |

```c
void MIP_CC_ReleaseStringList(mip_cc_string_list stringList);
```

## <a name="mip_cc_dispatch_task_callback_fn"></a>mip_cc_dispatch_task_callback_fn

用于调度异步任务的回调函数定义

**Parameters**

参数 | 说明
|---|---|
| taskId | 唯一任务标识符 |

```c
MIP_CC_CALLBACK(mip_cc_dispatch_task_callback_fn,
    void,
    const mip_cc_async_task*);
```

## <a name="mip_cc_cancel_task_callback_fn"></a>mip_cc_cancel_task_callback_fn

用于取消后台任务的回调函数

**Parameters**

参数 | 说明
|---|---|
| taskId | 唯一任务标识符 |

**返回**：如果已成功取消任务，则返回 True; 否则返回 false

```c
MIP_CC_CALLBACK(mip_cc_cancel_task_callback_fn,
    bool,
    const char*);
```

## <a name="mip_cc_createtaskdispatcherdelegate"></a>MIP_CC_CreateTaskDispatcherDelegate

创建可用于重写 MIP 的默认异步任务处理的任务调度程序委托

**Parameters**

参数 | 说明
|---|---|
| dispatchTaskCallback | 用于调度异步任务的函数指针 |
| cancelTaskCallback | 用于取消后台任务的函数指针 |
| cancelAllTasksCallback | 用于取消所有后台任务的函数指针 |
| taskDispatcher | 输出任务调度程序委托对象的句柄 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateTaskDispatcherDelegate(
    const mip_cc_dispatch_task_callback_fn dispatchTaskCallback,
    const mip_cc_cancel_task_callback_fn cancelTaskCallback,
    const mip_cc_cancel_all_tasks_callback_fn cancelAllTasksCallback,
    mip_cc_task_dispatcher_delegate* taskDispatcher,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_executedispatchedtask"></a>MIP_CC_ExecuteDispatchedTask

通知 TaskDispatcher 委托任务计划立即在当前线程上执行

**Parameters**

参数 | 说明
|---|---|
| taskDispatcher | 任务调度程序委托对象的句柄 |
| taskId | 与此操作关联的异步任务的 ID |

**注意**：当任务计划为执行时，应用程序必须调用此函数。 它将导致立即在当前线程上执行任务。 ID 应与以前调度的、未取消的任务的 ID 匹配。 

```c
void MIP_CC_ExecuteDispatchedTask(const mip_cc_task_dispatcher_delegate taskDispatcher, const char* taskId);
```

## <a name="mip_cc_releasetaskdispatcherdelegate"></a>MIP_CC_ReleaseTaskDispatcherDelegate

释放与任务调度程序委托句柄关联的资源

**Parameters**

参数 | 说明
|---|---|
| taskDispatcher | 要释放的任务调度程序委托 |

```c
void MIP_CC_ReleaseTaskDispatcherDelegate(mip_cc_task_dispatcher_delegate taskDispatcher);
```

## <a name="mip_cc_createtelemetryconfiguration"></a>MIP_CC_CreateTelemetryConfiguration

创建用于创建保护配置文件的设置对象

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 输出新创建的包含默认设置的遥测配置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateTelemetryConfiguration(
    mip_cc_telemetry_configuration* telemetryConfig,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethostname"></a>MIP_CC_TelemetryConfiguration_SetHostName

设置将替代内部遥测设置的遥测主机名

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| hostName | 主机名 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：当客户端应用程序使用相同的 ARIA/1DS 遥测组件并希望使用其内部遥测设置（缓存、日志记录、优先级等）而不是 MIP 的默认设置时，将设置此属性 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHostName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* hostName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setlibraryname"></a>MIP_CC_TelemetryConfiguration_SetLibraryName

设置遥测共享库替代

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| libraryName | 实现 Aria/1DS SDK 的 C API 的 DLL 的名称 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：当客户端具有一个现有遥测 DLL，该 DLL 实现了应使用而不是 mip_ClientTelemetry .dll 的程序时，将设置此属性。 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetLibraryName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* libraryName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethttpdelegate"></a>MIP_CC_TelemetryConfiguration_SetHttpDelegate

重写客户端自己的默认遥测 HTTP 堆栈

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| httpDelegate | 由客户端应用程序实现的 HTTP 回调实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果未设置此属性，则遥测组件将使用 MIP 的默认 HTTP 堆栈 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHttpDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_settaskdispatcherdelegate"></a>MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate

用客户端自己的替换默认的异步任务调度程序

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| taskDispatcherDelegate | 由客户端应用程序实现的任务调度程序回调实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setisnetworkdetectionenabled"></a>MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled

设置是否允许遥测组件在后台线程上 ping 网络状态

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isCachingEnabled | 是否允许遥测组件在后台线程上 ping 网络状态 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：默认值为 "true" 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isNetworkDetectionEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setislocalcachingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled

设置是否允许遥测组件将缓存写入磁盘

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isCachingEnabled | 是否允许遥测组件将缓存写入磁盘 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：默认值为 "true" 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsLocalCachingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isCachingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistraceloggingenabled"></a>MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled

设置是否允许遥测组件将日志写入磁盘

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isTraceLoggingEnabled | 是否允许遥测组件将日志写入磁盘 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：默认值为 "true" 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTraceLoggingEnabled(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTraceLoggingEnabled,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setistelemetryoptedout"></a>MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut

设置应用程序/用户是否已选择不使用可选遥测

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isTelemetryOptedOut | 应用程序/用户是否已选择不使用可选遥测 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：默认值为 "false" 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetIsTelemetryOptedOut(
    const mip_cc_telemetry_configuration telemetryConfig,
    const bool isTelemetryOptedOut,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setcustomsettings"></a>MIP_CC_TelemetryConfiguration_SetCustomSettings

设置自定义遥测设置

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| customSettings | 自定义遥测设置 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetCustomSettings(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_addmaskedproperty"></a>MIP_CC_TelemetryConfiguration_AddMaskedProperty

将遥测属性设置为屏蔽

**Parameters**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| eventName | 事件名称 |
| propertyName | 属性名称 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TelemetryConfiguration_AddMaskedProperty(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* eventName,
    const char* propertyName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetelemetryconfiguration"></a>MIP_CC_ReleaseTelemetryConfiguration

释放与保护配置文件设置关联的资源

**Parameters**

参数 | 说明
|---|---|
| profileSettings | 要发布的保护配置文件设置 |

```c
void MIP_CC_ReleaseTelemetryConfiguration(mip_cc_telemetry_configuration telemetryConfig);
```

## <a name="mip_cc_releaseprotectionengine"></a>MIP_CC_ReleaseProtectionEngine

释放与保护引擎关联的资源

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 要发布的保护引擎 |

```c
void MIP_CC_ReleaseProtectionEngine(mip_cc_protection_engine engine);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforpublishing"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing

创建用于发布新内容的保护处理程序

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 将在其下创建处理程序的引擎 |
| 设置 | 保护处理程序设置 |
| 上下文 | 将以不透明的形式传递给 HttpDelegate 和 AuthDelegate 的客户端上下文 |
| 处理程序 (handler) | 输出新创建的保护处理程序实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForPublishing(
    const mip_cc_protection_engine engine,
    const mip_cc_protection_handler_publishing_settings settings,
    const void* context,
    mip_cc_protection_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_createprotectionhandlerforconsumption"></a>MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption

创建用于使用现有内容的保护处理程序

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 将在其下创建处理程序的引擎 |
| 设置 | 保护处理程序设置 |
| 上下文 | 将以不透明的形式传递给 HttpDelegate 和 AuthDelegate 的客户端上下文 |
| 处理程序 (handler) | 输出新创建的保护处理程序实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionEngine_CreateProtectionHandlerForConsumption(
  const mip_cc_protection_engine engine,
  const mip_cc_protection_handler_consumption_settings settings,
  const void* context,
  mip_cc_protection_handler* handler,
  mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineidsize"></a>MIP_CC_ProtectionEngine_GetEngineIdSize

获取引擎 ID 所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 保护引擎 |
| idSize | 输出保留引擎 ID 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineIdSize(
    const mip_cc_protection_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getengineid"></a>MIP_CC_ProtectionEngine_GetEngineId

获取引擎 ID

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 保护引擎 |
| idBuffer | 输出该 id 将被复制到中。 |
| idBufferSize | IdBuffer 的大小（字符数）。 |
| actualIdSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 idBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualIdSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetEngineId(
    const mip_cc_protection_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplatessize"></a>MIP_CC_ProtectionEngine_GetTemplatesSize

获取与保护引擎关联的 RMS 模板的数目

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 保护引擎 |
| 上下文 | 将以不透明的形式传递给 HttpDelegate 和 AuthDelegate 的客户端上下文 |
| templatesSize | 输出模板数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：此 API 可能导致独立的 HTTP 操作。 请考虑直接将 "MIP_CC_ProtectionEngine_GetTemplates" 与预定义的缓冲区一起使用，以避免不必要的额外 HTTP 操作。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplatesSize(
    const mip_cc_protection_engine engine,
    const void* context,
    int64_t* templatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_gettemplates"></a>MIP_CC_ProtectionEngine_GetTemplates

获取可供用户使用的模板集合

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 保护引擎 |
| 上下文 | 将以不透明的形式传递给 HttpDelegate 和 AuthDelegate 的客户端上下文 |
| mip_cc_template_descriptor | [Output] 用于创建模板处理程序的缓冲区。 |
| templateBufferSize | TemplateBuffer 的大小（按项数）。 |
| actualTemplatesSize | 输出写入缓冲区的模板 Id 的数目 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 templateBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualTemplateSize 设置为所需的最小缓冲区大小。 每个 mip_cc_template_descriptor 都必须通过调用 MIP_CC_ReleaseTemplateDescriptor （）来由调用方释放。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetTemplates(
    const mip_cc_protection_engine engine,
    const void* context,
    mip_cc_template_descriptor* templateDescriptors,
    const int64_t templateBufferSize,
    int64_t* actualTemplatesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getrightsforlabelid"></a>MIP_CC_ProtectionEngine_GetRightsForLabelId

获取向用户授予的标签 ID 的权限列表

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 保护引擎 |
| 上下文 | 将以不透明的形式传递给 HttpDelegate 和 AuthDelegate 的客户端上下文 |
| documentId | 分配给文档的文档 ID |
| 面部 | 应用于文档的标签 ID |
| ownerEmail | 文档的所有者 |
| delagedUserEmail | 用户的电子邮件（如果身份验证用户/应用程序代表另一个用户操作），如果没有，则为空 |
| 权限 | 输出向用户授予的权限列表，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "rights" 变量 MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetRightsForLabelId(
    const mip_cc_protection_engine engine,
    const void* context,
    const char* documentId,
    const char* labelId,
    const char* ownerEmail,
    const char* delegatedUserEmail,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdatasize"></a>MIP_CC_ProtectionEngine_GetClientDataSize

获取与保护引擎关联的客户端数据的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 保护引擎 |
| clientDataSize | 输出客户端数据的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientDataSize(
    const mip_cc_protection_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionengine_getclientdata"></a>MIP_CC_ProtectionEngine_GetClientData

获取与保护引擎关联的客户端数据

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 保护引擎 |
| clientDataBuffer | 输出将客户端数据复制到其中的缓冲区 |
| clientDataBufferSize | ClientDataBuffer 的大小（字符数）。 |
| actualClientDataSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 clientDataBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualClientDataSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionEngine_GetClientData(
    const mip_cc_protection_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionenginesettingswithidentity"></a>MIP_CC_CreateProtectionEngineSettingsWithIdentity

创建用于创建全新保护引擎的设置对象

**Parameters**

参数 | 说明
|---|---|
| identity | 将与 ProtectionEngine 关联的标识 |
| clientData | 与引擎一起存储的可自定义客户端数据 |
| locale | 文本结果将输出到的区域设置 |
| engineSettings | 输出新创建的设置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateProtectionEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    mip_cc_protection_engine_settings* engineSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setclientdata"></a>MIP_CC_ProtectionEngineSettings_SetClientData

设置客户端数据，该数据将与此引擎透明存储并跨会话保存

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| clientData | 客户端数据 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetClientData(
    const mip_cc_protection_engine_settings engineSettings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcustomsettings"></a>MIP_CC_ProtectionEngineSettings_SetCustomSettings

配置自定义设置，用于功能的门和测试。

**Parameters**

参数 | 说明
|---|---|
| engineSettings | 引擎设置 |
| customSettings | 自定义设置的键/值对 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCustomSettings(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setsessionid"></a>MIP_CC_ProtectionEngineSettings_SetSessionId

设置可用于关联日志和遥测的会话 ID

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| sessionID | 表示保护引擎生存期的会话 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetSessionId(
    const mip_cc_protection_engine_settings engineSettings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloud"></a>MIP_CC_ProtectionEngineSettings_SetCloud

设置影响所有服务请求的终结点 Url 的云

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| 云 | Cloud 标识符（默认值 = 未知） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果未指定 cloud，则它将由引擎的标识域的 DNS 查找决定（如果可能），否则将回退到全局云。 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloud(
    const mip_cc_protection_engine_settings engineSettings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionenginesettings_setcloudendpointbaseurl"></a>MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl

设置所有服务请求的基 URL

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| cloudEndpointBaseUrl | 基 URL （例如 "https://api.aadrm.com"） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：此值将仅被读取，并且必须设置为 Cloud = MIP_CLOUD_CUSTOM 

```c
mip_cc_result MIP_CC_ProtectionEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_protection_engine_settings engineSettings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionenginesettings"></a>MIP_CC_ReleaseProtectionEngineSettings

释放与保护引擎设置关联的资源

**Parameters**

参数 | 说明
|---|---|
| engineSettings | 要发布的保护引擎设置 |

```c
void MIP_CC_ReleaseProtectionEngineSettings(mip_cc_protection_engine_settings engineSettings);
```

## <a name="mip_cc_createprotectionhandlerpublishingsettings"></a>MIP_CC_CreateProtectionHandlerPublishingSettings

创建用于创建用于发布新内容的保护处理程序的设置对象

**Parameters**

参数 | 说明
|---|---|
| 描述符 | 保护详细信息 |
| 设置 | 输出新创建的设置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateProtectionHandlerPublishingSettings(
    const mip_cc_protection_descriptor descriptor,
    mip_cc_protection_handler_publishing_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisdeprecatedalgorithmpreferred"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred

设置是否首选不推荐使用的加密算法（ECB）以实现向后兼容性

**Parameters**

参数 | 说明
|---|---|
| 设置 | 保护处理程序设置 |
| isDeprecatedAlgorithmPreferred | 是否优先使用不推荐使用的算法 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsDeprecatedAlgorithmPreferred(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isDeprecatedAlgorithmPreferred,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setisauditedextractionallowed"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed

设置是否允许非 MIP 感知应用程序打开受保护的内容

**Parameters**

参数 | 说明
|---|---|
| 设置 | 保护处理程序设置 |
| isAuditedExtractionAllowed | 是否允许非 MIP 感知应用程序打开受保护的内容 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsAuditedExtractionAllowed(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isAuditedExtractionAllowed,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setispublishingformatjson"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson

设置 PL 是否为 JSON 格式（默认值为 XML）

**Parameters**

参数 | 说明
|---|---|
| 设置 | 保护处理程序设置 |
| isPublishingFormatJson | 生成的 PL 是否应采用 JSON 格式 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetIsPublishingFormatJson(
    const mip_cc_protection_handler_publishing_settings settings,
    const bool isPublishingFormatJson,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail

设置委派的用户

**Parameters**

参数 | 说明
|---|---|
| 设置 | 保护处理程序设置 |
| delegatedUserEmail | 委托用户的电子邮件地址 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：当正在进行身份验证的用户/应用程序代表其他用户时，将指定委派的用户 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerpublishingsettings_setprelicenseuseremail"></a>MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail

设置许可前用户

**Parameters**

参数 | 说明
|---|---|
| 设置 | 保护处理程序设置 |
| preLicenseUserEmail | 预先许可用户的电子邮件地址 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：在发布时，应获取预许可用户 

```c
mip_cc_result MIP_CC_ProtectionHandlerPublishingSettings_SetPreLicenseUserEmail(
    const mip_cc_protection_handler_publishing_settings settings,
    const char* preLicenseUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettings"></a>MIP_CC_CreateProtectionHandlerConsumptionSettings

创建用于创建保护处理程序以使用现有内容的设置对象

**Parameters**

参数 | 说明
|---|---|
| publishingLicenseBuffer | 包含原始发布许可证的缓冲区 |
| publishingLicenseBufferSize | 发布许可证缓冲区的大小 |
| 设置 | 输出新创建的设置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettings(
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createprotectionhandlerconsumptionsettingswithprelicense"></a>MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense

创建用于创建保护处理程序以使用现有内容的设置对象

**Parameters**

参数 | 说明
|---|---|
| preLicenseBuffer | 包含原始预许可证缓冲区的缓冲区 |
| preLicenseBufferSize | 预先许可缓冲区的大小 |
| publishingLicenseBuffer | 包含原始发布许可证的缓冲区 |
| publishingLicenseBufferSize | 发布许可证缓冲区的大小 |
| 设置 | 输出新创建的设置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateProtectionHandlerConsumptionSettingsWithPreLicense(
    const uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    const uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    mip_cc_protection_handler_consumption_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setisofflineonly"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly

设置保护处理程序创建是否允许联机 HTTP 操作

**Parameters**

参数 | 说明
|---|---|
| 设置 | 保护处理程序设置 |
| isOfflineOnly | 如果禁止 HTTP 操作，则为 True，否则为 false |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果将此属性设置为 true，则仅当以前已解密内容并缓存其未过期许可证时，保护处理程序创建才会成功。 如果找不到缓存的内容，将返回 MIP_RESULT_ERROR_NETWORK 结果。 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetIsOfflineOnly(
    const mip_cc_protection_handler_consumption_settings settings,
    const bool isOfflineOnly,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandlerconsumptionsettings_setdelegateduseremail"></a>MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail

设置委派的用户

**Parameters**

参数 | 说明
|---|---|
| 设置 | 保护处理程序设置 |
| delegatedUserEmail | 委托用户的电子邮件地址 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：当正在进行身份验证的用户/应用程序代表其他用户时，将指定委派的用户 

```c
mip_cc_result MIP_CC_ProtectionHandlerConsumptionSettings_SetDelegatedUserEmail(
    const mip_cc_protection_handler_consumption_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize

获取发布许可证的大小（以字节为单位）

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| publishingLicenseBufferSize | 输出发布许可证的大小（以字节为单位） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicenseSize(
    const mip_cc_protection_handler handler,
    int64_t* publishingLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedpublishinglicense"></a>MIP_CC_ProtectionHandler_GetSerializedPublishingLicense

获取发布许可证

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| publishingLicenseBuffer | 输出发布许可证将写入的缓冲区 |
| publishingLicenseBufferSize | 发布许可证缓冲区的大小 |
| actualPublishingLicenseSize | 输出发布许可证的实际大小（以字节为单位） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 publishingLicenseBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualPublishingLicenseSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPublishingLicense(
    const mip_cc_protection_handler handler,
    uint8_t* publishingLicenseBuffer,
    const int64_t publishingLicenseBufferSize,
    int64_t* actualPublishingLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicensesize"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize

获取预许可证的大小（以字节为单位）

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| format | 预许可格式 |
| preLicenseBufferSize | 输出预先许可的大小（以字节为单位） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicenseSize(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    int64_t* preLicenseBufferSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getserializedprelicense"></a>MIP_CC_ProtectionHandler_GetSerializedPreLicense

获取预许可

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| format | 预许可格式 |
| preLicenseBuffer | 输出将向其写入预许可证的缓冲区 |
| preLicenseBufferSize | 预许可缓冲区的大小 |
| actualPreLicenseSize | 输出预先许可的实际大小（以字节为单位） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 preLicenseBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualPreLicenseSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetSerializedPreLicense(
    const mip_cc_protection_handler handler,
    mip_cc_pre_license_format format,
    uint8_t* preLicenseBuffer,
    const int64_t preLicenseBufferSize,
    int64_t* actualPreLicenseSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectiondescriptor"></a>MIP_CC_ProtectionHandler_GetProtectionDescriptor

获取保护描述符

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| 描述符 | 输出保护描述符 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectionDescriptor(
    const mip_cc_protection_handler handler,
    mip_cc_protection_descriptor* descriptor,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getrights"></a>MIP_CC_ProtectionHandler_GetRights

获取授予用户的权限的列表

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| 权限 | 输出向用户授予的权限列表，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "rights" 变量 MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetRights(
    const mip_cc_protection_handler handler,
    mip_cc_string_list* rights,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getprotectedcontentsize"></a>MIP_CC_ProtectionHandler_GetProtectedContentSize

计算受保护内容的大小，在填充中进行因式分解，等等。

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| unprotectedSize | 未保护/明文内容的大小（以字节为单位） |
| includesFinalBlock | 介绍相关的未受保护内容是否包括最终块。 |
| protectedSize | 输出受保护内容的大小 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetProtectedContentSize(
    const mip_cc_protection_handler handler,
    const int64_t unprotectedSize,
    const bool includesFinalBlock,
    int64_t* protectedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getblocksize"></a>MIP_CC_ProtectionHandler_GetBlockSize

获取保护处理程序所使用的密码模式的块大小（以字节为单位）

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| 大小 | 输出块大小（以字节为单位） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetBlockSize(
    const mip_cc_protection_handler handler,
    int64_t* blockSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissuedusersize"></a>MIP_CC_ProtectionHandler_GetIssuedUserSize

获取存储已被授予对受保护内容的访问权限的用户所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| issuedUserSize | 输出用于保存已颁发用户的缓冲区大小（以字符数为限） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUserSize(
    const mip_cc_protection_handler handler,
    int64_t* issuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getissueduser"></a>MIP_CC_ProtectionHandler_GetIssuedUser

获取已被授予对受保护内容的访问权限的用户

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| issuedUserBuffer | 输出发出的用户将被复制到的缓冲区。 |
| issuedUserBufferSize | IssuedUserBuffer 的大小（字符数）。 |
| actualIssuedUserSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 issuedUserBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualIssuedUserSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetIssuedUser(
    const mip_cc_protection_handler handler,
    char* issuedUserBuffer,
    const int64_t issuedUserBufferSize,
    int64_t* actualIssuedUserSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getownersize"></a>MIP_CC_ProtectionHandler_GetOwnerSize

获取存储受保护内容的所有者所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| ownerSize | 输出用于保存已颁发用户的缓冲区大小（以字符数为限） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwnerSize(
    const mip_cc_protection_handler handler,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getowner"></a>MIP_CC_ProtectionHandler_GetOwner

获取受保护内容的所有者

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| ownerBuffer | 输出发出的用户将被复制到的缓冲区。 |
| ownerBufferSize | OwnerBuffer 的大小（字符数）。 |
| actualOwnerSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 ownerBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualOwnerSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectionHandler_GetOwner(
    const mip_cc_protection_handler handler,
    char* ownerBuffer,
    const int64_t ownerBufferSize,
    int64_t* actualOwnerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_getcontentid"></a>MIP_CC_ProtectionHandler_GetContentId

获取受保护内容的 IE 内容

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| Id 为 | 输出内容 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_GetContentId(
    const mip_cc_protection_handler handler,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_doesusedeprecatedalgorithm"></a>MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm

获取保护处理程序是否使用不推荐使用的加密算法（ECB）来实现向后兼容性

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 表示受保护内容的处理程序 |
| doesUseDeprecatedAlgorithm | 输出保护处理程序是否使用不推荐使用的加密算法 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_DoesUseDeprecatedAlgorithm(
    const mip_cc_protection_handler handler,
    bool* doesUseDeprecatedAlgorithm,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionhandler_decryptbuffer"></a>MIP_CC_ProtectionHandler_DecryptBuffer

解密缓冲区

**Parameters**

参数 | 说明
|---|---|
| offsetFromStart | 从加密内容的最开始位置 inputBuffer 的相对位置 |
| inputBuffer | 要解密的加密内容的缓冲区 |
| inputBufferSize | 输入缓冲区的大小（以字节为单位） |
| outputBuffer | 输出解密内容将复制到的缓冲区 |
| outputBufferSize | 输出缓冲区的大小（以字节为单位） |
| isFinal | 如果输入缓冲区包含最终加密字节 |
| actualDecryptedSize | 输出加密内容的实际大小（以字节为单位） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionHandler_DecryptBuffer(
    const mip_cc_protection_handler handler,
    const int64_t offsetFromStart,
    const uint8_t* inputBuffer,
    const int64_t inputBufferSize,
    uint8_t* outputBuffer,
    const int64_t outputBufferSize,
    const bool isFinal,
    int64_t *actualDecryptedSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionhandlerpublishingsettings"></a>MIP_CC_ReleaseProtectionHandlerPublishingSettings

释放与保护处理程序设置关联的资源

**Parameters**

参数 | 说明
|---|---|
| 设置 | 要发布的保护处理程序设置 |

```c
void MIP_CC_ReleaseProtectionHandlerPublishingSettings(mip_cc_protection_handler_publishing_settings settings);
```

## <a name="mip_cc_releaseprotectionhandlerconsumptionsettings"></a>MIP_CC_ReleaseProtectionHandlerConsumptionSettings

释放与保护处理程序设置关联的资源

**Parameters**

参数 | 说明
|---|---|
| 设置 | 要发布的保护处理程序设置 |

```c
void MIP_CC_ReleaseProtectionHandlerConsumptionSettings(mip_cc_protection_handler_consumption_settings settings);
```

## <a name="mip_cc_releaseprotectionhandler"></a>MIP_CC_ReleaseProtectionHandler

释放与保护处理程序关联的资源

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 要发布的保护处理程序 |

```c
void MIP_CC_ReleaseProtectionHandler(mip_cc_protection_handler handler);
```

## <a name="mip_cc_loadprotectionprofile"></a>MIP_CC_LoadProtectionProfile

加载配置文件

**Parameters**

参数 | 说明
|---|---|
| 设置 | 个人资料设置 |
| profile | 输出新创建的保护配置文件实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_LoadProtectionProfile(
    const mip_cc_protection_profile_settings settings,
    mip_cc_protection_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofile"></a>MIP_CC_ReleaseProtectionProfile

释放与保护配置文件关联的资源

**Parameters**

参数 | 说明
|---|---|
| profile | 要发布的保护配置文件 |

```c
void MIP_CC_ReleaseProtectionProfile(mip_cc_protection_profile profile);
```

## <a name="mip_cc_createprotectionprofilesettings"></a>MIP_CC_CreateProtectionProfileSettings

创建用于创建保护配置文件的设置对象

**Parameters**

参数 | 说明
|---|---|
| mipContext | 跨所有配置文件共享的全局上下文 |
| cacheStorageType | 存储缓存配置 |
| authCallback | 要用于身份验证的回调对象，由客户端应用程序实现 |
| consentCallback | 要用于同意的回调对象，由客户端应用程序实现 |
| 设置 | 输出新创建的设置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateProtectionProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    const mip_cc_consent_callback consentCallback,
    mip_cc_protection_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setsessionid"></a>MIP_CC_ProtectionProfileSettings_SetSessionId

设置可用于关联日志和遥测的会话 ID

**Parameters**

参数 | 说明
|---|---|
| 设置 | 个人资料设置 |
| sessionID | 表示保护配置文件生存期的会话 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetSessionId(
    const mip_cc_protection_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcancachelicenses"></a>MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses

配置最终用户许可证（Eul）是否将缓存在本地

**Parameters**

参数 | 说明
|---|---|
| 设置 | 个人资料设置 |
| canCacheLicenses | 打开受保护的内容时，引擎是否应缓存许可证 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCanCacheLicenses(
    const mip_cc_protection_profile_settings settings,
    const bool canCacheLicenses,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_sethttpdelegate"></a>MIP_CC_ProtectionProfileSettings_SetHttpDelegate

用客户端自己的替换默认的 HTTP 堆栈

**Parameters**

参数 | 说明
|---|---|
| 设置 | 将向其分配 HTTP 委托的配置文件设置 |
| httpDelegate | 由客户端应用程序实现的 HTTP 回调实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetHttpDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate

用客户端自己的替换默认的异步任务调度程序

**Parameters**

参数 | 说明
|---|---|
| 设置 | 任务调度程序委托将被分配到的配置文件设置 |
| taskDispatcherDelegate | 由客户端应用程序实现的任务调度程序回调实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectionprofilesettings_setcustomsettings"></a>MIP_CC_ProtectionProfileSettings_SetCustomSettings

配置自定义设置，用于功能的门和测试。

**Parameters**

参数 | 说明
|---|---|
| 设置 | 个人资料设置 |
| customSettings | 自定义设置的键/值对 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionProfileSettings_SetCustomSettings(
    const mip_cc_protection_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseprotectionprofilesettings"></a>MIP_CC_ReleaseProtectionProfileSettings

释放与保护配置文件设置关联的资源

**Parameters**

参数 | 说明
|---|---|
| 设置 | 要发布的保护配置文件设置 |

```c
void MIP_CC_ReleaseProtectionProfileSettings(mip_cc_protection_profile_settings profilsettingseSettings);
```

## <a name="mip_cc_templatedescriptor_getid"></a>MIP_CC_TemplateDescriptor_GetId

获取模板 ID

**Parameters**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| templateId | 输出与保护关联的模板 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetId(
    const mip_cc_template_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getnamesize"></a>MIP_CC_TemplateDescriptor_GetNameSize

获取存储名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| nameSize | 输出保留名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetNameSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getname"></a>MIP_CC_TemplateDescriptor_GetName

获取模板名称

**Parameters**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 NameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetName(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescriptionsize"></a>MIP_CC_TemplateDescriptor_GetDescriptionSize

获取存储说明所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| descriptionSize | 输出要保存的缓冲区大小说明（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescriptionSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescription"></a>MIP_CC_TemplateDescriptor_GetDescription

获取模板说明

**Parameters**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| descriptionBuffer | 输出将此说明复制到的缓冲区。 |
| descriptionBufferSize | DescriptionBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 descriptionBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualDescriptionSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescription(
    const mip_cc_template_descriptor templateDescriptor,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasetemplatedescriptor"></a>MIP_CC_ReleaseTemplateDescriptor

释放与模板描述符关联的资源

**Parameters**

参数 | 说明
|---|---|
| templateDescriptor | 要发布的模板描述符 |

```c
void MIP_CC_ReleaseTemplateDescriptor(mip_cc_template_descriptor templateDescriptor);
```

## <a name="mip_cc_action_gettype"></a>MIP_CC_Action_GetType

获取操作的类型

**Parameters**

参数 | 说明
|---|---|
| action | 操作 |
| actionType | 输出操作类型 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Action_GetType(
    const mip_cc_action action,
    mip_cc_action_type* actionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_action_getid"></a>MIP_CC_Action_GetId

获取操作的 ID

**Parameters**

参数 | 说明
|---|---|
| action | 操作 |
| id | 输出唯一操作 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Action_GetId(
    const mip_cc_action action,
    mip_cc_guid* id,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_actionresult_getactions"></a>MIP_CC_ActionResult_GetActions

获取构成操作结果的操作

**Parameters**

参数 | 说明
|---|---|
| actionResult | 源操作结果 |
| actions | 输出操作数组、由 mip_cc_action_result 对象拥有的内存 |
| 计数 | 输出键/值对的数目 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "操作" 的内存由 mip_cc_action_result 对象拥有，因此不应独立释放 

```c
mip_cc_result MIP_CC_ActionResult_GetActions(
    const mip_cc_action_result actionResult,
    mip_cc_action** actions,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaseactionresult"></a>MIP_CC_ReleaseActionResult

释放与操作结果关联的资源

**Parameters**

参数 | 说明
|---|---|
| actionResult | 要释放的操作结果 |

```c
void MIP_CC_ReleaseActionResult(mip_cc_action_result actionResult);
```

## <a name="mip_cc_addcontentfooteraction_getuielementnamesize"></a>MIP_CC_AddContentFooterAction_GetUIElementNameSize

获取存储 "添加内容脚注" 操作的 UI 元素名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameSize | 输出保存 UI 元素名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getuielementname"></a>MIP_CC_AddContentFooterAction_GetUIElementName

获取 "添加内容脚注" 操作的 UI 元素名称

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameBuffer | 输出将 UI 元素名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettextsize"></a>MIP_CC_AddContentFooterAction_GetTextSize

获取存储 "添加内容脚注" 操作文本所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameSize | 输出要保存文本的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettext"></a>MIP_CC_AddContentFooterAction_GetText

获取 "添加内容脚注" 操作的文本

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| textBuffer | 输出Buffer 文本将复制到中。 |
| textBufferSize | TextBuffer 的大小（字符数）。 |
| actualTextSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 textBuffer 为 null 或不充分，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualTextSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontnamesize"></a>MIP_CC_AddContentFooterAction_GetFontNameSize

获取存储 "添加内容脚注" 操作字体名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameSize | 输出用于保存字体名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontname"></a>MIP_CC_AddContentFooterAction_GetFontName

获取 "添加内容脚注" 操作的字体名称

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameBuffer | 输出将字体名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontsize"></a>MIP_CC_AddContentFooterAction_GetFontSize

获取整数字号

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| fontSize | 输出字号 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolorsize"></a>MIP_CC_AddContentFooterAction_GetFontColorSize

获取存储 "添加内容脚注" 操作字体颜色所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| colorSize | 输出保存字体颜色的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolor"></a>MIP_CC_AddContentFooterAction_GetFontColor

获取 "添加内容脚注" 操作的字体颜色（例如，"#000000"）

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| colorBuffer | 输出缓冲区字体颜色将被复制到中。 |
| colorBufferSize | ColorBuffer 的大小（字符数）。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 colorBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualColorSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getalignment"></a>MIP_CC_AddContentFooterAction_GetAlignment

获取对齐方式

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| 对齐 (alignment) | 输出关联 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getmargin"></a>MIP_CC_AddContentFooterAction_GetMargin

获取边距大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| marginSize | 输出边距大小（毫米） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementnamesize"></a>MIP_CC_AddContentHeaderAction_GetUIElementNameSize

获取存储 "添加内容标头" 操作的 UI 元素名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameSize | 输出保存 UI 元素名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementname"></a>MIP_CC_AddContentHeaderAction_GetUIElementName

获取 "添加内容标头" 操作的 UI 元素名称

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameBuffer | 输出将 UI 元素名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettextsize"></a>MIP_CC_AddContentHeaderAction_GetTextSize

获取存储 "添加内容标头" 操作文本所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameSize | 输出要保存文本的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettext"></a>MIP_CC_AddContentHeaderAction_GetText

获取 "添加内容标头" 操作的文本

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| textBuffer | 输出Buffer 文本将复制到中。 |
| textBufferSize | TextBuffer 的大小（字符数）。 |
| actualTextSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 textBuffer 为 null 或不充分，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualTextSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontnamesize"></a>MIP_CC_AddContentHeaderAction_GetFontNameSize

获取存储 "添加内容标头" 操作字体名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameSize | 输出用于保存字体名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontname"></a>MIP_CC_AddContentHeaderAction_GetFontName

获取 "添加内容标头" 操作的字体名称

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameBuffer | 输出将字体名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontsize"></a>MIP_CC_AddContentHeaderAction_GetFontSize

获取整数字号

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| fontSize | 输出字号 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolorsize"></a>MIP_CC_AddContentHeaderAction_GetFontColorSize

获取存储 "添加内容标头" 操作字体颜色所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| colorSize | 输出保存字体颜色的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolor"></a>MIP_CC_AddContentHeaderAction_GetFontColor

获取 "添加内容标头" 操作的字体颜色（例如，"#000000"）

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| colorBuffer | 输出缓冲区字体颜色将被复制到中。 |
| colorBufferSize | ColorBuffer 的大小（字符数）。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 colorBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualColorSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getalignment"></a>MIP_CC_AddContentHeaderAction_GetAlignment

获取对齐方式

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| 对齐 (alignment) | 输出关联 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getmargin"></a>MIP_CC_AddContentHeaderAction_GetMargin

获取边距大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| marginSize | 输出边距大小（毫米） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementnamesize"></a>MIP_CC_AddWatermarkAction_GetUIElementNameSize

获取存储 "添加水印" 操作的 UI 元素名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameSize | 输出保存 UI 元素名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementname"></a>MIP_CC_AddWatermarkAction_GetUIElementName

获取 "添加水印" 操作的 UI 元素名称

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameBuffer | 输出将 UI 元素名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getlayout"></a>MIP_CC_AddWatermarkAction_GetLayout

获取水印布局

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| 布局 | 输出水印布局 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetLayout(
    const mip_cc_action action,
    mip_cc_watermark_layout* layout,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettextsize"></a>MIP_CC_AddWatermarkAction_GetTextSize

获取存储 "添加水印" 操作文本所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| textSize | 输出要保存文本的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettext"></a>MIP_CC_AddWatermarkAction_GetText

获取 "添加水印" 操作的文本

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| textBuffer | 输出Buffer 文本将复制到中。 |
| textBufferSize | TextBuffer 的大小（字符数）。 |
| actualTextSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 textBuffer 为 null 或不充分，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualTextSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetText(
    const mip_cc_action action,
    char* textBuffer,
    const int64_t textBufferSize,
    int64_t* actualTextSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontnamesize"></a>MIP_CC_AddWatermarkAction_GetFontNameSize

获取存储 "添加水印" 操作字体名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameSize | 输出用于保存字体名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontname"></a>MIP_CC_AddWatermarkAction_GetFontName

获取 "添加水印" 操作的字体名称

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameBuffer | 输出将字体名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontsize"></a>MIP_CC_AddWatermarkAction_GetFontSize

获取整数字号

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| fontSize | 输出字号 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolorsize"></a>MIP_CC_AddWatermarkAction_GetFontColorSize

获取存储 "添加水印" 操作字体颜色所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| colorSize | 输出保存字体颜色的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolor"></a>MIP_CC_AddWatermarkAction_GetFontColor

获取 "添加水印" 操作的字体颜色（例如，"#000000"）

**Parameters**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| colorBuffer | 输出缓冲区字体颜色将被复制到中。 |
| colorBufferSize | ColorBuffer 的大小（字符数）。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 colorBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualColorSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColor(
    const mip_cc_action action,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasecontentlabel"></a>MIP_CC_ReleaseContentLabel

释放与内容标签关联的资源

**Parameters**

参数 | 说明
|---|---|
| contentLabel | 要释放的标签 |

```c
void MIP_CC_ReleaseContentLabel(mip_cc_content_label contentLabel);
```

## <a name="mip_cc_contentlabel_getcreationtime"></a>MIP_CC_ContentLabel_GetCreationTime

获取应用标签的时间

**Parameters**

参数 | 说明
|---|---|
| contentLabel | Label |
| creationTime | 输出将标签应用于文档的时间（从 epoch 开始到几秒） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ContentLabel_GetCreationTime(
    const mip_cc_content_label contentLabel,
    int64_t* creationTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getassignmentmethod"></a>MIP_CC_ContentLabel_GetAssignmentMethod

获取标签分配方法

**Parameters**

参数 | 说明
|---|---|
| contentLabel | Label |
| assignmentMethod | 输出分配方法（例如 "标准" 或 "特权"） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ContentLabel_GetAssignmentMethod(
    const mip_cc_content_label contentLabel,
    mip_cc_label_assignment_method* assignmentMethod,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getextendedproperties"></a>MIP_CC_ContentLabel_GetExtendedProperties

获取扩展属性

**Parameters**

参数 | 说明
|---|---|
| contentLabel | Label |
| properties | 输出扩展属性的字典，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "properties" 变量 MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_ContentLabel_GetExtendedProperties(
    const mip_cc_content_label contentLabel,
    mip_cc_metadata_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_isprotectionappliedfromlabel"></a>MIP_CC_ContentLabel_IsProtectionAppliedFromLabel

获取一个标签是否应用了保护。

**Parameters**

参数 | 说明
|---|---|
| contentLabel | Label |
| isProtectionAppliedByLabel | 输出如果文档受到保护并且此标签显式应用了保护。 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ContentLabel_IsProtectionAppliedFromLabel(
    const mip_cc_content_label contentLabel,
    bool* isProtectionAppliedByLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getlabel"></a>MIP_CC_ContentLabel_GetLabel

从内容标签实例获取一般标签属性

**Parameters**

参数 | 说明
|---|---|
| contentLabel | Label |
| label | 输出泛型标签，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "label" 变量 MIP_CC_ReleaseLabel 

```c
mip_cc_result MIP_CC_ContentLabel_GetLabel(
    const mip_cc_content_label contentLabel,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getnamesize"></a>MIP_CC_CustomAction_GetNameSize

获取存储 "自定义" 操作名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| action | "自定义" 操作 |
| nameSize | 输出保留名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CustomAction_GetNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getname"></a>MIP_CC_CustomAction_GetName

获取 "自定义" 操作的名称

**Parameters**

参数 | 说明
|---|---|
| action | "自定义" 操作 |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_CustomAction_GetName(
    const mip_cc_action action,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getproperties"></a>MIP_CC_CustomAction_GetProperties

获取 "自定义" 操作的属性

**Parameters**

参数 | 说明
|---|---|
| action | "自定义" 操作 |
| properties | 输出属性字典，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "properties" 变量 MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CustomAction_GetProperties(
    const mip_cc_action action,
    mip_cc_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadata_callback"></a>mip_cc_metadata_callback

用于检索文档元数据的回调函数定义，按名称/前缀筛选

**Parameters**

参数 | 说明
|---|---|
| 姓名 | 要包含在结果中的元数据密钥名称数组 |
| namesSize | "名称" 数组中的值的数目 |
| namePrefixes | 要包含在结果中的元数据密钥名称前缀数组 |
| namePrefixesSize | "NamesPrefixes" 数组中的值的数目 |
| 上下文 | 从 API 调用以不透明形式传递到回调的应用程序上下文 |
| metadata | 输出由客户端应用程序创建的元数据键/值的字典。 此字典将由 MIP 发布。 |

```c
MIP_CC_CALLBACK(mip_cc_metadata_callback,
    void,
    const char**,
    const int64_t,
    const char**,
    const int64_t,
    const void*,
    mip_cc_metadata_dictionary*);
```

## <a name="mip_cc_releaselabel"></a>MIP_CC_ReleaseLabel

释放与标签关联的资源

**Parameters**

参数 | 说明
|---|---|
| label | 要释放的标签 |

```c
void MIP_CC_ReleaseLabel(mip_cc_label label);
```

## <a name="mip_cc_label_getid"></a>MIP_CC_Label_GetId

获取标签 ID

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| 面部 | 输出标签 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetId(
    const mip_cc_label label,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getnamesize"></a>MIP_CC_Label_GetNameSize

获取存储名称所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| nameSize | 输出保留名称的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetNameSize(
    const mip_cc_label label,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getname"></a>MIP_CC_Label_GetName

获取标签名称

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | NameBuffer 的大小（字符数）。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 nameBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualNameSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_Label_GetName(
    const mip_cc_label label,
    char* nameBuffer,
    const int64_t nameBufferSize,
    int64_t* actualNameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescriptionsize"></a>MIP_CC_Label_GetDescriptionSize

获取存储说明所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| descriptionSize | 输出要保存的缓冲区大小说明（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetDescriptionSize(
    const mip_cc_label label,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescription"></a>MIP_CC_Label_GetDescription

获取标签说明

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| descriptionBuffer | 输出将此说明复制到的缓冲区。 |
| descriptionBufferSize | DescriptionBuffer 的大小（字符数）。 |
| actualDescriptionSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 descriptionBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualDescriptionSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_Label_GetDescription(
    const mip_cc_label label,
    char* descriptionBuffer,
    const int64_t descriptionBufferSize,
    int64_t* actualDescriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolorsize"></a>MIP_CC_Label_GetColorSize

获取存储颜色所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| colorSize | 输出要保存颜色的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetColorSize(
    const mip_cc_label label,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolor"></a>MIP_CC_Label_GetColor

获取标签颜色

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| colorBuffer | 输出缓冲区，颜色将被复制到中（#RRGGBB 格式）。 |
| colorBufferSize | ColorBuffer 的大小（字符数）。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 colorBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualColorSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_Label_GetColor(
    const mip_cc_label label,
    char* colorBuffer,
    const int64_t colorBufferSize,
    int64_t* actualColorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getsensitivity"></a>MIP_CC_Label_GetSensitivity

获取标签的敏感度级别。 较高的值意味着更敏感。

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| sensitivity | 输出敏感度级别 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetSensitivity(
    const mip_cc_label label,
    int32_t* sensitivity,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltipsize"></a>MIP_CC_Label_GetTooltipSize

获取存储工具提示所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| tooltipSize | 输出要保存 tooltip 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltip"></a>MIP_CC_Label_GetTooltip

获取标签工具提示

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| tooltipBuffer | 输出将工具提示复制到的缓冲区。 |
| tooltipBufferSize | TooltipBuffer 的大小（字符数）。 |
| actualTooltipSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 tooltipBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualTooltipSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_Label_GetTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltipsize"></a>MIP_CC_Label_GetAutoTooltipSize

获取存储自动分类工具提示所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| tooltipSize | 输出要保存 tooltip 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetAutoTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltip"></a>MIP_CC_Label_GetAutoTooltip

获取标签自动分类工具提示

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| tooltipBuffer | 输出将工具提示复制到的缓冲区。 |
| tooltipBufferSize | TooltipBuffer 的大小（字符数）。 |
| actualTooltipSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 tooltipBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualTooltipSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_Label_GetAutoTooltip(
    const mip_cc_label label,
    char* tooltipBuffer,
    const int64_t tooltipBufferSize,
    int64_t* actualTooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_isactive"></a>MIP_CC_Label_IsActive

获取一个标签是否处于活动状态

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| isActive | 输出标签是否被视为处于活动状态。 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：只能应用活动标签。 Inactivte 标签无法应用，仅用于显示目的。 

```c
mip_cc_result MIP_CC_Label_IsActive(
    const mip_cc_label label,
    bool* isActive,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getparent"></a>MIP_CC_Label_GetParent

获取父标签（如果有）

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| 父级 (parent) | 输出父标签（如果有）; 否则为 null |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetParent(
    const mip_cc_label label,
    mip_cc_label* parent,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildrensize"></a>MIP_CC_Label_GetChildrenSize

获取子标签的数目

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| childrenSize | 输出子级数量 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetChildrenSize(
    const mip_cc_label label,
    int64_t* childrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildren"></a>MIP_CC_Label_GetChildren

获取子标签

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| childrenBuffer | 输出Buffer，子标签将被复制到中。 子标签 |
| childrenBufferSize | ChildrenBuffer 的大小（以标签数为限）。 |
| actualChildrenSize | 输出写入缓冲区的子标签数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 childrenBuffer 为 null 或为空，则将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualChildrenSize 设置为所需的最小缓冲区大小 

```c
mip_cc_result MIP_CC_Label_GetChildren(
    const mip_cc_label label,
    mip_cc_label* childrenBuffer,
    const int64_t childrenBufferSize,
    int64_t* actualChildrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcustomsettings"></a>MIP_CC_Label_GetCustomSettings

获取标签的策略定义的自定义设置

**Parameters**

参数 | 说明
|---|---|
| label | Label |
| 设置 | 输出调用方拥有的设置字典 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "settings" 变量 MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_Label_GetCustomSettings(
    const mip_cc_label label,
    mip_cc_dictionary* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoremove"></a>MIP_CC_MetadataAction_GetMetadataToRemove

获取要移除的 "元数据" 操作的元数据

**Parameters**

参数 | 说明
|---|---|
| action | "metadata" 操作 |
| metadataNames | 输出要删除的元数据的键名，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "metadataNames" 变量必须由调用方释放，方法是调用 MIP_CC_ReleaseStringList @note在添加元数据之前删除元数据 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToRemove(
    const mip_cc_action action,
    mip_cc_string_list* metadataNames,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoadd"></a>MIP_CC_MetadataAction_GetMetadataToAdd

获取要添加的 "元数据" 操作的元数据

**Parameters**

参数 | 说明
|---|---|
| action | "metadata" 操作 |
| metadata | [输出] 要添加的元数据条目列表，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "metadata" 变量必须由调用方释放，方法是调用 MIP_CC_ReleaseDictionary @note在添加元数据之前应完成删除元数据 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToAdd(
    const mip_cc_action action,
    mip_cc_metadata_dictionary* metadata,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmetadatadictionary"></a>MIP_CC_CreateMetadataDictionary

创建字符串键/值的字典

**Parameters**

参数 | 说明
|---|---|
| entries | 元数据项数组 |
| 计数 | 元数据项的数目 |
| 字典 | 输出新创建的字典 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：必须通过调用 MIP_CC_ReleaseDictionary 释放 mip_cc_dictionary 

```c
mip_cc_result MIP_CC_CreateMetadataDictionary(
    const mip_cc_metadata_entry* entries,
    const int64_t count,
    mip_cc_metadata_dictionary* dictionary,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadatadictionary_getentries"></a>MIP_CC_MetadataDictionary_GetEntries

获取构成字典的元数据项

**Parameters**

参数 | 说明
|---|---|
| 字典 | 源字典 |
| entries | 输出元数据项数组、mip_cc_dictionary 对象拥有的内存 |
| 计数 | 输出元数据项的数目 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "条目" 的内存由 mip_cc_dictionary 对象拥有，因此不应独立释放 

```c
mip_cc_result MIP_CC_MetadataDictionary_GetEntries(
    const mip_cc_metadata_dictionary dictionary,
    mip_cc_metadata_entry** entries,
    int64_t* count,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasemetadatadictionary"></a>MIP_CC_ReleaseMetadataDictionary

释放与字典关联的资源

**Parameters**

参数 | 说明
|---|---|
| 字典 | 要释放的字典 |

```c
void MIP_CC_ReleaseMetadataDictionary(mip_cc_metadata_dictionary dictionary);
```

## <a name="mip_cc_releasepolicyengine"></a>MIP_CC_ReleasePolicyEngine

释放与策略引擎关联的资源

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 要释放的策略引擎 |

```c
void MIP_CC_ReleasePolicyEngine(mip_cc_policy_engine engine);
```

## <a name="mip_cc_policyengine_getengineidsize"></a>MIP_CC_PolicyEngine_GetEngineIdSize

获取引擎 ID 所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| idSize | 输出保留引擎 ID 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineIdSize(
    const mip_cc_policy_engine engine,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getengineid"></a>MIP_CC_PolicyEngine_GetEngineId

获取引擎 ID

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| idBuffer | 输出该 id 将被复制到中。 |
| idBufferSize | IdBuffer 的大小（字符数）。 |
| actualIdSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 idBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualIdSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetEngineId(
    const mip_cc_policy_engine engine,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourlsize"></a>MIP_CC_PolicyEngine_GetMoreInfoUrlSize

获取与策略引擎关联的客户端数据的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| moreInfoUrlSize | 输出客户端数据的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrlSize(
    const mip_cc_policy_engine engine,
    int64_t* moreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getmoreinfourl"></a>MIP_CC_PolicyEngine_GetMoreInfoUrl

获取与策略引擎关联的客户端数据

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| moreInfoUrlBuffer | 输出将客户端数据复制到其中的缓冲区 |
| moreInfoUrlBufferSize | MoreInfoUrlBuffer 的大小（字符数）。 |
| actualMoreInfoUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 moreInfoUrlBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualMoreInfoUrlSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetMoreInfoUrl(
    const mip_cc_policy_engine engine,
    char* moreInfoUrlBuffer,
    const int64_t moreInfoUrlBufferSize,
    int64_t* actualMoreInfoUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_islabelingrequired"></a>MIP_CC_PolicyEngine_IsLabelingRequired

获取策略是否指示必须标记文档。

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| isLabelingRequired | 输出策略是否规定必须标记文档 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_IsLabelingRequired(
    const mip_cc_policy_engine engine,
    bool* isLabelingRequired,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileidsize"></a>MIP_CC_PolicyEngine_GetPolicyFileIdSize

获取与策略引擎关联的客户端数据的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| policyFileIdSize | 输出客户端数据的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* policyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicyfileid"></a>MIP_CC_PolicyEngine_GetPolicyFileId

获取与策略引擎关联的客户端数据

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| policyFileIdBuffer | 输出将客户端数据复制到其中的缓冲区 |
| policyFileIdBufferSize | PolicyFileIdBuffer 的大小（字符数）。 |
| actualPolicyFileIdSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 policyFileIdBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualPolicyFileIdSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyFileId(
    const mip_cc_policy_engine engine,
    char* policyFileIdBuffer,
    const int64_t policyFileIdBufferSize,
    int64_t* actualPolicyFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileidsize"></a>MIP_CC_PolicyEngine_GetSensitivityFileIdSize

获取与策略引擎关联的客户端数据的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| sensitivityFileIdSize | 输出客户端数据的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileIdSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivityfileid"></a>MIP_CC_PolicyEngine_GetSensitivityFileId

获取与策略引擎关联的客户端数据

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| sensitivityFileIdBuffer | 输出将客户端数据复制到其中的缓冲区 |
| sensitivityFileIdBufferSize | SensitivityFileIdBuffer 的大小（字符数）。 |
| actualSensitivityFileIdSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 sensitivityFileIdBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualSensitivityFileIdSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityFileId(
    const mip_cc_policy_engine engine,
    char* sensitivityFileIdBuffer,
    const int64_t sensitivityFileIdBufferSize,
    int64_t* actualSensitivityFileIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_hasclassificationrules"></a>MIP_CC_PolicyEngine_HasClassificationRules

获取策略是否具有自动或建议规则

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| hasClassificationRules | 输出策略是否具有自动规则或建议规则 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_HasClassificationRules(
    const mip_cc_policy_engine engine,
    bool* hasClassificationRules,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlastpolicyfetchtime"></a>MIP_CC_PolicyEngine_GetLastPolicyFetchTime

获取上次提取策略的时间

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| lastPolicyFetchTime | 输出上次提取策略的时间（从 epoch 起的秒数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetLastPolicyFetchTime(
    const mip_cc_policy_engine engine,
    int64_t* lastPolicyFetchTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabelssize"></a>MIP_CC_PolicyEngine_GetSensitivityLabelsSize

获取与策略引擎关联的敏感度标签的数目

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| labelsSize | 输出标签数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabelsSize(
    const mip_cc_policy_engine engine,
    int64_t* labelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitylabels"></a>MIP_CC_PolicyEngine_GetSensitivityLabels

获取与策略引擎关联的敏感度标签

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| labelBuffer | 输出缓冲标签将被复制到中。 标签由客户端拥有 |
| labelBufferSize | LabelBuffer 的大小（以标签数为限）。 |
| actualLabelsSize | 输出写入缓冲区的标签数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 labelBuffer 为 null 或为空，则将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualLabelsSize 设置为所需的最小缓冲区大小 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityLabels(
    const mip_cc_policy_engine engine,
    mip_cc_label* labelBuffer,
    const int64_t labelBufferSize,
    int64_t* actualLabelsSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getlabelbyid"></a>MIP_CC_PolicyEngine_GetLabelById

按 ID 获取敏感度标签

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| 面部 | 标签 ID |
| label | 输出敏感度标签。 此值由调用方拥有，必须随 MIP_CC_ReleaseLabel 一起发布。 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetLabelById(
    const mip_cc_policy_engine engine,
    const char* labelId,
    mip_cc_label* label,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypessize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesSize

获取与策略引擎关联的敏感度类型的数目

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| sensitivityTypesSize | 输出敏感度类型的数目 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesSize(
    const mip_cc_policy_engine engine,
    int64_t* sensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypes"></a>MIP_CC_PolicyEngine_GetSensitivityTypes

获取与策略引擎关联的敏感度类型

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| sensitivityTypeBuffer | 输出缓冲区，敏感度类型将被复制到中。 敏感性 |
| sensitivityTypeBufferSize | SensitivityTypeBuffer 的大小（以敏感度类型的数量为位数）。 |
| actualSensitivityTypesSize | 输出写入缓冲区的敏感度类型的数目 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 sensitivityTypeBuffer 为 null 或为空，则将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualSensitivityTypesSize 设置为所需的最小缓冲区大小 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypes(
    const mip_cc_policy_engine engine,
    mip_cc_sensitivity_type* sensitivityTypeBuffer,
    const int64_t sensitivityTypeBufferSize,
    int64_t* actualSensitivityTypesSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_createpolicyhandler"></a>MIP_CC_PolicyEngine_CreatePolicyHandler

创建策略处理程序以执行策略相关的函数

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| isAuditDiscoveryEnabled | 是否启用审核发现 |
| 处理程序 (handler) | 输出新创建的策略处理程序实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_CreatePolicyHandler(
    const mip_cc_policy_engine engine,
    const bool isAuditDiscoveryEnabled,
    mip_cc_policy_handler* handler,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_sendapplicationauditevent"></a>MIP_CC_PolicyEngine_SendApplicationAuditEvent

将特定于应用程序的事件记录到审核管道

**Parameters**

参数 | 说明
|---|---|
| 级别 | 事件级别：信息/错误/警告 |
| eventType | 事件类型的说明 |
| eventData | 与事件关联的数据 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_SendApplicationAuditEvent(
    const mip_cc_policy_engine engine,
    const char* level,
    const char* eventType,
    const char* eventData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantidsize"></a>MIP_CC_PolicyEngine_GetTenantIdSize

获取租户 ID 的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| tenantIdSize | 输出租户 ID 的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantIdSize(
    const mip_cc_policy_engine engine,
    int64_t* tenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_gettenantid"></a>MIP_CC_PolicyEngine_GetTenantId

获取租户 ID

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| tenantIdBuffer | 输出将租户 ID 复制到的缓冲区。 |
| tenantIdBufferSize | TenantIdBuffer 的大小（字符数）。 |
| actualTenantIdSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 tenantIdBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualTenantIdSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetTenantId(
    const mip_cc_policy_engine engine,
    char* tenantIdBuffer,
    const int64_t tenantIdBufferSize,
    int64_t* actualTenantIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxmlsize"></a>MIP_CC_PolicyEngine_GetPolicyDataXmlSize

获取策略数据 xml 的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| xmlSize | 输出策略数据 xml 的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getpolicydataxml"></a>MIP_CC_PolicyEngine_GetPolicyDataXml

获取策略数据 xml

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| xmlBuffer | 输出将 xml 复制到的缓冲区。 |
| xmlBufferSize | XmlBuffer 的大小（字符数）。 |
| actualXmlSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 xmlBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualXmlSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetPolicyDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxmlsize"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize

获取敏感类型数据 xml 的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| xmlSize | 输出策略数据 xml 的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXmlSize(
    const mip_cc_policy_engine engine,
    int64_t* xmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getsensitivitytypesdataxml"></a>MIP_CC_PolicyEngine_GetSensitivityTypesDataXml

获取敏感类型数据 xml

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| xmlBuffer | 输出将 xml 复制到的缓冲区。 |
| xmlBufferSize | XmlBuffer 的大小（字符数）。 |
| actualXmlSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 xmlBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualXmlSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetSensitivityTypesDataXml(
    const mip_cc_policy_engine engine,
    char* xmlBuffer,
    const int64_t xmlBufferSize,
    int64_t* actualXmlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdatasize"></a>MIP_CC_PolicyEngine_GetClientDataSize

获取与策略引擎关联的客户端数据的大小

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| clientDataSize | 输出客户端数据的大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientDataSize(
    const mip_cc_policy_engine engine,
    int64_t* clientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyengine_getclientdata"></a>MIP_CC_PolicyEngine_GetClientData

获取与策略引擎关联的客户端数据

**Parameters**

参数 | 说明
|---|---|
| 引擎 | 策略引擎 |
| clientDataBuffer | 输出将客户端数据复制到其中的缓冲区 |
| clientDataBufferSize | ClientDataBuffer 的大小（字符数）。 |
| actualClientDataSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 clientDataBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualClientDataSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_PolicyEngine_GetClientData(
    const mip_cc_policy_engine engine,
    char* clientDataBuffer,
    const int64_t clientDataBufferSize,
    int64_t* actualClientDataSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createpolicyenginesettingswithidentity"></a>MIP_CC_CreatePolicyEngineSettingsWithIdentity

创建用于创建全新策略引擎的设置对象

**Parameters**

参数 | 说明
|---|---|
| identity | 将与 PolicyEngine 关联的标识 |
| clientData | 与引擎一起存储的可自定义客户端数据 |
| locale | 文本结果将输出到的区域设置 |
| loadSensitivityTypes | 是否还应加载敏感度类型数据（用于分类） |
| 设置 | 输出新创建的设置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：仅当应用程序需要稍后调用 MIP_CC_PolicyEngine_GetSensitivityTypes 时，"loadSensitivityTypes" 才应为 "true"。 否则，应为 false 以避免不必要的 HTTP 操作。 

```c
mip_cc_result MIP_CC_CreatePolicyEngineSettingsWithIdentity(
    const mip_cc_identity* identity,
    const char* clientData,
    const char* locale,
    bool loadSensitivityTypes,
    mip_cc_policy_engine_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setclientdata"></a>MIP_CC_PolicyEngineSettings_SetClientData

设置客户端数据，该数据将与此引擎透明存储并跨会话保存

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| clientData | 客户端数据 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetClientData(
    const mip_cc_policy_engine_settings settings,
    const char* clientData,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcustomsettings"></a>MIP_CC_PolicyEngineSettings_SetCustomSettings

配置自定义设置，用于功能的门和测试。

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| customSettings | 自定义设置的键/值对 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCustomSettings(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setsessionid"></a>MIP_CC_PolicyEngineSettings_SetSessionId

设置可用于关联日志和遥测的会话 ID

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| sessionID | 表示策略引擎生存期的会话 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetSessionId(
    const mip_cc_policy_engine_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloud"></a>MIP_CC_PolicyEngineSettings_SetCloud

设置影响所有服务请求的终结点 Url 的云

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| 云 | Cloud 标识符（默认值 = 未知） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果未指定 cloud，则默认为 "全局云"。 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloud(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_cloud cloud,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setcloudendpointbaseurl"></a>MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl

设置所有服务请求的基 URL

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| cloudEndpointBaseUrl | 基 URL （例如 "https://dataservice.protection.outlook.com"） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：此值将仅被读取，并且必须设置为 Cloud = MIP_CLOUD_CUSTOM 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetCloudEndpointBaseUrl(
    const mip_cc_policy_engine_settings settings,
    const char* cloudEndpointBaseUrl,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setdelegateduseremail"></a>MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail

设置委派的用户

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| delegatedUserEmail | 委托用户的电子邮件地址 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：当正在进行身份验证的用户/应用程序代表其他用户时，将指定委派的用户 

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetDelegatedUserEmail(
    const mip_cc_policy_engine_settings settings,
    const char* delegatedUserEmail,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyenginesettings_setlabelfilter"></a>MIP_CC_PolicyEngineSettings_SetLabelFilter

设置标签筛选器

**Parameters**

参数 | 说明
|---|---|
| 设置 | 引擎设置 |
| labelFilter | 表示标签筛选器的枚举，如果未设置，则默认值为 hyok，doublekeyencryption |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyEngineSettings_SetLabelFilter(
    const mip_cc_policy_engine_settings settings,
    const mip_cc_label_filter labelFilter,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyenginesettings"></a>MIP_CC_ReleasePolicyEngineSettings

释放与策略引擎设置关联的资源

**Parameters**

参数 | 说明
|---|---|
| 设置 | 要释放的策略引擎设置 |

```c
void MIP_CC_ReleasePolicyEngineSettings(mip_cc_policy_engine_settings settings);
```

## <a name="mip_cc_releasepolicyhandler"></a>MIP_CC_ReleasePolicyHandler

释放与策略处理程序关联的资源

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 要发布的策略处理程序 |

```c
void MIP_CC_ReleasePolicyHandler(mip_cc_policy_handler handler);
```

## <a name="mip_cc_policyhandler_getsensitivitylabel"></a>MIP_CC_PolicyHandler_GetSensitivityLabel

获取文档的当前标签

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 策略处理程序 |
| documentState | 文档状态 |
| 上下文 | 应用程序上下文不透明地转发到任何回调 |
| contentLabel | 当前应用于文档的标签 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyHandler_GetSensitivityLabel(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const void* context,
    mip_cc_content_label* contentLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_computeactions"></a>MIP_CC_PolicyHandler_ComputeActions

根据所提供的状态执行策略规则并确定相应的操作

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 策略处理程序 |
| documentState | 文档状态 |
| applicationState | 应用程序操作状态 |
| 上下文 | 应用程序上下文不透明地转发到任何回调 |
| actionResult | 输出应用程序应执行的操作，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "actionResult" 变量 MIP_CC_ReleaseActionResult 

```c
mip_cc_result MIP_CC_PolicyHandler_ComputeActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_action_result* actionResult,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyhandler_notifycommittedactions"></a>MIP_CC_PolicyHandler_NotifyCommittedActions

应用计算的操作并将数据提交到磁盘后，由应用程序调用

**Parameters**

参数 | 说明
|---|---|
| 处理程序 (handler) | 策略处理程序 |
| documentState | 文档状态 |
| applicationState | 应用程序操作状态 |
| 上下文 | 应用程序上下文不透明地转发到任何回调 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：若要传输完整的标签审核数据，则需要调用此函数。 

```c
mip_cc_result MIP_CC_PolicyHandler_NotifyCommittedActions(
    const mip_cc_policy_handler handler,
    const mip_cc_document_state* documentState,
    const mip_cc_application_action_state* applicationState,
    const void* context,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofile_acquireauthtoken"></a>MIP_CC_PolicyProfile_AcquireAuthToken

触发身份验证回拨

**Parameters**

参数 | 说明
|---|---|
| profile | 配置文件 |
| 云 | Azure 云 |
| authCallback | 要调用的身份验证回调 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： MIP 不会缓存或使用 auth 委托返回的值执行任何其他操作。 对于在 MIP 请求身份验证令牌之前未 "登录" 的应用程序，建议使用此函数。 它允许应用程序在 MIP 实际需要一个令牌之前提取令牌。 

```c
mip_cc_result MIP_CC_PolicyProfile_AcquireAuthToken(
    const mip_cc_policy_profile profile,
    const mip_cc_cloud cloud,
    const mip_cc_auth_callback authCallback,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_loadpolicyprofile"></a>MIP_CC_LoadPolicyProfile

加载配置文件

**Parameters**

参数 | 说明
|---|---|
| 设置 | 个人资料设置 |
| profile | 输出新创建的策略配置文件实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_LoadPolicyProfile(
    const mip_cc_policy_profile_settings settings,
    mip_cc_policy_profile* profile,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofile"></a>MIP_CC_ReleasePolicyProfile

释放与策略配置文件关联的资源

**Parameters**

参数 | 说明
|---|---|
| profile | 要释放的策略配置文件 |

```c
void MIP_CC_ReleasePolicyProfile(mip_cc_policy_profile profile);
```

## <a name="mip_cc_createpolicyprofilesettings"></a>MIP_CC_CreatePolicyProfileSettings

创建用于创建策略配置文件的设置对象

**Parameters**

参数 | 说明
|---|---|
| mipContext | 跨所有配置文件共享的全局上下文 |
| cacheStorageType | 存储缓存配置 |
| authCallback | 要用于身份验证的回调对象，由客户端应用程序实现 |
| 设置 | 输出新创建的设置实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreatePolicyProfileSettings(
    const mip_cc_mip_context mipContext,
    const mip_cc_cache_storage_type cacheStorageType,
    const mip_cc_auth_callback authCallback,
    mip_cc_policy_profile_settings* settings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setsessionid"></a>MIP_CC_PolicyProfileSettings_SetSessionId

设置可用于关联日志和遥测的会话 ID

**Parameters**

参数 | 说明
|---|---|
| 设置 | 个人资料设置 |
| sessionID | 表示策略配置文件生存期的会话 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetSessionId(
    const mip_cc_policy_profile_settings settings,
    const char* sessionId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_sethttpdelegate"></a>MIP_CC_PolicyProfileSettings_SetHttpDelegate

用客户端自己的替换默认的 HTTP 堆栈

**Parameters**

参数 | 说明
|---|---|
| 设置 | 将向其分配 HTTP 委托的配置文件设置 |
| httpDelegate | 由客户端应用程序实现的 HTTP 回调实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetHttpDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_http_delegate httpDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_settaskdispatcherdelegate"></a>MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate

用客户端自己的替换默认的异步任务调度程序

**Parameters**

参数 | 说明
|---|---|
| 设置 | 任务调度程序委托将被分配到的配置文件设置 |
| taskDispatcherDelegate | 由客户端应用程序实现的任务调度程序回调实例 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetTaskDispatcherDelegate(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_policyprofilesettings_setcustomsettings"></a>MIP_CC_PolicyProfileSettings_SetCustomSettings

配置自定义设置，用于功能的门和测试。

**Parameters**

参数 | 说明
|---|---|
| 设置 | 个人资料设置 |
| customSettings | 自定义设置的键/值对 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_PolicyProfileSettings_SetCustomSettings(
    const mip_cc_policy_profile_settings settings,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasepolicyprofilesettings"></a>MIP_CC_ReleasePolicyProfileSettings

释放与策略配置文件设置关联的资源

**Parameters**

参数 | 说明
|---|---|
| 设置 | 要释放的策略配置文件设置 |

```c
void MIP_CC_ReleasePolicyProfileSettings(mip_cc_policy_profile_settings profileSettings);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize

获取存储双密钥加密 url 所需的缓冲区大小。

**Parameters**

参数 | 说明
|---|---|
| action | "使用双键进行即席策略保护" 操作 |
| urlSize | 输出用于保存 url 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl

获取双密钥加密 url

**Parameters**

参数 | 说明
|---|---|
| action | "使用双键进行即席策略保护" 操作 |
| urlBuffer | 输出将 url 复制到的缓冲区。 |
| urlBufferSize | UrlBuffer 的大小（字符数）。 |
| actualUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 urlBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualUrlSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplateaction_gettemplateid"></a>MIP_CC_ProtectByTemplateAction_GetTemplateId

获取 "按模板保护" 操作的模板 ID

**Parameters**

参数 | 说明
|---|---|
| action | "按模板保护" 操作 |
| templateId | 输出定义保护的模板的 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectByTemplateAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_gettemplateid"></a>MIP_CC_ProtectByTemplateDkAction_GetTemplateId

获取 "使用双键保护模板" 操作的模板 ID

**Parameters**

参数 | 说明
|---|---|
| action | "按模板保护" 操作 |
| templateId | 输出定义保护的模板的 ID |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetTemplateId(
    const mip_cc_action action,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize

获取存储双密钥加密 url 所需的缓冲区大小。

**Parameters**

参数 | 说明
|---|---|
| action | "使用双键的模板保护" 操作 |
| urlSize | 输出用于保存 url 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectbytemplatedkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl

获取双密钥加密 url

**Parameters**

参数 | 说明
|---|---|
| action | "使用双键的模板保护" 操作 |
| urlBuffer | 输出将 url 复制到的缓冲区。 |
| urlBufferSize | UrlBuffer 的大小（字符数）。 |
| actualUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 urlBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualUrlSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectByTemplateDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize

获取存储双密钥加密 url 所需的缓冲区大小。

**Parameters**

参数 | 说明
|---|---|
| action | "不使用双键值转发策略" 操作 |
| urlSize | 输出用于保存 url 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl

获取双密钥加密 url

**Parameters**

参数 | 说明
|---|---|
| action | "不使用双键值转发策略" 操作 |
| urlBuffer | 输出将 url 复制到的缓冲区。 |
| urlBufferSize | UrlBuffer 的大小（字符数）。 |
| actualUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 urlBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualUrlSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl(
    const mip_cc_action action,
    char* urlBuffer,
    const int64_t urlBufferSize,
    int64_t* actualUrlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentfooteraction_getuielementnames"></a>MIP_CC_RemoveContentFooterAction_GetUIElementNames

获取要移除的 "删除内容脚注" 操作的 UI 元素名称

**Parameters**

参数 | 说明
|---|---|
| action | "删除内容脚注" 操作 |
| 姓名 | 输出要移除的 UI 元素的名称，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：名称变量必须由调用方释放，方法是调用 MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentFooterAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removecontentheaderaction_getuielementnames"></a>MIP_CC_RemoveContentHeaderAction_GetUIElementNames

获取要移除的 "删除内容标头" 操作的 UI 元素名称

**Parameters**

参数 | 说明
|---|---|
| action | "删除内容标头" 操作 |
| 姓名 | 输出要移除的 UI 元素的名称，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：名称变量必须由调用方释放，方法是调用 MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveContentHeaderAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_removewatermarkaction_getuielementnames"></a>MIP_CC_RemoveWatermarkAction_GetUIElementNames

获取要移除的 "删除水印" 操作的 UI 元素名称

**Parameters**

参数 | 说明
|---|---|
| action | "删除水印页脚" 操作 |
| 姓名 | 输出要移除的 UI 元素的名称，由调用方拥有的内存 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：名称变量必须由调用方释放，方法是调用 MIP_CC_ReleaseStringList 

```c
mip_cc_result MIP_CC_RemoveWatermarkAction_GetUIElementNames(
    const mip_cc_action action,
    mip_cc_string_list* names,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releasesensitivitytype"></a>MIP_CC_ReleaseSensitivityType

释放与敏感度类型关联的资源

**Parameters**

参数 | 说明
|---|---|
| sensitivityType | 要释放的敏感度类型 |

```c
void MIP_CC_ReleaseSensitivityType(mip_cc_sensitivity_type sensitivityType);
```

## <a name="mip_cc_sensitivitytype_getrulepackageidsize"></a>MIP_CC_SensitivityType_GetRulePackageIdSize

获取存储敏感度类型的规则包 ID 所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| idSize | 输出保留规则包 ID 的缓冲区大小（字符数） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageIdSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackageid"></a>MIP_CC_SensitivityType_GetRulePackageId

获取敏感度类型的规则包 ID

**Parameters**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| idBuffer | 输出该 ID 将被复制到中。 |
| idBufferSize | IdBuffer 的大小（字符数）。 |
| actualIdSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 idBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualIdSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageId(
    const mip_cc_sensitivity_type sensitivityType,
    char* idBuffer,
    const int64_t idBufferSize,
    int64_t* actualIdSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackagesize"></a>MIP_CC_SensitivityType_GetRulePackageSize

获取存储敏感度类型的规则包所需的缓冲区大小

**Parameters**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| rulePackageSize | 输出保留规则包的缓冲区大小（以字符数为限） |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* rulePackageSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackage"></a>MIP_CC_SensitivityType_GetRulePackage

获取敏感度类型的规则包

**Parameters**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| rulePackageBuffer | 输出将规则包复制到的缓冲区。 |
| rulePackageBufferSize | RulePackageBuffer 的大小（字符数）。 |
| actualRulePackageSize | 输出写入缓冲区的字符数 |
| errorInfo | 输出可有可无如果操作结果为错误，则为失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：如果 rulePackageBuffer 为 null 或为空，将返回 MIP_RESULT_ERROR_INSUFFICIENT_BUFFER，并将 actualRulePackageSize 设置为所需的最小缓冲区大小。 

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackage(
    const mip_cc_sensitivity_type sensitivityType,
    char* rulePackageBuffer,
    const int64_t rulePackageBufferSize,
    int64_t* actualRulePackageSize,
    mip_cc_error* errorInfo);
```

