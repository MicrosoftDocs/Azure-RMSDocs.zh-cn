---
title: 枚举
description: 枚举
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: f1ad15819d10bcded670fe519db07667b7e7331e
ms.sourcegitcommit: 7a8eef5eb9d6440c6e2300cb3f264da31061b00d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73591618"
---
# <a name="enumerations"></a>枚举

## <a name="mip_cc_cache_storage_type"></a>mip_cc_cache_storage_type

缓存的存储类型

| 字段 | 描述 |
|---|---|
|  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0         | 内存中存储  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1           | 磁盘上存储  |
|  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2  | 使用加密的磁盘上存储（如果平台支持）  |


```c
typedef enum {
  MIP_CACHE_STORAGE_TYPE_IN_MEMORY = 0,        
  MIP_CACHE_STORAGE_TYPE_ON_DISK = 1,          
  MIP_CACHE_STORAGE_TYPE_ON_DISK_ENCRYPTED = 2 
} mip_cc_cache_storage_type;

```

## <a name="mip_cc_content_format"></a>mip_cc_content_format

内容格式

| 字段 | 描述 |
|---|---|
|  MIP_CONTENT_FORMAT_DEFAULT = 0  | 标准文件格式  |
|  MIP_CONTENT_FORMAT_EMAIL = 1    | 电子邮件  |


```c
typedef enum {
  MIP_CONTENT_FORMAT_DEFAULT = 0, 
  MIP_CONTENT_FORMAT_EMAIL = 1,   
} mip_cc_content_format;

```

## <a name="mip_cc_label_assignment_method"></a>mip_cc_label_assignment_method

描述如何应用新标签

| 字段 | 描述 |
|---|---|
|  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0    | 标准标签分配不会覆盖以前的特权分配。  |
|  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1  | 将来的标准分配将不会重写特权标签分配。  |
|  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2        | 保留。 请不要使用。  |


```c
typedef enum {
  MIP_LABEL_ASSIGNMENT_METHOD_STANDARD = 0,   
  MIP_LABEL_ASSIGNMENT_METHOD_PRIVILEGED = 1, 
  MIP_LABEL_ASSIGNMENT_METHOD_AUTO = 2,       
} mip_cc_label_assignment_method;

```

## <a name="mip_cc_content_mark_alignment"></a>mip_cc_content_mark_alignment

内容标记的对齐方式（内容标头或内容页脚）

| 字段 | 描述 |
|---|---|
|  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0    | 内容标记靠左对齐  |
|  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1   | 内容标记与右侧对齐  |
|  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2  | 内容标记居中  |


```c
typedef enum {
  MIP_CONTENT_MARK_ALIGNMENT_LEFT = 0,   
  MIP_CONTENT_MARK_ALIGNMENT_RIGHT = 1,  
  MIP_CONTENT_MARK_ALIGNMENT_CENTER = 2, 
} mip_cc_content_mark_alignment;

```

## <a name="mip_cc_watermark_layout"></a>mip_cc_watermark_layout

水印布局

| 字段 | 描述 |
|---|---|
|  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0  | 水印布局为水平  |
|  MIP_WATERMARK_LAYOUT_DIAGONAL = 1    | 水印布局为对角线  |


```c
typedef enum {
  MIP_WATERMARK_LAYOUT_HORIZONTAL = 0, 
  MIP_WATERMARK_LAYOUT_DIAGONAL = 1,   
} mip_cc_watermark_layout;

```

## <a name="mip_cc_consent"></a>mip_cc_consent

请求同意连接到无法识别的服务终结点时，用户的响应

| 字段 | 描述 |
|---|---|
|  MIP_CONSENT_ACCEPT_ALWAYS = 0  | 同意并记住此决定  |
|  MIP_CONSENT_ACCEPT = 1         | 只同意一次  |
|  MIP_CONSENT_REJECT = 2          | 不许可  |


```c
typedef enum {
  MIP_CONSENT_ACCEPT_ALWAYS = 0, 
  MIP_CONSENT_ACCEPT = 1,        
  MIP_CONSENT_REJECT = 2         
} mip_cc_consent;

```

## <a name="mip_cc_flighting_feature"></a>mip_cc_flighting_feature

按名称定义新功能

