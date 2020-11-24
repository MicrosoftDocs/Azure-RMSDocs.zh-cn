---
title: 类 FileHandler
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 filehandler：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: bf3866fb1ec06156ebf40b2efed8c44f8af4a4ce
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565137"
---
# <a name="class-filehandler"></a>类 FileHandler 
适用于所有文件处理函数的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std：： shared_ptr \<ContentLabel\> GetLabel ( # A1  |  开始从文件检索敏感度标签。
公共 std：： vector \<std::pair\<std::string, std::string\> \> GetProperties (uint32_t 版本)   |  根据版本 Retrievs 文件 propertries。
public std：： shared_ptr \<ProtectionHandler\> GetProtection ( # A1  |  开始从文件检索保护策略。
public std：： shared_ptr \<AsyncControl\> RegisterContentForTrackingAndRevocationAsync (Bool isOwnerNotificationEnabled，const std：： shared_ptr \<ProtectionEngine::Observer\>& 观察程序，const std：： shared_ptr \<void\>& 上下文)   |  # # # # 个参数
public std：： shared_ptr \<AsyncControl\> RevokeContentAsync (const std：： shared_ptr \<ProtectionEngine::Observer\>& 观察程序，const std：： shared_ptr \<void\>& 上下文)   |  对内容执行吊销。
public void ClassifyAsync (const std：： shared_ptr \<void\>& 上下文)   |  在处理程序中执行规则，并返回要执行的操作的列表。
public void InspectAsync (const std：： shared_ptr \<void\>& 上下文)   |  创建文件检查器对象，该对象用于检索兼容文件格式的文件内容。
public void SetLabel (const std：： shared_ptr \<Label\>& label，Const LabelingOptions& LabelingOptions，Const ProtectionSettings& ProtectionSettings)   |  设置文件的敏感度标签。
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  从文件删除敏感度标签。
public void SetProtection (const std：： shared_ptr \<ProtectionDescriptor\>& protectionDescriptor，Const ProtectionSettings& ProtectionSettings)   |  （根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
public void SetProtection (const std：： shared_ptr \<ProtectionHandler\>& protectionHandler)   |  使用现有的保护处理程序对文档设置保护。
public void RemoveProtection()  |  删除文件保护。 如果原始文件格式不支持标签，则删除保护时，标签将丢失。 当本机格式支持标签时，将保留标签元数据。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr\<void\>& context) | 将所做的更改写入到 \|outputFilePath\ 参数指定的文件 |  个参数。
public void CommitAsync(const std::shared_ptr\<Stream\>& outputStream, const std::shared_ptr\<void\>& context) | 将所做的更改写入到 \|outputStream\ 参数指定的流。 |  个参数。
public bool IsModified ( # A1  |  检查是否有要提交到文件的更改。
public void GetDecryptedTemporaryFileAsync (const std：： shared_ptr \<void\>& 上下文)   |  返回临时文件的路径 (如果可能) 表示已解密的内容，将删除该文件。
public void GetDecryptedTemporaryStreamAsync (const std：： shared_ptr \<void\>& 上下文)   |  返回表示已解密内容的流。
public void NotifyCommitSuccessful (const std：： string& actualFilePath)   |  在将更改提交到磁盘后调用。
public std::string GetOutputFileName()  |  基于原始文件名和累积的更改，计算输出文件名称和扩展名。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
开始从文件检索敏感度标签。
  
### <a name="getproperties-function"></a>GetProperties 函数
根据版本 Retrievs 文件 propertries。
  
### <a name="getprotection-function"></a>GetProtection 函数
开始从文件检索保护策略。
  
### <a name="registercontentfortrackingandrevocationasync-function"></a>RegisterContentForTrackingAndRevocationAsync 函数

参数：  
* **isOwnerNotificationEnabled**：设置为 true 可在文档解密时通过电子邮件通知所有者，或设置为 false 将不发送通知。 


* **observer**：实现 ProtectionHandler::Observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。
  
### <a name="revokecontentasync-function"></a>RevokeContentAsync 函数
对内容执行吊销。

参数：  
* **observer**：实现 ProtectionHandler::Observer 接口的类 


* **上下文**：将以不透明转发到观察者和可选 HttpDelegate 的客户端上下文



  
**返回**： Async control 对象。
  
### <a name="classifyasync-function"></a>ClassifyAsync 函数
在处理程序中执行规则，并返回要执行的操作的列表。

  
**返回结果**：应该应用于内容的操作列表。
  
### <a name="inspectasync-function"></a>InspectAsync 函数
创建文件检查器对象，该对象用于检索兼容文件格式的文件内容。

  
**返回**：文件检查器。
  
### <a name="setlabel-function"></a>SetLabel 函数
设置文件的敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 JustificationRequiredError。
  
### <a name="deletelabel-function"></a>DeleteLabel 函数
从文件删除敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 JustificationRequiredError。
  
### <a name="setprotection-function"></a>SetProtection 函数
（根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="setprotection-function"></a>SetProtection 函数
使用现有的保护处理程序对文档设置保护。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="removeprotection-function"></a>RemoveProtection 函数
删除文件保护。 如果原始文件格式不支持标签，则删除保护时，标签将丢失。 当本机格式支持标签时，将保留标签元数据。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="commitasync-function"></a>CommitAsync 函数
将所做的更改写入到 |outputFilePath| 参数指定的文件。
FileHandler::Observer 将在成功或失败时调用。
  
### <a name="commitasync-function"></a>CommitAsync 函数
将所做的更改写入到 |outputStream| 参数指定的流。
FileHandler::Observer 将在成功或失败时调用。
  
### <a name="ismodified-function"></a>IsModified 函数
检查是否有要提交到文件的更改。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync 函数
返回临时文件的路径 (如果可能) 表示已解密的内容，将删除该文件。
FileHandler::Observer 将在成功或失败时调用。
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync 函数
返回表示已解密内容的流。
FileHandler::Observer 将在成功或失败时调用。
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful 函数
在将更改提交到磁盘后调用。

参数：  
* **actualFilePath**：输出文件的实际文件路径 


触发审核事件
  
### <a name="getoutputfilename-function"></a>GetOutputFileName 函数
基于原始文件名和累积的更改，计算输出文件名称和扩展名。