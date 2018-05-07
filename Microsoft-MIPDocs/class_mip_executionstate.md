# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
执行引擎所需的所有状态的接口。
客户端应只调用方法来获取所需的状态。 因此，为了提高效率，客户端可能想要实现该接口，以此动态计算相应的状态而不是提前计算。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId | 获取应在文档上应用的敏感度标签 ID。
public bool IsDowngradeJustified | 实现应传递是否提供了降级现有标签的合理理由。
public AssignmentMethod GetNewLabelAssignmentMethod | 获取新标签的分配方法。
public std::vector< std::pair< std::string, std::string > > GetContentMetadata | 从内容中获取元数据项。
public std::string GetTemplateId | 获取权限管理服务保护模板 ID。
public ContentFormat GetContentFormat | 获取内容格式。
public const ActionType GetSupportedActions
## <a name="members"></a>成員
### <a name="getnewlabelid"></a>GetNewLabelId
获取应在文档上应用的敏感度标签 ID。
#### <a name="returns"></a>Returns
如果存在，则返回要应用于内容的敏感度标签 ID，否则为空以删除标签。
### <a name="isdowngradejustified"></a>IsDowngradeJustified
实现应传递是否提供了降级现有标签的合理理由。
#### <a name="returns"></a>Returns
如果降级合理，返回 true，如果尚未进行合理性验证，则返回 false。 
另请参阅：[mip::JustifyAction](#classmip_1_1_justify_action)
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
获取新标签的分配方法。
#### <a name="returns"></a>Returns
分配方法 STANDARD、PRIVILEGED、AUTO。 
另请参阅：mip::AssignmentMethod
### <a name="getcontentmetadata"></a>GetContentMetadata
从内容中获取元数据项。
#### <a name="returns"></a>Returns
表示应用于内容的元数据的键值对的矢量。 每个元数据项都是名称和值对。
### <a name="gettemplateid"></a>GetTemplateId
获取权限管理服务保护模板 ID。
#### <a name="returns"></a>Returns
如果存在，将返回权限管理服务保护模板 ID，否则以不带括号的 guid 格式返回一个空字符串。
### <a name="getcontentformat"></a>GetContentFormat
获取内容格式。
#### <a name="returns"></a>Returns
默认情况下，电子邮件另请参阅：mip::ContentFormat
### <a name="actiontype"></a>ActionType
返回应用程序支持的操作列表。 所有操作类型都在 [mip/upe/action.h](#action_8h) 中列出。