| 字段 | 描述 |
|---|---|
|  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0      | 依靠单独的 HTTP 调用来确定 RMS 服务终结点（默认值为 false） |
|  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1        | 缓存每个域/租户的 OAuth2 难题，减少不必要的401响应。 为管理自己的 HTTP 身份验证的应用/服务禁用（默认值为 true）  |
|  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2  | 为 Linux 平台启用加密缓存（默认值为 false）  |
|  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3     | 启用单一公司名称进行 dns 查找。 例如 https://corprights  |
|  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4            | 为发送到策略服务的请求启用自动 HTTP 身份验证。 为管理自己的 HTTP 身份验证的应用/服务禁用（默认值为 true）  |


```c
typedef enum {
  MIP_FLIGHTING_FEATURE_SERVICE_DISCOVERY = 0,     
  MIP_FLIGHTING_FEATURE_AUTH_INFO_CACHE = 1,       
  MIP_FLIGHTING_FEATURE_LINUX_ENCRYPTED_CACHE = 2, 
  MIP_FLIGHTING_FEATURE_SINGLE_DOMAIN_NAME = 3,    
  MIP_FLIGHTING_FEATURE_POLICY_AUTH = 4,           
} mip_cc_flighting_feature;

```

## <a name="mip_cc_http_request_type"></a>mip_cc_http_request_type

HTTP 请求类型

| 字段 | 描述 |
|---|---|
|  HTTP_REQUEST_TYPE_GET = 0   | HTTP GET  |
|  HTTP_REQUEST_TYPE_POST = 1  | HTTP POST  |


```c
typedef enum {
  HTTP_REQUEST_TYPE_GET = 0,  
  HTTP_REQUEST_TYPE_POST = 1, 
} mip_cc_http_request_type;

```

## <a name="mip_cc_http_result"></a>mip_cc_http_result

HTTP 操作的成功/失败状态

| 字段 | 描述 |
|---|---|
|  HTTP_RESULT_OK = 0       | 已成功完成 HTTP 操作  |
|  HTTP_RESULT_FAILURE = 1  | HTTP 操作失败（例如，超时、网络故障等）  |


```c
typedef enum {
  HTTP_RESULT_OK = 0,      
  HTTP_RESULT_FAILURE = 1, 
} mip_cc_http_result;

```

## <a name="mip_cc_log_level"></a>mip_cc_log_level

日志级别

| 字段 | 描述 |
|---|---|
|  MIP_LOG_LEVEL_TRACE = 0   | Trace  |
|  MIP_LOG_LEVEL_INFO        | 信息  |
|  MIP_LOG_LEVEL_WARNING     | 警告  |
|  MIP_LOG_LEVEL_ERROR       | 错误  |


```c
typedef enum {
  MIP_LOG_LEVEL_TRACE = 0,  
  MIP_LOG_LEVEL_INFO,       
  MIP_LOG_LEVEL_WARNING,    
  MIP_LOG_LEVEL_ERROR,      
} mip_cc_log_level;

```

## <a name="mip_cc_protection_type"></a>mip_cc_protection_type

描述保护是由模板定义还是临时定义

| 字段 | 描述 |
|---|---|
|  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0  | 基于 RMS 模板  |
|  MIP_PROTECTION_TYPE_CUSTOM = 1          | 自定义、即席保护  |


```c
typedef enum {
  MIP_PROTECTION_TYPE_TEMPLATE_BASED = 0, 
  MIP_PROTECTION_TYPE_CUSTOM = 1,         
} mip_cc_protection_type;

```

## <a name="mip_cc_result"></a>mip_cc_result

API 成功/失败结果

