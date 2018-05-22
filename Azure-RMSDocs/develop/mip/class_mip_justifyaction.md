# <a name="class-mipjustifyaction"></a>class mip::JustifyAction 
合理性验证[操作](class_mip_action.md)需要向标签降级提供合理理由，并在执行状态下设置响应。
另请参阅：[mip::ExecutionState::IsDowngradeJustified](class_mip_executionstate.md#isdowngradejustified)
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public ActionType GetType() const  |  获取[操作](class_mip_action.md)类型。
  
## <a name="members"></a>成員
  
### <a name="actiontype"></a>ActionType
获取[操作](class_mip_action.md)类型。

  
**返回结果**：ActionType：此基类可以转换成的派生操作类型。