---
title: 結構
description: 构造.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 11/4/2019
ms.openlocfilehash: aa544dfbd046ae8c3137cbc115d9af6ea219bc07
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "73591604"
---
# <a name="structures"></a>結構

## <a name="mip_cc_application_info"></a>mip_cc_application_info

包含应用程序特定信息的结构 

| 字段 | 描述 |
|---|---|
| applicationId | AAD 门户中设置的应用程序标识符（应为不带方括号的 GUID）。  |
| applicationName | 应用程序名称（应仅包含有效 ASCII 字符，不包括 ";"）  |
| applicationVersion | 所使用的应用程序的版本（应只包含有效的 ASCII 字符，不包括 ";"）   |


```c
typedef struct {
  const char* applicationId;      
  const char* applicationName;    
  const char* applicationVersion; 
} mip_cc_application_info;

```

## <a name="mip_cc_oauth2_challenge"></a>mip_cc_oauth2_challenge

服务器提供的用于生成 OAuth2 令牌的信息

| 字段 | 描述 |
|---|---|
| authority | OAuth2 机构  |
| resource | OAuth2 资源  |
| scope | OAuth2 范围  |


```c
typedef struct {
  const char* authority; 
  const char* resource;  
  const char* scope;     
} mip_cc_oauth2_challenge;

```

## <a name="mip_cc_guid"></a>mip_cc_guid

GUID

```c
typedef struct {
  char guid[37];
} mip_cc_guid;

```

## <a name="mip_cc_kv_pair"></a>mip_cc_kv_pair

键/值对

| 字段 | 描述 |
|---|---|
| key | Key  |
| value | 值  |


```c
typedef struct {
  const char* key;   
  const char* value; 
} mip_cc_kv_pair;

```

## <a name="mip_cc_http_header"></a>mip_cc_http_header

HTTP 请求/响应标头

| 字段 | 描述 |
|---|---|
| name | 标头名称/键  |
| value | 标头值  |


```c
typedef struct {
  const char* name;  
  const char* value; 
} mip_cc_http_header;

```

## <a name="mip_cc_http_request"></a>mip_cc_http_request

HTTP 请求

| 字段 | 描述 |
|---|---|
| ID | 唯一请求 ID--与 mip_cc_http_response 中的同一属性关联  |
| 类型 | HTTP 请求类型（例如 GET 和 POST）  |
| url | HTTP 请求 URL  |
| bodySize | HTTP 请求正文的大小（字节）  |
| 正文 | Buffer 包含 HTTP 请求正文  |
| headersCount | HTTP 请求标头的数目  |
| 页眉 | 包含 HTTP 请求标头的缓冲区  |


```c
typedef struct {
  const char* id;                    
  mip_cc_http_request_type type;     
  const char* url;                   
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_request;

```

## <a name="mip_cc_http_response"></a>mip_cc_http_response

HTTP 响应

| 字段 | 描述 |
|---|---|
| ID | 唯一请求 ID--与 mip_cc_http_request 中的同一属性关联  |
| statusCode | HTTP 响应状态代码  |
| bodySize | HTTP 响应正文大小（字节）  |
| 正文 | Buffer 包含 HTTP 响应正文  |
| headersCount | HTTP 响应标头数  |
| 页眉 | 包含 HTTP 响应标头的缓冲区  |


```c
typedef struct {
  const char* id;                    
  int32_t statusCode;                
  int64_t bodySize;                  
  const uint8_t* body;               
  int64_t headersCount;              
  const mip_cc_http_header* headers; 
} mip_cc_http_response;

```

## <a name="mip_cc_identity"></a>mip_cc_identity

包含应用程序特定信息的结构 

| 字段 | 描述 |
|---|---|
| 电子邮件 | 用户电子邮件地址  |


```c
typedef struct {
  const char* email;          
} mip_cc_identity;

```

## <a name="mip_cc_feature_override"></a>mip_cc_feature_override

定义单个功能的启用/禁用状态

| 字段 | 描述 |
|---|---|
| 功能 | 功能名称  |
| value | 启用/禁用状态  |


