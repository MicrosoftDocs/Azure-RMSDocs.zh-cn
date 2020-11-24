---
title: 函数
description: 函数。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 9/22/2020
ms.openlocfilehash: 8cb8d6550ecdc0d7ea342c3e6484a7a23b7f590d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565259"
---
# <a name="functions"></a>函数

## <a name="mip_cc_auth_callback"></a>mip_cc_auth_callback

用于获取 OAuth2 标记的回调函数定义

**参数**

参数 | 说明
|---|---|
| identity | 要获取其令牌的电子邮件地址 |
| challenge | OAuth2 质询 |
| 上下文 | 传递给导致此身份验证回调的 MIP API 的不透明应用程序上下文 |
| tokenBuffer | 输出要将令牌复制到其中的缓冲区。 如果为 null，则将填充 "actualTokenSize"，但 |
| tokenBufferSize | 输出缓冲区的大小 (（以字节为单位）)  |
| actualTokenSize | 输出标记的实际大小 (（以字节为单位）)  |

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

**参数**

参数 | 描述
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

**参数**

参数 | 说明
|---|---|
| entries | 键/值对的数组 |
| count | 键/值对的数目 |
| 字典 | 输出新创建的字典 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| 字典 | 源字典 |
| entries | 输出键/值对的数组、mip_cc_dictionary 对象拥有的内存 |
| count | 输出键/值对的数目 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| 字典 | 要释放的字典 |

```c
void MIP_CC_ReleaseDictionary(mip_cc_dictionary dictionary);
```

## <a name="mip_cc_http_send_callback_fn"></a>mip_cc_http_send_callback_fn

发出 HTTP 请求的回调函数定义

**参数**

参数 | 说明
|---|---|
| request | 要由应用程序执行的 HTTP 请求 |
| 上下文 | 传递给由此 HTTP 请求导致的 MIP API 调用的不透明上下文 |

```c
MIP_CC_CALLBACK(mip_cc_http_send_callback_fn,
    void,
    const mip_cc_http_request*,
    const void*);
```

## <a name="mip_cc_http_cancel_callback_fn"></a>mip_cc_http_cancel_callback_fn

用于取消 HTTP 请求的回调函数定义

**参数**

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

**参数**

参数 | 说明
|---|---|
| sendCallback | 用于发出 HTTP 请求的函数指针 |
| cancelCallback | 用于取消 HTTP 请求的函数指针 |
| httpDelegate | 输出HTTP 委托对象的句柄 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

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

**参数**

参数 | 说明
|---|---|
| httpDelegate | 要释放的 HTTP 委托 |

```c
void MIP_CC_ReleaseHttpDelegate(mip_cc_http_delegate httpDelegate);
```

## <a name="mip_cc_logger_init_callback_fn"></a>mip_cc_logger_init_callback_fn

记录器初始化的回调函数定义

**参数**

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

**参数**

参数 | 说明
|---|---|
| 级别 | log 语句的日志级别。 |
| message | log 语句的消息。 |
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

**参数**

参数 | 说明
|---|---|
| initCallback | 用于初始化的函数指针 |
| flushCallback | 用于刷新日志的函数指针 |
| writeCallback | 用于写入 log 语句的函数指针 |
| loggerDelegate | 输出记录器委托对象的句柄 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| loggerDelegate | 要释放的记录器委托 |

```c
void MIP_CC_ReleaseLoggerDelegate(mip_cc_logger_delegate loggerDelegate);
```

## <a name="mip_cc_createmipcontext"></a>MIP_CC_CreateMipContext

创建 MIP 上下文以管理所有配置文件实例中共享的状态

**参数**

