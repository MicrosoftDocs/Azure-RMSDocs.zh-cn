---
title: class mip::FileHandler
description: '记录 Microsoft 信息保护 (MIP) SDK 的 mip:: filehandler 类。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 93e4ed2210632a051bc9e1aaa06069d246860041
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055015"
---
# <a name="class-mipfilehandler"></a>class mip::FileHandler 
适用于所有文件处理函数的接口。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetLabel ()  |  开始从文件检索敏感度标签。
public std:: shared_ptr\<ProtectionHandler\> GetProtection ()  |  开始从文件检索保护策略。
public void ClassifyAsync (const std:: shared_ptr\<void\>& 上下文)  |  在处理程序中执行规则, 并返回要执行的操作的列表。
public void InspectAsync (const std:: shared_ptr\<void\>& 上下文)  |  创建文件检查器对象, 该对象用于检索兼容文件格式的文件内容。
public void SetLabel (const std:: shared_ptr\<label\>& label, const LabelingOptions & LabelingOptions, const ProtectionSettings & ProtectionSettings)  |  设置文件的敏感度标签。
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  从文件删除敏感度标签。
static bool IsProtected (const std:: string & filePath, const std:: shared_ptr<MipContext>& mipContext) | 检查文件是否受保护。
public void SetProtection (const std:: shared_ptr\<ProtectionDescriptor\>& ProtectionDescriptor, const ProtectionSettings & ProtectionSettings)  |  （根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
public void RemoveProtection()  |  删除文件保护。 如果文件已添加标签，标签将丢失。
public void CommitAsync (const std:: string & outputFilePath, const std:: shared_ptr\<void\>& context) | 将所做的更改写入到 \|outputFilePath\ 参数指定的文件 |  参数指定的网络接口启用 iSCSI 访问。
public void CommitAsync (const std:: shared_ptr\<Stream\>& outputStream, const std:: shared_ptr\<void\>& context) | 将所做的更改写入到 \|outputStream\ 参数指定的流。 |  参数指定的网络接口启用 iSCSI 访问。
public void GetDecryptedTemporaryFileAsync(const std::shared_ptr\<void\>& context)  |  返回一个指向临时文件的路径 (如果可能, 将删除该文件), 表示已解密的内容。
public void GetDecryptedTemporaryStreamAsync (const std:: shared_ptr\<void\>& 上下文)  |  返回表示已解密内容的流。
public void NotifyCommitSuccessful (const std:: string & actualFilePath)  |  在将更改提交到磁盘后调用。
public std::string GetOutputFileName()  |  基于原始文件名和累积的更改，计算输出文件名称和扩展名。
  
## <a name="members"></a>成员
  
### <a name="getlabel-function"></a>GetLabel 函数
开始从文件检索敏感度标签。
  
### <a name="getprotection-function"></a>GetProtection 函数
开始从文件检索保护策略。
  
### <a name="classifyasync-function"></a>ClassifyAsync 函数
在处理程序中执行规则, 并返回要执行的操作的列表。

  
**返回**:应对内容应用的操作的列表。
  
### <a name="inspectasync-function"></a>InspectAsync 函数
创建文件检查器对象, 该对象用于检索兼容文件格式的文件内容。

  
**返回**:文件检查器。
  
### <a name="setlabel-function"></a>SetLabel 函数
设置文件的敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  
### <a name="deletelabel-function"></a>DeleteLabel 函数
从文件删除敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  

### <a name="isprotected-function"></a>IsProtected 函数
检查文件是否受保护。

### <a name="setprotection-function"></a>SetProtection 函数
（根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="removeprotection-function"></a>RemoveProtection 函数
删除文件保护。 如果文件已添加标签，标签将丢失。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="commitasync-function"></a>CommitAsync 函数
将所做的更改写入到 |outputFilePath| 参数指定的文件。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="commitasync-function"></a>CommitAsync 函数
将所做的更改写入到 |outputStream| 参数指定的流。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync 函数
返回一个指向临时文件的路径 (如果可能, 将删除该文件), 表示已解密的内容。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync 函数
返回表示已解密内容的流。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful 函数
在将更改提交到磁盘后调用。

参数：  
* **actualFilePath**:输出文件的实际文件路径 


触发审核事件
  
### <a name="getoutputfilename-function"></a>GetOutputFileName 函数
基于原始文件名和累积的更改，计算输出文件名称和扩展名。