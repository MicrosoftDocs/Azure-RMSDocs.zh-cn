---
title: 类
description: 功能
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: fb6c857d06da7a68d01d095db556216fee990dc6
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555970"
---
# <a name="functions"></a>功能



## <a name="namespace-mip"></a>命名空间 mip

| 按命名空间范围的函数   | 说明                                |
|--------------------------------|---------------------------------------------|
public std：： string GetAssignmentMethodString （AssignmentMethod 方法）       |  将 AssignmentMethod 枚举转换为字符串说明。
public static std：： string GetActionSourceString （ActionSource actionSource）       |  获取操作源名称。
public static std：： string GetDataStateString （mip：:D ataState 状态）       |  获取内容状态名称。
public const std::string& GetCustomSettingPolicyDataName()       |  用于明确指定策略数据的设置的名称。
public const std::string& GetCustomSettingExportPolicyFileName()       |  用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。
public const std：： string & GetCustomSettingSensitivityTypesDataName （）       |  用于显式指定敏感度数据的设置的名称。
public const std::string& GetCustomSettingPolicyDataFile()       |  用于明确指定策略数据文件路径的设置的名称。
public const std：： string & GetCustomSettingSensitivityTypesDataFile （）       |  用于显式指定敏感度类型数据文件路径的设置的名称。
public const std：： string & GetCustomSettingLabelCustomPropertiesSyncEnabled （）       |  允许按照标签功能按自定义属性和自定义属性启用标签的设置的名称。
public const std：： map\<FlightingFeature，bool\>& GetDefaultFeatureSettings （）       |  获取默认情况下是否启用功能。
public MIP_API std：： shared_ptr\<MIP：： Stream\> CreateStreamFromStdStream （const std：： shared_ptr\<std：： istream\>& stdIStream）       |  从 std：： istream 创建流。
public MIP_API std：： shared_ptr\<MIP：： Stream\> CreateStreamFromStdStream （const std：： shared_ptr\<std：： ostream\>& stdOStream）       |  从 std：： ostream 创建流。
public MIP_API std：： shared_ptr\<MIP：： Stream\> CreateStreamFromStdStream （const std：： shared_ptr\<std：： iostream\>& stdIOStream）       |  从 std：： iostream 创建流。
public MIP_API std：： shared_ptr\<MIP：： Stream\> CreateStreamFromBuffer （uint8_t * buffer，const int64_t size）       |  从缓冲区创建流。
public MIP_API std：： vector\<uint8_t\> ReadFromStream （const std：： shared_ptr\<MIP：： Stream\>& 流）       |  读取所有流的字节数。
公有 ActionType 运算符 & （ActionType a，ActionType b）       |  操作类型枚举的和（&）运算符。
public ActionType operator ^ （ActionType a，ActionType b）       |  操作类型枚举的 Xor （^）运算符。

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString 函数
将 AssignmentMethod 枚举转换为字符串说明。

参数：  
* **方法**：赋值方法。 



  
**返回**：分配方法的字符串说明。
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString 函数
获取操作源名称。

参数：  
* **actionSource**：操作源。 



  
**返回**：操作源的字符串表示形式。
  
### <a name="getdatastatestring-function"></a>GetDataStateString 函数
获取内容状态名称。

参数：  
* **actionSource**：正在处理的内容的状态。 



  
**返回**：内容状态的字符串表示形式。
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName 函数
用于明确指定策略数据的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName 函数
用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName 函数
用于显式指定敏感度数据的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile 函数
用于明确指定策略数据文件路径的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile 函数
用于显式指定敏感度类型数据文件路径的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getcustomsettinglabelcustompropertiessyncenabled-function"></a>GetCustomSettingLabelCustomPropertiesSyncEnabled 函数
允许按照标签功能按自定义属性和自定义属性启用标签的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getdefaultfeaturesettings-function"></a>GetDefaultFeatureSettings 函数
获取默认情况下是否启用功能。

  
**返回**：试验功能的默认状态
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
从 std：： istream 创建流。

参数：  
* **stdIStream**：回溯 std::istream



  
**返回**：对 std：： istream 的流包装
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
从 std：： ostream 创建流。

参数：  
* **stdOStream**：回溯 std::ostream



  
**返回**：对流封装 std：： ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
从 std：： iostream 创建流。

参数：  
* **stdIOStream**：回溯 std::iostream



  
**返回**：对流封装 std：： iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer 函数
从缓冲区创建流。

参数：  
* **buffer**：指向缓冲区的指针



  
**返回结果**：缓冲区大小
  
### <a name="readfromstream-function"></a>ReadFromStream 函数
读取所有流的字节数。

参数：  
* **指针**：到流。



  
**返回**：字节向量。
  
### <a name="operator-function"></a>运算符 |才能
或（|）运算符的操作类型枚举。
  
### <a name="operator-function"></a>运算符 & 函数
操作类型枚举的和（&）运算符。
  
### <a name="operator-function"></a>operator ^ 函数
操作类型枚举的 Xor （^）运算符。

