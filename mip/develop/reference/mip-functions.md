---
title: 函数
description: 函数
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: bryanla
ms.openlocfilehash: 614e4bdd589e8c7ad3efdbf9be2f807e6d4ec43a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254180"
---
# <a name="functions"></a>函数

## <a name="summary"></a>总结

| 按命名空间范围函数   | 说明                                |
|--------------------------------|---------------------------------------------|
**Namespace `mip` :** |
public std:: string GetAssignmentMethodString （AssignmentMethod 方法）       |  将 AssignmentMethod 枚举转换为字符串说明。
public static std::string GetActionSourceString(ActionSource actionSource)       |  获取操作的源名称。
public static std::string GetContentStateString(mip::ContentState state)       |  获取内容的状态名称。
public const std::string& GetCustomSettingPolicyDataName()       |  用于明确指定策略数据的设置的名称。
public const std::string& GetCustomSettingExportPolicyFileName()       |  用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。
public const std:: string & GetCustomSettingSensitivityTypesDataName()       |  若要显式指定敏感度数据的设置的名称。
public const std::string& GetCustomSettingPolicyDataFile()       |  用于明确指定策略数据文件路径的设置的名称。
public const std::string& GetCustomSettingSensitivityTypesDataFile()       |  若要显式指定敏感度类型数据的文件路径的设置的名称。
公共 MIP_API void __CDECL ReleaseAllResources()       |  在关闭之前释放所有资源（线程等）。
公共 MIP_API std:: shared_ptr\<mip::Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::istream\>& stdIStream)       |  通过 std::istream 创建 [Stream](class_mip_stream.md)。
公共 MIP_API std:: shared_ptr\<mip::Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::ostream\>& stdOStream)       |  通过 std::ostream 创建 [Stream](class_mip_stream.md)。
公共 MIP_API std:: shared_ptr\<mip::Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std::iostream\>& stdIOStream)       |  通过 std::iostream 创建 [Stream](class_mip_stream.md)。
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  通过缓冲区创建 [Stream](class_mip_stream.md)。
 | 
**Namespace `mip::auditmetadatakeys` :** |
public std:: string Sender()       |  审核字符串表示形式中的元数据密钥。
public std:: string Recipients()       | _尚无记录。_
public std:: string LastModifiedBy()       | _尚无记录。_
public std::string LastModifiedDate()       | _尚无记录。_
 | 
**Namespace `mip::rights` :** |
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
public std:: vector\<std:: string\> EmailRights()       |  获取适用于电子邮件的权限列表。
public std::vector\<std::string\> EditableDocumentRights()       |  获取适用于文档的权限列表。
public std:: vector\<std:: string\> CommonRights()       |  获取适用于所有方案的权限列表。
 | 
**Namespace `mip::roles` :** |
public std::string Viewer()       |  获取“查看者”角色的字符串标识符。
public std::string Reviewer()       |  获取“审阅者”角色的字符串标识符。
public std::string Author()       |  获取“作者”角色的字符串标识符。
public std::string CoOwner()       |  获取“共有者”角色的字符串标识符。



## <a name="namespace-mip"></a>Namespace `mip`

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString 函数
将 AssignmentMethod 枚举转换为字符串说明。

参数：  
* **方法**： 分配方法。 



  
**返回**:分配方法的字符串说明。
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString 函数
获取操作的源名称。

参数：  
* **actionSource**:操作源中。 



  
**返回**:操作源的字符串表示形式。
  
### <a name="getcontentstatestring-function"></a>GetContentStateString 函数
获取内容的状态名称。

参数：  
* **actionSource**:正在处理后的内容的状态。 



  
**返回**:内容状态的字符串表示形式。
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName 函数
用于明确指定策略数据的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName 函数
用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName 函数
若要显式指定敏感度数据的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile 函数
用于明确指定策略数据文件路径的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile 函数
若要显式指定敏感度类型数据的文件路径的设置的名称。

  
**返回**:自定义设置键。
  
### <a name="releaseallresources-function"></a>ReleaseAllResources 函数
在关闭之前释放所有资源（线程等）。
如果应用程序延迟加载 MIP 动态库，则必须在应用程序显式卸载这些 MIP 库之前调用此函数，以避免死锁。 例如，在 win32 中，调用此函数必须之前显式调用卸载通过 FreeLibrary 或 __FUnloadDelayLoadedDLL2 MIP Dll。 在调用此函数之前，应用程序必须释放对所有 MIP 对象（例如，配置文件、引擎、处理程序）的引用。
  
