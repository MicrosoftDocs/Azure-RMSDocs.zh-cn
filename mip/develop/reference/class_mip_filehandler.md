---
title: class mip::FileHandler
description: 记录 mip::filehandler 类的 Microsoft 信息保护 (MIP) SDK。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ee0545346eef2c143946496f56af77b7081b1e06
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184648"
---
# <a name="class-mipfilehandler"></a>class mip::FileHandler 
适用于所有文件处理函数的接口。
  
## <a name="summary"></a>总结
 成員                        | 说明                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<ContentLabel\> GetLabel()  |  开始从文件检索敏感度标签。
public std::\<ProtectionHandler\> GetProtection()  |  开始从文件检索保护策略。
public void ClassifyAsync(const std::shared_ptr\<void\>& context)  |  在处理程序中执行的规则，并返回要执行的操作列表。
public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  设置文件的敏感度标签。
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  从文件删除敏感度标签。
public void SetProtection (const std::\<ProtectionDescriptor\>& protectionDescriptor)  |  （根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
public void SetProtection (const std:: vector\<uint8_t\>& serializedPublishingLicense，const std:: vector\<uint8_t\>& serializedProtectionInfo)  |  设置文件 （根据 serializedPublishingLicense 和 serializedProtectionInfo） 可以自定义的或基于模板的权限。
public void RemoveProtection()  |  删除文件保护。 如果文件已添加标签，标签将丢失。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr\<void\>& context) | 将所做的更改写入到 \|outputFilePath\ 参数指定的文件 |  参数指定的网络接口启用 iSCSI 访问。
public void CommitAsync (const std::\<Stream\>& outputStream，const std:: shared_ptr\<void\>& 上下文) | 将所做的更改写入到 \|outputStream\ 参数指定的流。 |  参数指定的网络接口启用 iSCSI 访问。
public void GetDecryptedTemporaryFileAsync(const std::shared_ptr\<void\>& context)  |  返回的临时文件 （将在可能的情况删除）-表示已解密的内容的路径。
public void NotifyCommitSuccessful(const std::string& actualFilePath)  |  在将更改提交到磁盘后调用。
public std::string GetOutputFileName()  |  基于原始文件名和累积的更改，计算输出文件名称和扩展名。
  
## <a name="members"></a>成員
  
### <a name="getlabel-function"></a>GetLabel 函数
开始从文件检索敏感度标签。
  
### <a name="getprotection-function"></a>GetProtection 函数
开始从文件检索保护策略。
  
### <a name="classifyasync-function"></a>ClassifyAsync 函数
在处理程序中执行的规则，并返回要执行的操作列表。

  
**返回**:应应用于内容的操作的列表。
  
### <a name="setlabel-function"></a>SetLabel 函数
设置文件的敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  
### <a name="deletelabel-function"></a>DeleteLabel 函数
从文件删除敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  
### <a name="setprotection-function"></a>SetProtection 函数
（根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="setprotection-function"></a>SetProtection 函数
设置文件 （根据 serializedPublishingLicense 和 serializedProtectionInfo） 可以自定义的或基于模板的权限。
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
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync function
返回的临时文件 （将在可能的情况删除）-表示已解密的内容的路径。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful 函数
在将更改提交到磁盘后调用。

参数：  
* **actualFilePath**:输出文件的实际文件路径 


触发审核事件
  
### <a name="getoutputfilename-function"></a>GetOutputFileName 函数
基于原始文件名和累积的更改，计算输出文件名称和扩展名。