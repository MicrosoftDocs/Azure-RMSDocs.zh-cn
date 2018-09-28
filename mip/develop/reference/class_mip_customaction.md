# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](class_mip_customaction.md) 是一个泛型操作类，它捕获操作的所有子属性作为一个属性包。 调用方负责理解操作的含义。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::vector<std::pair<std::string, std::string>>& GetProperties() const  |  获取属性键值对列表。
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="getproperties"></a>GetProperties
获取属性键值对列表。

  
**返回结果**：键值对列表。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。