### <a name="operator-function"></a>运算符 |函数
ProtectionHandlerCreationOptions 位 OR 运算符。

参数：  
* :左的值 


* **b**:正确的值



  
**返回**:按位 OR ProtectionHandlerCreationOptions
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
通过 std::istream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdIStream**:后备 std::istream



  
**返回**:[Stream](class_mip_stream.md)包装 std::istream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
通过 std::ostream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdOStream**:后备 std::ostream



  
**返回**:[Stream](class_mip_stream.md)包装 std::ostream
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 函数
通过 std::iostream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdIOStream**:后备 std::iostream



  
**返回**:[Stream](class_mip_stream.md)包装 std::iostream
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer 函数
通过缓冲区创建 [Stream](class_mip_stream.md)。

参数：  
* **缓冲区**:指向缓冲区的指针



  
**返回**:大小的缓冲区大小
  



## <a name="namespace-mipauditmetadatakeys"></a>Namespace `mip::auditmetadatakeys`

### <a name="sender-function"></a>发件人函数
审核字符串表示形式中的元数据密钥。
  
### <a name="recipients-function"></a>收件人函数
_尚无记录。_

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy 函数
_尚无记录。_
  
### <a name="lastmodifieddate-function"></a>LastModifiedDate 函数
_尚无记录。_





## <a name="namespace-miprights"></a>Namespace `mip::rights`

### <a name="owner-function"></a>所有者函数
获取“所有者”权限的字符串标识符。

  
**返回**:所有者右侧的字符串标识符
  
### <a name="view-function"></a>视图函数
获取“查看”权限的字符串标识符。

  
**返回**:右侧字符串提取视图的标识符
  
### <a name="auditedextract-function"></a>AuditedExtract 函数
获取“已审核的提取”权限的字符串标识符。

  
**返回**:右侧字符串提取审核提取的标识符
  
### <a name="edit-function"></a>编辑函数
获取“编辑”权限的字符串标识符。

  
**返回**:编辑右侧的字符串标识符
  
### <a name="export-function"></a>导出函数
获取“导出”权限的字符串标识符。

  
**返回**:右侧字符串提取导出的标识符
  
### <a name="extract-function"></a>提取函数
获取“提取”权限的字符串标识符。

  
**返回**:提取右侧的字符串标识符
  
### <a name="print-function"></a>打印函数
获取“打印”权限的字符串标识符。

  
**返回**:打印右侧的字符串标识符
  
### <a name="comment-function"></a>注释函数
获取“注释”权限的字符串标识符。

  
**返回**:右侧字符串提取 comment 的标识符
  
### <a name="reply-function"></a>回复函数
获取“回复”权限的字符串标识符。

  
**返回**:右侧字符串提取答复的标识符
  
### <a name="replyall-function"></a>全部答复函数
获取“全部回复”权限的字符串标识符。

  
**返回**:全部答复右侧的字符串标识符
  
### <a name="forward-function"></a>转发函数
获取“转发”权限的字符串标识符。

  
**返回**:转发权限的字符串标识符
  
### <a name="emailrights-function"></a>EmailRights 函数
获取适用于电子邮件的权限列表。

  
**返回**:电子邮件应用权限的列表
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights 函数
获取适用于文档的权限列表。

  
**返回**:将应用于文档的权限的列表
  
### <a name="commonrights-function"></a>CommonRights 函数
获取适用于所有方案的权限列表。

  
**返回**:在所有方案中应用的权限的列表




## <a name="namespace-miproles"></a>Namespace `mip::roles`

### <a name="viewer-function"></a>查看器函数
获取“查看者”角色的字符串标识符。

  
**返回**:查看者角色查看器的字符串标识符只能查看内容。 无法编辑、复制或打印内容。
  
### <a name="reviewer-function"></a>审阅者函数
获取“审阅者”角色的字符串标识符。

  
**返回**:审阅者角色审阅者可以查看和编辑内容的字符串标识符。 但无法复制或打印内容。
  
### <a name="author-function"></a>作者函数
获取“作者”角色的字符串标识符。

  
**返回**:作者角色作者可以查看、 编辑、 复制和打印内容的字符串标识符。
  
### <a name="coowner-function"></a>CoOwner 函数
获取“共有者”角色的字符串标识符。

  
**返回**:字符串标识符为共有者角色共同所有者拥有的所有权限
