# <a name="class-consentdelegate"></a>类 ConsentDelegate 
执行许可相关操作的委托。
此委托由客户端应用程序实现，以了解应何时向用户显示许可请求通知。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
 public Consent GetUserConsent(const std::string& url)  |  在 SDK 要求用户许可连接到服务终结点时调用。
  
## <a name="members"></a>成員
  
### <a name="consent"></a>Consent
在 SDK 要求用户许可连接到服务终结点时调用。

参数：  
* **url**：SDK 要求用户许可的 URL



  
**返回结果**：包含用户决定的许可枚举。
如果 SDK 通过这种方法请求获取用户许可，客户端应用程序应向用户显示 URL。 客户端应用程序应提供一些用于获取用户许可的方法，并返回与用户决定对应的相应许可枚举。