---
title: 结构
description: 构造.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 4/16/2020
ms.openlocfilehash: 0d24a2fedad93ecca3b4d5a48f5434746a7a7c4e
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763842"
---
# <a name="structures"></a>结构

## <a name="mip_cc_application_info"></a>mip_cc_application_info

包含应用程序特定信息的结构 

| 字段 | 说明 |
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

| 字段 | 说明 |
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

## <a name="mip_cc_handle"></a>mip_cc_handle

MIP 对象的不透明句柄

| 字段 | 说明 |
|---|---|
| typeId | 用于唯一标识特定句柄类型的幻数  |
| data | 原始处理数据  |


```c
typedef struct {
  uint32_t typeId; 
  void* data;      
} mip_cc_handle;

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

| 字段 | 说明 |
|---|---|
| key | 键  |
| value | “值”  |


```c
typedef struct {
  const char* key;   
  const char* value; 
} mip_cc_kv_pair;

```

## <a name="mip_cc_error"></a>mip_cc_error

错误信息

```c
typedef struct {
  mip_cc_result result;
  char description[ERROR_STRING_BUFFER_SIZE];

  // MIP_RESULT_ERROR_NETWORK details
  mip_cc_network_error_category networkError_Category;
  int32_t networkError_ResponseCode;

  // MIP_RESULT_ERROR_NO_PERMISSIONS details
  char noPermissionsError_Owner[ERROR_STRING_BUFFER_SIZE];
  char noPermissionsError_Referrer[ERROR_STRING_BUFFER_SIZE];

  // MIP_RESULT_ERROR_SERVICE_DISABLED details
  mip_cc_service_disabled_error_extent serviceDisabledError_Extent;
} mip_cc_error;

```

## <a name="mip_cc_http_header"></a>mip_cc_http_header

HTTP 请求/响应标头

| 字段 | 说明 |
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

| 字段 | 说明 |
|---|---|
| ID | 唯一请求 ID--与 mip_cc_http_response 中的同一属性关联  |
| type | HTTP 请求类型（例如 GET 和 POST）  |
| url | HTTP 请求 URL  |
| bodySize | HTTP 请求正文的大小（字节）  |
| body | Buffer 包含 HTTP 请求正文  |
| headersCount | HTTP 请求标头的数目  |
| headers | 包含 HTTP 请求标头的缓冲区  |


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

| 字段 | 说明 |
|---|---|
| ID | 唯一请求 ID--与 mip_cc_http_request 中的同一属性关联  |
| statusCode | HTTP 响应状态代码  |
| bodySize | HTTP 响应正文大小（字节）  |
| body | Buffer 包含 HTTP 响应正文  |
| headersCount | HTTP 响应标头数  |
| headers | 包含 HTTP 响应标头的缓冲区  |


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

包含用户标识信息的结构

| 字段 | 说明 |
|---|---|
| 电子邮件 | 用户电子邮件地址  |
| name | 用户友好名称，用于标记内容。  |


```c
typedef struct {
  const char* email;          
  const char* name;           
} mip_cc_identity;

```

## <a name="mip_cc_feature_override"></a>mip_cc_feature_override

定义单个功能的启用/禁用状态

| 字段 | 说明 |
|---|---|
| feature | 功能名称  |
| value | 启用/禁用状态  |


```c
typedef struct {
  mip_cc_flighting_feature feature; 
  bool value;                       
} mip_cc_feature_override;

```

## <a name="mip_cc_user_rights"></a>mip_cc_user_rights

一组用户和与之关联的权限

| 字段 | 说明 |
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

| 字段 | 说明 |
|---|---|
| 用户 | 用户列表  |
| usersCount | 用户数  |
| 角色 | 角色列表  |
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

| 字段 | 说明 |
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

| 字段 | 说明 |
|---|---|
| actionState | 描述应用程序是否正在尝试更改标签状态。  |
| newLabel | 如果 "actionType" 为 "UPDATE"：新标签。  |
| newLabelExtendedProperties | 如果 "actionType" 为 "UPDATE"：要写入元数据的附加属性。  |
| newLabelAssignmentMethod | 如果 "actionType" 为 "UPDATE"：新标签的分配方法。  |
| isDowngradeJustified | 如果 "actionType" 为 "UPDATE"：标签降级是否已由用户对齐。  |
| downgradeJustification | 如果 "actionType" 为 "UPDATE"：标签降级用户提供的对齐文本。  |
| supportedActions | 描述应用程序可以执行的与标签相关的操作的枚举掩码。  |


```c
typedef struct {
  mip_cc_label_action_state actionState;                    
  mip_cc_label newLabel;                                    
  mip_cc_dictionary newLabelExtendedProperties;             
  mip_cc_label_assignment_method newLabelAssignmentMethod;  
  bool isDowngradeJustified;                                
  const char* downgradeJustification;                       
  mip_cc_label_action_type supportedActions;                
} mip_cc_application_action_state;

```

## <a name="mip_cc_document_state"></a>mip_cc_document_state

用于检索文档元数据的回调函数定义，按名称/前缀筛选

```c
typedef struct {
  /**
   * Human-readable document description visible in tenant audit portal
   *     Example for a file: [path\filename]
   *     Example for an email: [Subject:Sender]
   */
  const char* contentId;

  /**
   * State of document data as application interacts with it
   */
  mip_cc_data_state dataState;

  /**
   * Document metadata callback
   */
  mip_cc_metadata_callback contentMetadataCallback;

  /**
   * Protection descriptor if document is currently protected, else null
   */
  mip_cc_protection_descriptor protectionDescriptor;

  /**
   * Format of document (file vs. email)
   */
  mip_cc_content_format contentFormat;

  /**
   * Optional application-specific metadata that is used when sending audit reports
   *     Recognized values:
   *       'Sender': Sender email address
   *       'Recipients': JSON array of email recipients
   *       'LastModifiedBy': Email address of the user who last modified a document
   *       'LastModifiedDate': Date a document was last modified
   */
  mip_cc_dictionary auditMetadata;
  
  /**
   * Document metadata version, default should be 0.
   */
  unsigned int contentMetadataVersion;
} mip_cc_document_state;

```

## <a name="mip_cc_metadata_entry"></a>mip_cc_metadata_entry

元数据条目

| 字段 | 说明 |
|---|---|
| key | 密钥输入 |
| value | 值输入  |
| version | 版本项应初始化为0，除非另外知道 |


```c
typedef struct {
  const char* key;        
  const char* value;      
  uint32_t version;       
} mip_cc_metadata_entry;

```

