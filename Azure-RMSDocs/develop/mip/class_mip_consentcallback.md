# <a name="class-mipconsentcallback"></a>class mip::ConsentCallback 
同意请求通知的接口。
此回调由客户端应用程序实现，以了解应何时向用户显示同意通知。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public ConsentList Consents(ConsentList& consents)  |  SDK 需要用户同意操作时调用。
  
## <a name="members"></a>成員
  
### <a name="consentlist"></a>ConsentList
SDK 需要用户同意操作时调用。
  
#### <a name="parameters"></a>参数
* consents：SDK 请求的同意列表
  
#### <a name="returns"></a>Returns
[同意](#classmip_1_1_consent)结果：如果是由 SDK 请求同意，客户端应用程序应从用户那里获取同意，每个同意的结果应通过 [Consent::Result(const ConsentResult&)](#classmip_1_1_consent_1ad6c17d9af548a40b2fe854fe0d9bca64) 存储，且应返回已解决的同意列表。