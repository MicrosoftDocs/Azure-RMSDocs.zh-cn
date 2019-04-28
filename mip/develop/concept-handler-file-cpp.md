---
title: 概念 - MIP SDK 中的文件处理程序。
description: 本文将帮助你了解如何创建文件 API 处理程序并将其用于调用操作。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: 7e436d27ae48ee6d3589faaf55943b8ffd314450
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175967"
---
# <a name="microsoft-information-protection-sdk---file-handler-concepts"></a>Microsoft 信息保护 SDK - 文件处理程序概念

在 MIP SDK 文件 API 中，`mip::FileHandler` 公开可用于跨一组文件类型（内置支持）读取和写入标签或保护信息的各种操作。 

## <a name="supported-file-types"></a>支持的文件类型

- 基于 OCP 的 Office 文件格式（Office 2010 及更高版本）
- 旧版 Office 文件格式 (Office 2007)
- PDF
- 通用 PFILE 支持
- 支持 Adobe XMP 的文件

## <a name="file-handler-functions"></a>文件处理程序函数

`mip::FileHandler` 公开用于读取、写入和删除标签及保护信息的方法。 有关完整列表，请参阅 [API 参考](reference/class_mip_filehandler.md)。

本文将介绍以下方法：

- `GetLabelAsync()`
- `SetLabel()`
- `DeleteLabel()`
- `CommitAsync()`

## <a name="requirements"></a>要求

创建 `FileHandler` 用于处理特定文件需要使用以下对象：

- `FileProfile`
- 已添加到 `FileProfile` 的 `FileEngine`
- 继承 `mip::FileHandler::Observer` 的类

## <a name="create-a-file-handler"></a>创建文件处理程序

管理文件 API 中的任何文件所需执行的第一步都是创建 `FileHandler` 对象。 此类实现获取、设置、更新、删除和提交对文件的标签更改所需的全部功能。

创建 `FileHandler` 就像使用 promise/future 模式调用 `FileEngine` 的 `CreateFileHandlerAsync` 函数一样简单。

`CreateFileHandlerAsync` 接受三个参数：应读取或修改的文件的路径`mip::FileHandler::Observer`异步事件通知和 promise `FileHandler`。

**注意：** `mip::FileHandler::Observer` 类必须在派生类中实现，因为 `CreateFileHandler` 需要 `Observer` 对象。 

```cpp
auto createFileHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::FileHandler>>>();
auto createFileHandlerFuture = createFileHandlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(filePath, std::make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = createFileHandlerFuture.get();
```

成功创建 `FileHandler` 对象后，可以执行文件操作（获取/设置/删除/提交）。

## <a name="read-a-label"></a>读取标签

### <a name="metadata-requirements"></a>元数据要求

若要从文件中成功读取元数据并将其转换为可在应用程序中使用的内容，需要满足一些要求。

- 要读取的标签必须仍然存在于 O365 服务中。 如果它已被完全删除，SDK 将无法获取有关该标签的信息，并将返回错误。
- 文件元数据必须保持完整。 此元数据包括：
  - Attribute1
  - Attribute2

### <a name="getlabelasync"></a>GetLabelAsync()

创建指向特定文件的处理程序后，我们可返回 promise/future 模式来异步读取标签。 Promise 适用于 `mip::ContentLabel` 对象，该对象包含关于所应用标签的全部信息。

在实例化 `promise` 和 `future` 对象后，我们通过调用 `handler->GetLabelAsync()` 并提供 `promise` 作为单独的参数来读取标签。 最后，标签可以存储在 `mip::ContentLabel` 对象中，我们将从 `future` 获取该对象。

```cpp
auto loadPromise = std::make_shared<std::promise<std::shared_ptr<mip::ContentLabel>>>();
auto loadFuture = loadPromise->get_future();
handler->GetLabelAsync(loadPromise);
auto label = loadFuture.get();
```

可从 `label` 对象读取标签数据，并将其传递给应用程序中的任何其他组件或功能。

***

## <a name="set-a-label"></a>设置标签

设置标签分为两步。 首先，创建指向相关文件的处理程序后，可通过使用几个参数调用 `FileHandler->SetLabel()` 来设置标签。

```cpp
handler->SetLabel(label->GetId(), mip::LabelingOptions{ mip::AssignmentMethod::PRIVILEGED, "" });
```

第一个参数即来自 `ListLabelsAsync()` 的标签标识符。 此值可以存储在专用变量中，也可以通过读取 `mip::Label->GetId()` 来存储。

上面的示例假设我们已将所需的 `mip::Label` 存储在名为 `label` 的对象中。

### <a name="labeling-options"></a>标签选项

设置标签所需的第二个参数是我们在调用 `SetLabel()` 函数时以内联方式创建的 `mip::LabelingOptions` 对象， 也可以提前创建该对象。

`LabelingOptions` 指定有关标签的其他信息，例如 `AssignmentMethod` 和操作的理由。

- `mip::AssignmentMethod` 只是一个具有三个值的枚举器：`STANDARD`、`PRIVILEGED` 或 `AUTO`。 有关更多详细信息，请查看 `mip::AssignmentMethod` 参考。
- 只有在服务策略要求提供时*以及*在降低文件的*现有*敏感度时才需要提供理由。

```cpp
auto labelingOptions = mip::LabelingOptions();
labelingOptions.SetMethod(mip::AssignmentMethod::STANDARD);
labelingOptions.SetJustificationMessage("Because I made an educated decision based upon the contents of this file.");
```

现在，标签选项不会以内联方式创建，而是可以传递到 `SetLabel()` 函数。

```cpp
handler->SetLabel(label->GetId(), labelingOptions);
```

现已在处理程序引用的文件上设置了标签，还需要再完成一个步骤来提交更改并将文件写入磁盘，或创建输出流。

### <a name="commit-changes"></a>提交更改

在 MIP SDK 中提交对文件所做任何更改的最后一步是**提交**更改。 这可以通过使用 `FileHandler->CommitAsync()` 函数来实现。 

若要实现 commitment 函数，我们可返回 promise/future 模式，为 `bool` 创建 promise。 如果操作成功，则 `CommitAsync()` 函数将返回 true；如果因任何原因失败，则返回 false。 

在创建后`promise`并`future`，`CommitAsync()`称为和提供的两个参数：输出文件路径 (`std::string`)，并承诺。 最后，通过获取 `future` 对象的值来获得结果。

```cpp
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
auto wasCommitted = commitFuture.get();
```

**重要：**`FileHandler`将不更新或覆盖现有文件。 开发人员负责实现对标记文件的**替换**操作。 

如果将标签写入 **FileA.docx**，则会创建文件的副本 **FileB.docx** 并应用标签。 必须编写代码来删除/重命名 **FileA.docx** 以及重命名 **FileB.docx**。

***

## <a name="delete-a-label"></a>删除标签

```cpp
auto handler = mEngine->CreateFileHandler(filePath, std::make_shared<FileHandlerObserverImpl>());
handler->DeleteLabel(mip::AssignmentMethod::PRIVILEGED, "Label unnecessary.");
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
```
