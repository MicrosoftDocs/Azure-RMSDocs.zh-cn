# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
应用标签操作要求，必须调用应用程序，才能应用特定标签。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const std::string& GetLabelId() const  |  获取所需的标签 ID。
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getlabelid"></a>GetLabelId
获取所需的标签 ID。

  
**返回结果**：标签 ID。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。