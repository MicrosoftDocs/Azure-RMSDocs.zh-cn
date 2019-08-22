---
title: 函数
description: 函数
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: 80d13de3778648c2e0230ac37c559b0ca1f62a07
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882805"
---
# <a name="functions"></a>函数

## <a name="summary"></a>总结 

### <a name="namespace-mip"></a>命名空间 mip
| 按命名空间范围的函数   | 说明                                |
|--------------------------------|---------------------------------------------|
public std:: string GetAssignmentMethodString (AssignmentMethod 方法)       |  将 AssignmentMethod 枚举转换为字符串说明。
public static std:: string GetActionSourceString (ActionSource actionSource)       |  获取操作源名称。
public static std:: string GetDataStateString (mip::D ataState 状态)       |  获取内容状态名称。
public const std::string& GetCustomSettingPolicyDataName()       |  用于明确指定策略数据的设置的名称。
public const std::string& GetCustomSettingExportPolicyFileName()       |  用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。
public const std:: string & GetCustomSettingSensitivityTypesDataName ()       |  用于显式指定敏感度数据的设置的名称。
public const std::string& GetCustomSettingPolicyDataFile()       |  用于明确指定策略数据文件路径的设置的名称。
public const std:: string & GetCustomSettingSensitivityTypesDataFile ()       |  用于显式指定敏感度类型数据文件路径的设置的名称。
public const std:: string & GetCustomSettingLabelCustomPropertiesSyncEnabled ()       |  允许按照标签功能按自定义属性和自定义属性启用标签的设置的名称。
public const std:: map\<FlightingFeature, bool\>& GetDefaultFeatureSettings ()       |  获取默认情况下是否启用功能。
public MIP_API void __CDECL ReleaseAllResources ()       |  在关闭之前释放所有资源 (线程等)。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: istream\>& stdIStream)       |  通过 std::istream 创建 [Stream](class_mip_stream.md)。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: ostream\>& stdOStream)       |  通过 std::ostream 创建 [Stream](class_mip_stream.md)。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: iostream\>& stdIOStream)       |  通过 std::iostream 创建 [Stream](class_mip_stream.md)。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromBuffer (uint8_t * buffer, const int64_t size)       |  通过缓冲区创建 [Stream](class_mip_stream.md)。
public MIP_API std:: vector\<uint8_t\> ReadFromStream (const std:: shared_ptr\<MIP:: stream\>& 流)       |  读取所有流的字节数。

### <a name="namespace-mipauditmetadatakeys"></a>命名空间 mip:: auditmetadatakeys
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std:: string Sender ()       |  审核字符串表示形式的元数据密钥。
public std:: string 接收者 ()       | _尚无记录。_
public std:: string LastModifiedBy ()       | _尚无记录。_
public std:: string LastModifiedDate ()       | _尚无记录。_


### <a name="namespace-miprights"></a>命名空间 mip:: 权限

 成员                        | 说明                                
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
public std:: vector\<std:: string\> EmailRights ()       |  获取适用于电子邮件的权限列表。
public std:: vector\<std:: string\> EditableDocumentRights ()       |  获取适用于文档的权限列表。
public std:: vector\<std:: string\> CommonRights ()       |  获取适用于所有方案的权限列表。

### <a name="namespace-miproles"></a>命名空间 mip:: roles

 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  获取“查看者”角色的字符串标识符。
public std::string Reviewer()       |  获取“审阅者”角色的字符串标识符。
public std::string Author()       |  获取“作者”角色的字符串标识符。
public std::string CoOwner()       |  获取“共有者”角色的字符串标识符。

## <a name="namespace-mip"></a>命名空间 mip

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString 函数
将 AssignmentMethod 枚举转换为字符串说明。

参数：  
* **方法**: 赋值方法。 



  
**返回**:分配方法的字符串说明。
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString 函数
获取操作源名称。

参数：  
* **actionSource**:操作源。 



  
**返回**:操作源的字符串表示形式。
  
### <a name="getdatastatestring-function"></a>GetDataStateString 函数
获取内容状态名称。

