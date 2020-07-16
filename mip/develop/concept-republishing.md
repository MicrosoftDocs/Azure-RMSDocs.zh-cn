---
title: 在 MIP SDK 中重新发布
description: 本文将帮助你了解如何为重新发布方案重复使用保护处理程序的方案。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 499e4881175920fdf3127856fa9056b10ae22b79
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86405180"
---
# <a name="republishing-c"></a>重新发布（c + +）

## <a name="overview"></a>概述

本概述重点介绍如何在 MIP SDK 中重新发布：当应用程序必须允许用户编辑文件，但需要维护有关所有者、权限、内容密钥等的原始[发布许可证](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/licenses-and-certificates-and-how-ad-rms-protects-and-consumes/ba-p/247309)信息时遇到的特定情况。

模式可能类似于：

- 用户打开受保护的文档以进行编辑。
- 如果用户已被授予适当的权限，则必须只允许用户编辑该文件。
- 用户编辑并保存文档。

完成此任务的 MIP SDK 伪代码可能如下所示：

- 创建一个 `mip::FileHandler` 指向目标文件的。
- `mip::ProtectionHandler`通过的方法存储公开 `mip::FileHandler` 的 `GetProtection()` 。
- 检查用户是否具有通过调用方法的**编辑**权限 `AccessCheck()` 。
- 使用 `mip::FileHandler` `GetDecryptedTemporaryFileAsync()` 或 `GetDecryptedTemporaryStreamAsync()` 获取临时的解密输出。
- 编辑临时文件或流内容并保存。
- 创建 `mip::FileHandler` 指向 temp 文件的新实例，并使用 `SetProtection()` 方法，并提供存储 `mip::ProtectionHandler` 为参数的。
- 提交更改。

使用 `mip::ProtectionHandler` 原始文件中的，所有者、内容 ID、内容密钥等将保留在编辑过的文档上。 此重新发布方案要求应用程序维护对原始的引用 `mip::ProtectionHandler` 。

## <a name="implementation"></a>实现

如前文所述， `mip::FileHandler` 类公开了用于读取、写入和删除标签和保护信息的方法。 有关支持的操作的完整列表，请查看[API 参考](./reference/class_mip_filehandler.md#summary)。

此方案使用的以下方法 `mip::FileHandler` ：

- `GetProtection()`
- `CommitAsync()`
- `GetDecryptedTemporaryFileAsync()`
- `SetProtection()`

此方案还使用 `mip::ProtectionHandler` ，它公开用于加密和解密受保护的流和缓冲区的函数，执行访问检查，获取发布许可证，并从受保护的信息获取属性。 此 `AccessCheck()` 方法将用于验证用户是否有权编辑该文件。

若要成功完成此重新保护方案，请查看 "后续步骤" 下的 "快速启动"，并确保应用程序生成并可以成功列出标签。

## <a name="create-a-protection-handler-from-the-file-and-decrypt-the-file"></a>从文件创建保护处理程序并对文件进行解密

`mip::ProtectionHandler`公开用于加密和解密受保护的流和缓冲区的函数，执行访问检查，获取发布许可证，并从受保护的信息获取属性。 `mip::ProtectionHandler`对象是通过提供 ProtectionDescriptor 或序列化发布许可证来构造的。 对于此用例，我们将在解密已受保护的内容时或在保护已构造了许可证的内容时使用发布许可证作为发布许可证。

`mip::FileHandler`公开一个名为 `GetProtection()` 的方法，该方法 `mip::ProtectionHandler` 从与关联的文件中进行检索 `mip::FileHandler` 。 `mip::ProtectionHandler`检索对象后，可以使用相同的方法来验证用户对文件的访问权限级别，对文件进行解密，以后在编辑文件后对其进行加密。

`mip::ProtectionHandler``AccessCheck()`用于验证用户对文件是否具有特定权限，并根据结果返回布尔值响应。 例如，若要验证用户是否有权编辑，请调用方法，并传入值 "EDIT"。 如果结果为*true*，则允许用户编辑该文件。 验证**编辑**权限后，使用 `mip::FileHandler` `GetDecryptedTemporaryFileAsync()` 来检索临时解密文件。

有关各种用户权限的详细信息，请参阅[Azure 信息保护的用户权限](/azure/information-protection/configure-usage-rights)。

 > [!IMPORTANT]
 > 访问检查和强制仅适用于应用程序开发人员。 具有 "查看" 权限的用户能够解密受保护的信息。 由应用程序来验证授予用户的权限集，并通过信息保护控件（例如阻止复制、编辑或拍摄屏幕截图）强制实施这些权限。 未能正确实现保护控制可能会导致敏感信息泄露。

## <a name="save-and-publish-the-edited-file-by-applying-protection"></a>通过应用保护来保存并发布编辑过的文件

文件解密后，可以编辑该文件。 编辑操作完成后，可以提交更改。 `IFileHandler`使用上述临时文件创建对象以处理提交的文件。 然后，可以使用 `IProtectionHandler` 从原始文件中检索到的对象保护临时文件。

## <a name="next-steps"></a>后续步骤

- [查看 c + + 重新发布入门](quick-file-republishing-cpp.md)
- [查看 C 的重新发布快速入门#](quick-file-republishing-csharp.md)