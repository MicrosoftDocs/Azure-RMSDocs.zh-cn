# <a name="class-mipremovewatermarkaction"></a>class mip::RemoveWatermarkAction 
一个操作类，指定从文档中移除水印。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::vector< std::string > & GetUIElementNames | 获取应用于查找应删除的 UI 元素的名称列表。
public ActionType GetType
## <a name="members"></a>成員
### <a name="getuielementnames"></a>GetUIElementNames
获取应用于查找应删除的 UI 元素的名称列表。
#### <a name="returns"></a>Returns
UI 元素名称列表。
### <a name="actiontype"></a>ActionType
获取[操作](#classmip_1_1_action)类型。
#### <a name="returns"></a>Returns
ActionType：此基类可以转换成的派生操作类型。