```c
typedef struct {
  mip_cc_flighting_feature feature; 
  bool value;                       
} mip_cc_feature_override;

```

## <a name="mip_cc_user_rights"></a>mip_cc_user_rights

一组用户和与之关联的权限

| 字段 | 描述 |
|---|---|
| 用户 | 用户列表  |
| usersCount | 用户数  |
| 权限 | 权限列表  |
| rightsCount | 权限数量  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** rights; 
  int64_t rightsCount; 
} mip_cc_user_rights;

```

## <a name="mip_cc_user_roles"></a>mip_cc_user_roles

一组用户和与之关联的角色

| 字段 | 描述 |
|---|---|
| 用户 | 用户列表  |
| usersCount | 用户数  |
| roles | 角色列表  |
| rolesCount | 角色数量  |


```c
typedef struct {
  const char** users;  
  int64_t usersCount;  
  const char** roles; 
  int64_t rolesCount; 
} mip_cc_user_roles;

```

## <a name="mip_cc_async_task"></a>mip_cc_async_task

定义单个异步任务调度请求

| 字段 | 描述 |
|---|---|
| ID | 任务 ID  |
| delayMs | 在任务执行之前延迟（以毫秒为单位）  |
| executeOnIndependentThread | 此任务是应在完全独立的线程上执行，还是可以重复使用共享线程  |


```c
typedef struct {
  const char* id;                   
  int64_t delayMs;                  
  bool executeOnIndependentThread;  
} mip_cc_async_task;

```

## <a name="mip_cc_application_action_state"></a>mip_cc_application_action_state

表示应用程序的当前状态，因为它执行与标签相关的操作

| 字段 | 描述 |
|---|---|
| actionState | 描述应用程序是否正在尝试更改标签状态。  |
| newLabel | 如果 "actionType" 为 "UPDATE"：新标签。  |
| newLabelExtendedProperties | 如果 "actionType" 为 "UPDATE"：要写入元数据的附加属性。  |
| newLabelAssignementMethod | 如果 "actionType" 为 "UPDATE"：新标签的分配方法。  |
| isDowngradeJustified | 如果 "actionType" 为 "UPDATE"：标签降级是否已由用户对齐。  |
| downgradeJustification | 如果 "actionType" 为 "UPDATE"：标签降级用户提供的对齐文本。  |
| supportedActions | 描述应用程序可以执行的与标签相关的操作的枚举掩码。  |


```c
typedef struct {
  mip_cc_label_action_state actionState;                    
  mip_cc_label newLabel;                                    
  mip_cc_dictionary newLabelExtendedProperties;             
  mip_cc_label_assignment_method newLabelAssignementMethod; 
  bool isDowngradeJustified;                                
  const char* downgradeJustification;                       
  mip_cc_label_action_type supportedActions;                
} mip_cc_application_action_state;

```

## <a name="mip_cc_document_state"></a>mip_cc_document_state

表示标签感知文档的当前状态。

| 字段 | 描述 |
|---|---|
| contentId | 可在租户审核门户中看到的可读文档说明。 文件示例： [path\filename];电子邮件的示例： [Subject： Sender]。 |
| dataState | 应用程序与之进行交互时的文档数据状态  |
| contentMetadataCallback | 文档元数据回调  |
| protectionDescriptor | 如果文档当前受保护，则为保护描述符; 否则为 null  |
| contentFormat | 文档格式（文件与电子邮件）  |
| auditMetadata | 发送审核报告时使用的特定于应用程序的可选元数据。 识别的值： "发送方"：发件人电子邮件地址;"收件人"：电子邮件收件人的 JSON 数组;"LastModifiedBy"：最后修改文档的用户的电子邮件地址;"LastModifiedDate"：文档上次修改的日期。 |

```c
typedef struct {
  const char* contentId;
  mip_cc_data_state dataState;
  mip_cc_metadata_callback contentMetadataCallback;
  mip_cc_protection_descriptor protectionDescriptor;
  mip_cc_content_format contentFormat;
  mip_cc_dictionary auditMetadata;
} mip_cc_document_state;