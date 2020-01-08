---
title: 概念 - Microsoft 信息保护 SDK 文件 API 中的审核
description: 本文将帮助你了解如何使用 Microsoft 信息保护 SDK 来将文件 API 审核事件提交到 Azure 信息保护分析。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 0e7fdde8194603917186f5771ca1a782fd209fa7
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556259"
---
# <a name="auditing-in-the-mip-sdk-file-api"></a>MIP SDK 文件 API 中的审核

Azure 信息保护管理门户提供对管理员报表的访问。 通过这些报告，可以查看用户在已集成了 MIP SDK 的任何应用程序或服务上手动或自动应用的标签。 使用 SDK 的开发合作伙伴可以启用此功能，以便在客户报表中显示其应用程序的信息。

## <a name="event-types"></a>事件类型

可通过 SDK 向 Azure 信息保护分析提交三种类型的事件。 检测信号事件、发现事件和更改事件

### <a name="heartbeat-events"></a>检测信号事件

对于已集成文件 API 的任何应用程序，系统将自动生成检测信号事件。 检测信号事件包括：

* TenantId
* 生成时间
* 用户主体名称
* 生成审核的计算机的名称
* 进程名称
* 平台
* 应用 ID - 对应于 Azure AD 应用程序 ID。

在检测企业中使用 Microsoft 信息保护 SDK 的应用程序时，这些事件会十分有用。

### <a name="discovery-events"></a>发现事件

发现事件提供关于文件 API 读取或使用的标记信息的信息。 由于这些事件可以显示设备、位置以及组织中访问信息的用户，因此它们十分有用。

通过在创建新的 `mip::FileHandler` 时将 `AuditDiscoveryEnabled` 参数设置为 true，可以将这些事件提交给 Azure 信息保护分析。 另外，还提供采用某种人工可读格式标识文件的内容标识符。 建议使用此标识符的文件路径。

以下示例会创建启用了审核发现的新 `mip::FileHandler`。 在 `mip::FileEngine` 上调用 `CreateFileHandler()` 方法，并将 `AuditDiscoveryEnabled` 设置为 true。 在 `FileHanlder` 读取标签之后，便会生成发现审核。

```cpp
// Create FileHandler with discovery enabled
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(inputFilePath, actualFilePath, true /*AuditDiscoveryEnabled*/, make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = handlerFuture.get();

// Read label. This generates the discovery audit.
auto label = handler->GetLabel();
```

### <a name="change-events"></a>更改事件

更改事件提供有关文件、已应用或更改的标签以及用户提供的任何依据的信息。 在将更改成功提交到文件之后，通过调用 `mip::FileHandler` 上的 `NotifyCommitSuccessful()` 来生成更改事件。

```cpp
// Create labeling options, set label
string contentId = "C:\users\myuser\Documents\MyPlan.docx";
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
handler->SetLabel(labelId, labelingOptions, mip::ProtectionSettings());
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();

// CommitAsync() returns a bool. If the change was successful, call NotifyCommitSuccessful().
fileHandler->CommitAsync(outputFile, commitPromise);
if(commitFuture.get()) {

    // Submit audit event.
    handler->NotifyCommitSuccessful(contentId);
}
```

## <a name="audit-dashboard"></a>审核仪表板

提交到 Azure 信息保护审核管道的事件将显示在 https://portal.azure.com 的报表中。 

## <a name="next-steps"></a>后续步骤

有关 Azure 信息保护中的审核体验的详细信息，请查看[技术社区中的预览版公告博客](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)。