| 字段 | 描述 |
|---|---|
|  MIP_RESULT_ERROR_UNKNOWN                    | 未知错误  |
|  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER        | 应用程序提供的缓冲区太小  |
|  MIP_RESULT_ERROR_BAD_INPUT                  | 应用程序传递了错误输入  |
|  MIP_RESULT_ERROR_FILE_IO_ERROR              | 常规文件 i/o 错误  |
|  MIP_RESULT_ERROR_NETWORK                    | 常规网络错误（例如无法访问的服务）  |
|  MIP_RESULT_ERROR_TRANSIENT_NETWORK          | 暂时性网络错误（例如网关错误）  |
|  MIP_RESULT_ERROR_INTERNAL                   | 内部错误意外  |
|  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED     | 应提供对齐方式，才能完成对文件执行的操作。  |
|  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION    | 不支持 Opeation  |
|  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED        | 当带有标准方法时，不能重写特权标签  |
|  MIP_RESULT_ERROR_ACCESS_DENIED              | 用户无权访问服务  |
|  MIP_RESULT_ERROR_CONSENT_DENIED             | 未向用户授予许可要求的操作  |
|  MIP_RESULT_ERROR_POLICY_SYNC                | 尝试同步策略数据失败  |
|  MIP_RESULT_ERROR_NO_PERMISSIONS             | 用户无法获取内容的访问权限（例如，没有权限，已撤消内容）  |
|  MIP_RESULT_ERROR_NO_AUTH_TOKEN              | 由于身份验证令牌为空，用户无法访问内容  |
|  MIP_RESULT_ERROR_SERVICE_DISABLED           | 由于服务被禁用，用户无法访问内容  |
|  MIP_RESULT_ERROR_PROXY_AUTH                 | 代理身份验证失败  |
|  MIP_RESULT_ERROR_NO_POLICY                  | 未为用户/租户配置策略  |
|  MIP_RESULT_ERROR_OPERATION_CANCELLED        | 操作已取消  |
|  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED  | 应设置即席保护来完成对文件的操作  |
|  MIP_RESULT_ERROR_DEPRECATED_API             | 调用方调用了已弃用的 API  |
|  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND         | 无法识别模板 ID  |
|  MIP_RESULT_ERROR_LABEL_NOT_FOUND            | 无法识别标签 ID  |
|  MIP_RESULT_ERROR_LABEL_DISABLED             | 标签已禁用或处于非活动状态  |


```c
typedef enum {
  MIP_RESULT_SUCCESS = 0,

  // MIP C API errors
  MIP_RESULT_ERROR_UNKNOWN,                   
  MIP_RESULT_ERROR_INSUFFICIENT_BUFFER,       

  // MIP C++ exceptions
  MIP_RESULT_ERROR_BAD_INPUT,                 
  MIP_RESULT_ERROR_FILE_IO_ERROR,             
  MIP_RESULT_ERROR_NETWORK,                   
  MIP_RESULT_ERROR_TRANSIENT_NETWORK,         
  MIP_RESULT_ERROR_INTERNAL,                  
  MIP_RESULT_ERROR_JUSTIFICATION_REQUIRED,    
  MIP_RESULT_ERROR_NOT_SUPPORTED_OPERATION,   
  MIP_RESULT_ERROR_PRIVILEGED_REQUIRED,       
  MIP_RESULT_ERROR_ACCESS_DENIED,             
  MIP_RESULT_ERROR_CONSENT_DENIED,            
  MIP_RESULT_ERROR_POLICY_SYNC,               
  MIP_RESULT_ERROR_NO_PERMISSIONS,            
  MIP_RESULT_ERROR_NO_AUTH_TOKEN,             
  MIP_RESULT_ERROR_SERVICE_DISABLED,          
  MIP_RESULT_ERROR_PROXY_AUTH,                
  MIP_RESULT_ERROR_NO_POLICY,                 
  MIP_RESULT_ERROR_OPERATION_CANCELLED,       
  MIP_RESULT_ERROR_ADHOC_PROTECTION_REQUIRED, 
  MIP_RESULT_ERROR_DEPRECATED_API,            
  MIP_RESULT_ERROR_TEMPLATE_NOT_FOUND,        
  MIP_RESULT_ERROR_LABEL_NOT_FOUND,           
  MIP_RESULT_ERROR_LABEL_DISABLED,            
} mip_cc_result;

```

## <a name="mip_cc_action_type"></a>mip_cc_action_type

操作类型位掩码

| 字段 | 描述 |
|---|---|
|  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | 向文档操作类型添加内容页脚。 |
|  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | 向文档操作类型添加内容页眉。 |
|  MIP_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | 向整个文档操作类型添加水印。 |
|  MIP_ACTION_TYPE_CUSTOM = 1 < < 3                  | 自定义的操作类型。 |
|  MIP_ACTION_TYPE_JUSTIFY = 1 < < 4                 | 两端对齐操作类型。 |
|  MIP_ACTION_TYPE_METADATA = 1 < < 5                | 元数据更改操作类型。 |
|  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | 临时策略保护操作类型。 |
|  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | 模板保护操作类型。 |
|  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | “不转发”保护操作类型。 |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | 删除内容页脚操作类型。 |
|  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | 删除内容页眉操作类型。 |
|  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | 删除保护操作类型。 |
|  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | 删除水印操作类型。 |
|  MIP_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | 应用标签操作类型。 |
|  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | 建议标签操作类型。 |


