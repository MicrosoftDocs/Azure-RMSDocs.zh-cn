# <a name="functions"></a>函数

 函数（作用域）                        | 描述                                
--------------------------------|---------------------------------------------
public const std::string& GetCustomSettingExportPolicyFileName()       |  用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。
public const std::string& GetCustomSettingPolicyDataFile()       |  用于明确指定策略数据文件路径的设置的名称。
public const std::string& GetCustomSettingPolicyDataName()       |  用于明确指定策略数据的设置的名称。
**mip 函数** |
public std::shared_ptr<mip::Stream> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  通过缓冲区创建 [Stream](class_mip_stream.md)。
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::iostream>& stdIOStream)       |  通过 std::iostream 创建 [Stream](class_mip_stream.md)。
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::istream>& stdIStream)       |  通过 std::istream 创建 [Stream](class_mip_stream.md)。
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::ostream>& stdOStream)       |  通过 std::ostream 创建 [Stream](class_mip_stream.md)。
**mip::Rights 函数**|
public std::string AuditedExtract()       |  获取“已审核的提取”权限的字符串标识符。
public std::string Comment()       |  获取“注释”权限的字符串标识符。
public std::vector<std::string> CommonRights()       |  获取适用于所有方案的权限列表。
public std::string Edit()       |  获取“编辑”权限的字符串标识符。
public std::vector<std::string> EditableDocumentRights()       |  获取适用于文档的权限列表。
public std::vector<std::string> EmailRights()       |  获取适用于电子邮件的权限列表。
public std::string Export()       |  获取“导出”权限的字符串标识符。
public std::string Extract()       |  获取“提取”权限的字符串标识符。
public std::string Forward()       |  获取“转发”权限的字符串标识符。
public std::string Owner()       |  获取“所有者”权限的字符串标识符。
public std::string Print()       |  获取“打印”权限的字符串标识符。
public std::string Reply()       |  获取“回复”权限的字符串标识符。
public std::string ReplyAll()       |  获取“全部回复”权限的字符串标识符。
public std::string View()       |  获取“查看”权限的字符串标识符。
**mip::Roles 函数**|
public std::string Author()       |  获取“作者”角色的字符串标识符。
public std::string CoOwner()       |  获取“共有者”角色的字符串标识符。
public std::string Reviewer()       |  获取“审阅者”角色的字符串标识符。
public std::string Viewer()       |  获取“查看者”角色的字符串标识符。

  
## <a name="enumeration-details"></a>枚举详细信息
  
## <a name="functions-common"></a>函数（通用）

### <a name="getcustomsettingpolicydataname"></a>GetCustomSettingPolicyDataName
用于明确指定策略数据的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getcustomsettingexportpolicyfilename"></a>GetCustomSettingExportPolicyFileName
用于明确指定将 SCC 策略数据导出到的文件路径的设置的名称。

  
**返回结果**：自定义设置键。
  
### <a name="getcustomsettingpolicydatafile"></a>GetCustomSettingPolicyDataFile
用于明确指定策略数据文件路径的设置的名称。

  
**返回结果**：自定义设置键。

## <a name="functions-mip"></a>函数 (mip)

### <a name="mipstream-istream"></a>mip::Stream (istream)

通过 std::istream 创建 [Stream](class_mip_stream.md)。

参数：  

* **stdIStream**：回溯 std::istream
  
**返回结果**：包装 std::istream 的 [Stream](class_mip_stream.md)
  
### <a name="mipstream-ostream"></a>mip::Stream (ostream)

通过 std::ostream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdOStream**：回溯 std::ostream

  
**返回结果**：包装 std::ostream 的 [Stream](class_mip_stream.md)
  
### <a name="mipstream-iostream"></a>mip::Stream (iostream)

通过 std::iostream 创建 [Stream](class_mip_stream.md)。

参数：  
* **stdIOStream**：回溯 std::iostream
  
**返回结果**：包装 std::iostream 的 [Stream](class_mip_stream.md)
  
### <a name="mipstream-buffer"></a>mip::Stream（缓冲区）

通过缓冲区创建 [Stream](class_mip_stream.md)。

参数：  
* **buffer**：指向缓冲区的指针

**返回结果**：缓冲区大小
  
## <a name="functions-miprights"></a>函数 (mip::rights)

### <a name="auditedextract"></a>AuditedExtract
获取“已审核的提取”权限的字符串标识符。

  
**返回结果**：“已审核的提取”权限的字符串标识符
  
### <a name="comment"></a>注释
获取“注释”权限的字符串标识符。

  
**返回结果**：“注释”权限的字符串标识符
  
### <a name="commonrights"></a>CommonRights
获取适用于所有方案的权限列表。

  
**返回结果**：适用于所有方案的权限列表

### <a name="edit"></a>编辑
获取“编辑”权限的字符串标识符。

  
**返回结果**：“编辑”权限的字符串标识符
  
### <a name="editabledocumentrights"></a>EditableDocumentRights
获取适用于文档的权限列表。

  
**返回结果**：适用于文档的权限列表
  
### <a name="emailrights"></a>EmailRights
获取适用于电子邮件的权限列表。

  
**返回结果**：适用于电子邮件的权限列表
  
### <a name="export"></a>导出
获取“导出”权限的字符串标识符。

  
**返回结果**：“导出”权限的字符串标识符
  
### <a name="extract"></a>提取
获取“提取”权限的字符串标识符。

  
**返回结果**：“提取”权限的字符串标识符
  

### <a name="forward"></a>转发
获取“转发”权限的字符串标识符。

  
**返回结果**：“转发”权限的字符串标识符
  
### <a name="owner"></a>Owner
获取“所有者”权限的字符串标识符。

  
**返回结果**：“所有者”权限的字符串标识符
  
### <a name="print"></a>打印
获取“打印”权限的字符串标识符。

  
**返回结果**：“打印”权限的字符串标识符
  
### <a name="reply"></a>答复
获取“回复”权限的字符串标识符。

  
**返回结果**：“回复”权限的字符串标识符
  
### <a name="replyall"></a>全部答复
获取“全部回复”权限的字符串标识符。

  
**返回结果**：“全部回复”权限的字符串标识符
  
### <a name="view"></a>视图
获取“查看”权限的字符串标识符。

  
**返回结果**：“查看”权限的字符串标识符
  
## <a name="functions-miproles"></a>函数 (mip::roles)

### <a name="author"></a>作者
获取“作者”角色的字符串标识符。

  
**返回结果**：“作者”角色的字符串标识符。作者可以查看、编辑、复制和打印内容。
  
### <a name="coowner"></a>CoOwner
获取“共有者”角色的字符串标识符。

  
**返回结果**：“共有者”角色的字符串标识符。共有者拥有全部权限

### <a name="reviewer"></a>审阅者
获取“审阅者”角色的字符串标识符。

  
**返回结果**：“审阅者”的字符串标识符。审阅者可以查看和编辑内容， 但无法复制或打印内容。

### <a name="viewer"></a>查看器
获取“查看者”角色的字符串标识符。

  
**返回结果**：“查看者”的字符串标识符。查看者只能查看内容， 无法编辑、复制或打印内容。
  
  
