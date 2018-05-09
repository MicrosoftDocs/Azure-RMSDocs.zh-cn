# <a name="class-mippolicyengine"></a>class mip::PolicyEngine 
此类提供适用于所有引擎功能的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  获取策略引擎[设置](#classmip_1_1_policy_engine_1_1_settings)。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  列出与策略引擎关联的敏感度标签。
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  从现有内容获取敏感度标签。
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  获取默认敏感度标签。
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  根据所提供的状态执行引擎中的规则，并返回要执行的操作列表。
  
## <a name="members"></a>成員
  
### <a name="settings"></a>设置
获取策略引擎[设置](#classmip_1_1_policy_engine_1_1_settings)。
  
#### <a name="returns"></a>Returns
策略引擎设置。 
另请参阅：[mip::PolicyEngine::Settings](#classmip_1_1_policy_engine_1_1_settings)
  
### <a name="label"></a>Label
列出与策略引擎关联的敏感度标签。
  
#### <a name="returns"></a>Returns
敏感度标签列表。
  
### <a name="contentlabel"></a>ContentLabel
从现有内容获取敏感度标签。
检索标签所需的信息将通过使用提供的执行状态获得。 
  
#### <a name="parameters"></a>参数
* state 
  
#### <a name="returns"></a>Returns
一个包含敏感度标签以及其他信息的内容标签对象。 如果不存在，则返回空。 
另请参阅：[mip::ContentLabel](#classmip_1_1_content_label)。
  
### <a name="label"></a>Label
获取默认敏感度标签。
  
#### <a name="returns"></a>Returns
如果存在，则返回默认敏感度标签，如果未设置默认标签，则返回 nullptr。
  
### <a name="action"></a>操作
根据所提供的状态执行引擎中的规则，并返回要执行的操作列表。
  
#### <a name="parameters"></a>参数
* state：在其中运行规则的内容的当前执行状态。 
  
#### <a name="returns"></a>Returns
应应用于内容的操作列表。