参数：  
* **actionSource**:正在处理的内容的状态。 



  
**返回**:内容状态的字符串表示形式。
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName 函数
用于明确指定策略数据的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName 函数
用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName 函数
用于显式指定敏感度数据的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile 函数
用于明确指定策略数据文件路径的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile 函数
用于显式指定敏感度类型数据文件路径的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingexternallabelsenabled-function"></a>GetCustomSettingExternalLabelsEnabled 函数
允许启用 "外部标签" 功能的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="releaseallresources-function"></a>ReleaseAllResources 函数
在关闭之前释放所有资源 (线程等)。
在终止进程之前, 必须只调用一次此函数。 它为您提供了一种方法, 以便在其依赖库仍可保证加载并且仍可以进行线程联接的一段时间内自行取消初始化。 在调用此函数之前，应用程序必须释放对所有 MIP 对象（例如，配置文件、引擎、处理程序）的引用。
如果未调用此函数, 则在标准进程拆卸过程中将自然卸载 MIP。 在某些平台上, 这可能会导致死锁 (例如, 无法在 win32 上联接线程以响应进程拆卸) 或发生故障 (例如, win32 上延迟加载库的 DLL 卸载顺序不受 MIP 控制, 因此它的依赖库可能已在 MIP 关闭代码执行时被卸载, 从而导致无效的读取失败)。
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
通过 std::istream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdIStream**:支持 std:: istream



  
**返回**:[流](class_mip_stream.md)包装 std:: istream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
通过 std::ostream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdOStream**:支持 std:: ostream



  
**返回**:[流](class_mip_stream.md)包装 std:: ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
通过 std::iostream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdIOStream**:支持 std:: iostream



  
**返回**:[流](class_mip_stream.md)包装 std:: iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer 函数
通过缓冲区创建 [Stream](class_mip_stream.md)。

参数：  
* **缓冲区**:指向缓冲区的指针



  
**返回**:缓冲区大小
  



## <a name="namespace-mipauditmetadatakeys"></a>命名空间 mip:: auditmetadatakeys

### <a name="sender-function"></a>Sender 函数
审核字符串表示形式的元数据密钥。
  
### <a name="recipients-function"></a>收件人函数
_尚无记录。_

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy 函数
_尚无记录。_

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate 函数
_尚无记录。_






## <a name="namespace-miprights"></a>命名空间 mip:: 权限

### <a name="owner-function"></a>所有者函数
获取“所有者”权限的字符串标识符。

  
**返回**:"Owner" 权限的字符串标识符
  
### <a name="view-function"></a>查看函数
获取“查看”权限的字符串标识符。

  
**返回**:"View" 权限的字符串标识符
  
### <a name="auditedextract-function"></a>AuditedExtract 函数
获取“已审核的提取”权限的字符串标识符。

  
**返回**:"审核提取" 权限的字符串标识符
  
### <a name="edit-function"></a>编辑函数
获取“编辑”权限的字符串标识符。

  
**返回**:"编辑" 权限的字符串标识符
  
### <a name="export-function"></a>导出函数
获取“导出”权限的字符串标识符。

  
**返回**:"Export" 权限的字符串标识符
  
### <a name="extract-function"></a>提取函数
获取“提取”权限的字符串标识符。

  
**返回**:"提取" 权限的字符串标识符
  
### <a name="print-function"></a>Print 函数
获取“打印”权限的字符串标识符。

  
**返回**:"Print" 右侧的字符串标识符
  
### <a name="comment-function"></a>Comment 函数
获取“注释”权限的字符串标识符。

  
**返回**:"Comment" 权限的字符串标识符
  
### <a name="reply-function"></a>Reply 函数
获取“回复”权限的字符串标识符。

  
**返回**:"答复" 权限的字符串标识符
  
### <a name="replyall-function"></a>ReplyAll 函数
获取“全部回复”权限的字符串标识符。

  
**返回**:"全部答复" 权限的字符串标识符
  
### <a name="forward-function"></a>Forward 函数
获取“转发”权限的字符串标识符。

  
**返回**:"转发" 权限的字符串标识符
  
### <a name="emailrights-function"></a>EmailRights 函数
获取适用于电子邮件的权限列表。

  
**返回**:适用于电子邮件的权限列表
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights 函数
获取适用于文档的权限列表。

  
**返回**:适用于文档的权限列表
  
### <a name="commonrights-function"></a>CommonRights 函数
获取适用于所有方案的权限列表。

  
**返回**:适用于所有方案的权限列表


## <a name="namespace-miproles"></a>命名空间 mip:: roles

### <a name="viewer-function"></a>查看器函数
获取“查看者”角色的字符串标识符。

  
**返回**:"查看者" 角色的字符串标识符查看器只能查看内容。 无法编辑、复制或打印内容。
  
### <a name="reviewer-function"></a>审校函数
获取“审阅者”角色的字符串标识符。

  
**返回**:"审阅者" 角色的字符串标识符审阅者可以查看和编辑内容。 但无法复制或打印内容。
  
### <a name="author-function"></a>Author 函数
获取“作者”角色的字符串标识符。

  
**返回**:作者可以查看、编辑、复制和打印内容的 "author" 角色的字符串标识符。
  
### <a name="coowner-function"></a>CoOwner 函数
获取“共有者”角色的字符串标识符。

  
**返回**:"共同所有者" 角色的字符串标识符共同所有者拥有所有权限