参数 | 说明
|---|---|
| applicationInfo | 有关使用保护 SDK 的应用程序的信息 |
| path | 用于存储日志记录、遥测和其他保护宣传品的文件路径 |
| logLevel | Miplog 的最小日志级别 |
| isOfflineOnly | 启用/禁用网络操作 (脱机时不支持的所有操作)  |
| loggerDelegateOverride |  (可选) 记录器替代实现 |
| telemetryOverride |  (可选) 重写遥测设置。 如果为 NULL，则将使用默认设置 |
| mipContext | 输出新创建的 MIP 上下文实例 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| applicationInfo | 有关使用保护 SDK 的应用程序的信息 |
| path | 用于存储日志记录、遥测和其他保护宣传品的文件路径 |
| logLevel | Miplog 的最小日志级别 |
| isOfflineOnly | 启用/禁用网络操作 (脱机时不支持的所有操作)  |
| loggerDelegateOverride |  (可选) 记录器替代实现 |
| telemetryOverride |  (可选) 重写遥测设置。 如果为 NULL，则将使用默认设置 |
| featureSettings |  (可选) 自定义功能重写数组 |
| featureSettingsSize | 自定义功能的大小会重写 # of 重写 ()  |
| mipContext | 输出新创建的 MIP 上下文实例 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| mipContext | 要释放的 MIP 上下文 |

```c
void MIP_CC_ReleaseMipContext(mip_cc_mip_context mipContext);
```

## <a name="mip_cc_protectiondescriptor_getprotectiontype"></a>MIP_CC_ProtectionDescriptor_GetProtectionType

