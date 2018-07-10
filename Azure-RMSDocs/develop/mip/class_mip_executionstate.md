# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
执行引擎所需的所有状态的接口。
客户端应只调用方法来获取所需的状态。 因此，为了提高效率，客户端可能想要实现该接口，以此动态计算相应的状态而不是提前计算。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  获取应在文档上应用的敏感度标签 ID。
 public bool IsDowngradeJustified() const  |  实现应传递是否提供了降级现有标签的合理理由。
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  获取新标签的分配方法。
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  返回新标签的扩展属性。
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  从内容中获取元数据项。
 public std::string GetTemplateId() const  |  获取权限管理服务保护模板 ID。
 public ContentFormat GetContentFormat() const  |  获取内容格式。
 public ActionType GetSupportedActions() const  |  获取表示所有支持操作类型的掩码枚举。
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  返回分类结果的映射。
  
## <a name="members"></a>成員
  
### <a name="getnewlabelid"></a>GetNewLabelId
获取应在文档上应用的敏感度标签 ID。

  
**返回结果**：如果存在，则返回要应用于内容的敏感度标签 ID，否则为空以删除标签。
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
实现应传递是否提供了降级现有标签的合理理由。

  
**返回结果**：如果降级合理，返回 true，如果尚未进行合理性验证，则返回 false。 
  
另请参阅：[mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
获取新标签的分配方法。

  
**返回结果**：分配方法 STANDARD、PRIVILEGED、AUTO。 
  
另请参阅：mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
返回新标签的扩展属性。

  
**返回结果**：键值对矢量，表示应用到内容的扩展属性。
  
### <a name="getcontentmetadata"></a>GetContentMetadata
从内容中获取元数据项。

  
**返回结果**：表示应用于内容的元数据的键值对的矢量。 每个元数据项都是名称和值对。
  
### <a name="gettemplateid"></a>GetTemplateId
获取权限管理服务保护模板 ID。

  
**返回结果**：权限管理服务保护模板 ID（若有），否则返回空字符串（不带括号的 GUID 格式）。
  
### <a name="getcontentformat"></a>GetContentFormat
获取内容格式。

  
**返回结果**：DEFAULT、EMAIL 
  
**另请参阅**：mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
获取表示所有支持操作类型的掩码枚举。

  
**返回结果**：表示所有支持操作类型的掩码枚举。
  
### <a name="classificationresult"></a>ClassificationResult
返回分类结果的映射。

参数：  
* **classificationId**：分类 ID 的列表。 



  
**返回结果**：分类结果列表。