# <a name="class-mipprotectbytemplateaction"></a>class mip::ProtectByTemplateAction 
指定向文档添加模板保护的操作类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public const std::string& GetTemplateId() const  |  获取与操作关联的保护模板 ID。
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="gettemplateid"></a>GetTemplateId
获取与操作关联的保护模板 ID。

  
**返回结果**：包含保护模板 ID 的字符串。
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。