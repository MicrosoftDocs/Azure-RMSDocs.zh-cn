# <a name="class-mipfileengine"></a>class mip::FileEngine 
适用于所有引擎功能的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline virtual ~FileEngine()  |  
public const Settings& GetSettings() const  |  返回引擎设置。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  返回敏感度标签列表。
public std::shared_ptr<FileHandler> CreateFileHandler(const std::string& inputFilePath, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  返回给定文件路径的文件处理程序。
public std::shared_ptr<FileHandler> CreateFileHandler(const std::shared_ptr<Stream>& inputStream, const std::string& inputFileName, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  返回给定文件流的文件处理程序。
protected inline FileEngine()  |  
  
## <a name="members"></a>成員
  
### <a name="fileengine"></a>~FileEngine
  
### <a name="settings"></a>设置
返回引擎设置。
  
### <a name="label"></a>Label
返回敏感度标签列表。
  
### <a name="filehandler"></a>FileHandler
返回给定文件路径的文件处理程序。
  
#### <a name="parameters"></a>参数
* 要打开的文件。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 
* 实现 [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) 接口的类。
  
### <a name="filehandler"></a>FileHandler
返回给定文件流的文件处理程序。
  
#### <a name="parameters"></a>参数
* 表示文件的流。 
* 文件路径。 路径必须包含文件名称，如果已存在，则包含文件扩展名。 
* 实现 [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) 接口的类。
  
### <a name="fileengine"></a>FileEngine