## <a name="namespace-mipauditmetadatakeys"></a>命名空间 mip：： auditmetadatakeys

 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std：： string Sender （）       |  审核字符串表示形式的元数据密钥。
public std：： string 接收者（）       | 尚未记录。
public std：： string LastModifiedBy （）       | 尚未记录。
public std：： string LastModifiedDate （）       | 尚未记录。
  
### <a name="sender-function"></a>Sender 函数
审核字符串表示形式的元数据密钥。
  
### <a name="recipients-function"></a>收件人函数
_尚无记录。_

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy 函数
_尚无记录。_

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate 函数
_尚无记录。_


## <a name="namespace-miprights"></a>命名空间 `mip::rights` 
  
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string Owner()       |  获取“所有者”权限的字符串标识符。
public std::string View()       |  获取“查看”权限的字符串标识符。
public std::string AuditedExtract()       |  获取“已审核的提取”权限的字符串标识符。
public std::string Edit()       |  获取“编辑”权限的字符串标识符。
public std::string Export()       |  获取“导出”权限的字符串标识符。
public std::string Extract()       |  获取“提取”权限的字符串标识符。
public std::string Print()       |  获取“打印”权限的字符串标识符。
public std::string Comment()       |  获取“注释”权限的字符串标识符。
public std::string Reply()       |  获取“回复”权限的字符串标识符。
public std::string ReplyAll()       |  获取“全部回复”权限的字符串标识符。
public std::string Forward()       |  获取“转发”权限的字符串标识符。
public std：： vector\<std：： string\> EmailRights （）       |  获取适用于电子邮件的权限列表。
public std：： vector\<std：： string\> EditableDocumentRights （）       |  获取适用于文档的权限列表。
public std：： vector\<std：： string\> CommonRights （）       |  获取适用于所有方案的权限列表。
  

### <a name="owner-function"></a>所有者函数
获取“所有者”权限的字符串标识符。

  
**返回结果**：“所有者”权限的字符串标识符
  
### <a name="view-function"></a>查看函数
获取“查看”权限的字符串标识符。

  
**返回结果**：“查看”权限的字符串标识符
  
### <a name="auditedextract-function"></a>AuditedExtract 函数
获取“已审核的提取”权限的字符串标识符。

  
**返回结果**：“已审核的提取”权限的字符串标识符
  
### <a name="edit-function"></a>编辑函数
获取“编辑”权限的字符串标识符。

  
**返回结果**：“编辑”权限的字符串标识符
  
### <a name="export-function"></a>导出函数
获取“导出”权限的字符串标识符。

  
**返回结果**：“导出”权限的字符串标识符
  
### <a name="extract-function"></a>Extract 函数
获取“提取”权限的字符串标识符。

  
**返回结果**：“提取”权限的字符串标识符
  
### <a name="print-function"></a>Print 函数
获取“打印”权限的字符串标识符。

  
**返回结果**：“打印”权限的字符串标识符
  
### <a name="comment-function"></a>Comment 函数
获取“注释”权限的字符串标识符。

  
**返回结果**：“注释”权限的字符串标识符
  
### <a name="reply-function"></a>Reply 函数
获取“回复”权限的字符串标识符。

  
**返回结果**：“回复”权限的字符串标识符
  
### <a name="replyall-function"></a>ReplyAll 函数
获取“全部回复”权限的字符串标识符。

  
**返回结果**：“全部回复”权限的字符串标识符
  
### <a name="forward-function"></a>Forward 函数
获取“转发”权限的字符串标识符。

  
**返回结果**：“转发”权限的字符串标识符
  
### <a name="emailrights-function"></a>EmailRights 函数
获取适用于电子邮件的权限列表。

  
**返回结果**：适用于电子邮件的权限列表
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights 函数
获取适用于文档的权限列表。

  
**返回结果**：适用于文档的权限列表
  
### <a name="commonrights-function"></a>CommonRights 函数
获取适用于所有方案的权限列表。

  
**返回结果**：适用于所有方案的权限列表

## <a name="namespace-miproles"></a>命名空间 mip：： roles
  
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  获取“查看者”角色的字符串标识符。
public std::string Reviewer()       |  获取“审阅者”角色的字符串标识符。
public std::string Author()       |  获取“作者”角色的字符串标识符。
public std::string CoOwner()       |  获取“共有者”角色的字符串标识符。
  
### <a name="viewer-function"></a>查看器函数
获取“查看者”角色的字符串标识符。

  
**返回结果**：“查看者”的字符串标识符。查看者只能查看内容， 无法编辑、复制或打印内容。
  
### <a name="reviewer-function"></a>审校函数
获取“审阅者”角色的字符串标识符。

  
**返回结果**：“审阅者”的字符串标识符。审阅者可以查看和编辑内容， 但无法复制或打印内容。
  
### <a name="author-function"></a>Author 函数
获取“作者”角色的字符串标识符。

  
**返回结果**：“作者”角色的字符串标识符。作者可以查看、编辑、复制和打印内容。
  
### <a name="coowner-function"></a>CoOwner 函数
获取“共有者”角色的字符串标识符。

  
**返回结果**：“共有者”角色的字符串标识符。共有者拥有全部权限