```c
typedef enum {
  MIP_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_action_type;

```

## <a name="mip_cc_label_action_state"></a>mip_cc_label_action_state

描述应用程序尝试对当前标签执行的操作

| 字段 | 描述 |
|---|---|
|  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0  | 当前标签不应更改。  |
|  MIP_LABEL_ACTION_STATE_REMOVE = 1     | 应删除当前标签。  |
|  MIP_LABEL_ACTION_STATE_UPDATE = 2     | 应更改当前标签。  |


```c
typedef enum {
  MIP_LABEL_ACTION_STATE_NO_CHANGE = 0, 
  MIP_LABEL_ACTION_STATE_REMOVE = 1,    
  MIP_LABEL_ACTION_STATE_UPDATE = 2,    
} mip_cc_label_action_state;

```

## <a name="mip_cc_label_action_type"></a>mip_cc_label_action_type

应用程序了解和支持的与标签相关的操作

| 字段 | 描述 |
|---|---|
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 < < 0      | 向文档操作类型添加内容页脚。  |
|  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 < < 1      | 向文档操作类型添加内容页眉。  |
|  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 < < 2           | 向整个文档操作类型添加水印。  |
|  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 < < 3                  | 自定义的操作类型。  |
|  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 < < 4                 | 两端对齐操作类型。  |
|  MIP_LABEL_ACTION_TYPE_METADATA = 1 < < 5                | 元数据更改操作类型。  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 < < 6           | 临时策略保护操作类型。  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 < < 7     | 模板保护操作类型。  |
|  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 < < 8  | “不转发”保护操作类型。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 < < 9   | 删除内容页脚操作类型。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 < < 10  | 删除内容页眉操作类型。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 < < 11      | 删除保护操作类型。  |
|  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 < < 12       | 删除水印操作类型。  |
|  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 < < 13            | 应用标签操作类型。  |
|  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 < < 14        | 建议标签操作类型。  |


```c
typedef enum {
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_FOOTER = 1 << 0,     
  MIP_LABEL_ACTION_TYPE_ADD_CONTENT_HEADER = 1 << 1,     
  MIP_LABEL_ACTION_TYPE_ADD_WATERMARK = 1 << 2,          
  MIP_LABEL_ACTION_TYPE_CUSTOM = 1 << 3,                 
  MIP_LABEL_ACTION_TYPE_JUSTIFY = 1 << 4,                
  MIP_LABEL_ACTION_TYPE_METADATA = 1 << 5,               
  MIP_LABEL_ACTION_TYPE_PROTECT_ADHOC = 1 << 6,          
  MIP_LABEL_ACTION_TYPE_PROTECT_BY_TEMPLATE = 1 << 7,    
  MIP_LABEL_ACTION_TYPE_PROTECT_DO_NOT_FORWARD = 1 << 8, 
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_FOOTER = 1 << 9,  
  MIP_LABEL_ACTION_TYPE_REMOVE_CONTENT_HEADER = 1 << 10, 
  MIP_LABEL_ACTION_TYPE_REMOVE_PROTECTION = 1 << 11,     
  MIP_LABEL_ACTION_TYPE_REMOVE_WATERMARK = 1 << 12,      
  MIP_LABEL_ACTION_TYPE_APPLY_LABEL = 1 << 13,           
  MIP_LABEL_ACTION_TYPE_RECOMMEND_LABEL = 1 << 14,       
} mip_cc_label_action_type;

```

## <a name="mip_cc_data_state"></a>mip_cc_data_state

定义应用程序在其上操作时的数据状态

| 字段 | 描述 |
|---|---|
|  MIP_DATA_STATE_REST = 0    | 以物理方式存储在数据库/文件/仓库中的非活动数据  |
|  MIP_DATA_STATE_MOTION = 1  | 遍历网络或临时驻留在计算机内存中以供读取或更新的数据  |
|  MIP_DATA_STATE_USE = 2     | 在物理上存储在数据库/文件/仓库等中的恒定变化的活动数据  |


```c
typedef enum {
  MIP_DATA_STATE_REST = 0,   
  MIP_DATA_STATE_MOTION = 1, 
  MIP_DATA_STATE_USE = 2,    
} mip_cc_data_state;

```

