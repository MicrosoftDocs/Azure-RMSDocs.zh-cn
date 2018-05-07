# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
指定应将哪些元数据信息添加到内容的[操作](#classmip_1_1_action)。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::vector< std::string > & GetMetadataToRemove | 获取需要从内容中删除的元数据名称的列表。
public const std::vector< std::pair< std::string, std::string > > & GetMetadataToAdd | 获取作为键值对的元数据的列表。 元数据需要添加到内容元数据。
public ActionType GetType
## <a name="members"></a>成員
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
获取需要从内容中删除的元数据名称的列表。
#### <a name="returns"></a>Returns
要删除的字符串矢量。 在添加元数据之前应先删除元数据。
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
获取作为键值对的元数据的列表。 元数据需要添加到内容元数据。
#### <a name="returns"></a>Returns
const std::vector<std::pair<std::string, std::string>>& 在添加元数据之前应先删除元数据。
### <a name="actiontype"></a>ActionType
获取[操作](#classmip_1_1_action)类型。
#### <a name="returns"></a>Returns
ActionType：此基类可以转换成的派生操作类型。