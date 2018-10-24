---
title: 类 mip FileHandler
description: 类 mip FileHandler 的参考信息
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: efae18bdc10f8878f255f35c608a50482a29887b
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446118"
---
# <a name="class-mipfilehandler"></a>class mip::FileHandler 
适用于所有文件处理函数的接口。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  开始从文件检索敏感度标签。
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  开始从文件检索保护策略。
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  设置文件的敏感度标签。
 public void DeleteLabel(const LabelingOptions& labelingOptions)  |  从文件删除敏感度标签。
public void SetProtection(const std::shared_ptr<ProtectionDescriptor>& protectionDescriptor)  |  （根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
 public void RemoveProtection()  |  删除文件保护。 如果文件已添加标签，标签将丢失。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | 将所做的更改写入到 \|outputFilePath\ 参数指定的文件 |  参数。
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | 将所做的更改写入到 \|outputStream\ 参数指定的流。 |  参数。
 public void NotifyCommitSuccessful(const std::string& contentIdentifier)  |  在将更改提交到磁盘后调用。
 public std::string GetOutputFileName()  |  基于原始文件名和累积的更改，计算输出文件名称和扩展名。
  
## <a name="members"></a>成員
  
### <a name="getlabelasync"></a>GetLabelAsync
开始从文件检索敏感度标签。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="getprotectionasync"></a>GetProtectionAsync
开始从文件检索保护策略。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。

参数：  
* **context**：将以不透明形式传递回观察程序的客户端上下文。


  
### <a name="setlabel"></a>SetLabel
设置文件的敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  
### <a name="deletelabel"></a>DeleteLabel
从文件删除敏感度标签。
在调用 CommitAsync 之前，不会将更改写入文件。 Privilegd 和 Auto 方法使得此 API 可以重写任何现有标签。如果在设置标签时需要提供合理理由（通过 labelingOptions 参数），则引发 [JustificationRequiredError](class_mip_justificationrequirederror.md)。
  
### <a name="setprotection"></a>SetProtection
（根据 protectionDescriptor->GetProtectionType）设置对文件的自定义权限或基于模板的权限。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="removeprotection"></a>RemoveProtection
删除文件保护。 如果文件已添加标签，标签将丢失。
在调用 CommitAsync 之前，不会将更改写入文件。
  
### <a name="commitasync"></a>CommitAsync
将所做的更改写入到 |outputFilePath| 参数指定的文件。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="commitasync"></a>CommitAsync
将所做的更改写入到 |outputStream| 参数指定的流。
[FileHandler::Observer](class_mip_filehandler_observer.md) 将在成功或失败时调用。
  
### <a name="notifycommitsuccessful"></a>NotifyCommitSuccessful
在将更改提交到磁盘后调用。

参数：  
* **contentIdentifier**：文件示例：“C:\mip-sdk-for-cpp\files\audit.docx”[路径]，电子邮件示例：“RE: Audit design:user1@contoso.com”[主题:发件人] 


触发审核事件
  
### <a name="getoutputfilename"></a>GetOutputFileName
基于原始文件名和累积的更改，计算输出文件名称和扩展名。