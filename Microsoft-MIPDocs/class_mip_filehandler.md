# <a name="class-mipfilehandler"></a>class mip::FileHandler 
适用于所有文件处理函数的接口。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public void GetLabelAsync | 开始从文件检索敏感度标签。
public void GetProtectionAsync | 开始从文件检索保护策略。
public void SetLabelLabelingOptions & labelingOptions) | 设置文件的敏感度标签。
public void DeleteLabel | 从文件删除敏感度标签。
public void SetCustomPermissionsPolicyDescriptor > & policyDescriptor) | 设置文件的自定义权限。
public void RemoveProtection | 删除文件保护。 如果文件已添加标签，标签将丢失。
public void CommitAsync | 将所做的更改写入到 \|outputFilePath\| 参数指定的文件。
public void CommitAsyncStream > & outputStream,const std::shared_ptr< void > & context) | 将所做的更改写入到 \|outputStream\| 参数指定的流。
public std::string GetOutputFileName | 基于原始文件名和累积的更改，计算输出文件名称和扩展名。
public inline virtual  ~FileHandler | 
protected inline  FileHandler | 
## <a name="members"></a>成員
### <a name="getlabelasync"></a>GetLabelAsync
开始从文件检索敏感度标签。
[FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) 将在成功或失败时调用。
#### <a name="parameters"></a>参数
* context：将以不透明形式传递回观察程序的客户端上下文。
### <a name="getprotectionasync"></a>GetProtectionAsync
开始从文件检索保护策略。
[FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) 将在成功或失败时调用。
#### <a name="parameters"></a>参数
* context：将以不透明形式传递回观察程序的客户端上下文。
### <a name="setlabel"></a>SetLabel
设置文件的敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。
在设置标签时需要提供合理理由，如果未通过 labelingOptions 参数提供所需理由，将引发 [JustificationRequiredError](#classmip_1_1_justification_required_error)。
### <a name="deletelabel"></a>DeleteLabel
从文件中删除敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。在设置标签时需要提供合理理由，如果未通过 justificationMessage 参数提供所需理由，将引发 [JustificationRequiredError](#classmip_1_1_justification_required_error)。
### <a name="setcustompermissions"></a>SetCustomPermissions
设置文件的自定义权限。
在调用 CommitAsync 之前，不会将更改写入文件。
### <a name="removeprotection"></a>RemoveProtection
删除文件保护。 如果文件已添加标签，标签将丢失。
在调用 CommitAsync 之前，不会将更改写入文件。
### <a name="commitasync"></a>CommitAsync
将所做的更改写入到 |outputFilePath| 参数指定的文件。
[FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) 将在成功或失败时调用。
### <a name="commitasync"></a>CommitAsync
将所做的更改写入到 |outputStream| 参数指定的流。
[FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) 将在成功或失败时调用。
### <a name="getoutputfilename"></a>GetOutputFileName
基于原始文件名和累积的更改，计算输出文件名称和扩展名。
### <a name="filehandler"></a>~FileHandler
### <a name="filehandler"></a>FileHandler