获取保护类型，无论其是否由 RMS 模板定义

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| protectionType | 输出保护类型 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetProtectionType(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_protection_type* protectionType,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getownersize"></a>MIP_CC_ProtectionDescriptor_GetOwnerSize

获取存储所有者所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| ownerSize | 输出保留所有者 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetOwnerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* ownerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getowner"></a>MIP_CC_ProtectionDescriptor_GetOwner

获取保护所有者

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| ownerBuffer | 输出将所有者复制到的缓冲区。 |
| ownerBufferSize | 大小 (ownerBuffer 中的字符数) 。 |
| actualOwnerSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| nameSize | 输出要保留名称 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetNameSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getname"></a>MIP_CC_ProtectionDescriptor_GetName

获取保护名称

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| descriptionSize | 输出要保持其说明 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDescriptionSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdescription"></a>MIP_CC_ProtectionDescriptor_GetDescription

获取保护说明

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| descriptionBuffer | 输出将此说明复制到的缓冲区。 |
| descriptionBufferSize | 大小 (descriptionBuffer 中的字符数) 。 |
| actualDescriptionSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| templateId | 输出与保护关联的模板 ID |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetTemplateId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getlabelid"></a>MIP_CC_ProtectionDescriptor_GetLabelId

获取标签 ID

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| 面部 | 输出与保护关联的标签 ID |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetLabelId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentid"></a>MIP_CC_ProtectionDescriptor_GetContentId

获取内容 ID

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| Id 为 | 输出与保护关联的内容 ID |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentId(
    const mip_cc_protection_descriptor protectionDescriptor,
    mip_cc_guid* contentId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doescontentexpire"></a>MIP_CC_ProtectionDescriptor_DoesContentExpire

获取内容是否具有过期时间

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| doesContentExpire | 输出内容是否过期 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesContentExpire(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesContentExpire,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getcontentvaliduntil"></a>MIP_CC_ProtectionDescriptor_GetContentValidUntil

从 epoch 开始，获取保护过期时间 (秒) 

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| contentValidUntil | 输出内容过期时间 (自 epoch 以来的秒数)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetContentValidUntil(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* contentValidUntil,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_doesallowofflineaccess"></a>MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess

获取是否允许脱机访问

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| doesAllowOfflineAccess | 输出是否允许脱机访问 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_DoesAllowOfflineAccess(
    const mip_cc_protection_descriptor protectionDescriptor,
    bool* doesAllowOfflineAccess,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrersize"></a>MIP_CC_ProtectionDescriptor_GetReferrerSize

获取存储引用站点所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| referrerSize | 输出用于保存引用 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetReferrerSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* referrerSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getreferrer"></a>MIP_CC_ProtectionDescriptor_GetReferrer

获取保护引用

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| referrerBuffer | 输出将引用的缓冲区复制到中。 |
| referrerBufferSize | 大小 (referrerBuffer 中的字符数) 。 |
| actualReferrerSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| url | 输出用于保存双引号 (的缓冲区大小)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectionDescriptor_GetDoubleKeyUrlSize(
    const mip_cc_protection_descriptor protectionDescriptor,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectiondescriptor_getdoublekeyurl"></a>MIP_CC_ProtectionDescriptor_GetDoubleKeyUrl

获取双键 URL

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| urlBuffer | 输出将 url 复制到的缓冲区。 |
| urlBufferSize | 大小 (urlBuffer 中的字符数) 。 |
| actualUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 要发布的保护描述符 |

```c
void MIP_CC_ReleaseProtectionDescriptor(mip_cc_protection_descriptor protectionDescriptor);
```

## <a name="mip_cc_createstringlist"></a>MIP_CC_CreateStringList

创建字符串列表

**参数**

参数 | 说明
|---|---|
| 字符串 | 字符串数组 |
| count | 字符串数 |
| stringList | 输出新创建的字符串列表 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| stringList | 源字符串列表 |
| 字符串 | 输出字符串数组、mip_cc_string_list 对象拥有的内存 |
| count | 输出字符串数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| stringList | 要释放的字符串列表 |

```c
void MIP_CC_ReleaseStringList(mip_cc_string_list stringList);
```

## <a name="mip_cc_dispatch_task_callback_fn"></a>mip_cc_dispatch_task_callback_fn

用于调度异步任务的回调函数定义

**参数**

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

**参数**

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

**参数**

参数 | 说明
|---|---|
| dispatchTaskCallback | 用于调度异步任务的函数指针 |
| cancelTaskCallback | 用于取消后台任务的函数指针 |
| cancelAllTasksCallback | 用于取消所有后台任务的函数指针 |
| taskDispatcher | 输出任务调度程序委托对象的句柄 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

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

**参数**

参数 | 说明
|---|---|
| taskDispatcher | 要释放的任务调度程序委托 |

```c
void MIP_CC_ReleaseTaskDispatcherDelegate(mip_cc_task_dispatcher_delegate taskDispatcher);
```

## <a name="mip_cc_createtelemetryconfiguration"></a>MIP_CC_CreateTelemetryConfiguration

创建用于创建保护配置文件的设置对象

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 输出新创建的包含默认设置的遥测配置实例 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CreateTelemetryConfiguration(
    mip_cc_telemetry_configuration* telemetryConfig,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethostname"></a>MIP_CC_TelemetryConfiguration_SetHostName

设置将替代内部遥测设置的遥测主机名

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| hostName | 主机名 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：当客户端应用程序使用同一个 ARIA/1DS 遥测组件，并希望其内部遥测设置 (缓存、日志记录、优先级等，而不是使用 MIP 的默认设置时，将设置此属性 ) 。 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetHostName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* hostName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setlibraryname"></a>MIP_CC_TelemetryConfiguration_SetLibraryName

设置遥测共享库替代

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| libraryName | 实现 Aria/1DS SDK 的 C API 的 DLL 的名称 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：当客户端具有实现 ARIA/1DS SDK C API 的现有遥测 DLL （应使用而不是 mip_ClientTelemetry.dll）时，将设置此属性。 

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetLibraryName(
    const mip_cc_telemetry_configuration telemetryConfig,
    const char* libraryName,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_sethttpdelegate"></a>MIP_CC_TelemetryConfiguration_SetHttpDelegate

重写客户端自己的默认遥测 HTTP 堆栈

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| httpDelegate | 由客户端应用程序实现的 HTTP 回调实例 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| taskDispatcherDelegate | 由客户端应用程序实现的任务调度程序回调实例 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetTaskDispatcherDelegate(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_task_dispatcher_delegate taskDispatcherDelegate,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_setisnetworkdetectionenabled"></a>MIP_CC_TelemetryConfiguration_SetIsNetworkDetectionEnabled

设置是否允许遥测组件在后台线程上 ping 网络状态

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isCachingEnabled | 是否允许遥测组件在后台线程上 ping 网络状态 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isCachingEnabled | 是否允许遥测组件将缓存写入磁盘 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isTraceLoggingEnabled | 是否允许遥测组件将日志写入磁盘 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| isTelemetryOptedOut | 应用程序/用户是否已选择不使用可选遥测 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| customSettings | 自定义遥测设置 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TelemetryConfiguration_SetCustomSettings(
    const mip_cc_telemetry_configuration telemetryConfig,
    const mip_cc_dictionary customSettings,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_telemetryconfiguration_addmaskedproperty"></a>MIP_CC_TelemetryConfiguration_AddMaskedProperty

将遥测属性设置为屏蔽

**参数**

参数 | 说明
|---|---|
| telemetryConfig | 遥测配置 |
| eventName | 事件名称 |
| propertyName | 属性名称 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| profileSettings | 要发布的保护配置文件设置 |

```c
void MIP_CC_ReleaseTelemetryConfiguration(mip_cc_telemetry_configuration telemetryConfig);
```

## <a name="mip_cc_templatedescriptor_getid"></a>MIP_CC_TemplateDescriptor_GetId

获取模板 ID

**参数**

参数 | 说明
|---|---|
| protectionDescriptor | 与受保护的内容关联的描述符 |
| templateId | 输出与保护关联的模板 ID |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetId(
    const mip_cc_template_descriptor protectionDescriptor,
    mip_cc_guid* templateId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getnamesize"></a>MIP_CC_TemplateDescriptor_GetNameSize

获取存储名称所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| nameSize | 输出要保留名称 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetNameSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getname"></a>MIP_CC_TemplateDescriptor_GetName

获取模板名称

**参数**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| descriptionSize | 输出要保持其说明 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_TemplateDescriptor_GetDescriptionSize(
    const mip_cc_template_descriptor templateDescriptor,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_templatedescriptor_getdescription"></a>MIP_CC_TemplateDescriptor_GetDescription

获取模板说明

**参数**

参数 | 说明
|---|---|
| templateDescriptor | 与模板关联的描述符 |
| descriptionBuffer | 输出将此说明复制到的缓冲区。 |
| descriptionBufferSize | 大小 (descriptionBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| templateDescriptor | 要发布的模板描述符 |

```c
void MIP_CC_ReleaseTemplateDescriptor(mip_cc_template_descriptor templateDescriptor);
```

## <a name="mip_cc_actionresult_getactions"></a>MIP_CC_ActionResult_GetActions

获取构成操作结果的操作

**参数**

参数 | 说明
|---|---|
| actionResult | 源操作结果 |
| actions | 输出操作数组、由 mip_cc_action_result 对象拥有的内存 |
| count | 输出键/值对的数目 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| actionResult | 要释放的操作结果 |

```c
void MIP_CC_ReleaseActionResult(mip_cc_action_result actionResult);
```

## <a name="mip_cc_addcontentfooteraction_getuielementnamesize"></a>MIP_CC_AddContentFooterAction_GetUIElementNameSize

获取存储 "添加内容脚注" 操作的 UI 元素名称所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameSize | 输出用于保存 UI 元素名称的缓冲区大小（以字符数为 ()  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getuielementname"></a>MIP_CC_AddContentFooterAction_GetUIElementName

获取 "添加内容脚注" 操作的 UI 元素名称

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameBuffer | 输出将 UI 元素名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameSize | 输出要保存文本 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_gettext"></a>MIP_CC_AddContentFooterAction_GetText

获取 "添加内容脚注" 操作的文本

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| textBuffer | 输出Buffer 文本将复制到中。 |
| textBufferSize | 值的大小 (textBuffer) 的字符数。 |
| actualTextSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameSize | 输出保留字符数 (的缓冲区大小)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontname"></a>MIP_CC_AddContentFooterAction_GetFontName

获取 "添加内容脚注" 操作的字体名称

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| nameBuffer | 输出将字体名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| fontSize | 输出字号 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolorsize"></a>MIP_CC_AddContentFooterAction_GetFontColorSize

获取存储 "添加内容脚注" 操作字体颜色所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| colorSize | 输出用于保存字体颜色的缓冲区大小 (字符数)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getfontcolor"></a>MIP_CC_AddContentFooterAction_GetFontColor

获取 "添加内容脚注" 操作的字体颜色 (例如 "#000000" ) 

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| colorBuffer | 输出缓冲区字体颜色将被复制到中。 |
| colorBufferSize | 大小 (colorBuffer 中的字符数) 。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| 对齐 (alignment) | 输出关联 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentfooteraction_getmargin"></a>MIP_CC_AddContentFooterAction_GetMargin

获取边距大小

**参数**

参数 | 说明
|---|---|
| action | "添加内容页脚" 操作 |
| marginSize | 输出边距大小 (毫米)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentFooterAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementnamesize"></a>MIP_CC_AddContentHeaderAction_GetUIElementNameSize

获取存储 "添加内容标头" 操作的 UI 元素名称所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameSize | 输出用于保存 UI 元素名称的缓冲区大小（以字符数为 ()  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getuielementname"></a>MIP_CC_AddContentHeaderAction_GetUIElementName

获取 "添加内容标头" 操作的 UI 元素名称

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameBuffer | 输出将 UI 元素名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameSize | 输出要保存文本 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_gettext"></a>MIP_CC_AddContentHeaderAction_GetText

获取 "添加内容标头" 操作的文本

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| textBuffer | 输出Buffer 文本将复制到中。 |
| textBufferSize | 值的大小 (textBuffer) 的字符数。 |
| actualTextSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameSize | 输出保留字符数 (的缓冲区大小)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontname"></a>MIP_CC_AddContentHeaderAction_GetFontName

获取 "添加内容标头" 操作的字体名称

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| nameBuffer | 输出将字体名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| fontSize | 输出字号 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolorsize"></a>MIP_CC_AddContentHeaderAction_GetFontColorSize

获取存储 "添加内容标头" 操作字体颜色所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| colorSize | 输出用于保存字体颜色的缓冲区大小 (字符数)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getfontcolor"></a>MIP_CC_AddContentHeaderAction_GetFontColor

获取 "添加内容标头" 操作的字体颜色 (例如 "#000000" ) 

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| colorBuffer | 输出缓冲区字体颜色将被复制到中。 |
| colorBufferSize | 大小 (colorBuffer 中的字符数) 。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| 对齐 (alignment) | 输出关联 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetAlignment(
    const mip_cc_action action,
    mip_cc_content_mark_alignment* alignment,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addcontentheaderaction_getmargin"></a>MIP_CC_AddContentHeaderAction_GetMargin

获取边距大小

**参数**

参数 | 说明
|---|---|
| action | "添加内容标头" 操作 |
| marginSize | 输出边距大小 (毫米)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddContentHeaderAction_GetMargin(
    const mip_cc_action action,
    int32_t* marginSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementnamesize"></a>MIP_CC_AddWatermarkAction_GetUIElementNameSize

获取存储 "添加水印" 操作的 UI 元素名称所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameSize | 输出用于保存 UI 元素名称的缓冲区大小（以字符数为 ()  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetUIElementNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getuielementname"></a>MIP_CC_AddWatermarkAction_GetUIElementName

获取 "添加水印" 操作的 UI 元素名称

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameBuffer | 输出将 UI 元素名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| 布局 | 输出水印布局 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetLayout(
    const mip_cc_action action,
    mip_cc_watermark_layout* layout,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettextsize"></a>MIP_CC_AddWatermarkAction_GetTextSize

获取存储 "添加水印" 操作文本所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| textSize | 输出要保存文本 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetTextSize(
    const mip_cc_action action,
    int64_t* textSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_gettext"></a>MIP_CC_AddWatermarkAction_GetText

获取 "添加水印" 操作的文本

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| textBuffer | 输出Buffer 文本将复制到中。 |
| textBufferSize | 值的大小 (textBuffer) 的字符数。 |
| actualTextSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameSize | 输出保留字符数 (的缓冲区大小)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontname"></a>MIP_CC_AddWatermarkAction_GetFontName

获取 "添加水印" 操作的字体名称

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| nameBuffer | 输出将字体名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| fontSize | 输出字号 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontSize(
    const mip_cc_action action,
    int32_t* fontSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolorsize"></a>MIP_CC_AddWatermarkAction_GetFontColorSize

获取存储 "添加水印" 操作字体颜色所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| colorSize | 输出用于保存字体颜色的缓冲区大小 (字符数)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_AddWatermarkAction_GetFontColorSize(
    const mip_cc_action action,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_addwatermarkaction_getfontcolor"></a>MIP_CC_AddWatermarkAction_GetFontColor

获取 "添加水印" 操作的字体颜色 (例如 "#000000" ) 

**参数**

参数 | 说明
|---|---|
| action | "添加水印" 操作 |
| colorBuffer | 输出缓冲区字体颜色将被复制到中。 |
| colorBufferSize | 大小 (colorBuffer 中的字符数) 。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| contentLabel | 要释放的标签 |

```c
void MIP_CC_ReleaseContentLabel(mip_cc_content_label contentLabel);
```

## <a name="mip_cc_contentlabel_getcreationtime"></a>MIP_CC_ContentLabel_GetCreationTime

获取应用标签的时间

**参数**

参数 | 说明
|---|---|
| contentLabel | Label |
| creationTime | 输出从 epoch 开始将标签应用到文档的时间 (秒)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ContentLabel_GetCreationTime(
    const mip_cc_content_label contentLabel,
    int64_t* creationTime,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getassignmentmethod"></a>MIP_CC_ContentLabel_GetAssignmentMethod

获取标签分配方法

**参数**

参数 | 说明
|---|---|
| contentLabel | Label |
| assignmentMethod | 输出分配方法 (例如 "standard" 或 "特权" )  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ContentLabel_GetAssignmentMethod(
    const mip_cc_content_label contentLabel,
    mip_cc_label_assignment_method* assignmentMethod,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getextendedproperties"></a>MIP_CC_ContentLabel_GetExtendedProperties

获取扩展属性

**参数**

参数 | 说明
|---|---|
| contentLabel | Label |
| properties | 输出扩展属性的字典，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| contentLabel | Label |
| isProtectionAppliedByLabel | 输出如果文档受到保护并且此标签显式应用了保护。 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ContentLabel_IsProtectionAppliedFromLabel(
    const mip_cc_content_label contentLabel,
    bool* isProtectionAppliedByLabel,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_contentlabel_getlabel"></a>MIP_CC_ContentLabel_GetLabel

从内容标签实例获取一般标签属性

**参数**

参数 | 说明
|---|---|
| contentLabel | 标签 |
| 标签 | 输出泛型标签，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "自定义" 操作 |
| nameSize | 输出要保留名称 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_CustomAction_GetNameSize(
    const mip_cc_action action,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_customaction_getname"></a>MIP_CC_CustomAction_GetName

获取 "自定义" 操作的名称

**参数**

参数 | 说明
|---|---|
| action | "自定义" 操作 |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "自定义" 操作 |
| properties | 输出属性字典，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

**注意**：调用方必须由调用方释放 "properties" 变量 MIP_CC_ReleaseDictionary 

```c
mip_cc_result MIP_CC_CustomAction_GetProperties(
    const mip_cc_action action,
    mip_cc_dictionary* properties,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_releaselabel"></a>MIP_CC_ReleaseLabel

释放与标签关联的资源

**参数**

参数 | 说明
|---|---|
| label | 要释放的标签 |

```c
void MIP_CC_ReleaseLabel(mip_cc_label label);
```

## <a name="mip_cc_label_getid"></a>MIP_CC_Label_GetId

获取标签 ID

**参数**

参数 | 说明
|---|---|
| label | Label |
| 面部 | 输出标签 ID |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetId(
    const mip_cc_label label,
    mip_cc_guid* labelId,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getnamesize"></a>MIP_CC_Label_GetNameSize

获取存储名称所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| label | Label |
| nameSize | 输出要保留名称 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetNameSize(
    const mip_cc_label label,
    int64_t* nameSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getname"></a>MIP_CC_Label_GetName

获取标签名称

**参数**

参数 | 说明
|---|---|
| label | Label |
| nameBuffer | 输出将该名称复制到的缓冲区。 |
| nameBufferSize | 大小 (nameBuffer 中的字符数) 。 |
| actualNameSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| label | Label |
| descriptionSize | 输出要保持其说明 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetDescriptionSize(
    const mip_cc_label label,
    int64_t* descriptionSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getdescription"></a>MIP_CC_Label_GetDescription

获取标签说明

**参数**

参数 | 说明
|---|---|
| label | Label |
| descriptionBuffer | 输出将此说明复制到的缓冲区。 |
| descriptionBufferSize | 大小 (descriptionBuffer 中的字符数) 。 |
| actualDescriptionSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| label | Label |
| colorSize | 输出要在多个字符中保留颜色 (的缓冲区大小)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetColorSize(
    const mip_cc_label label,
    int64_t* colorSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getcolor"></a>MIP_CC_Label_GetColor

获取标签颜色

**参数**

参数 | 说明
|---|---|
| label | Label |
| colorBuffer | 输出缓冲区中，颜色将被复制到) #RRGGBB 格式 (中。 |
| colorBufferSize | 大小 (colorBuffer 中的字符数) 。 |
| actualColorSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| label | Label |
| sensitivity | 输出敏感度级别 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetSensitivity(
    const mip_cc_label label,
    int32_t* sensitivity,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltipsize"></a>MIP_CC_Label_GetTooltipSize

获取存储工具提示所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| label | Label |
| tooltipSize | 输出用于保存 tooltip (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_gettooltip"></a>MIP_CC_Label_GetTooltip

获取标签工具提示

**参数**

参数 | 说明
|---|---|
| label | Label |
| tooltipBuffer | 输出将工具提示复制到的缓冲区。 |
| tooltipBufferSize | 大小 (tooltipBuffer 中的字符数) 。 |
| actualTooltipSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| label | Label |
| tooltipSize | 输出用于保存 tooltip (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetAutoTooltipSize(
    const mip_cc_label label,
    int64_t* tooltipSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getautotooltip"></a>MIP_CC_Label_GetAutoTooltip

获取标签自动分类工具提示

**参数**

参数 | 说明
|---|---|
| label | Label |
| tooltipBuffer | 输出将工具提示复制到的缓冲区。 |
| tooltipBufferSize | 大小 (tooltipBuffer 中的字符数) 。 |
| actualTooltipSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| label | Label |
| isActive | 输出标签是否被视为处于活动状态。 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| label | Label |
| 父级 (parent) | 输出父标签（如果有）; 否则为 null |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetParent(
    const mip_cc_label label,
    mip_cc_label* parent,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildrensize"></a>MIP_CC_Label_GetChildrenSize

获取子标签的数目

**参数**

参数 | 说明
|---|---|
| label | Label |
| childrenSize | 输出子级数量 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_Label_GetChildrenSize(
    const mip_cc_label label,
    int64_t* childrenSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_label_getchildren"></a>MIP_CC_Label_GetChildren

获取子标签

**参数**

参数 | 说明
|---|---|
| label | Label |
| childrenBuffer | 输出Buffer，子标签将被复制到中。 子标签 |
| childrenBufferSize | ChildrenBuffer 的标签数量)  (大小。 |
| actualChildrenSize | 输出写入缓冲区的子标签数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| label | Label |
| 设置 | 输出调用方拥有的设置字典 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "metadata" 操作 |
| metadataNames | 输出要删除的元数据的键名，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "metadataNames" 变量必须由调用方释放，方法是调用 MIP_CC_ReleaseStringList @note 在添加元数据之前删除元数据 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToRemove(
    const mip_cc_action action,
    mip_cc_string_list* metadataNames,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_metadataaction_getmetadatatoadd"></a>MIP_CC_MetadataAction_GetMetadataToAdd

获取要添加的 "元数据" 操作的元数据

**参数**

参数 | 说明
|---|---|
| action | "metadata" 操作 |
| metadata | [输出] 要添加的元数据条目列表，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

**注意**： "metadata" 变量必须由调用方释放，方法是调用 MIP_CC_ReleaseDictionary @note 在添加元数据之前应完成删除元数据 

```c
mip_cc_result MIP_CC_MetadataAction_GetMetadataToAdd(
    const mip_cc_action action,
    mip_cc_metadata_dictionary* metadata,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_createmetadatadictionary"></a>MIP_CC_CreateMetadataDictionary

创建字符串键/值的字典

**参数**

参数 | 说明
|---|---|
| entries | 元数据项数组 |
| count | 元数据项的数目 |
| 字典 | 输出新创建的字典 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| 字典 | 源字典 |
| entries | 输出元数据项数组、mip_cc_dictionary 对象拥有的内存 |
| count | 输出元数据项的数目 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| 字典 | 要释放的字典 |

```c
void MIP_CC_ReleaseMetadataDictionary(mip_cc_metadata_dictionary dictionary);
```

## <a name="mip_cc_releasepolicyhandler"></a>MIP_CC_ReleasePolicyHandler

释放与策略处理程序关联的资源

**参数**

参数 | 说明
|---|---|
| 处理程序 (handler) | 要发布的策略处理程序 |

```c
void MIP_CC_ReleasePolicyHandler(mip_cc_policy_handler handler);
```

## <a name="mip_cc_policyhandler_getsensitivitylabel"></a>MIP_CC_PolicyHandler_GetSensitivityLabel

获取文档的当前标签

**参数**

参数 | 说明
|---|---|
| 处理程序 (handler) | 策略处理程序 |
| documentState | 文档状态 |
| 上下文 | 应用程序上下文不透明地转发到任何回调 |
| contentLabel | 当前应用于文档的标签 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| 处理程序 (handler) | 策略处理程序 |
| documentState | 文档状态 |
| applicationState | 应用程序操作状态 |
| 上下文 | 应用程序上下文不透明地转发到任何回调 |
| actionResult | 输出应用程序应执行的操作，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| 处理程序 (handler) | 策略处理程序 |
| documentState | 文档状态 |
| applicationState | 应用程序操作状态 |
| 上下文 | 应用程序上下文不透明地转发到任何回调 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize

获取存储双密钥加密 url 所需的缓冲区大小。

**参数**

参数 | 说明
|---|---|
| action | "使用双键进行即席策略保护" 操作 |
| urlSize | 输出用于保存 url 的缓冲区大小（以字符数为 ()  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectadhocdkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectAdhocDkAction_GetDoubleKeyEncryptionUrl

获取双密钥加密 url

**参数**

参数 | 说明
|---|---|
| action | "使用双键进行即席策略保护" 操作 |
| urlBuffer | 输出将 url 复制到的缓冲区。 |
| urlBufferSize | 大小 (urlBuffer 中的字符数) 。 |
| actualUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurlsize"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize

获取存储双密钥加密 url 所需的缓冲区大小。

**参数**

参数 | 说明
|---|---|
| action | "不使用双键值转发策略" 操作 |
| urlSize | 输出用于保存 url 的缓冲区大小（以字符数为 ()  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrlSize(
    const mip_cc_action action,
    int64_t* urlSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_protectdonotforwarddkaction_getdoublekeyencryptionurl"></a>MIP_CC_ProtectDoNotForwardDkAction_GetDoubleKeyEncryptionUrl

获取双密钥加密 url

**参数**

参数 | 说明
|---|---|
| action | "不使用双键值转发策略" 操作 |
| urlBuffer | 输出将 url 复制到的缓冲区。 |
| urlBufferSize | 大小 (urlBuffer 中的字符数) 。 |
| actualUrlSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "删除内容脚注" 操作 |
| 姓名 | 输出要移除的 UI 元素的名称，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "删除内容标头" 操作 |
| 姓名 | 输出要移除的 UI 元素的名称，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| action | "删除水印页脚" 操作 |
| 姓名 | 输出要移除的 UI 元素的名称，由调用方拥有的内存 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| sensitivityType | 要释放的敏感度类型 |

```c
void MIP_CC_ReleaseSensitivityType(mip_cc_sensitivity_type sensitivityType);
```

## <a name="mip_cc_sensitivitytype_getrulepackageidsize"></a>MIP_CC_SensitivityType_GetRulePackageIdSize

获取存储敏感度类型的规则包 ID 所需的缓冲区大小

**参数**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| idSize | 输出保留规则包 ID (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageIdSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* idSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackageid"></a>MIP_CC_SensitivityType_GetRulePackageId

获取敏感度类型的规则包 ID

**参数**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| idBuffer | 输出该 ID 将被复制到中。 |
| idBufferSize | 大小 (idBuffer 中的字符数) 。 |
| actualIdSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

**参数**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| rulePackageSize | 输出要保留规则包 (的缓冲区大小（以字符数为)  |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

**Return**：指示成功或失败的结果代码

```c
mip_cc_result MIP_CC_SensitivityType_GetRulePackageSize(
    const mip_cc_sensitivity_type sensitivityType,
    int64_t* rulePackageSize,
    mip_cc_error* errorInfo);
```

## <a name="mip_cc_sensitivitytype_getrulepackage"></a>MIP_CC_SensitivityType_GetRulePackage

获取敏感度类型的规则包

**参数**

参数 | 说明
|---|---|
| sensitivityType | 敏感度类型 |
| rulePackageBuffer | 输出将规则包复制到的缓冲区。 |
| rulePackageBufferSize | 大小 (rulePackageBuffer 中的字符数) 。 |
| actualRulePackageSize | 输出写入缓冲区的字符数 |
| errorInfo | [输出] 如果操作结果为错误，则 (可选) 失败信息 |

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

