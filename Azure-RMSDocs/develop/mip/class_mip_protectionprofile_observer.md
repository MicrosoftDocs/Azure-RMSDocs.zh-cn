# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
接收与 [ProtectionProfile](#classmip_1_1_protection_profile) 相关通知的接口。
此接口必须由应用程序通过使用保护 SDK 来实现
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccessProtectionProfile > & profile,const std::shared_ptr< void > & context) | 在成功加载配置文件时调用。
public inline virtual void OnLoadFailure | 在加载配置文件引发错误时调用。
## <a name="members"></a>成員
### <a name="onloadsuccess"></a>OnLoadSuccess
在成功加载配置文件时调用。
#### <a name="parameters"></a>参数
* profile：对新创建的 [ProtectionProfile](#classmip_1_1_protection_profile) 的引用
* context：传递到 [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) 的相同上下文。应用程序可以将任何类型的上下文（例如 std::promise、std::function 等）传递到 [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) 或 [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)
### <a name="onloadfailure"></a>OnLoadFailure
在加载配置文件引发错误时调用。
#### <a name="parameters"></a>参数
* error：加载时发生的[错误](#classmip_1_1_error) 
* context：传递到 [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) 的相同上下文。应用程序可以将任何类型的上下文（例如 std::promise、std::function 等）传递到 [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031)，而此相同上下文将按原样转发给 [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) 或 [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291)