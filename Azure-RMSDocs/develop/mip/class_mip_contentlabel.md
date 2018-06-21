# <a name="class-mipcontentlabel"></a>class mip::ContentLabel 
Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
除了标签信息，它还包含特定应用标签的属性。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  获取标签的创建时间。
 public AssignmentMethod GetAssignmentMethod() const  |  获取标签的分配方法。
public std::shared_ptr<Label> GetLabel() const  |  获取应用于内容的实际标签对象。
  
## <a name="members"></a>成員
  
### <a name="getcreationtime"></a>GetCreationTime
获取标签的创建时间。

  
**返回结果**：gmt 字符串的创建时间。
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
获取标签的分配方法。

  
**返回结果**：AssignmentMethod STANDARD | PRIVILEGED | AUTO。 
另请参阅：mip::AssignmentMethod
  
### <a name="label"></a>Label
获取应用于内容的实际标签对象。

  
**返回结果**：应用于内容的标签对象。 
另请参阅：[mip::Label](class_mip_label.md)