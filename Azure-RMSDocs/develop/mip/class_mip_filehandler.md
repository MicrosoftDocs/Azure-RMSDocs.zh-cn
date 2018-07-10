# <a name="class-mipfilehandler"></a>class mip::FileHandler 
适用于所有文件处理函数的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  开始从文件检索敏感度标签。
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  开始从文件检索保护策略。
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  设置文件的敏感度标签。
 public void DeleteLabel(AssignmentMethod method, const std::string& justificationMessage)  |  从文件删除敏感度标签。
public void SetProtection(const std::shared_ptr<ProtectionDescriptor>& protectionDescriptor)  |  （根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
 public void RemoveProtection()  |  删除文件保护。 如果文件已添加标签，标签将丢失。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | 将所做的更改写入到 \|outputFilePath\ 参数指定的文件 |  参数。
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | 将所做的更改写入到 \|outputStream\ 参数指定的流。 |  参数。
 public std::string GetOutputFileName()  |  基于原始文件名和累积的更改，计算输出文件名称和扩展名。
 public virtual ~FileHandler()  | _尚无记录。_
 受保护的 FileHandler()  | _尚无记录。_
  
## <a name="members"></a>成員
  
### <a name="getlabelasync"></a>GetLabelAsync
开始从文件检索敏感度标签。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="getprotectionasync"></a>GetProtectionAsync
开始从文件检索保护策略。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="setlabel"></a>SetLabel
设置文件的敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。
在设置标签时需要提供合理理由，如果未通过 labelingOptions 参数提供所需理由，将引发 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  
### <a name="deletelabel"></a>DeleteLabel
从文件删除敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 借助特权自动方法，此 API 可以重写任何现有标签。如果在设置标签时需要提供合理解释，但未通过 justificationMessage 参数提供合理解释消息，就会抛出 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  
### <a name="setprotection"></a>SetProtection
（根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="removeprotection"></a>RemoveProtection
删除文件保护。 如果文件已添加标签，标签将丢失。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="commitasync"></a>CommitAsync
将所做的更改写入到 |outputFilePath| 参数指定的文件。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="commitasync"></a>CommitAsync
将所做的更改写入到 |outputStream| 参数指定的流。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="getoutputfilename"></a>GetOutputFileName
基于原始文件名和累积的更改，计算输出文件名称和扩展名。
  
### <a name="filehandler"></a>~FileHandler
_尚无记录。_

  
### <a name="filehandler"></a>FileHandler
_尚无记录。_
